
> [!question]- Структура БД, свойства СУБД.
> ***Структура БД***
>>	База данных (БД) — это организованная совокупность данных, структурированная таким образом, чтобы упростить хранение, обработку и поиск информации.
>
>>	Таблица — одна из основных структур хранения данных. Состоит из строк (записей) и столбцов (полей).
>
>>	Первичный ключ (Primary Key) — уникальный идентификатор для каждой строки в таблице.
>
>>	СУБД (DBMS) — система управления базами данных (например, MySQL, PostgreSQL, SQLite)
>
>  ***Свойства СУБД***
>>	1.Целостность данных
>
>>	2.Безопасность и надёжность
>
>>	3.Высокая производительность
>
>>	4.Масштабируемость

> [!question]- Основные типы данных в языке SQL. Базовые операции над типами.
>
> ***Типы данных***
>
>> 	CHAR(size) - строка фиксированного размера size
>
>> 	VARCHAR(size) - строка переменной длины длины не более size
>
>> 	BOOL/BOOLEAN
>
>> 	SMALLINT, MEDIUMINT, INT/INTEGER - целые числа (16, 32 и 64 бита сответственно)
>
>> 	FLOAT, DOUBLE - числа с плавающей точкой размером 32 и 64 бита соответственно
>
>> 	DATE, TIME, DATETIME, TIMESTAMP
>> 	Также в любой* колонке могут встречаться NULL-значения.
>
>
> ***Базовые операции***
>> 	Стандартные математические операции: +, -, *, /, %
>
>>	Битовые операции: &, ˆ , |, ∼
>
>>	Операции сравнения: >, <, <=, >=, =, <>, BETWEEN
>
>>	Логические операции: AND, OR, NOT, ALL, ANY/SOME, IN, LIKE, IS NULL, IS NOT NULL
>
>>	Приведение типов: cast(column_name as type)
>

> [!question]- Команда SELECT. Назначение и синтаксис. Привести примеры.
>**Назначение**
>>	SELECT указывает, какие столбцы (или вычисления) нужно вывести.
>>	FROM указывает, из какой таблицы получаем данные.
>>	WHERE — условие фильтрации строк.
>>	GROUP BY — группировка по одному или нескольким столбцам.
>> 	HAVING — условие для отфильтрованных групп.
>> 	ORDER BY — сортировка (по возрастанию или убыванию).
>>	LIMIT — ограничение количества возвращаемых строк.
>
> **Синтаксис**
>
>>```sql
>>SELECT <столбцы или выражения>
>>FROM <название_таблицы>
>>[WHERE <условие>]
>>[GROUP BY <столбцы>]
>>[HAVING <условие_для_групп>]
>>[ORDER BY <столбцы> [ASC|DESC]]
>>[LIMIT <количество_строк>];
>>```
>
>**Примеры**
>
>	Структура таблицы employees:
>>		id (PRIMARY KEY)
>>		name
>>		position
>>		salary
>Запрос:
>>```sql
>>SELECT name, position
>>FROM employees;
>>```
>Описание: Этот запрос вернёт столбцы name и position из таблицы employees.

>[!question]- Псевдонимы при выборке данных.Синтаксис и мотивация применения. Привести примеры. Синтаксис и мотивация применения
>Определение и мотивация применения
>>	- Aliasing позволяет давать временные имена столбцам или таблицам.
>>	- Удобно при использовании вычисляемых полей или при работе с длинными названиями таблиц.
>Примеры:
>
>>	Структура таблицы employees:
>>
>>		id (PRIMARY KEY)
>>		name
>>		position
>>		salary
>
>Пример: Использование псевдонима столбца
>>```sql
>> SELECT name AS employee_name,
>> salary * 1.2 AS new_salary
>> FROM employees;
>>-- AS задаёт псевдоним для отображаемого столбца.
>>--В результате в итоговой выборке столбец будет называться employee_name, а второй — new_salary.
>>```
>
>Пример: Псевдоним таблицы
>>```sql
>>SELECT e.name, e.position
>>FROM employees AS e;
>>```
>

