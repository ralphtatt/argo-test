# ArgoCD "Chart of Charts"

## Setting up ArgoCD

Install ArgoCD (https://argo-cd.readthedocs.io/en/stable/operator-manual/installation/):

```sh
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm upgrade --install argocd argo/argo-cd \
  --namespace argocd \
  --create-namespace
```

Now you can connect to the server:

```sh
# Open port forward to 
kubectl port-forward service/argocd-server -n argocd 8080:443

# Get admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Applying Configuration

```sh
helm upgrade --install argo-cd-bootstrap bootstrap\
  --namespace argocd \
  --create-namespace \
  --set environment=dev
```

This deploys an application for the apps defined in the `argo-cd` directory.  Any future additions or changes to this `argo-cd` directory are then updated in ArgoCD automatically.

The `argo-cd` application definition pass the environment variable to the applications defined in the `apps` directory, which then have a relevant `ENV.yaml` with the charts values for the environment. Updating these files will reflect in the relevant environment.
