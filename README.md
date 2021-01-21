## Fork of Amazon ECS "Render Task Definition" Action for GitHub Actions

Inserts a container image URI into an Amazon ECS task definition JSON file, creating a new task definition file.

This is a fork from `aws-actions/amazon-ecs-deploy-task-definition`. The added feature is to support overriding `environment` in task definition. `environment` sets the envs to pass to `docker run`.

## Usage

To insert the image URI `amazon/amazon-ecs-sample:latest` as the image for the `web` container in the task definition file, and then deploy the edited task definition file to ECS:

```yaml
- name: Render Amazon ECS task definition
  id: render-web-container
  uses: SickSAMA/amazon-ecs-render-task-definition@v1
  with:
    task-definition: task-definition.json
    container-name: web
    image: amazon/amazon-ecs-sample:latest
    environment: |-
      PORT: 80
      NODE_ENV: production

- name: Deploy to Amazon ECS service
  uses: aws-actions/amazon-ecs-deploy-task-definition@v1
  with:
    task-definition: ${{ steps.render-web-container.outputs.task-definition }}
    service: my-service
    cluster: my-cluster
```

See [action.yml](action.yml) for the full documentation for this action's inputs and outputs.

## License Summary

This code is made available under the MIT license.

## Security Disclosures

If you would like to report a potential security issue in this project, please do not create a GitHub issue. Instead, please follow the instructions [here](https://aws.amazon.com/security/vulnerability-reporting/) or [email AWS security directly](mailto:aws-security@amazon.com).
