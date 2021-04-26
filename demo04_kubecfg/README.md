# Kubcfg

### Рассказываем, что есть jsonnet шаблон из которого генерируется yaml конфигурация.

### Смотрим сгенерированную конфигурацию:
wget https://github.com/bitnami/kubecfg/releases/download/v0.18.0/kubecfg-linux-amd64 \
chmod +x kubecfg-linux-amd64 \
mv kubecfg-linux-amd64 /usr/sbin/kubecfg

kubecfg show workers.jsonnet

### Применяем

kubecfg update workers.jsonnet
http://localhost:40541/api/v1/namespaces/default/services/http:worker01:8000/proxy/

### Смотрим node port и идем в браузер

<!-- kubectl get svc
kubectl get nodes -o wide
gcloud compute firewall-rules create test-node-port --allow tcp:31070
minikube: minikube service worker01 -->

### Добавляем второй worker

### Применяем

kubecfg update workers.jsonnet

### Смотрим node port и идем в браузер
http://localhost:40541/api/v1/namespaces/default/services/http:worker02:8000/proxy/
<!-- kubectl get svc
kubectl get nodes -o wide -->