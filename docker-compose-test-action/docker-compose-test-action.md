# **Docker-Compose Test Action** #

TBC

## **Invocation** ##

```yaml

jobs:
  build:
    name: docker compose ci
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3

    - name: Docker compose test
      uses: Tsanton/pda-githubactions-commons/docker-compose-test-action@main
      with:
        compose_file: ${{ inputs.compose_file }}
        test_service_name: ${{ inputs.test_service_name }}   
        additional_compose_test_files: ${{ inputs.additional_compose_files }}   
```