> [!question]- Основные аггрегирующие функции. Привести примеры запросов.
>**Функции**
>>	MIN - минимальное значение в колонке MAX - максимальное значение в колонке
>>	AVG - среднее значение в колонке
>>	SUM - сумма значений в колонке
>>	COUNT - количество значений в колонке
>>	Важно: все аггрегирующие функции игнорируют NULL-значения кроме COUNT.
>
>**Примеры**
>>```sql
>>SELECT MIN(цена) AS минимальная_цена
>>FROM товары;
>>```
>
>>```sql
>>SELECT город, AVG(возраст) AS средний_возраст
>>FROM клиенты
>>GROUP BY город
>>HAVING AVG(возраст) > 30;
>>-- Этот запрос возвращает средний возраст клиентов в каждом городе.
>>```
>
>>```sql
>>SELECT SUM(цена) AS общая_цена
>>FROM заказы;
>>```
>
>>```sql
>>SELECT COUNT(*) AS количество_заказов
>>FROM заказы;
>> -- **COUNT** - возвращает количество строк в таблице.
>>```

> [!question]- Фильтрация результатов запроса. Привести несколько разных по сложности примеров.
>
>**Определение**
>
>>	Фильтрация результатов запроса - это процесс ограничения количества строк, возвращаемых запросом, на основе определенных условий. В SQL для фильтрации результатов используются операторы WHERE, HAVING и BETWEEN.
>
>Примеры:
>>
>**Простые примеры**
>
>>	1. Фильтрация по одному условию:
>
>>```sql
>>SELECT *
>>FROM клиенты
>>WHERE возраст > 30;
>>```
>
>
>>	2. Фильтрация по двум условиям:
>
>>```sql
>>SELECT *
>>FROM клиенты
>>WHERE возраст > 30 AND город = 'Москва';
>>```
>
>**Примеры со сложными условиями**
>
>>	1. Фильтрация по диапазону значений:
>
>>```sql
>>SELECT *
>>FROM клиенты
>>WHERE возраст BETWEEN 25 AND 40;
>>```
>
>
>>	2. Фильтрация по списку значений:
>
>>```sql
>>SELECT *
>>FROM клиенты
>>WHERE город IN ('Москва', 'Санкт-Петербург', 'Киев');
>>```
>
>
>>	3. Фильтрация по условию, содержащему NULL:
>
>>```sql
>>SELECT *
>>FROM клиенты
>>WHERE телефон IS NOT NULL;
>>```
>
>**Примеры с использованием оператора HAVING**
>
>>	1. Фильтрация по среднему значению:
>
>>```sql
>>SELECT город, AVG(возраст) AS средний_возраст
>>FROM клиенты
>>GROUP BY город
>>HAVING AVG(возраст) > 30;
>>```
>
>
>>	2. Фильтрация по нескольким средним значениям:
>
>>```sql
>>SELECT город, AVG(возраст) AS средний_возраст, SUM(доход) AS общий_доход
>>FROM клиенты
>>GROUP BY город
>>HAVING AVG(возраст) > 30 AND SUM(доход) > 100000;
>>```


