# Homework 1: SQL
## Установка PostgreSQL

Источник: https://www.postgresql.org/download/linux/ubuntu/

```
# Import the repository signing key:
sudo apt install curl ca-certificates
sudo install -d /usr/share/postgresql-common/pgdg
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Update the package lists:
sudo apt update

# Install the latest version of PostgreSQL:
# If you want a specific version, use 'postgresql-16' or similar instead of 'postgresql'
sudo apt -y install postgresql
```

Хорошо, теперь настроим терминальный клиент [psql](https://www.postgresql.org/docs/current/app-psql.html) для работы с PostgreSQL так, чтобы при каждом подключении к базе данных нам не нужно было вводить имя пользователя.
Для начала узнаем, какой у нас логин в Ubuntu. В терминале введите:
```
$ whoami
```
Например, в моём случае вывод был следующим:
```
andrey
```
Теперь подключимся к консоли с помощью предустановленного суперпользователя `postgres` -- именно он используется чаще всего для начальной настройки PostgreSQL
```
sudo -u postgres psql
```
Вы должны увидеть что-то вроде:
```
psql (16.4 (Ubuntu 16.4-1.pgdg20.04+1))
Type "help" for help.   

postgres=#
```
`#` означает, что вы подключились как суперпользователь. Теперь добавим нового пользователя:
```
CREATE USER <username> WITH SUPERUSER;
```
В моём случае `<username>` = `andrey`. Выйдем из _psql_ с помощью:
```
\q
```

## Загрузка базы данных
Скачайте файл с базой данных (`olympics.sql`) из этого репозитория. 
Создайте базу данных PostgreSQL (из консоли):
```sh
$ createdb <dbname>
```
В моём случае:
- `<dbname>` = `olympics` или любое другое удобное вам имя
Добавьте `olympics.sql` в PostgreSQL:
```sh
psql -d <dbname> -f olympics.sql
```

# Полезные команды
Чтобы выполнять sql-запрос из файла, воспользуйтесь мета-командой '\i':
```sql
\i /path/to/your_query.sql
```
Чтобы посмотреть, каким пользователям принадлежат базы данных, воспользуйтесь мета-командой `\l`:
```sql
\l
```
Чтобы посмотреть, от какого имени какого пользователя вы сейчас работаете, выполните:
```sql
select current_user;
```
**Все доступные** мета-команды можно посмотреть, выполнив команду `\?`.

Готово! Теперь можно выполнять [задание](https://15445.courses.cs.cmu.edu/fall2024/homework1/).
