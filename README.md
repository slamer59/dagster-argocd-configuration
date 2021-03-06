# dagster-argocd-configuration

https://github.com/dagster-io/dagster/issues/3099

https://blog.filador.fr/argo-cd-la-gestion-simplifiee-de-vos-deploiements-sur-kubernetes/

## [Microk8s](https://microk8s.io/)

```bash
sudo snap install microk8s --classic 
sudo usermod -a -G microk8s thomas
sudo chown -f -R thomas ~/.kube
newgrp microk8s
microk8s enable dashboard dns registry istio 
```

Changement port 16443 -> 8443
[Change port](https://docs.onepanel.ai/docs/deployment/configuration/remote-microk8s/)

## ArgoCD

### Installation

```bash
cd charts\argocd
kubectl create namespace argocd
helm dependency update
helm install --version 2.2.2 argocd . -f .\values.yaml
```

or

``bash
helm repo add argo-cd https://argoproj.github.io/argo-helm
helm dep update charts/argo-cd/
``

### First password

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

### Add helm repo to argoCD

First login
argocd login localhost:8080 --username admin --password 
somepassword
argocd repo add https://charts.bitnami.com/bitnami --type helm --name bitnami --server "localhost:8080" --insecure

![Helm repos](docs/images/helm-repo.png)

https://argo-cd.readthedocs.io/en/latest/user-guide/commands/argocd_repo_add/

## Dagster with helm
https://docs.dagster.io/deployment/guides/kubernetes/deploying-with-helm

<!-- $ helm repo add dagster https://dagster-io.github.io/helm -->

## Jupyterhub
Si effectué sans argocd:

``helm upgrade --cleanup-on-fail --install jupyterhub jupyterhub/jupyterhub  --namespace jupyterhub --create-namespace -f values.yaml``

(Zero to Jupyterhub)[https://zero-to-jupyterhub.readthedocs.io/en/latest/jupyterhub/installation.html]

## [n8n](https://n8n.io/)

Extendable workflow automation [with all plugins.](https://n8n.io/integrations)