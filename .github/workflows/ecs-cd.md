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

## **Dependencies** ##

This reusable workflow is composed of multiple action, one of whom is "aws-actions/amazon-ecs-render-task-definition@v1". \
One prerequisites for this reusable workflow to work is that, if the task is defined with an ECR image, the task must have been defined with a ```task execution role```. \
If that's not the case you'll be greeted ever so kindly with the following error:

```txt
Failed to register task definition in ECS: Fargate requires task definition to have execution role ARN to support ECR images.
```