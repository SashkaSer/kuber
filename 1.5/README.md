# Домашнее задание к занятию "`Сетевое взаимодействие в K8S. Часть 2`" - `Сергиенко А. В.`

### Задание 1 Создать Deployment приложений backend и frontend
1. Создать Deployment приложения frontend из образа nginx с количеством реплик 3 шт.
2. Создать Deployment приложения backend из образа multitool.
3. Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера.
4. Продемонстрировать, что приложения видят друг друга с помощью Service.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.   

Запущенные поды, деплойменты и сервисы
![podservice](https://github.com/SashkaSer/kuber/blob/main/1.5/img/podservice.png)`  

Манифесты к заданию 1 лежат в manifests/task1

---
### Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

1. Включить Ingress-controller в MicroK8S.  
![ingress](https://github.com/SashkaSer/kuber/blob/main/1.5/img/ingressnginx.png)` 
2. Создать Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался frontend а при добавлении /api - backend.
3. Продемонстрировать доступ с помощью браузера или curl с локального компьютера.  

Запрос на http://sergienko-kuber.com/
![nginx](https://github.com/SashkaSer/kuber/blob/main/1.5/img/nginx1.png)`  

![nginx2](https://github.com/SashkaSer/kuber/blob/main/1.5/img/nginx2.png)`  

Запрос на http://sergienko-kuber.com/api
![multitool](https://github.com/SashkaSer/kuber/blob/main/1.5/img/multitool1.png)`  

![multitool2](https://github.com/SashkaSer/kuber/blob/main/1.5/img/multitool2.png)`  

4. Предоставить манифесты и скриншоты или вывод команды п.2.

Манифест деплоймента такой же как и в задании 1. Манифест сервиса в manifests/task2