# Digital Post Komponent
Github repository hosting the setup for the Digital Post Komponent.

## Project Architecture
[![](https://mermaid.ink/img/pako:eNqdU8GO0zAQ_RXLJ5DWTrX0sjkgtU3bBVaiSnJLevA6k9Y0sSN7AkKr_Ry-hB_DbtVtWgpa8Gky896bzPP4iUpTAY0pY6zUucIGYpKojULRkJVxSD6ZtjMaNJZ6j6kb801uhUXykJaa-DMpcivqWsn14dv1jxsrui3JZxlhpOp2DMHhoRjOtEjnWU4ysF-VhDVj5GMynRHG3oeOGwvuhJ0ViXKdQLkFe8m4TvDFZbqaxXeju1HQnBdn85zk1tdJt4G0KDK0P380tbHuOiUpVsni5Y9O-flAahykklNt8Zfasphra5qmBXydM_dFChJU90r4MVO8OUYkESgehYO3w7HIH1VAVxcXPDR2IPFhmeVnpl_Ys0XsXBxFolM8bAavDtjOhHi3NyZoDMz5L9b9P7N-H9GvgRD7NTi_xqNu0Oys0sidNFqDDKpR_QWs3qejWz7ioyj0yfJ0MnlYfE6zwXKtLxpPyEDcPx3u7UfmDjfMHYoNcJSOo1WevuOyMX0Vj8fvoiEwjBtakim9oS3YVqjKP_Kn0KOkuIUWShr7sIJa9A2WtNTPHip6NNl3LWmMtocb2neVQEiU8Ga0NK5F4-D5Fx19Szc?type=png)](https://mermaid.live/edit#pako:eNqdU8GO0zAQ_RXLJ5DWTrX0sjkgtU3bBVaiSnJLevA6k9Y0sSN7AkKr_Ry-hB_DbtVtWgpa8Gky896bzPP4iUpTAY0pY6zUucIGYpKojULRkJVxSD6ZtjMaNJZ6j6kb801uhUXykJaa-DMpcivqWsn14dv1jxsrui3JZxlhpOp2DMHhoRjOtEjnWU4ysF-VhDVj5GMynRHG3oeOGwvuhJ0ViXKdQLkFe8m4TvDFZbqaxXeju1HQnBdn85zk1tdJt4G0KDK0P380tbHuOiUpVsni5Y9O-flAahykklNt8Zfasphra5qmBXydM_dFChJU90r4MVO8OUYkESgehYO3w7HIH1VAVxcXPDR2IPFhmeVnpl_Ys0XsXBxFolM8bAavDtjOhHi3NyZoDMz5L9b9P7N-H9GvgRD7NTi_xqNu0Oys0sidNFqDDKpR_QWs3qejWz7ioyj0yfJ0MnlYfE6zwXKtLxpPyEDcPx3u7UfmDjfMHYoNcJSOo1WevuOyMX0Vj8fvoiEwjBtakim9oS3YVqjKP_Kn0KOkuIUWShr7sIJa9A2WtNTPHip6NNl3LWmMtocb2neVQEiU8Ga0NK5F4-D5Fx19Szc)

## DPK-Projects
- [REST-Service](https://github.com/trifork/dpk-rest-service): Service implementing the REST API that calling systems will use to send post
- [PDF-Service](https://github.com/trifork/dpk-pdf-service): Service responsible for creating PDFs to be sent to Digital Post or Strålfors based on a template
- [Dispatcher-Service](https://github.com/trifork/dpk-dispatcher): (Cron/Batch) Service responsible for figuring out which letters to send and which specific dispatcher service should send it. Also handles some sub-dispatcher errors
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-straalfors): Service responsible for having PDFs generated for a physical letter and sending it to Strålfors
- [Digital-Post-Services](https://github.com/trifork/dpk-digital-post): Github repository containing all relevant Digital Post services
  - [Digital-Post-Dispatcher-Service](https://github.com/trifork/dpk-digital-post): Service responsible for having PDFs generated for digital post and sending it to Digital Post
  - [Enrollment-Service](https://github.com/trifork/dpk-digital-post) - (Cron/Batch) Service responsible for maintaining Digital Post enrollment lists
  - [Receipt-Service](https://github.com/trifork/dpk-digital-post) - (Cron/Batch) Service responsible for maintaining Digital Post receipts
- [Common-Submodule](https://github.com/trifork/dpk-common-submodule) - Github submodule containing the datamodel (SQL) and protobuf messages
- [Flux](https://github.com/trifork/dpk-flux/) - TCS test/prod repository
- [Docker](https://github.com/trifork/dpk-docker) - Repository hosting a docker-compose setup
- [Test-Data-Generator](https://github.com/trifork/dpk-test-data-generator) - Small service for sending test data

## Technology Used
* **Git** for source control, and **Github** as source repository
* **Github Workflow** for continuous integration
* **Java 21**, **Kotlin 1.9.22** and **Go 1.22** as programming language
* **Maven** for building the Java/Kotlin services
* **Makefile** for easy scripting of Go build and run targets
* **Docker** for containerization
* **Github Container Registry** as docker image repository
* **PostgresDB** for persistence
* **SpringBoot** for Java/Kotlin projects
* **protobuf** and **gRPC** for communication
* **Kubernetes** as the infrastructure environment (hosted at Netic)
* **kubectl** CLI for accessing the Kubernetes cluster and viewing logs

## Continuous integration

We use Github Actions as our continuous integration flow, which triggers build and test runs for every PR created and on the main branch.

The Github workflow, which has been enabled at setup for each repository, will build the source code and run the available unit tests on each branch in the repo.

An overview and status of the workflow runs can be viewed in the `Actions` tab of each project.

## Continuous deployment

We take advantage of the ideas behind [GitOps](https://www.gitops.tech/) for working with CI/CD in the DPK project. 

We use Github Actions and have added a workflow for continuous deployment. So when a new release has been created (manually, from Github Releases) of a given repository, it triggers the Github action for build and deployment of the service.

We use Github Container Registry to store the built release images of the services. The images which are built and are available can be viewed from the `Packages` site on the repository (found in the right hand side of the Code tab).

The deployment process is maintained by [flux](https://fluxcd.io/) using helm charts for deployng docker images to Kubernetes.

## Release procedure

This section describes how to create a new release and publish the built docker image to Github Container Registry automatically:

We use Github actions for managing workflows in the DPK project. This means that the workflow named "Build and test code" is triggered when a pull request is merged to the main branch, and the workflow for building and publishing a Docker image of the service is triggered when a release is created.

### Create a new release

Navigate to the `Releases` section in the Code tab of your Github repo (in the right hand side of the page) and press the `Draft a new release` button. Create a new tag, for example v0.0.7 and add a title for your release, for example `Release v0.0.7`.

Check the check-box `This is a pre-release`, if this is a pre-release version, and then press the `Publish release` button. A release should be marked as pre-release if it's not production ready (or not intended to be deployed directly to production).
