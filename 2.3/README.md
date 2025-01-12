# Домашнее задание к занятию "`Конфигурация приложений`" - `Сергиенко А. В.`

### Задание 1. Создать Deployment приложения и решить возникшую проблему с помощью ConfigMap. Добавить веб-страницу
1. Создать Deployment приложения, состоящего из контейнеров nginx и multitool.
2. Решить возникшую проблему с помощью ConfigMap.
3. Продемонстрировать, что pod стартовал и оба конейнера работают.
4. Сделать простую веб-страницу и подключить её к Nginx с помощью ConfigMap. Подключить Service и показать вывод curl или в браузере.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.  

Порт для multitool переопределен с помощью ConfigMap. Вырезка из Deployment
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: multitool-port
data:
  port: "8080"

#Вырезка из Deployment
containers:
    - name: multitool
        image: praqma/network-multitool
        ports:
            - containerPort: 8080
        env:
        - name: HTTP_PORT
          valueFrom:
            configMapKeyRef:
                name: multitool-port
                key:port
```
Оба контейнера запущены  
![pods](https://github.com/SashkaSer/kuber/blob/main/2.3/img/pods.png)`  

Кастомная веб страница с помощью ConfigMap
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config-map
data:
  index.html: |
    <html>
    <h1>Hello from netology</h1>
    </br>
    <h1>| Sergienko_A.</h1>
    </html>
#Вырезка из Deployment
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
      volumeMounts:
        - name: nginx-config-map
            mountPath: /usr/share/nginx/html
volumes:
    - name: nginx-config-map
      configMap:
        name: nginx-config-map
```

Кастомная страница доступа  
![web](https://github.com/SashkaSer/kuber/blob/main/2.3/img/web.png)` 

Запущенные объекты  
![kinds](https://github.com/SashkaSer/kuber/blob/main/2.3/img/kinds.png)` 

Манифесты к заданию 1 лежат в manifests/task1

---
### Задание 2 Создать приложение с вашей веб-страницей, доступной по HTTPS
1. Создать Deployment приложения, состоящего из Nginx.
2. Создать собственную веб-страницу и подключить её как ConfigMap к приложению.
3. Выпустить самоподписной сертификат SSL. Создать Secret для использования сертификата.
4. Создать Ingress и необходимый Service, подключить к нему SSL в вид. Продемонстировать доступ к приложению по HTTPS.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

Кастомная веб страница с помощью ConfigMap
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-page
data:
  index.html: |
    <html>
    <h1>Hello from netology. This is HTTPS</h1>
    </br>
    <h1>| Sergienko_A.</h1>
    </html>   
#Вырезка из Deployment
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
          volumeMounts:
            - name: page
              mountPath: /usr/share/nginx/html
      volumes:
        - name: page
          configMap:
            name: nginx-page
```

Созданный серкет, помещенный в Ingress  
![secret](https://github.com/SashkaSer/kuber/blob/main/2.3/img/secret.png)` 

```
  tls:
    - hosts:
        - useful-quarter.aeza.network
      secretName: web-tls
```