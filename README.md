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
