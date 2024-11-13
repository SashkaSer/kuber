# Домашнее задание к занятию "`Kubernetes. Причины появления. Команда kubectl`" - `Сергиенко А. В.`

### Задание 1
1. Создать манифест (yaml-конфигурацию) Pod.
2. Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Подключиться локально к Pod с помощью kubectl port-forward и вывести значение (curl или в браузере).  

Манифест
```
apiVersion: v1
kind: Pod
metadata:
  name: echoserver
spec:
  containers:
  - name: echoserver
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```
![port](https://github.com/SashkaSer/kuber/blob/main/1.2/images/portforward.png)`
---

### Задание 2. Установка и настройка локального kubectl
1. Установить на локальную машину kubectl.  
![kubectl](https://github.com/SashkaSer/kuber/blob/main/1.1/images/kubctl_win.png)`
3. Настроить локально подключение к кластеру.
Удаленное подключение к кластеру  
![getnodes](https://github.com/SashkaSer/kuber/blob/main/1.1/images/getnodes.png)`
3. Подключиться к дашборду с помощью port-forward.
Подключение к дашборду  
![dashboard](https://github.com/SashkaSer/kuber/blob/main/1.1/images/dashboard.png)`  
