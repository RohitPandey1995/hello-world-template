apiVersion: scaffolder.backstage.io/v1beta3
kind: Template
metadata:
  name: hello-world-service
  title: Hello World Service
  description: Scaffolds a basic service with a Dockerfile and CI pipeline
spec:
  owner: guests
  type: service
  parameters:
    - title: Service details
      required: [name]
      properties:
        name:
          title: Name
          type: string
          description: Unique name of the new service
  steps:
    - id: fetch
      name: Fetch skeleton
      action: fetch:template
      input:
        url: ./content
        values:
          name: '{{ parameters.name }}'
    - id: publish
      name: Publish to GitHub
      action: publish:github
      input:
        allowedHosts: ['github.com']
        description: 'Hello World service'
        repoUrl: 'github.com?owner=RohitPandey1995&repo={{ parameters.name }}'
    - id: register
      name: Register in catalog
      action: catalog:register
      input:
        repoContentsUrl: '${{ steps.publish.output.repoContentsUrl }}'
        catalogInfoPath: '/catalog-info.yaml'
