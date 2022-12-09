# **Compose CI reusable workflow** #

## **Variables** ##

See [this](./compose-ci.yaml) file for variable explanation.

## **Invocation** ##

```yaml
name: demo

on: [workflow_dispatch]

jobs:
  ci:
    name: Demo CI Invocation
    uses: Fremtind/pda-githubactions-commons/.github/workflows/compose-ci.yaml@main
    with:
      aws_region: "eu-west-1"
      aws_role_arn: "arn:aws:iam::123456789123:role/github-actions-cd"
      compose_file_path: ./application/
      compose_file_name: docker-compose.yaml
      additional_compose_build_files: |
        ./application/docker-compose.build-override.yaml
      run_test: true
      additional_compose_test_files: |
        ./application/docker-compose.testing.yaml
        ./application/docker-compose.ci-testing.yaml
      test_service_name: testsuite
      tags: |
        latest
        ${{ github.run_number }}
```