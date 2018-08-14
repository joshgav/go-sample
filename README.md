# Web App

Continuously build and deploy a Go web app using Azure App Service and Azure
Container Registry.

This package includes a basic Go web app and scripts to set up infrastructure
for it in Azure.

Requires [Azure CLI][].

## Try It!

Set configuration in a local .env file in the package root by copying
`.env.tpl` to `.env`. Then run ./[setup.sh][] to build and deploy your container
to Container Registry and App Service.

If run within the Azure Go SDK samples repo, this will run a one-off build and
push to your registry, which will trigger refresh of the App Service Web App.

If instead run from your own repo, you can specify an image name in
`IMAGE_NAME` (in `.env`) to match your GitHub 'org/repo' structure and setup.sh
will also arrange continuous build and deploy for you.  To try it, after
setting things up, make a change and push it to your repo.  Container Registry
build tasks should detect the change, rebuild your container, and notify App
Service; which should then refresh and reload your container image.

## More Details

[setup.sh][] ensures an Azure resource group, container registry, app service
plan, and container-based web app are provisioned and connected in the
subscription currently logged in to [Azure CLI][].

It uses the following environment variables to choose names:

* IMAGE\_NAME: Name of container image (aka "repo").
* IMAGE\_TAG: Tag for container image.
* AZURE\_BASE\_NAME: Prefix for Azure resources.
* AZURE\_DEFAULT\_LOCATION: Location for Azure resources. 

These names can be specified in a .env file in the root of the package. If a
`.env` file isn't found, `.env.tpl` is copied to `.env` and used.

Explicit parameters can also be passed, see comments at beginning of
[setup.sh][] for details.

[Azure CLI]: https://github.com/Azure/azure-cli
[setup.sh]: ./setup.sh