- Группировка данных по признакам. Группировка с фильтрацией. Привести несколько разных по сложности примеров.
- Вложенные запросы. Мотивация использования. Привести несколько разных по сложности примеров.
- JOIN. Различные виды JOIN’ов. Привести несколько примеров с разными видами.
- Различия между JOIN и вложенными запросами (производительность, читабельность, применимость). Привести пример аналогичных запросов с использованием JOIN и подзапросов.
- Типы связей между таблицами в БД. Привести примеры структур.
- ER-модель. Основные элементы и правила построения. Чтение готовой ER-модели.
- Создание таблицы. Синтаксис. Обязательные и опциональные ключевые слова. Объявление внешних ключей в таблице. Привести пример.
- Изменение структуры таблицы. Особенности реализации стандарта SQL в SQLite. Привести несколько примеров.
- Добавление и удаление данных в таблице (в том числе разобрать случай с наличием связей в таблице). Возможные нарушения целостности структуры БД при модифицирующих операциях. При- вести несколько примеров.
- Ограничения целостности при создании таблицы. Привести основные типы и несколько осмысленных примеров.
- Реализация различных типов связей средствами SQL. Приести пример структуры БД не менее чем из 4 таблиц с различными типами связей.
- Создание и удаление представлений в SQL. Отличия представлений от таблиц. Привести несколько примеров.
> [!question]- Оконные функции. Общий синтаксис, основные функции. Отличия оконных функций от аггрегирующих.
>**Определение**
>>Оконные функции (window functions) — специальные функции SQL, позволяющие выполнять вычисления по «окну» строк .
>
> **Синтаксис**
>>```sql
>>function()  OVER (
>>[PARTITION BY column_list]
>>[ORDER BY column_list]
>>)
>>```
>
>>	PARTITION BY
>>группирует строки в «окна» по колонке(-ам).
>
>>	ORDER BY
>>порядок, важный для функции ранжирования (function()) .
>
>**Основные функции**
>>	ROW_NUMBER()
>>дает порядковый номер каждой строки в рамках указанного окна.
>
>>	RANK()
>>дает "топ" (т.е. если значение одно, то топ одинаковый), в котором находится вхождение (с пропуском мест), e.g.  1, 1, 3, ...
>
>>	DENSE_RANK()
>>дает "топ", в котором находится вхождение (без пропуска мест), e.g. 1, 1, 2
>
>>	LAG(return_value, offset, default_value)
>>дает значение из offset-ой предыдущей строки столбца return_value (по дефолту offset = 1, т.е. значение на строку выше). Если этой строки нет, то дает default_value (по дефолту default_value = NULL)
>
>>	LEAD(return_value, offset, default_value)
>>дает значение из offset-ой следующей строки столбца return_value (по дефолту offset = 1, т.е. значение на строку ниже). Если этой строки нет, то дает default_value (по дефолту default_value = NULL)
>
>>	AVG()
>
>**Отличия от аггрегирующих функций**
>> Не  свертывают строки в одну, а «распределяют» вычисленное значение по каждой строке.
>
>>Поддерживают больше функций (не аггрегатных).
>
>**Пример**
>>```sql
>>SELECT
>>	employee_id,
>>	salary,
>>	AVG(salary)  OVER (
>>		PARTITION BY dept_id
>>	)  AS avg_salary_in_dept
>>FROM employees;
>>```
>>Для каждого сотрудника возвращает его зарплату и среднюю зарплату по отделу

> [!question]- Различные виды упорядочивания в оконных функциях. Привести несколько примеров.
> **Теория**
>>	ASC
>>по возрастанию (дефолт).
>
>>	DESC
>> по убывания
>
> **Примеры**
>> ```sql
>> SELECT
>> 	RANK() OVER (ORDER BY salary DESC) AS salary_rank
>> FROM employees;
>>  ```
>>  Возвращает топ зарплаты
>
>>```sql
>>SELECT
>>	RANK() OVER (ORDER BY salary) AS salary_bottom_rank
>>FROM employees;
>>```
>>Возвращает нижний топ зарплаты

 > [!question]- Основные правила работы с sqlite3. Создание БД и подключение к уже существующей БД. Описание основных объектов при работе с БД (подключение, курсор).
 >**Синтаксис и теория**
 >> Является встроенным модулем.
>> ```python
>> import sqlite
>> ```
 >
 >> Нужно подключение к бд через sqlite.connect(), оно же откртие/создание файла (т.е. если файла нет, то он создастся).
>> ```python
>> conn = sqlite3.connect('example.db')
>> ```
 >
 >> Все запросы выполняются с помощью курсора sqlite3.connect().cursor()
>> ```python
>> cursor = conn.cursor()
>> ```
 >
>> В конце обзяательно нужно закрыть файл/соединение через sqlite3.connection().close()
>> ```python
>> conn.close()
>> ```
>
>>***Итого***
>>```python
>>import sqlite3
>>conn = sqlite3.connect('example.db')
>>cursor = conn.cursor()
>>conn.close()
>>```

