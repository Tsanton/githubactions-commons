# **ECS Deploy** #

## **Variables** ##

See [this](../.github/workflows/ecs-cd.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Configure AWS Credentials
  uses: Fremtind/pda-githubactions-commons/actions/configure-aws-credentials-1@main
  with:
    role-to-assume: arn:aws:iam::<aws-account-id>:role/<aws-iam-role-name>
    aws-region: <aws-region>

- name: Update and deploy ECS task revision
  uses: Fremtind/pda-githubactions-commons/actions/ecs-deploy@main
  with:
    ecs_cluster_name: my-demo-cluster
    ecs_service_name: my-demo-app
    task_definition_family_name: my-demo-app
    task_definition_container_name: my-demo-app
    image: <aws-account-id>.dkr.ecr.<aws-region>.amazonaws.com/my-demo-app
```