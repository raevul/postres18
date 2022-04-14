# 
`\c` -> показывает в какой  бд мы находимся и через какого юзера 

`\c` -> name_of_db -> переключается к этой бд

`\l` -> показывает все бд

`\dt` -> показывает все таблицы в бд

`\du` -> показывает всех юзеров

`\q` -> выход

# Создание БД и Таблиц
```sql
CREATE DATABASE name_of_db;
-- создает базу данных
```

```sql
CREATE TABLE name_of_table(
    name_of_column1 data_type(int, varchar) consttaint,
    name_of_column2 data_type consttaint,
    ...
);
-- создает таблицу с полями
```
# Заполнение таблиц
```sql
INSERT INTO name_of_table (name_of_column1, name_of_column2) 
VALUES (vall1, vall2);
-- добавляет запись в таблицу
```
# Вывод данных 
```sql
SELECT * FROM name_of_table;
-- достает все поля и записи из таблицы
```
```sql
SELECT name_of_column1, name_of_column2 FROM name_of_table;
-- достает только указанные столбцы из таблицы
```
# Связи
## pk fk
> primary key (pk) - первичный ключ
> это ограничение, которое мы указываем на те поля, который должны быть уникальными для того, 
> чтобы потом их использовать в связях (например в id)

> foreign key (fk) - внешний кляч 
> это ограничение, которое мы указываем на те поля, которые будут ссылаться на pk в другой таблице, для создания связи

```sql
CREATE TABLE author (
    id serial primary key,
    first_name varchar(50),
    last_name varchar(50)
)
CREATE TABLE book (
    id serial,
    title varchar(100),
    published year,
    author_id int foreign key references author (id)
)
```

> JOIN - инструкция, которая  позволяет  в  запросах SELECT брать данные из несколько таблицы 

> INNER JOIN (JOIN) - когда достаются только те записи, у которых есть полная связь

> FULL JOIN - когда достаются абсолютно все записи со всех таблиц

> LEFT JOIN - когда достаются все записи с 'левой' таблицы и так же те записи с полной связью

> RIGHT JOIN - когда достаются все записи с 'правой' таблицы и так же те записи с полной связью

```sql
SELECT author.first_name, book.title
FROM author
JOIN book ON author.id = book.id
```
# Импорт и экспорт данных
Write from file to db
```bash
psql db_name < file sql
```
write from db to file 
```bash
pg_dump db_name > file.sql
```
