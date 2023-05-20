# UI Component - HTML Element

Tips and best practices for components that render HTML Elements like `button`, `input`, `video` etc.

## Spread attributes to HTML elements

This will allow consumers of the component to set all HTML properties that an element has. That's great since we can't know what usecases
will be applicable in the future. 

It also abides to the SOLID principles where the Liskov substitution principle basically states that you should be able to replace any subclass/derived class (`<Button />`) with 
its base class (`<button>`). This will make refactoring easier in the future. 

```tsx
type ButtonProps = JSX.IntrinsicElements["button"] & {
  children?: React.ReactNode;
};

function Button({ children, ...restProps }: ButtonProps) {
  return <button {...restProps}>{children}</button>;
}
```

If you for some reason don't want a specific attribute to be allowed it's easy to just omit that from the `ButtonProps`.

```tsx
// Omit `type` from allowed <button> attributes
type ButtonProps = Omit<JSX.IntrinsicElements["button"], "type"> & {
  children?: React.ReactNode;
};

function Button({ children, ...restProps }: ButtonProps) {
  return <button type="button" {...restProps}>{children}</button>;
}

// ✅ `name` is ok
<Button name="click-me-button">Click me 🙏</Button>;
// 💥 This will cause a TypeScript error
<Button type="submit">Click me 🙏</Button>;
```

And as an oposite, if you want to make a HTML attribute required you can use a helper type to remove the optional `?` flag.

```tsx
// Remove the optional flag in `T` from `K`
type MakeRequired<T, K extends keyof T> = Omit<T, K> &
  Required<{ [P in K]: T[P] }>;

type ButtonProps = MakeRequired<JSX.IntrinsicElements["button"], "type"> & {
  children?: React.ReactNode;
};

function Button({ children, ...restProps }: ButtonProps) {
  return <button {...restProps}>{children}</button>;
}

// 💥 Missing `type` 
<Button name="click-me-button">Click me 🙏</Button>;
// ✅ This is ok now since we passed `type`
<Button type="submit">Click me 🙏</Button>;

```
