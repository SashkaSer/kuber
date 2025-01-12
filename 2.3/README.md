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
### Задание 2 Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода.
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

NFS-сервер на MicroK8S настроен согласно https://microk8s.io/docs/how-to-nfs

Как видно из скриншота PV создался автоматически через SC на сервере NFS
![createpvviasc](https://github.com/SashkaSer/kuber/blob/main/2.2/img/createpvviasc.png)`  

Видно, что multitool может читать данные из общей директории, а так же данный доступны локально на машине  
![datafromsc](https://github.com/SashkaSer/kuber/blob/main/2.2/img/datafromsc.png)`  

Манифесты к заданию 1 лежат в manifests/task2