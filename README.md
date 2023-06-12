# hw_10-3_rsync
HW_10-2_Резервное копирование

# Домашнее задание к занятию 3 "Резервное копирование"

### Задание 1

1. Команда **Rsync**, которая позволяет создавать зеркальную копию **/home/mityaevg** в расположении **/tmp/backup**:
```
mityaevg@rsync-server1:~$ rsync -a --progress --delete /home/mityaevg /tmp/backup
```
2. Добавим исключение из синхронизации всех скрытых директорий (начинающихся с ".") и удаление уже добавленных:
```
mityaevg@rsync-server1:~$ rsync -a --progress --delete --exclude=".*/" --delete-excluded . /tmp/backup
```
3. Добавим проверку контрольных сумм файлов:
```
mityaevg@rsync-server1:~$ rsync -a --progress --delete --exclude=".*/" --delete-excluded --checksum . /tmp/backup
```

<kbd>![Выполнение команды из Задания 1](img/assignment1_command.png)</kbd>

<kbd>![Результат выполнения команды из Задания 1](img/assignment1_command_result.png)</kbd>

### Задание 2

Создадим скрипт файл **my_rsync_job.sh**, который будет осуществлять резервное копирование домашней директории пользователя
**/home/mityaevg** в **/tmp/backup**:
```
#!/bin/bash
if $(rsync -a --delete --exclude=".*/" --delete-excluded --checksum /home/mityaevg /tmp/backup); then
echo "$(date) RSYNC: Резервная копия домашней директории пользователя создана успешно" >> /var/log/syslog; else
echo "$(date) RSYNC: Не удалось создать резервную копию домашней директории пользователя" >> /var/log/syslog
fi
```
Результат выполнения резервного копирования будет записан в системный журнал **/var/log/syslog**.

Создадим расписание выполнения задания с помощью **Cron** - **ежедневно в 14:55**:
```
crontab -e
```
<kbd>![Создание расписания в Cron](img/crontab.png)</kbd>

Скриншот, на котором с результатом работы утилиты:

<kbd>![Запись RSYNC из системного журнала](img/rsync_syslog.png)</kbd>


