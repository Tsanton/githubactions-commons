# **Docker-Compose Build Action** #

## **Variables** ##

See [this](../.github/workflows/compose-ci.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Docker compose build
  uses: Fremtind/pda-githubactions-commons/docker-compose-build-action@main
  with:
    compose_file_path: ./
    compose_file_name: docker-compose.yaml
    additional_compose_build_files: |
      ./compose-files/docker-compose.build1-override.yaml
      ./compose-files/docker-compose.build2-override.yaml
```