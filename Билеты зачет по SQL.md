
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

> [!question]- Группировка данных по признакам. Группировка с фильтрацией. Привести несколько разных по сложности примеров.
>
>**Определение**
>
>> **Группировка данных по признакам** — это процесс объединения данных в группы (категории) на основе одного или нескольких общих признаков (атрибутов). Цель группировки — структурировать данные для дальнейшего анализа, например, для подсчета средних значений, сумм или других статистических показателей.
>
>>**Группировка с фильтрацией** — это процесс, при котором данные сначала фильтруются по определенным критериям, а затем группируются по выбранным признакам. Это позволяет анализировать только те данные, которые соответствуют заданным условиям.
>
>Примеры:
>>
>**Простые примеры**
>
>>	1. Простая группировка
>
>>```sql
>>SELECT Category, SUM(Quantity) AS Total_Quantity
>>FROM Sales
>>GROUP BY Category;
>>```
>
>
>>	2. Группировка по нескольким признакам:
>
>>```sql
>>SELECT Department, Position, AVG(Salary) AS Average_Salary
>>FROM Employees
>>GROUP BY Department, Position;
>>```
>
>**Примеры группировки с фильтрацией**
>
>>	3. Простая фильтрация и группировка:
>
>>```sql
>>SELECT Category, SUM(Quantity) AS Total_Quantity
>>FROM Sales
>>WHERE Category = 'Electronics' AND Date >= '2023-09-01'
>>GROUP BY Category;
>>```
>
>
>>	4. Сложная фильтрация и группировка:
>
>>```sql
>>SELECT Customer, AVG(OrderAmount) AS Average_Amount
>>FROM Orders
>>WHERE Status = 'Completed' AND OrderAmount > 1000
>>GROUP BY Customer;
>>```
>
>
>>	5. Группировка с фильтрацией по агрегированным данным
>
>>```sql
>>SELECT Category, SUM(Quantity * Price) AS Total_Revenue
>>FROM Sales
>>GROUP BY Category
>>HAVING SUM(Quantity * Price) > 50000;
>>```

> [!question]- Вложенные запросы. Мотивация использования. Привести несколько разных по сложности примеров.
>
>**Определение**
>
>> **Вложенные запросы** — это SQL-запросы, используемые внутри других запросов. Они разбивают сложные задачи на более простые шаги, возвращая отдельные значения, наборы данных или таблицы для использования в основном запросе. Применяются для фильтрации, агрегации или анализа данных, часто в частях запроса, таких как `SELECT`, `FROM`, `WHERE`, `HAVING`.
>
>Примеры:
>>
>**Простые примеры**
>
>>	1. Простой вложенный запрос в WHERE:
>
>>```sql
>>SELECT Name, Salary
>>FROM Employees
>>WHERE Salary > (SELECT AVG(Salary) FROM Employees);
>>```
>
>>	2. Вложенный запрос в FROM
>
>>```sql
>>SELECT Department, Position, AVG(Salary) AS Average_Salary
>>FROM Employees
>>GROUP BY Department, Position;
>>```
>
>>	3. Вложенный запрос в SELECT:
>
>>```sql
>>SELECT Customer,
>> (SELECT COUNT(*)
>> 	FROM Orders AS O2
>> 	WHERE O2.Customer = O1.Customer) AS OrderCount
>>FROM Orders AS O1
>>GROUP BY Customer;
>>```
>
>
>>	4. Вложенный запрос с фильтрацией в HAVING:
>
>>```sql
>>SELECT Category, SUM(Quantity * Price) AS Total_Revenue
>>FROM Sales
>>GROUP BY Category
>>HAVING SUM(Quantity * Price) > (
>>    SELECT AVG(Total_Revenue)
>>    FROM (
>> 	   SELECT SUM(Quantity * Price) AS Total_Revenue
>> 	   FROM Sales
>> 	   GROUP BY Category
>> ) AS AvgRevenue);
>>```
>
>
>>	5. Сложный вложенный запрос с несколькими уровнями
>
>>```sql
>>SELECT Name, Department, Salary
>>FROM Employees AS E1
>>WHERE Salary > (
>> 	SELECT AVG(Salary)
>> 	FROM Employees AS E2
>> 	WHERE E2.Department = E1.Department
>>);
>>```

