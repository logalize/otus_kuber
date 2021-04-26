# Helm

### Показываем набор манифестов из socks-shop в all.yaml

### Создаем заготовку helm-chart

helm create socks-shop

### Показываем что создалось после инициализации
### Удаляем ненужное

rm -rf socks-shop/templates/*
rm -rf socks-shop/values.yaml

### Переносим all.yaml в templates

cp all.yaml socks-shop/templates/
cp values.yaml socks-shop/

### Проверяем resources
helm template .

### Устанавливаем release
kubectl create ns socks-shop

helm upgrade --install socks-shop ./socks-shop --namespace socks-shop
kubectl get pods -n socks-shop -w
http://localhost:8001/api/v1/namespaces/socks-shop/services/http:front-end:/proxy

### Идем на адрес любой ноды и проверяем, что магазин работает
http://localhost:8001/api/v1/namespaces/socks-shop/services/http:front-end:/proxy
<!-- gcloud compute firewall-rules create sock-shop --allow tcp:<port> -->

<!-- ### Вытаскиваем frontend в отдельный чарт

helm create frontend

Меняем:

* containerPort в шаблоне deployment на 8079
* ingress в values на frontend.IP.nip.io + другие настройки ingress (ниже)
* параметры image (ниже)

```yaml
ingress:
  enabled: true
  annotations:
    kubernetes.io/ingress.class: nginx
  hosts:
    - host: frontend.IP.nip.io
      paths:
        - /

image:
  repository: weaveworksdemos/front-end
  tag: 0.3.12
  pullPolicy: IfNotPresent
```

### Удаляем манифесты про frontend из all и переустанавливаем chart socks-shop

helm upgrade --install socks-shop ./socks-shop --namespace socks-shop

### Устанавливаем frontend

helm upgrade --install frontend ./frontend --namespace socks-shop

### Идем через ingress и проверяем, что frontend развернулся

### Генерируем документацию

helm-docs md frontend -->

### Пакуем в tgz

helm package socks-shop
helm delete socks-shop --namespace socks-shop