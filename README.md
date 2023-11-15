# Kyma community modules

## Overview

Install Kyma modules in your Kubernetes cluster

## Prerequisites

- kubectl
- kubernetes cluster (KUBECONFIG configured)
- kyma-system namespace created (some modules installation can fail without it)

## Installation

Download [kyma.html](https://raw.githubusercontent.com/kyma-project/community-modules/main/app/kyma.html) file and save it in any folder:
```
curl https://kyma-project.github.io/community-modules/kyma.html -o kyma.html
```
Go to that folder and execute kubectl proxy command:
```
kubectl proxy -w='.'
```
Open Web UI with this link: [http://127.0.0.1:8001/static/kyma.html](http://127.0.0.1:8001/static/kyma.html)


## Contribute your module

Checkout the community-modules repository and add your own module by adding an entry in the [channels.json](app/channels.json) file. Example:
```
    {
      "name": "api-gateway",
      "deploymentYaml": "https://github.com/kyma-project/api-gateway/releases/latest/download/api-gateway-manager.yaml",
      "crYaml": "https://github.com/kyma-project/api-gateway/releases/latest/download/apigateway-default-cr.yaml",
      "documentation": "https://kyma-project.io/#/api-gateway/user/README",
      "repository": "https://github.com/kyma-project/api-gateway.git",
      "managedResources": [
        "/apis/operator.kyma-project.io/v1alpha1/apigateways",
        "/apis/gateway.kyma-project.io/v1beta1/apirules"
      ]
    },
```
Mandatory fields:
- **name** - name of your module (keep it short)
- **deploymentYaml** - URL of your module deployment YAML (usually the artifact of your module release)
- **crYaml** - URL of your module default configuration (custom resource)
- **documentatio** - documentation URL
- **repository** - main source code repository
- **managedResources** - list of api server resources (paths) that are managed by your module (including the configuration resource)

The channels.json file is processed by the build process and generates release channels files (right now only latest release is generated: [https://kyma-project.github.io/community-modules/latest.json](https://kyma-project.github.io/community-modules/latest.json)
If you want to test your module, you can generate that file on your own:
```
cd script
npm install
cd ../app
node ../script/release-channels.js
```
The latest.json file should be created. To test the UI with this file just add `channel` query parameter pointing to the desired channel: [http://127.0.0.1:8001/static/kyma.html?channel=latest.json](http://127.0.0.1:8001/static/kyma.html?channel=latest.json)

For standard contribution rules see [CONTRIBUTING.md](CONTRIBUTING.md).

## Code of Conduct
<!--- mandatory section - do not change this! --->

See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## Licensing
<!--- mandatory section - do not change this! --->

See the [LICENSE file](./LICENSE).
