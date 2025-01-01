# Домашнее задание к занятию "`Хранение в K8s. Часть 1`" - `Сергиенко А. В.`

### Задание 1 Cоздать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории.
4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV. Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
6. Предоставить манифесты, а также скриншоты или вывод необходимых команд.  

Созданный Pod, PV и PVC
![podpvpvc](https://github.com/SashkaSer/kuber/blob/main/2.2/img/podpvpvc.png)`  

Манифесты к заданию 1 лежат в manifests/task1

---