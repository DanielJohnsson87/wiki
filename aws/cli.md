# AWS CLI

Setup IAM credentials for the AWS Account. (`PowerUserAccess` is a good permission set to user for dev purposes) 

Login with settings in `.~/aws/config`
```
aws sso login
```

Verify identity 
```
aws sts get-caller-identity
```

Verify for specific identity (Setup identity in .~/aws/config

```
aws sts get-caller-identity --profile ${identity}
```
