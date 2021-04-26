# Kustomize

kustomize build overlays/dev

kubectl kustomize overlays/dev

kustomize build overlays/prod

kubectl kustomize overlays/prod

kubectl create ns dev
kubectl apply -k overlays/dev

kubectl get svc -n dev
http://localhost:40541/api/v1/namespaces/dev/services/http:dev-nginx:/proxy/