
---
Задание 1: Создание таблицы и изменение данных
---
Задание: Создайте таблицу EmployeeDetails для хранения информации о
сотрудниках. Таблица должна содержать следующие столбцы:
● EmployeeID (INTEGER, PRIMARY KEY)
● EmployeeName (TEXT)
● Position (TEXT)
● HireDate (DATE)
● Salary (NUMERIC)
После создания таблицы добавьте в неё три записи с произвольными данными о
сотрудниках.

---
Создал таблицы
---

CREATE TABLE EmployeeDetails (
EmployeeID INTEGER PRIMARY KEY,
EmployeeName TEXT,
Position TEXT,
HireDate DATE,
Salary NUMERIC
);

---
Добавил данные
---

INSERT INTO EmployeeDetails (EmployeeID, EmployeeName, Position,
HireDate, Salary) VALUES (1, 'Mammont Ne', 'Sales Manager',
'2025-01-15', 50000);
INSERT INTO EmployeeDetails (EmployeeID, EmployeeName, Position,
HireDate, Salary) VALUES (2, 'Svetlana Ladygina', 'Marketing Specialist',
'2020-06-30', 40000);
INSERT INTO EmployeeDetails (EmployeeID, EmployeeName, Position,
HireDate, Salary) VALUES (3, 'Leroi Djencins', 'Software Engineer',
'2025-03-22', 66666);




Задание 2: Создание представления
---
Задание: Создайте представление HighValueOrders для отображения всех заказов,
сумма которых превышает 10000. В представлении должны быть следующие столбцы:
● OrderID (идентификатор заказа),
● OrderDate (дата заказа),
● TotalAmount (общая сумма заказа, вычисленная как сумма всех Quantity *
Price).
Используйте таблицы Orders, OrderDetails и Products.

---
Решение
---
CREATE VIEW HighValueOrders AS
SELECT
o.OrderID,
o.OrderDate,
SUM(od.Quantity * p.Price) AS TotalAmount
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
JOIN Products p ON od.ProductID = p.ProductID
GROUP BY o.OrderID, o.OrderDate
HAVING SUM(od.Quantity * p.Price) > 10000;


Задание 3: Удаление данных и таблиц
---
Задание: Удалите все записи из таблицы EmployeeDetails, где Salary меньше
50000. Затем удалите таблицу EmployeeDetails из базы данных.

---
Удалил записи меньше 50000
---

DELETE FROM EmployeeDetails WHERE Salary < 50000;

---
все удалил
---

DROP TABLE EmployeeDetails;


Задание 4: Создание хранимой процедуры
---
Задание: Создайте хранимую процедуру GetProductSales с одним параметром
ProductID. Эта процедура должна возвращать список всех заказов, в которых
участвует продукт с заданным ProductID, включая следующие столбцы:
● OrderID (идентификатор заказа),
● OrderDate (дата заказа),
● CustomerID (идентификатор клиента).


---
Создайте хранимую процедуру
---

CREATE PROCEDURE GetProductSales(pProductID INT)
SELECT
od.ProductID,
o.OrderID,
o.OrderDate,
o.CustomerID
FROM Orders AS o
JOIN OrderDetails AS od ON o.OrderID = od.OrderID
WHERE od.ProductID = pProductID;

---
Вызов хранимой процедуры
---
CALL GetProductSales(10);
