# Install helm

curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

# Install public charts

## ops-view and harbor
- check ssh-tunnel
- check kubectl proxy
- check kubectl

1. # add repos
helm repo add stable https://charts.helm.sh/stable &&
helm repo add incubator https://charts.helm.sh/incubator &&
helm repo add harbor https://helm.goharbor.io &&
helm repo update

2. # inspect values
helm inspect values stable/kube-ops-view > kube-ops-view.yaml
vim kube-ops-view.yaml:
- rbac: true
- ingress: true

3. # install ops-view chart
helm install ops-view --namespace kube-system stable/kube-ops-view -f kube-ops-view.yaml

4. # check UI
http://localhost:8001/api/v1/namespaces/kube-system/services/http:ops-view-kube-ops-view:/proxy/

5. # pull harbor chart
helm pull harbor/harbor --untar

6. # inspect harbor values
vim harbor/values.yaml

7. # install harbor chart
kubectl create ns harbor &&
helm upgrade --install harbor harbor/harbor --namespace harbor

8. # check UI
http://localhost:8001/api/v1/namespaces/harbor/services/http:harbor-harbor-portal:/proxy

9. # delete harbor chart and check UI
helm delete harbor -n harbor

10. # delete ops-view ui
<!-- helm delete ops-view -n kube-system -->