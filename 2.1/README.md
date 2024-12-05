# Домашнее задание к занятию "`Хранение в K8s. Часть 1`" - `Сергиенко А. В.`

### Задание 1 Создать Deployment приложения, состоящего из двух контейнеров и обменивающихся данными.
1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Сделать так, чтобы busybox писал каждые пять секунд в некий файл в общей директории.
3. Обеспечить возможность чтения файла контейнером multitool.
4. Продемонстрировать, что multitool может читать файл, который периодоически обновляется.
5. Предоставить манифесты Deployment в решении, а также скриншоты или вывод команды из п. 4.

busybox каждые 5 секунд пишет дату и время в файл /test/test.txt
```
command: ['sh', '-c', 'while true; do echo {`date`} >> ./test/test.txt; sleep 5; done;']
```
multitool имеет доступ к этому файлу через общий Volume
![file](https://github.com/SashkaSer/kuber/blob/main/2.1/img/date.png)`  

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

Манифест деплоймента такой же как и в задании 1. Манифест ingress в manifests/task2