# Task2

## Файлы
- `deployment.yaml` — Deployment с 1 репликой и лимитом памяти `30Mi`.
- `service.yaml` — Service для доступа к приложению.
- `hpa.yaml` — HPA по памяти с target `80%`, max replicas `10`.
- `locustfile.py` — сценарий нагрузки Locust.

## Команды запуска
```bash
minikube start
minikube addons enable metrics-server

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml

kubectl get pods -w
kubectl get hpa -w
```

## Нагрузка
1. Узнать URL сервиса:
```bash
minikube service scaletestapp --url
```
2. Запустить Locust из директории `Task2`:
```bash
locust --host=http://<SERVICE_URL>
```
3. Открыть интерфейс Locust: `http://localhost:8089`.

## Проверка масштабирования
```bash
kubectl top pod
kubectl describe hpa scaletestapp
kubectl get deployment scaletestapp
```
