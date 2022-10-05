# **ECS Deploy Action** #

## **Variables** ##

See [this](../.github/workflows/ecs-cd.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v1
  with:
    role-to-assume: arn:aws:iam::<aws-account-id>:role/<aws-iam-role-name>
    aws-region: <aws-region>

- name: Login to Amazon ECR
  id: login-ecr
  uses: aws-actions/amazon-ecr-login@v1

- name: Docker compose build
  uses: Fremtind/pda-githubactions-commons/docker-compose-build-action@main
  with:
    ecs_cluster_name: my-demo-cluster
    ecs_service_name: my-demo-app
    task_definition_family_name: my-demo-app
    task_definition_container_name: my-demo-app
    image: <aws-account-id>.dkr.ecr.<aws-region>.amazonaws.com/my-demo-app
```