# Домашнее задание Сартисона Евгения №10


🚧 Что нужно сделать
## **(1) Выбрать одну из СУБД**

— Это может быть ClickHouse, Greenplum, MongoDB, MySQL, Tarantool — что угодно, что установишь и сможешь сравнить с PostgreSQL.
**Решил использовать уже установленный в локальной виртуалке Postgres и дополнительно установить ClickHouse**

**Postgres**
<img width="1288" height="311" alt="image" src="https://github.com/user-attachments/assets/893dcd69-9c87-44cb-a584-893a108f4776" />

**Clickhouse**

(a) Установка Clickhouse
```
apt-get install -y apt-transport-https ca-certificates dirmngr
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 8919F6BD2B48D754
echo "deb https://packages.clickhouse.com/deb stable main" | sudo tee /etc/apt/sources.list.d/clickhouse.list
apt update
apt-get install -y clickhouse-server clickhouse-client
```

(б) разрешаем удаленные подключения к нашему серверу:
```
student:~$ sudo diff /etc/clickhouse-server/config.xml /etc/clickhouse-server/config.xml_bkp
269c269
<     <listen_host>0.0.0.0</listen_host> 
---
>     <!-- <listen_host>0.0.0.0</listen_host> -->
```

(в) Запуск Clickhouse-а
> sudo systemctl start clickhouse-server





## **(2) Убедись, что обе системы работают локально или в кластере (если хочешь — в Minikube).**

**Postgres**
<img width="1399" height="387" alt="image" src="https://github.com/user-attachments/assets/ac57f205-1342-45e6-be86-63d73ead4919" />


**Clickhouse**

<img width="733" height="198" alt="image" src="https://github.com/user-attachments/assets/0ed5a72a-b0ac-4705-ba5d-8932312cd8c9" />


Для чистоты эксперимента, оставляю все параметры в ClickHouse и Postgres по умолчанию. 




## **(3)Загрузить в неё данные**

— Объём данных: от 10 до 100 Гб (можно взять демо-наборы или сгенерировать их самостоятельно).

— Протестируй механизмы загрузки: COPY, INSERT, стриминг, параллельную загрузку, сторонние утилиты.

**Postgres**
https://www.cybertec-postgresql.com/en/postgresql-bulk-loading-huge-amounts-of-data/
https://www.crunchydata.com/blog/fast-csv-and-json-ingestion-in-postgresql-with-copy
https://www.crunchydata.com/blog/data-loading-in-postgres-for-newbies

create table employee (eid varchar(10), last_name varchar(100), first_name varchar(100), department varchar(4));

insert into employee (
    eid, last_name, first_name, department
)
select
    left(md5(i::text), 10),
    md5(random()::text),
    md5(random()::text),
    left(md5(random()::text), 4)
from generate_series(1, 1000000) s(i);

https://estuary.dev/blog/loading-data-into-postgresql/
COPY persons(first_name, last_name, dob, email)
FROM 'C:\sampledb\persons.csv'
DELIMITER ','
CSV HEADER;
Method 3: Loading Data to Postgres Via pgAdmin


https://www.postgis.us/presentations/PGOpen2018_data_loading.pdf


**Clickhouse**
https://clickhouse.com/docs/integrations/data-formats/sql
https://clickhouse.com/docs/integrations/data-formats/csv-tsv


## **(4)Провести сравнение Postgres и ClickHouse**

— Напиши 2–3 запроса: с фильтрацией, агрегацией и соединением.

— Сравни скорость выполнения на PostgreSQL и выбранной системе.

— Зафиксируй: план выполнения, время, объём данных, системные условия.

## **(5)Описать процесс**

— Что выбирал и почему

— Какие механизмы загрузки пробовал

— С какими проблемами столкнулся

— Что показалось удобным, а что — нет



## **(6) 📎Что сдавать**

📄 Отчёт (pdf, md или jupyter) с результатами, логами, объяснениями

💻 При желании — скрипты или ссылки на репозиторий
**Все ссылки уже в указаны в каждом шаге**




Критерии оценки:
Задание выполнено и описано в отчёте
Загружено от 10 до 100 Гб данных
Выполнено сравнение с PostgreSQL по времени выполнения запросов
Видны разные подходы к загрузке данных
Выводы обоснованы
