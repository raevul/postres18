# Команды
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
);

CREATE TABLE book (
    id serial,
    title varchar(100),
    published year,
    author_id int foreign key references author (id)
);
```
## Виды связи (теория)
> One to one - один к одному 
Например: 
* Один автор - одна биография
* Один флаг - одна страна
* Один человек - одно сердце

> One to many - один ко многим
Например:

* Один человек - много клеток, но у одной клетки только один человек
* Одни родители - много детей, но у одного ребенка только одни родители
* Один аккаунт - много постов, но у одного поста только один автор (аккаунт)
* Один makers - много студентов, но у одного студента только один makers

> Many to many - многие ко многим
Например:

* У человека много друзей и у одного друга много других друзей
* У доктора много пациентов и у пациента много докторов
* У пользователя много социальных сетей и у одной соцсети много пользователей


## Виды связей (практика)
### One to one
```sql
CREATE TABLE flag (
    id serial primary key,
    photo text
)

CREATE TABLE country (
    id serial primary key,
    title varchar(50),
    gimn text,
    flag_id int unique 
    foreign key fk_country_flag references flag(id) 
);
```
### One to many
```sql
CREATE TABLE accaunt (
    id serial primary key,
    nickname varchar(30) unique,
    user_password varchar(255)
);

CREATE TABLE post (
    id serial primary key,
    title varchar(100),
    body text,
    photo text,
    account_id int foreign key fk_account_post references account(id) 
);
```
### Many to many
```sql
CREATE TABLE doctor(
    id serial primary key,
    first_name varchar (30),
    last_name varchar (50)
);

CREATE TABLE patsient(
    id serial primary key,
    first_name varchar (30),
    last_name varchar (50)
);

CREATE TABLE doctor_patsient (
    doctor_id int foreign key fk_doctor references doctor(id)
    patsient_id int foreign key fk_patsient references patsient(id) 
);
```

# JOIN
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
