# Домашнее задание к занятию "`Резервное копирование баз данных`" - `Пешкин Евгений`

### Задание 1.
1.1.Необходимо восстанавливать данные в полном объёме за предыдущий день.

#### Ответ

Фул бэкап – инкрементный бэкап
<br/>
<br/>
Полный бэкап предоставит полный снимок данных на начало периода, а инкрементный бэкап зафиксирует все изменения произошедшие
<br/>
с данными после последнего бэкапа таким образом мы можем сделать полный бэкап в начале недели, 
<br/>
а затем продолжить делать ежедневные инкрементные бэкапы в течении остальных дней недели.
<br/>
Важно то что нам нужно будет восстановить последний полный бэкап и все последующие инкрементные 
<br/>
бэкапы сделанные до конца предыдущего дня именно так мы получим состояние данных на конец предыдущего дня в полном объеме
<br/>
<br/>
<br/>
1.2.Необходимо восстанавливать данные за час до предполагаемой поломки.
<br/>

#### Ответ

Полный бэкап в начале недели – Ежедневный дифференциальный бэкап – инкрементный бэкап каждый час
<br/>
<br/>
Полный бэкап в начале недели – Данный бэкап служит основой и содержит полную копию данных на момент его выполнения
<br/>
<br/>
Ежедневный дифференциальный бэкап – Ежедневное создание дифференциального бэкапа позволит
<br/>
нам зафиксировать изменения произошедшие с данными за день 
<br/>
<br/>
Инкрементный бэкап каждый час - Инкрементный бэкап резервирует только измененные данные с момента последнего бэкапа.
<br/>
Проведение инкрементного бэкапа каждый час позволит минимизировать потерю данных в случае возникновения проблем.

### Задание 2 PostgreSQL

#### Ответ

Cоздание дампа:
<br/>
pg_dump [connection-option...] [option...] [dbname]
<br/>
<br/>
Пример выгрузки базы данных mydb в файл SQL-Скрипта
<br/>
pg_dump mydb > db.sql
<br/>
<br/>
Восстановление дампа:
<br/>
pg_restore [connection-option...] [option...] [filename]
<br/>
Потом мы должны сконвертировать файл резервной копии в бинарный формат db.dump
<br/>
pg_dump -Fc mydb > db.dump
<br/>
<br/>
И теперь мы можем восстановить нашу базу данных
pg_restore -C -d databasename db.dump


### Задание 3 MySQL

#### Ответ

mysqlbackup --defaults-file=/home/dbadmin/my.cnf \
<br/>
  --incremental --incremental-base=history:last_backup \
<br/>
  --backup-dir=/home/dbadmin/temp_dir \
<br/>
  --backup-image=incremental_image1.bi \
<br/>  
 backup-to-image
 
