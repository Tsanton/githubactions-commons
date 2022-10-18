# **Docker-Compose Test** #

## **Variables** ##

See [this](../.github/workflows/compose-ci.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Docker compose test
  uses: Fremtind/pda-githubactions-commons/actions/docker-compose-test@main
  with:
    compose_file_path: ./
    compose_file_name: docker-compose.yaml
    test_service_name: testsuite
    additional_compose_test_files: |
      ./compose-files/docker-compose.testing.yaml
      ./compose-files/docker-compose.ci-testing.yaml
```