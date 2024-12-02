# Домашнее задание к занятию "`Сетевое взаимодействие в K8S. Часть 2`" - `Сергиенко А. В.`

### Задание 1 Создать Deployment приложений backend и frontend
1. Создать Deployment приложения frontend из образа nginx с количеством реплик 3 шт.
2. Создать Deployment приложения backend из образа multitool.
3. Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера.
4. Продемонстрировать, что приложения видят друг друга с помощью Service.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.   

Запущенные поды, деплойменты и сервисы
![podservice](https://github.com/SashkaSer/kuber/blob/main/1.4/img/podservice.png)`  

При запросе на порт 9001 отвечает Nginx, а при запросе на 9002 отвечает multitool
![nginx](https://github.com/SashkaSer/kuber/blob/main/1.3/img/nginx.png)`  

![multitool](https://github.com/SashkaSer/kuber/blob/main/1.3/img/multitool.png)`

Манифесты к заданию 1 лежат в manifests/task1

---
### Задание 2. Создать Service и обеспечить доступ к приложениям снаружи кластера

1. Создать отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort.
2. Продемонстрировать доступ с помощью браузера или curl с локального компьютера.
3. Предоставить манифест и Service в решении, а также скриншоты или вывод команды п.2.
  
![nginx](https://github.com/SashkaSer/kuber/blob/main/1.4/img/nginxnp.png)  
![multitool](https://github.com/SashkaSer/kuber/blob/main/1.4/img/multitoolnp.png)

Манифест деплоймента такой же как и в задании 1. Манифест сервиса в manifests/task2