>[!question]- Правила работы при запросе и изменении данных в БД с помощью sqlite3.
>>**Синтаксис и теория**
>
>>Все запросы выполняются с помощью курсора, у которого есть метод execute()
>>```python
>>cursor.execute(sql_script)
>>```
>
>>Для фиксирования (сохранения) изменений у соединения есть метод commit()
>>```python
>>conn.commit()
>>```
>
>**Примеры**
>
>>Создание таблицы
>>```sql
>>import sqlite3
>>conn = sqlite3.connect(’example.db’)
>>cursor = conn.cursor()
>>cursor.execute(’’’
>>	CREATE TABLE IF NOT EXISTS users (
>>		id INTEGER PRIMARY KEY AUTOINCREMENT,
>>		username TEXT NOT NULL,
>>		age INTEGER,
>>		city TEXT
>>	)
>>’’’)
>>conn.commit()
>>conn.close()
>>```
>
>>Добавление данных
>>```sql
>>import sqlite3
>>conn = sqlite3.connect(’example.db’)
>>cursor = conn.cursor()
>>cursor.execute(’’’
>>	INSERT INTO users (username, age, city)
>>	VALUES (?, ?, ?)
>>’’’, (’Иван’, 25, ’Москва’))
>>conn.commit()
>>conn.close()
>>```
>>Что такое плейсхолдеры написано в вопросе ниже
>
>>Выборка данных
>>```sql
>>import sqlite3
>>conn = sqlite3.connect(’example.db’)
>>cursor = conn.cursor()
>>cursor.execute('SELECT id, username, age, city FROM users')
>>rows = cursor.fetchall()
>>for row in rows:
>>	print(row)
>>conn.close()
>>```
>
>***Фетч*** (метод курсора)
>
>> 	fetchall()
>> возвращает список кортежей с результатами
>
>>	fetchone()
>> возвращает одну строку
>
>> 	fetchmany(n)
>> возвращает n строк
>
>**Еще примеры**
>>Обновление
>>```sql
>>cursor.execute(’’’
>>	UPDATE users
>>	SET age = ?
>>	WHERE username = ?
>>’’’, (26, ’Иван’))
>>```
>
>>Удаление
>>```sql
>>cursor.execute(’’’
>>	DELETE FROM users
>>	WHERE username = ?
>>’’’, (’Иван’,))
>>```

>[!question]- Плейсхолдеры. Назвать минимум 2 причины их применения вместо форматных строк.
>**Теория и синтаксис**
>>Скрипт может использовать плейсхолдеры (?). Тогда в execute вторым аргументом нужно передать кортеж значений, по длинне такой же, как и количество плейсхолдеров.
>
>>executemany() используется, чтобы один скрипт выполнить несколько раз с разными кортежами значений, которые передаются списком вторым аргументом
>
>>**Примеры**
>>Добавление данных
>>```sql
>>import sqlite3
>>conn = sqlite3.connect(’example.db’)
>>cursor = conn.cursor()
>>cursor.execute(’’’
>>	INSERT INTO users (username, age, city)
>>	VALUES (?, ?, ?)
>>’’’, (’Иван’, 25, ’Москва’))
>>conn.commit()
>>conn.close()
>>```
>
>>Добавление списка данных
>>```sql
>>import sqlite3
>>conn = sqlite3.connect(’example.db’)
>>cursor = conn.cursor()
>>params = [
>>	(’Иван’, 25, ’Москва’),
>>	('Саша', 17, 'Москва')
>>]
>>cursor.executemany(’’’
>>	INSERT INTO users (username, age, city)
>>	VALUES (?, ?, ?)
>>’’’, params)
>>conn.commit()
>>conn.close()
>>```
>
>**Причины их применения вместо форматных строк**
>>Защита от SQL-инъекций (безопасность данных)
>
>>Добавление сразу спика значений с помощью executemany()

