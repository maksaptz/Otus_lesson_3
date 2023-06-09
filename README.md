# Файловые системы и LVM

## Цель домашнего задания:
 - облегчить себе жизнь управления файловыми системами;
 - архитектура файловой системы Linux: суперблок, блоки, inodes, журналы;
 - разобраться в многообразии файловых систем.

В работе использовалася vagrant box: "centos/7" version "1804.02".

Описание домашнего задания:
1) уменьшить том под / до 8G;
2) прописать монтирование в fstab;
3) выделить том под /var;
4) работа со снапшотами:
    - home - сделать том для снэпшотов
    - сгенерировать файлы в /home/
    - снять снэпшот
    - удалить часть файлов
    - восстановиться со снэпшота

### Уменьшить том под / до 8G
Для выполнения поставленной задачи нам необходимо создать временный том, скопировать на него всю информацию и сконфигурировать загрузичик для того, чтобы запуститься с временного тома. После перзагрузки мы уменьшаем исходный том, и в обратном порядке переносим информацию.
### Прописать монтирование в fstab
Пример команды для настройки автомонтирования:

```echo "`blkid | grep var: | awk '{print $2}'` /var ext4 defaults  
 0 0" >> /etc/fstab```
### Выделить том под /var
Тот же алгоритм действий как и при уменьшении тома. Еденственное отличие заключается в том, что для хранения каталога /var будем использовать lvm зеркало настроенное на 2 физических томах.
### Работа со снапшотами
На выделенный том переносим католог /home. Генерируем файлы и создаем снэпшот. Удаляем файлы и пробуем откатиться.

#### typescript файлы содержат вывод команд с поясняющими комментариями!
