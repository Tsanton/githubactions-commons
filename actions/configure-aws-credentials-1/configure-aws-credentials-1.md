# **Configure AWS credentials** #

A wrapper action for the last version (by commit sha) that the organization has approved for usage

## **Variables** ##

See [this](./action.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Configure AWS credentials
  uses: Fremtind/pda-githubactions-commons/actions/configure-aws-credentials-1@main
  with:
    aws-region: eu-west-1
    role-to-assume: arn:aws:iam::123456789123:role/github-actions-cd
```

## **Permissions** ##

As per the [documentation](https://github.com/aws-actions/configure-aws-credentials#usage) the following permissions are required to interact with GitHub's OIDC Token endpoint: 
- ```id-token: write```
- ```contents: read```


```yaml
jobs:
  build:
    name: Demo
    runs-on: ubuntu-latest

    permissions:
      id-token: write
      contents: read

    steps:
      - name: Configure AWS Credentials
        ....
```