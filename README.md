# MLOps-homework-k8s
Результаты домашней работы по модулу MLOps, занятие "Kubernetes (к8s)"

# Ответы на вопросы

1. Что такое k8s?

Это платформа для упарвлениями контейнерами. Поддерживает автоматизацию и декларативную настройку

2. В чём преимущество контейнеризации над виртуализацией?

Контейнеры создаются под конкретные задачи, поэтому они занимают меньше и не конкурируют за ресурсы. Контейнеры не требовательны к железу, а также имею бОльшую изоляцию, что положительно сказывается на безопасности

3. В чём состоит принцип самоконтроля k8s?

Принцип самоконтроля заключается в том, что Kubernetes может подстраивать количество контейнеров под нагрузку в рамках, заданных пользователем. Также платформа следит за состоянием контейнеров и в случае необходимости может их остановить или перезагрузить

4. Как вы думаете, зачем Вам понимать принципы деплоя в k8s?

Data Engineers могут использовать Kubernetes для развертывания пайплайнов, потоковой обработки данных, хранения и обработки данных в распределенных системах, а также для автоматизации развёртывания моделей машинного обучения и API.

5. Какое из средств управления секретами наиболее распространено в использовании совместно с k8s?

HashiCorp Vault. Также используются встроенные Kubernetes Secrets, которые позволяют безопасно хранить пароли, токены API и сертификаты. 
      
6. Какие типы нод есть в k8s, каковы их базовые функции?

Master Node (Control Plane) — управляет кластером, включает API Server, Scheduler, Controller Manager и etcd; Worker Node — запускает поды с контейнерами, включает Kubelet, Kube Proxy и контейнерный runtime; Edge Node (необязательный) — используется для периферийных вычислений в IoT.

# Написать манифест, который будет содержать в себе следующие условия: ● apiVersion – v1 ● название – netology-ml ● внутри него сервер приложений tomcat версии 8.5.69 с портом 8080 ● наличие 2 реплик ● использование стратегии rollingupdate
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: netology-ml
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - image: tomcat:8.5.69
          name: tomcat
          ports:
            - containerPort: 8080
```
