# ArgoCD "Chart of Charts"

Once ArgoCD is installed, run the bootstrap for the desired environment:

```sh
helm install argo-cd-bootstrap bootstrap --set environment=dev # for dev
```

This deploys an application for the apps defined in the `argo-cd` directory.  Any future additions or changes to this `argo-cd` directory are then updated in ArgoCD automatically.

The `argo-cd` application definition pass the environment variable to the applications defined in the `apps` directory, which then have a relevant `ENV.yaml` with the charts values for the environment. Updating these files will reflect in the relevant environment.
