# UI Component - Compound Components

Compound components are components that work together to form a complete UI. A `<select>` component is a HTML example of such a component. 
The `<select>` handles the state shared state for the components and the `<option>` renders the selectable options, handles click events and knows what value to set in case it gets selected. But each component apart doesn't provide much use. 

```html
<select>
  <option value="red">Red</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
</select>
```

A simple implementation of this in React would probably look something like this 👇

```tsx
<Select
  onClick={(option: Option) => console.log(`Option ${option.value} clicked`)}
  initialValue="green"
  options={[
    { value: "red", text: "Red" },
    { value: "green", text: "Green" },
    { value: "blue", text: "Blue" },
  ]}
/>;
```
It's fine and will work in most cases, but when the requirements for the component change, and they usually do, the lack of flexibility will show. What if you want to allow multiple select? Or add an input that filters the options? You will have to add more props and modify the source code to handle the new requirments. Eventually the component will become bloated and hard to understand, test and maintain. 


### Compound component to the rescue

A better approach would be to use the compount component pattern. Such an API might look like this instead.

```tsx
<Select initialValue="green">
  <Option value="red" text="Red" />
  <Option id="green-id" value="green" text="Green" />
  <Option value="blue" text="Blue" />
</Select>
```

It would be fairly trivial to add a filter component within the `<Select>` and handle things like empty states.

```tsx
function Component({options}: ComponentProps) {
  const [filter, setFilter] = React.useState<string>("");
  const handleFilter = (event) => setFilter(event.target.value);
  const filteredOptions = filterOptions(filter, options);
  return (
    <Select initialValue="green">
      <Select.Filter onChange={handleFilter} value={filter} />
      <OptionsWithEmptyState filteredOptions={filteredOptions} />
    </Select>
  );
}

function OptionsWithEmptyState({filteredOptions}: OptionsWithEmptyStateProps) {
  if(filteredOptions.length <= 1) {
    return <EmptyState />
  }
  
  return filteredOptions.map(option => {
    return <Select.Option key={option.id} option={option} />
  })
}
```


// TODO: Add example component


