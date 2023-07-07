# ADO Pipeline Template for Docker Push

This template contains an Azure pipeline that can be extended to push a docker image to acr under different Azure pipelines.

## use case

You need to have a service connection related to GitHub on the Azure DevOps project.
To call this in your pipeline you can follow this example:

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

You can also use Variable Group and Azure Key Vault for values.