> [!question]- JOIN. Различные виды JOIN’ов. Привести несколько примеров с разными видами.
>
>**Определение**
>
>> 	JOIN — это операция, которая позволяет объединять данные из двух или более таблиц на основе связанных между ними столбцов. В зависимости от типа JOIN, результат может включать только совпадающие строки или все строки из одной или обеих таблиц.
>
>**Основные виды JOIN:**
>>
>>	1. INNER JOIN - возвращает только те строки, где есть совпадение в обеих таблицах.
>
>>	2. LEFT JOIN (или LEFT OUTER JOIN)- возвращает все строки из левой таблицы и соответствующие строки из правой таблицы. Если совпадений нет, то в правой таблице будут значения NULL.
>
>>	3. RIGHT JOIN (или RIGHT OUTER JOIN)- возвращает все строки из правой таблицы и соответствующие строки из левой таблицы. Если совпадений нет, то в левой таблице будут значения NULL.
>
>>	4. FULL JOIN (или FULL OUTER JOIN)- возвращает все строки из обеих таблиц. Если совпадений нет, то в недостающих частях будут значения NULL.
>
>>	5. CROSS JOIN - возвращает декартово произведение строк из обеих таблиц (все возможные комбинации строк).
>
>>	6. SELF JOIN- это JOIN таблицы с самой собой, часто используется для сравнения строк внутри одной таблицы.
>
>**Примеры:**
>
>>	 1. INNER JOIN:
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>NNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
>>```
>>	2. LEFT JOIN
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
>>```
>
>>	3. RIGHT JOIN:
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
>>```
>
>
>>	4 FULL JOIN:
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>FULL JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
>>```
>
>
>>	5. CROSS JOIN
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>CROSS JOIN Departments;
>>```
>
>
>> 	6. SELF JOIN
>
>>```sql
>>SELECT E1.Name AS Employee1, E2.Name AS Employee2
>>FROM Employees E1
>>INNER JOIN Employees E2 ON E1.DepartmentID = E2.DepartmentID
>>WHERE E1.EmployeeID <> E2.EmployeeID;
>>```

> [!question]- Различия между JOIN и вложенными запросами (производительность, читабельность, применимость). Привести пример аналогичных запросов с использованием JOIN и подзапросов.
>
>1. **Производительность**
>
>>- **JOIN**:
>>  Обычно работает быстрее, особенно для больших таблиц, так как оптимизатор СУБД может эффективно использовать индексы и выполнять объединение на уровне движка базы данных. Однако, если JOIN выполняется по сложным условиям или с большим количеством таблиц, производительность может снизиться.
>>- **Вложенные запросы**:
>>  Могут быть менее производительными, особенно если подзапрос выполняется для каждой строки основного запроса (например, в `SELECT` или `WHERE`). В некоторых случаях СУБД оптимизирует вложенные запросы, преобразуя их в JOIN, но это зависит от конкретной базы данных.
>
>
>2. **Читабельность**
>
>>- **JOIN**:
>>  Более нагляден для объединения таблиц, особенно если нужно связать данные из нескольких таблиц. Легче читать и поддерживать, особенно для простых запросов.
>>- **Вложенные запросы**:
>>  Могут быть менее читаемыми, особенно если подзапросы глубоко вложены или используются в нескольких частях запроса. Однако для некоторых задач (например, агрегации или фильтрации) вложенные запросы могут быть более интуитивно понятными.
>
>
>3. **Применимость**
>
>>- **JOIN**:
>>   Лучше подходит для объединения таблиц по условиям, где нужно получить данные из нескольких таблиц одновременно. Не подходит, если нужно выполнить агрегацию или фильтрацию перед объединением.
>>- **Вложенные запросы**:
>>  Полезны, когда нужно выполнить промежуточные вычисления (например, агрегацию) или фильтрацию перед использованием результата в основном запросе. Могут использоваться в частях запроса, где JOIN неприменим (например, в SELECT, WHERE, HAVING).
>
>**Примеры**
>>1. Задача: Получить список сотрудников с указанием их отдела.
>> - С использованием JOIN:
>
>>```sql
>>SELECT Employees.Name, Departments.DepartmentName
>>FROM Employees
>>INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
>>```
>> - С использованием вложенного запроса:
>
>>```sql
>>SELECT Employees.Name,
>>       (SELECT Departments.DepartmentName
>>        FROM Departments
>>        WHERE Departments.DepartmentID = Employees.DepartmentID) AS DepartmentName
>>FROM Employees;
>>```
>>2. Задача: Найти сотрудников, чья зарплата выше средней зарплаты в их отделе.
>> - С использованием JOIN:
>
>>```sql
>>SELECT E1.Name, E1.Salary
>>FROM Employees E1
>>INNER JOIN (
>>    SELECT DepartmentID, AVG(Salary) AS AvgSalary
>>    FROM Employees
>>    GROUP BY DepartmentID
>> ) AS DeptAvg ON E1.DepartmentID = DeptAvg.DepartmentID
>> WHERE E1.Salary > DeptAvg.AvgSalary;
>>```
>> - С использованием вложенного запроса:
>
>>```sql
>>SELECT Name, Salary
>>FROM Employees E1
>>WHERE Salary > (
>>    SELECT AVG(Salary)
>>    FROM Employees E2
>>    WHERE E2.DepartmentID = E1.DepartmentID
>> );
>>```
>
>>3. Задача: Найти отделы, в которых нет сотрудников.
>> - С использованием JOIN:
>
>>```sql
>>SELECT Departments.DepartmentName
>>FROM Departments
>>LEFT JOIN Employees ON Departments.DepartmentID = Employees.DepartmentID
>>WHERE Employees.EmployeeID IS NULL;
>>```
>> - С использованием вложенного запроса:
>
>>```sql
>>SELECT DepartmentName
>>FROM Departments
>>WHERE DepartmentID NOT IN (
>>    SELECT DepartmentID
>>    FROM Employees
>>    WHERE DepartmentID IS NOT NULL
>> );
>>```

>[!question]- Типы связей между таблицами в БД. Привести примеры структур.
>
>**Определение**
>
>> 	Связь таблиц в базе данных — это механизм, который позволяет устанавливать логические связи между данными в разных таблицах на основе общих атрибутов (ключей). Связи обеспечивают целостность данных, устраняют дублирование и позволяют эффективно организовывать информацию. Они реализуются с помощью первичных ключей (Primary Key) и внешних ключей (Foreign Key), где внешний ключ в одной таблице ссылается на первичный ключ в другой таблице.
>
>**Виды связей:**
>>
>>	1. Один к одному- каждая запись в одной таблице связана ровно с одной записью в другой таблице.
>
>>	2. Один ко многим- одна запись в одной таблице может быть связана с несколькими записями в другой таблице.
>
>>	3. Многие ко многим- каждая запись в одной таблице может быть связана с несколькими записями в другой таблице, и наоборот.
>
>
>
>**One-To-One**
>
>- **Таблица `Users`**:
>>| UserID | Name   |
>| ------ | ------ |
>| 1      | Ivanov |
>| 2      | Petrov |
>
>- **Таблица `Passports`**:
>>| PassportID | Number   | UserID |     |
>| ---------- | -------- | ------ | --- |
>| 101        | 12345678 | 1      |     |
>| 102        | 87654321 | 2      | >   |
>
>
>**One-To-Many**
>
>- **Таблица `Departments`**:
>>| DepartmentID | DepartmentName |
| ------------ | -------------- |
| 101          | IT             |
| 102          | HR             |
>
>- **Таблица `Passports`**:
>>| PassportID | Number   | UserID |
>| ---------- | -------- | ------ |
>| 101        | 12345678 | 1      |
>| 102        | 87654321 | 2      |
>
>**Many-To-Many**
>- **Таблица `Students`**:
>>| StudentID | Name   |
| --------- | ------ |
| 1         | Ivanov |
| 2         | Petrov |
>- **Таблица `Courses`**:
>>| CourseID | CourseName |
| -------- | ---------- |
| 101      | Math       |
| 102      | Physics    |
>- **Таблица-связка `StudentCourses`**:
>>| StudentID | CourseID |
| --------- | -------- |
| 1         | 101      |
| 1         | 102      |
| 2         | 101      |

> [!question]- ER-модель. Основные элементы и правила построения. Чтение готовой ER-модели.
>
>**Определение**
>
>> **ER-модель** (Entity-Relationship model) — это способ моделирования структуры базы данных с помощью сущностей (Entities) и связей (Relationships).
>
>**Основные элементы**
>
>>- **Сущность** (Entity) — это объект реального мира, информация о котором хранится (например, «Сотрудник»).
>>- **Связь** (Relationship) — показывает, как сущности соотносятся друг с другом (1:1, 1:N, M:N).
>>- **Атрибут** (Attribute) — свойство или характеристика сущности (например, «Имя», «Зарплата»).
>>- **Ключ** (Key) — атрибут или набор атрибутов, которые уникально идентифицируют запись в сущности.
>>- **Степень связи** (Cardinality) — определяет, сколько экземпляров одной сущности связано с экземплярами другой сущности.
>
>**Основные правила**
>
>>- **Сущностиа** — прямоугольники.
>>- **Атрибуты** — овалы, соединённые с сущностями..
>>- **Связи** — ромбы, соединённые с сущностями.
>>- **Степень связи** — обозначения на линиях (1:1, 1:N, M:N).
>>- **Ключи** — подчёркнутые атрибуты.
>
>**Чтение ER-модели**
>
>>1. **Идентифицируйте сущности**:Найдите прямоугольники, которые обозначают сущности (например, Пользователь, Заказ).
>>2. **Определите атрибуты**: Найдите овалы, соединённые с сущностями, которые обозначают атрибуты (например, Имя, Дата заказа).
>>3. **Определите связи**: Найдите ромбы, которые обозначают связи между сущностями (например, Пользователь делает Заказ).
>>4. **Определите степень связи**: Обратите внимание на обозначения возле связей (1:1, 1:N, M:N).
>>5. **Найдите ключи**: Найдите атрибуты, которые подчёркнуты — это первичные ключи.

> [!question]- Создание таблицы. Синтаксис. Обязательные и опциональные ключевые слова. Объявление внешних ключей в таблице. Привести пример.
>**Синтаксис**
>```sql
> CREATE TABLE table_name (
> 	column1 datatype [CONSTRAINT ...] [AUTOINCREMENT],
> 	column2 datatype [CONSTRAINT ...] [AUTOINCREMENT],
> 	...
>  );
>```
>**Обязательные элементы**:
>> 1. CREATE TABLE - ключевое слово чтобы создать таблицу
>> 2. Имя таблицы (например, users)
>> 3. Хотя бы один столбец с указанием типа данных(например, id INT, name VARCHAR(50))
>
>**Опциональные элементы**:
>> - PRIMARY KEY -  уникальный номер каждой строки
>> - FOREIGN KEY -связь с с другой таблицей
>> - UNIQUE - уникальность значений в столбце
>> - NOT NULL - запрет на пустые значения
>> - CHECK - проверка условия(например age > 52)
>> - DEFAULT - значение по умолчанию (например DEFAULT 'unknown')
>
>**Объявление внешних ключей в таблице**:
>	Внешний ключ обеспечивает ссылочную целостность между таблицами.
>
>**Синтаксис**
>```sql
>FOREIGN KEY (column_name) 
>REFERENCES parent_table (parent_column)
>[ON DELETE action] 
>[ON UPDATE action]
>```
>> - ON DELETE  и ON UPDATE - опциональные действия при удалении/изменении связанной записи
>> - CASCADE - автоматическое удаление/изменение зависимых строк
>> - SET NULL - установка NULL в столбец
>> - RESTRICT - (по умолчанию) - запрет на удаление/изменение
>```sql
>CREATE TABLE books (
>    book_id INT PRIMARY KEY,
>    title VARCHAR(200) NOT NULL,
>    author_id INT,
>    -- Объявление внешнего ключа
>    FOREIGN KEY (author_id) 
>    REFERENCES authors(author_id)
>    ON DELETE CASCADE
>);
>```

> [!question]- Изменение структуры таблицы. Особенности реализации стандарта SQL в SQLite. Привести несколько примеров.
> **Переименование таблицы**
> ```sql
ALTER TABLE employees RENAME TO staff;
> ```
> **Добавление столбца**
> ```sql
ALTER TABLE staff ADD COLUMN salary REAL;
> ```
> **Переименование столбца**
> (Поддерживается в SQLite начиная с версии 3.25.0).
>```sql
ALTER TABLE staff RENAME COLUMN salary TO monthly_salary;
>```
>**Удаление столбца (обходной путь)** 
>
>SQLite не поддерживает команду `ALTER TABLE ... DROP COLUMN`. Для удаления столбца нужно:
>
>1. Создать новую таблицу с нужной структурой.
>2. Перенести данные в новую таблицу.
>3. Удалить исходную таблицу.
>4. Переименовать новую таблицу.
>
>** Особенности реализации SQL в SQLite***
>
>1. **Гибкость типов данных** SQLite не строго контролирует типы данных столбцов. Например, столбцу с типом `INTEGER` можно присвоить текстовое значение.
>
>2. **Ограниченная поддержка `ALTER TABLE`** В отличие от других СУБД (например, PostgreSQL или MySQL), возможности команды `ALTER TABLE` в SQLite ограничены.
  >
>3. **Отсутствие расширенных ограничений** Например, в SQLite отсутствует поддержка внешних ключей по умолчанию (но её можно включить), а также проверка типов  данных менее строгая.

- Добавление и удаление данных в таблице (в том числе разобрать случай с наличием связей в таблице). Возможные нарушения целостности структуры БД при модифицирующих операциях. При- вести несколько примеров.
- Ограничения целостности при создании таблицы. Привести основные типы и несколько осмысленных примеров.
>[!question]- Реализация различных типов связей средствами SQL. Приести пример структуры БД не менее чем из 4 таблиц с различными типами связей.
>**Теория**
>>Реляционная модель данных предполагает хранение информации в таблицах, связанных между собой.
>
>>Связи (relationships) позволяют избегать дублирования данных и повышают целостность
>
>**Типы связей**
>>***One-to-One (1:1)***
>>>Один элемент (вхождение), и только он, в одной таблице соотвествует одному элементу в другой.
>>
>>>Один сотрудник - одна личная учетная запись.
>
>>***One-to-Many (1:N)***
>>>Один элемент, и только он,  в одной таблице соответсвует нескольким элементам в другой.
>>
>>> Один отдел содержит много сотрудников.
>
>>***Many-to-Many (M:N)***
>>>Один элемент в одной таблице соответсвует нескольким элементам в другой, и эти элименты соответсвуют нескольким элементам в первой таблице.
>>
>>> Одна книга может иметь несколько авторов, и один автор - несколько книг.
>
>**FOREIGN KEY**
>> Внешний ключ одной таблицы, указывающий на PRIMARY KEY другой таблицы. Реализует связь и гарантирует целостность (нельзя ссылаться на несуществующую запись).
>
>**Пример**
>>Реализуем следующую структуру бд (вхождения приведены для примера).
>>***Структура***
>>***`Users`***:
>>>| id | name | school_id |
>>| ------ | ------ | ------ |
>>| 1 | Ivanov | 1 |
>>| 2 | Petrov | 1 |
>>| 3 | Flexer | 2 |
>>
>>***`Passports`***:
>>>| id |  number | user_id |
>>| ------ | ------ | ------ |
>>| 1 | 42690 | 1 |
>>| 2 | 19684 | 2 |
>>| 3 | 11488 | 3 |
>>
>>***`Schools`***:
>>>| id |  number |
>>| ------ | ------ |
>>| 1 | 179 |
>>| 2 | 57 |
>>
>>***`Courses`***:
>>>| id |  name |
>>| ------ | ------ |
>>| 1 | 'Math' |
>>| 2 | 'CS' |
>>
>>***`UserCourseRelations`***:
>>>| id |  user_id | course_id |
>>| ------ | ------ | ------ |
>>| 1 | 1 | 1 |
>>| 2 | 1 | 2 |
>>| 3 | 2 | 1 |
>>| 4 | 3 | 1 |
>>| 5 | 3 | 2 |
>>
>>***Реализация***
>
>>```sql
>>CREATE TABLE Schools (
>>	id INTEGER PRIMARY KEY,
>>	number INTEGER NOT NULL
>>);
>>```
>
>>```sql
>>CREATE TABLE Users (
>>	id INTEGER PRIMARY KEY,
>>	name VARCHAR(100) NOT NULL,
>>	school_id INTEGER,
>>	FOREIGN KEY (school_id)
>>		REFERENCES Schools(id)
>>);
>>```
>
>>```sql
>>CREATE TABLE Passports (
>>	id INTEGER PRIMARY KEY,
>>	number INTEGER NOT NULL,
>>	user_id INTEGER,
>>	FOREIGN KEY (user_id)
>>		REFERENCES Users(id)
>>);
>>```
>
>>```sql
>>CREATE TABLE Courses (
>>	id INTEGER PRIMARY KEY,
>>	name VARCHAR(100) NOT NULL
>>);
>>```
>
>>```sql
>>CREATE TABLE UserCourseRelations (
>>	id INTEGER PRIMARY KEY,
>>	user_id INTEGER NOT NULL,
>>	course_id INTEGER NOT NULL,
>>	FOREIGN KEY (user_id)
>>		REFERENCES Users(id),
>>	FOREIGN KEY (course_id)
>>		REFERENCES Courses(id)
>>);
>>```

>[!question]- Создание и удаление представлений в SQL. Отличия представлений от таблиц. Привести несколько примеров.
>**Определение**
>>VIEW (представление) - виртуальная таблица, определяемая запросом SELECT.
>
>**Отличия от таблицы**
>>Хранит не сами данные, а только определение запроса.
>
>>Неизменяемо
>
>**Создание**
>>	CREATE [OR REPLACE] VIEW view_name AS
>>	SELECT ...
>>	FROM ...
>>	[WHERE ...];
>
>**Удаление**
>>	DROP VIEW view_name
>
>**Примеры**
>>Пусть у нас есть таблицы employees (id, name, salary, dept_id) и departments (id, name)
>>
>>```sql
>>CREATE VIEW v_emp_dept AS
>>SELECT
>>	e.id,
>>	e.name,
>>	e.salary,
>>	d.name
>>FROM employees AS e
>>JOIN departments AS d
>>	ON e.dept_id = d.id
>>WHERE e.salary > 50000;
>>```
>>
>>v_emp_dept покажет сотрудников с окладом > 50 000 и названия их отделов.
>>
>>Теперь можно селектом достать данные "из" этого представления
>>```sql
>>SELECT * FROM v_emp_dept;
>>```

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
