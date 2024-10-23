# jupyterhub-cluster-config 
This repo contains the configuration files for the Jupyterhub cluster setup based on kubernetes, [jupyterhub helm chart](https://jupyterhub.github.io/helm-chart/) and [fluxcd](https://fluxcd.io/flux/components/kustomize/kustomizations/) as gitops tool.

Our approach is to have a single jupyterhub cluster with user-dedicated IDEs in own pods for specific projects. The login in SSO via Azure Devops. Relevant credentials are deployed via Environment Variables on the Pods itself. 

## Howto use Jupyter

## Login
Go to: https://jupyter.analyticsinternal.iunera.com
Log in with azure ad

## Choose a Profile
* iunera Datascience environment

# How to use git

## Configure credential helper
Open a Terminal in your Jupyter Notebook `File->new->Terminal`

Add the following command line
```
git config --global credential.helper store
```

## Cluster Configuration 
Can be found [jupyterhub.helm.yaml](kubernetes/jupyterhub/jupyterhub.helm.yaml) 

### Provide the following secrets

* singleuser-secrets.yaml

```
apiVersion: v1
kind: Secret
metadata:
  name: singleuser-secrets
  namespace: jupyterhub
type: Opaque
stringData:
  s3_access_key_id: 
  s3_access_key_secret: 
  s3_endpoint: 
```

* custom-hub-secrets.yaml
```

apiVersion: v1
kind: Secret
metadata:
  name: custom-hub-secrets
  namespace: jupyterhub
type: Opaque
stringData:
  hub.config.ConfigurableHTTPProxy.auth_token: 
  hub.config.JupyterHub.cookie_secret: 
  client_id: 
  client_secret: 
  tenant_id: 
  oauth_callback_url: https://<domain>/hub/oauth_callback
```

## IDEs 
To provide more features and libs by default we have extended the `jupyter/datascience-notebook` container image in the [Dockerfile](docker/datascience-notebook/Dockerfile)

### Customize Images
You might need some additional Libs installed. You can just do this inside your environment (`File->new->Terminal`) using pip or conda.
If you want to change the notebook images here e.g. the `datascience-notebook` create a branch and extend the `Dockerfile`. The Jupyterhub entry `iunera Datascience environment LATEST-DEV IMAGE` always pulls the latest image build from a branch.

If you are done send a Pull Request.

The new Stable Image needs to be applied.
