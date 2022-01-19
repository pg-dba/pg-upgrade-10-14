# docker-postgres-upgrade 10 to 14

https://github.com/tianon/docker-postgres-upgrade

# Run

ls -la /data/postgres<BR>
 drwxr-xr-x 4  999 docker 4096 Jan 18 18:32 10<BR>
 drwxr-xr-x 3  999 docker 4096 Jan 18 18:22 14<BR>

cd /data/postgres/<BR>
docker run --rm  -v /data/postgres:/var/lib/postgresql sqldbapg/pg-upgrade:10-to-14 --link

Your installation contains extensions that should be updated<BR>
with the ALTER EXTENSION command.  The file<BR>
    update_extensions.sql<BR>
when executed by psql by the database superuser will update<BR>
these extensions.


Upgrade Complete<BR>
----------------<BR>
Optimizer statistics are not transferred by pg_upgrade.<BR>
Once you start the new server, consider running:<BR>
    /usr/lib/postgresql/14/bin/vacuumdb --all --analyze-in-stages<BR>

Running this script will delete the old cluster's data files:<BR>
    ./delete_old_cluster.sh

# Изменения
https://postgrespro.ru/docs/postgresql/11/release-11.html#id-1.11.6.19.4<BR>
pg_dump теперь выгружает и свойства базы данных, а не только её содержимое

https://postgrespro.ru/docs/postgresql/12/release-12.html#id-1.11.6.14.4<BR>
Ликвидация специальных столбцов oid<BR>
Удаление типов данных abstime, reltime и tinterval<BR>
Перенос параметров recovery.conf в postgresql.conf<BR>
В новых индексах btree максимальный размер записи индекса сокращён на 8 байт

https://postgrespro.ru/docs/postgresql/13/release-13.html#id-1.11.6.10.4<BR>
Переименование параметра конфигурации wal_keep_segments в wal_keep_size<BR>
Прекращение поддержки обновления неупакованных (созданных до версии 9.1) расширений

https://postgrespro.ru/docs/postgresql/14/release-14.html#id-1.11.6.6.4<BR>
Необходимо пересоздать пользовательские объекты, использующие некоторые встроенные функции для работы с массивами, в связи с изменением типов аргументов (Том Лейн)<BR>
Ликвидированы устаревшие операторы проверки включения @ и ~ для встроенных геометрических типов данных<BR>
Ликвидация операторов вычисления факториала ! и !!, а также функции numeric_fac()<BR>
Недопущение использования индексов GiST операторами включения (<@ и @>) из модуля intarray 
