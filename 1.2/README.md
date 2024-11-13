# Домашнее задание к занятию "`Базовые объекты K8S`" - `Сергиенко А. В.`

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

Curl на удаленном хосте  
![curl](https://github.com/SashkaSer/kuber/blob/main/1.2/images/curl.png)` 

---

### Задание 2. Установка и настройка локального kubectl
1. Создать Pod с именем netology-web.  
2. Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.  
Манифест пода
```
apiVersion: v1
kind: Pod
metadata:
  name: netology-web
  labels:
    app: myapp
spec:
  containers:
  - name: echoserver
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```
3. Создать Service с именем netology-svc и подключить к netology-web.  
Манифест сервиса  
```
apiVersion: v1
kind: Service
metadata:
  name: netology-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```
4. Подключиться локально к Service с помощью kubectl port-forward и вывести значение (curl или в браузере).  
![forward](https://github.com/SashkaSer/kuber/blob/main/1.2/images/forward.png)`  

Подключение с удаленной машины  
![connect](https://github.com/SashkaSer/kuber/blob/main/1.2/images/curl2.png)`

Манифесты лежат в Git рядом с ридми
