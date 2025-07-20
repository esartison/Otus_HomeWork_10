# Домашнее задание Сартисона Евгения №10


🚧 Что нужно сделать
## **(1) Выбрать одну из СУБД**

— Это может быть ClickHouse, Greenplum, MongoDB, MySQL, Tarantool — что угодно, что установишь и сможешь сравнить с PostgreSQL.
-- Решил использовать уже установленный в локальной виртуалке Postgres и дополнительно установить ClickHouse

Postgres
<img width="1288" height="311" alt="image" src="https://github.com/user-attachments/assets/893dcd69-9c87-44cb-a584-893a108f4776" />

Clickhouse
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




— Убедись, что обе системы работают локально или в кластере (если хочешь — в Minikube).

Загрузить в неё данные

— Объём данных: от 10 до 100 Гб (можно взять демо-наборы или сгенерировать их самостоятельно).

— Протестируй механизмы загрузки: COPY, INSERT, стриминг, параллельную загрузку, сторонние утилиты.

Провести сравнение

— Напиши 2–3 запроса: с фильтрацией, агрегацией и соединением.

— Сравни скорость выполнения на PostgreSQL и выбранной системе.

— Зафиксируй: план выполнения, время, объём данных, системные условия.

Описать процесс

— Что выбирал и почему

— Какие механизмы загрузки пробовал

— С какими проблемами столкнулся

— Что показалось удобным, а что — нет

📎Что сдавать

📄 Отчёт (pdf, md или jupyter) с результатами, логами, объяснениями

💻 При желании — скрипты или ссылки на репозиторий


💡 Эпилог

Ирина кивает, глядя на отчёт Алексея:

— "Скорость есть, гибкость — тоже. Но ты не сравнил с Oracle... Шучу! Пока."


Критерии оценки:
Задание выполнено и описано в отчёте
Загружено от 10 до 100 Гб данных
Выполнено сравнение с PostgreSQL по времени выполнения запросов
Видны разные подходы к загрузке данных
Выводы обоснованы
