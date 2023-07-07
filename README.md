# ADO Pipeline Template for Docker Login

This template contains an Azure pipeline that can be extended to build an image from a docker file under different Azure pipelines.

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

    - name: dockerfile
      type: string

    - name: tags
      type: string

  resources:
    repositories:
      - repository: Docker
        type: github
        name: knoldus/ado.docker.login
        ref: <respective branch name>
        endpoint: '<GitHub Service Connection>'

  steps:

  - template: build.yml@Docker
     parameters:
        containerRegistry: '${{parameters.RegistryToken}}'
        repository: '${{parameters.imageRepository}}'
        Dockerfile: '${{parameters.dockerfile}}'
        tags: ${{parameters.tags}}
  ```

You can also use Variable Group and Azure Key vault for values.