>[!question]- Object-relational mapping. Что такое и зачем применяется. Плюсы и минусы по сравнению с использованием SQL-скриптов.
>**Определение**
>>ORM  (Object-relational mapping, объектно-реляционное отображение) - технология, которая связывает бд с концепциями ООП, создавая «виртуальную объектную базу данных»
>
>**Плюсы по сравнению с использованием SQL-скриптов**
>> Отделение бизнес-логики от конкретных SQL-запросов
>
>> Кросс-база: без изменения кода можно подключить другую СУБД.
>
>> Удобство: вместо таблиц и строк — привычные классы и объекты. Уменьшает количество кода
>
>>Безопасность: автоматическая экранизация параметров, меньше риска SQL-инъекций.
>
>**Минусы**
>> Высокий уровень абстракции (более большая отдаленность от самой бд).
>
>>Может быть медленнее.
>
>**Литература**
>[пост про плюсы и минусы ORM](https://stackoverflow.com/questions/4667906/the-advantages-and-disadvantages-of-using-orm) (прочитайте ответы)

> [!question] 25. Основные правила работы с SQLAlchemy. Создание БД и подключение к уже существующей БД. Описание основных объектов при работе с БД (подключение, сессия).
>
> **Правила работы с SQLAlchemy**
> ???
> **Cоздание БД  и подключение**
>>  `create_engine` - осуществляется подключение к БД (ссылка на нёё)
>> `Session` -  объект, который создает соединения с БД. Объект транзакций
>>`session` - сама сессия
> ```python
> """ __init__.py """
> from sqlalchemy import create_engine
> from sqlalchemy.orm import sessionmaker # Пример для SQLite
> engine = create_engine("sqlite:///example.db")  # Создает,  если ДБ ещё нет
> Session = sessionmaker(bind=engine)
> session = Session()
> ```
>

> [!question] 26. Правила создания моделей и работы с ними. Создание колонок (примитивных типов).
>
> **Основные правила создания колонок**
>
> ```python
> column_name = Column(Type,  params)
> ```
> Параметры:
>>`nullable=False` - поле не может быть `NULL`
>>`primary_key` - является первичным ключом
>>`unique` - уникальные значения
>> `default` - установление дефолтного значения
>> `foreign_key` - установление внешнего ключа
>
>> есть и другие, но мы их не разбирали
>
**Создание колонок**
>
> ```python
> """ models.py """
> from sqlalchemy.ext.declarative import declarative_base
> from sqlalchemy import Column, Integer, String
>
> Base  = declarative_base()
>
> class User(Base):
> 	__tablename__ = ’users’ # Имя таблицы
> 	id = Column(Integer, primary_key=True) # Колонки как атрибуты класса
> 	name = Column(String, nullable=False, unique=True)
> 	age = Column(Integer, nullable=False)
> 	city = Column(String,  foreign_key=ForeignKey(cities.id))
>
> Base.metadata.create_all(engine) # Создает таблицы, если их еще не существует.
> ```
>
>> Важно, что `create_all()` только создает таблицы, которых еще не было. Через неё нельзя измениить колонки уже существующей таблицы.
>
> **Работа с моделями**
>> CRUD операции - create, read, update, delete.
>> Смотреть подробнее в №28
>
> **Create**
> ```python
> """ Создание пользователя """
> new_user = User(name=’Esha’, city=’Moscow’)
> session.add(new_user) # Подготовка объекта к вставке
> session.commit() # Только после этого изменение сохранится
> ```


> [!question] 27. Описание различных видов связей между моделями в SQLAlchemy. Привести несколько примеров.
> >`ForeignKey` -  внешний ключ для установления связи между таблицами
>> `relationship` - установление связи между моделями
>
>
> **One-to-Many** - для одной записи несколько записей в другой таблице.
>> `backref` -  автоматическая связь между колонками. Его не нужно в каждой модели прописывать, достаточно иметь колонку  с `ForeignKey`
>
> ```python
> """ models.py """
> from sqlalchemy import ForeignKey
> from sqlalchemy.orm import relationship
> class Department(Base):
> 	__tablename__ = ’departments’
> 	id = Column(Integer, primary_key=True)
> 	name = Column(String)
>
> class Employee(Base):
> 	__tablename__ = ’employees’
> 	id = Column(Integer, primary_key=True)
> 	name = Column(String)
> 	department_id = Column( Integer, ForeignKey(’departments.id’))
> 	department = relationship( ’Department’,  backref=’employees’)
> ```
> >У каждого департамента несколько сотрудников, но у каждый сотрудник работает только в одном департаменте.
>
> **One-to-One** - для каждой записи одна соответсвующая запись в другой таблице.
>>Реализация через связь One-to-Many с ограничением `uselist=False`
>> Таким образом, вместо того, чтобы связывать к списку объектов, принудительно связываем к одному объекту.
>
> ```python
> class Person(Base):
> 	__tablename__ = ’persons’
> 	id = Column(Integer, primary_key=True)
> 	name = Column(String)
>
> class Passport(Base):
> 	__tablename__ = ’passports’
> 	id = Column(Integer, primary_key=True)
> 	person_id = Column(Integer, ForeignKey(’persons.id’),  unique=True)
> 	person = relationship(’Person’, backref=’passport’, uselist=False)
> ```
> >У каждого человека один паспорт.
>
> **Many-to-Many** - каждая запись может быть связана с несколькими записями в другой таблице.
>> Для осуществления этой связи необходимо создать ассоциативную таблицу.
>> Также необходимо в `relationship` добавить параметр `secondary=association_table`
>
> ```python
> association_table = Table(
> 	’association’, Base.metadata, Column(’student_id’, Integer, ForeignKey(’students.id’)), Column(’course_id’, Integer, ForeignKey(’courses.id’)) )
> ```
>
> ```python
> class Student(Base):
> 	__tablename__ = ’students’
> 	id = Column(Integer, primary_key=True)
> 	name = Column(String)
> 	courses = relationship(’Course’, secondary=association_table, back_populates=’students’)
>
> class Course(Base):
> 	__tablename__ = ’courses’
> 	id = Column(Integer, primary_key=True)
> 	title = Column(String)
> 	students = relationship(’Student’, secondary=association_table, back_populates=’courses’)
>```
>> У каждого ученика несколько разных курсов, у каждого курса много различных учеников.
>


 > [!question] 28. Правила составления запросов на выборку и изменение данных в SQLAlchemy.
**Правила**
>> - Нельзя напрямую передавать SQL код для безопасности БД
>>- Нужно использовать конструкцию `try except` во избежании повреждения БД
>> - После изменение надо обязательно выполнять `session.commit()` .
>> - ???
>
> **Составление  запросов**
>> `.query()`  - метод для выполнения запросов
>> `.query().all()` - все объекты.  Возвращает список
>> `.query().first()`  - первый объект
>
> > Также можно использовать `filter`,  `order_by`,  `limit` и другие конструкции
>
> **Выборка**
> > `filter` - поддерживает условия, операторы сравнения
> > `filter_by` - упрощенный вариант, работает только с уравниваем
> > `or_` , `in_`, `and_`,  `like`, `between`, `is`,  `exisits`, `limit` и прочее - применяются внутри `filter`
>
> **Изменение данных**
> > `.update({'column': value})` - изменение выбранной записи
> > `.delete(object)` - удаление выбранного объекта
>
> **Примеры**
> **Read**
> ```python
> """ Чтение всех колонок """
> users = session.query(User).all() # Возвращается список
> for user in users:
> 	print(user.name, user.city)
> ```
>
> **Update**
> ```python
> """ Обновление данных """
> session.query(User).filter(User.name == "Eshas").update({"age": 26})
> session.commit()
> ```
>
> **Search**
> ```python
> """ По первичному ключу """
> user = session.get(User, 1)
> ```
>
> ```python
> """ С фильтрацией """
> from sqlalchemy import or_
>
> # Первый пользователей
> user = session.query(User).filter_by(name="Eshas").first()
>
> # Все пользователи старше 18
> users18 = session.query(User).filter(User.age > 18).all()
>
> # Все старше 18 и чьё имя начинается с "Е"
> users18E = session.query(User).filter(or_(User.age > 18, User.name.like("E%"))).all()
> ```
>
> **Delete**
> ```python
> """ Удаление """
> user_to_delete = session.query(User).filter_by(name=’Eshass’)
> session.delete(user_to_delete) # Подготовка объекта к удалению
> session.commit()
> ```

> [!question] 29. Чтение готового SQL-запроса и принцип его работы.
>
> **Примерный ход действий**
>> 1. Посмотреть какая таблица используется (`FROM`)
>>2. Определить какие условия фильтрации (`WHERE/ORDERBY/SORTBY`)
>> 3. Понять какое действие выполняется - изменение(`UPDATE/DELETE/INDERT INTO`) или же просто вывод(`SELECT`)
>
>** Принцип работы(?)**
>
>> - Парсинг запроса, проверка синтаксиса
>>- Обработка СУБД, оптимизация
>>- Выполнение запроса СУБД
>> - Вывод (если нужно)

> [!question] 30. Переписать готовый SQL-запрос с помощью SQLAlchemy.
> В основном все методы в SQLAlchemy называются так же, как и операторы в SQLite.
>
> |   SQLITE |    SQLAlchemy |
> | --- | --- |
> |  SELECT   |  session.query() |
> |INSERT INTO |  session.add()|
> |WHERE |session.query.filter()|
> |ORDER BY/GROUPBY|session.query.order_by()/ .query.group_by()|
> |SELECT * FROM table| session.query().all()|
> |UPDATE table  <br>SET column = value   <br>WHERE condition|session.query().update()|
> |DELETE FROM table<br>WHERE condition|session.delete(session.query(Column).filter(...))|
> **Пример**
> ```sql
> SELECT name, city
> FROM users
> WHERE city = Moscow
> ORDER BY age;
> ```
> ```python
> session.query(User.name, User.city).filter(User.city == 'Moscow').order_by(User.age).all()

