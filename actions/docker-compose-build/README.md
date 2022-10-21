# **Docker-Compose Build** #

## **Variables** ##

See [this](../../.github/workflows/compose-ci.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Docker compose build
  uses: Fremtind/pda-githubactions-commons/actions/docker-compose-build@main
  with:
    compose_file_path: ./
    compose_file_name: docker-compose.yaml
    additional_compose_build_files: |
      ./compose-files/docker-compose.build1-override.yaml
      ./compose-files/docker-compose.build2-override.yaml
```