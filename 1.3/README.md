# Домашнее задание к занятию "`Запуск приложений в K8S`" - `Сергиенко А. В.`

### Задание 1 Создать Deployment и обеспечить доступ к репликам приложения из другого Pod
1. Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool. Решить возникшую ошибку.
2. После запуска увеличить количество реплик работающего приложения до 2.
3. Продемонстрировать количество подов до и после масштабирования.  
До масштабирования, запущена одна реплика и один под
![before](https://github.com/SashkaSer/kuber/blob/main/1.3/img/before.png)`  

Увеличиваю количество реплик до двух через правку манифеста
![after](https://github.com/SashkaSer/kuber/blob/main/1.3/img/after.png)`  

4. Создать Service, который обеспечит доступ до реплик приложений из п.1.
```
apiVersion: v1
kind: Service
metadata:
  name: pod-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      name: nginx
      port: 80
      targetPort: 80
    - protocol: TCP
      name: multitool
      port: 8080
      targetPort: 8080
```  
![service](https://github.com/SashkaSer/kuber/blob/main/1.3/img/service.png)`

5. Создать отдельный Pod с приложением multitool и убедиться с помощью curl, что из пода есть доступ до приложений из п.1.

При запросе 80 порта отвечает Nginx
![nginx](https://github.com/SashkaSer/kuber/blob/main/1.3/img/nginx.png)`  

При запросе 8080 порта отвечает multitool
![nginx](https://github.com/SashkaSer/kuber/blob/main/1.3/img/multitool.png)`  

Манифесты к заданию 1 лежат в manifests/task1

---
### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

1. Создать Deployment приложения nginx и обеспечить старт контейнера только после того, как будет запущен сервис этого приложения.
2. Убедиться, что nginx не стартует. В качестве Init-контейнера взять busybox.  
Как видим под не запущен и находится в статусе init, хотя проверка проходит каждые 2 секунды в busybox
![init](https://github.com/SashkaSer/kuber/blob/main/1.3/img/init.png)`
3. Создать и запустить Service. Убедиться, что Init запустился.  
Создаю и запускаю service.
![nslookup](https://github.com/SashkaSer/kuber/blob/main/1.3/img/nslookup.png)

Не с первого раза получилось добиться ответа от DNS, методом эксперимента понял, что нужно добавлять доменное имя default.svc.cluster.local
3. Продемонстрировать состояние пода до и после запуска сервиса.
Сделал тоже самое но после отладки, видно что практически сразу же после поднятия сервиса init контейнер смог зарезолвить имя и запустился уже nginx  
![nslookup2](https://github.com/SashkaSer/kuber/blob/main/1.3/img/nslookup2.png)