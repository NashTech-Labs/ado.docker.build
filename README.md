# ADO Pipeline Template for Docker Push

This template contains an Azure pipeline that can be extended to push a docker image to acr under different Azure pipelines.

## use case

You need to have a service connection related to github on azure devops project.
To call this in you pipeline you can follow this example:
You can directly call a paticular template as per the requirement. for example: to use setup and init only.

   ```yaml
  # azure-pipeline.yml
  parameters:

    - name: RegistryToken
      type: string

    - name: imageRepository
      type: string

    - name: tags
      type: string

  resources:
    repositories:
      - repository: Docker
        type: github
        name: knoldus/ado.docker.build
        ref: <respective branch name>
        endpoint: '<GitHub Service Connection>'

  steps:

  - template: push.yml@Docker
    parameters:
        containerRegistry: '${{parameters.RegistryToken}}'
        repository: '${{parameters.imageRepository}}'
        tags: ${{parameters.tags}}
  ```

You can also use Variable Group and Azure Key vault for values.
