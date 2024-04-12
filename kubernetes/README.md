jupyterhub                      https://jupyterhub.github.io/helm-chart/


helm repo add jupyterhub https://hub.jupyter.org/helm-chart/



singleuser-secrets.yaml

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

custom-hub-secrets.yaml
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


helm upgrade --cleanup-on-fail \
  --install jupyterhub jupyterhub/jupyterhub \
  --namespace jupyterhub \
  --create-namespace \
  --version=3.3.7 \
  --values config.yaml




Node Labeling

# label your Core Instances (hub, proxy, etc)
kubectl label node cnode1 hub.jupyter.org/node-purpose=core --overwrite
kubectl label node cnode2 hub.jupyter.org/node-purpose=core --overwrite
kubectl label node cnode3 hub.jupyter.org/node-purpose=core --overwrite

# label your user node instances
kubectl label node cnode14 hub.jupyter.org/node-purpose=user --overwrite
kubectl label node cnode15 hub.jupyter.org/node-purpose=user --overwrite
kubectl label node cnode9 hub.jupyter.org/node-purpose-
