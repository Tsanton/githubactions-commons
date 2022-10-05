# **ECS CD reusable workflow** #

## **Variables** ##

See [this](./ecs-cd.yaml) file for variable explanation.

## **Invocation** ##

```yaml
name: ecs-cd

on: [workflow_dispatch]

jobs:
  cd-demo:
    name: ECS CD demo
    uses: Fremtind/pda-githubactions-commons/.github/workflows/ecs-cd.yaml@main
    with:
      aws_region: eu-west-1
      aws_role_arn: arn:aws:iam::123456789123:role/github-actions-cd
      image: 123456789123.dkr.ecr.eu-west-1.amazonaws.com/demo-ecr-cd:1
      ecs_cluster_name: cd-demo-cluster
      ecs_service_name: demo-svc
      task_definition_family_name: demo-svc
      task_definition_container_name: demo-svc
```