
# Content

| Title  | Solution  | Acceptance   | Difficulty | 
|:-------|:----------|:------------:|:----------:|
|175|<a href='#175'> Combine Two Tables </a>| 51.6%| Easy|
|176|<a href='#176'> Second Highest Salary </a>|27.1%| Easy|
|177|<a href='#177'> Nth Highest Salary </a>|26.2%| Medium|
|178|<a href='#178'> Rank Scores </a>|36.5%| Medium|
|180|<a href='#180'> Consecutive Numbers </a>|33.5%| Medium|
|181|<a href='#181'> Employees Earning More Than Their Managers </a>|48.3%| Easy|
|182|<a href='#182'> Duplicate Emails </a>|54.6%| Easy|
|183|<a href='#183'> Customers Who Never Order </a>|44.7%| Easy|
|184|<a href='#184'> Department Highest Salary </a>|28.8%| Medium|
|185|<a href='#185'> Department Top Three Salaries </a>|25.8%| Hard|
|196|<a href='#196'> Delete Duplicate Emails </a>|32.7%| Easy|
|197|<a href='#197'> Rising Temperature </a>|34.7%| Easy|
|262|<a href='#262'> Trips and Users </a>|24.9%| Hard|
|569|<a href='#569'> Median Employee Salary </a>|47.0%| Hard|
|570|<a href='#570'> Managers with at Least 5 Direct Reports </a>|62.5%| Medium|
|571|<a href='#571'> Find Median Given Frequency of Numbers </a>|46.9%| Hard|
|574|<a href='#574'> Winning Candidate </a>|36.2%| Medium|
|577|<a href='#577'> Employee Bonus </a>|59.3%| Easy|
|578|<a href='#578'> Get Highest Answer Rate Question </a>|35.5%| Medium|
|579|<a href='#579'> Find Cumulative Salary of an Employee </a>|34.3%| Hard|
|580|<a href='#580'> Count Student Number in Departments </a>|42.7%| Medium|
|584|<a href='#584'> Find Customer Referee </a>|67.5%| Easy|
|585|<a href='#585'> Investments in 2016 </a>|47.3%| Medium|
|586|<a href='#586'> Customer Placing the Largest Number of Orders </a>|66.4%| Easy|
|595|<a href='#595'> Big Countries </a>|73.7%| Easy|
|596|<a href='#596'> Classes More Than 5 Students </a>|35.5%| Easy|
|597|<a href='#597'> Friend Requests I: Overall Acceptance Rate </a>|39.6%| Easy|
|601|<a href='#601'> Human Traffic of Stadium </a>|36.4%| Hard|
|602|<a href='#602'> Friend Requests II: Who Has the Most Friends </a>|44.9%| Medium|
|603|<a href='#603'> Consecutive Available Seats </a>|58.2%| Easy|
|607|<a href='#607'> Sales Person </a>|56.8%| Easy|
|608|<a href='#608'> Tree Node </a>|58.7%| Medium|
|610|<a href='#610'> Triangle Judgement </a>|61.3%| Easy|
|612|<a href='#612'> Shortest Distance in a Plane </a>|53.5%| Medium|
|613|<a href='#613'> Shortest Distance in a Line </a>|73.0%| Easy|
|614|<a href='#614'> Second Degree Follower </a>|22.6%| Medium|
|615|<a href='#615'> Average Salary: Departments VS Company </a>|37.4%| Hard|
|618|<a href='#618'> Students Report By Geography </a>|42.8%| Hard|
|619|<a href='#619'> Biggest Single Number </a>|38.7%| Easy|
|620|<a href='#620'> Not Boring Movies </a>|62.1%| Easy|
|626|<a href='#626'> Exchange Seats </a>|54.4%| Medium|
|627|<a href='#627'> Swap Salary </a>|68.6%| Easy|
|1045|<a href='#1045'> Customers Who Bought All Products </a>|65.3%| Medium|
|1050|<a href='#1050'> Actors and Directors Who Cooperated At Least Three Times New </a>|79.6%| Easy|

# Key Questions and Answers

<a id='175'></a>
## 175. Combine Two Tables 

Table: Person 

| Column Name | Type    | 
|-------------|---------|
| PersonId    | int     |
| FirstName   | varchar | 
| LastName    | varchar |

PersonId is the primary key column for this table. 

Table: Address 

| Column Name | Type    | 
|-------------|---------|
| AddressId   | int     | 
| PersonId    | int     | 
| City        | varchar | 
| State       | varchar | 

AddressId is the primary key column for this table. 

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people: FirstName, LastName, City, State

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT FirstName, LastName, City, State FROM Person 
 LEFT JOIN Address 
 ON Person.PersonID = Address.PersonID;`
 
 <br>

**<font size="3" color='red'>Comments</font>**

The SQL code above is not efficient (faster) enough. Use Alias to make it run faster.

`SELECT t1.FirstName, t1.LastName, t2.City, t2.State FROM Person t1 
 LEFT JOIN Address t2 
 ON t1.PersonID = t2.PersonID;`

<a id='176'></a>
## 176. Second Highest Salary (Easy)

Write a SQL query to get the second highest salary from the Employee table. 

| Id | Salary | 
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    | 

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null. 

| SecondHighestSalary | 
|---------------------|
| 200 |


<br>

**<font size="3" color='blue'>Answer</font>**

**Tricky part**: the second highest refers to distinct values. If there is no second highest value, it needs to return null (rather than empty): so need to use IFNULL()

`SELECT IFNULL( (SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1,1), NULL) AS SecondHighestSalary;`

<a id='177'></a>
## 177. Nth Highest Salary (Medium)

Write a SQL query to get the nth highest salary from the Employee table.

| Id | Salary | 
|----|--------|
| 1 | 100 | 
| 2 | 200 | 
| 3 | 300 | 

For example, given the above Employee table, the nth highest salary where n = 2 is 200. If there is no nth highest salary, then the query should return null. 

| getNthHighestSalary(2) | 
|------------------------|
| 200 |

<br>

**<font size="3" color='blue'>Answer</font>**

**Tricky part**: Need to set N = N-1, because we cannot directly use LIMIT 1 OFFSET N-1.
If we want use other symbol, e.g. M, we need to DECLARE IT first: e.g. DECLARE M INT

`CREATE FUNCTION getNthHighestSalary(N INT) 
 RETURNS INT BEGIN SET N = N - 1; 
 RETURN ( SELECT IFNULL( (SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET N), NULL) ); 
 END`

<a id='178'></a>
## 178. Rank Scores (Medium)

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks. 

| Id | Score | 
|----|-------|
| 1 | 3.50 | 
| 2 | 3.65 |
| 3 | 4.00 |
| 4 | 3.85 |
| 5 | 4.00 |
| 6 | 3.65 |

For example, given the above Scores table, your query should generate the following report (order by highest score):

| Score | Rank | 
|-------|------| 
| 4.00 | 1 | 
| 4.00 | 1 |
| 3.85 | 2 |
| 3.65 | 3 |
| 3.65 | 3 |
| 3.50 | 4 |

<br>

**<font size="3" color='blue'>Answer</font>**

There is an easy answer by using DENSE_RANK() and window function, but we need to use MS SQL server. If not, here is the answer. There are something we need to pay attention: 
+ `@var`: this var is user-defined variable. We don't need to initialize it all the time. There are 3 types of variables in SQL:
    + User-defined variable: using `@var`
    + Local variable: Need to `DECLARE` first. E.g. `DECALRE var INT, SET var = 1`
    + Server system variable: using `@@var`
+ All created table is better to give them alias
+ We want to use and update user-defined variable `@num`, but this variable's value is not defined yet, therefore we need to let server know `@num` initial value in FROM sentence. That is why we use: `SELECT .., @num := ... FROM Table1, Table2;` where Table2 containst the initial value of `@num`.
+ Join function normally combines with `ON`, but if the two key variables are exactly the same then we can use `USING(variable)`

`SELECT s1.score AS Score, Rank 
 FROM Scores AS s1 
 LEFT JOIN ( SELECT Score, @num := @num + 1 as Rank 
             FROM (SELECT DISTINCT Score FROM Scores ORDER BY Score DESC) AS Table1, 
                  (SELECT @num := 0) AS Table2) AS s 
 USING (Score) 
 ORDER BY Rank;`

<a id='180'></a>
## 180. Consecutive Numbers (Medium)

Write a SQL query to find all numbers that appear at least three times consecutively. 

| Id | Num | 
|----|-----| 
| 1  | 1   | 
| 2  | 1   | 
| 3  | 1   | 
| 4  | 2   |
| 5  | 1   |
| 6  | 2   | 
| 7  | 2   |

For example, given the above Logs table, 1 is the only number that appears consecutively for at least three times. 

| ConsecutiveNums |
|-----------------| 
| 1 |

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is to create a new variable using `CASE WHEN...THEN END`. In the following, two variables were created: `@Record` and `@Count`. `@Record` ensures whether the record below is the same as the record before; `@Count` does the counting. `@var <> @var := num` means that: if `@var != num` then `@var:=num`

`SELECT DISTINCT Num AS ConsecutiveNums 
 FROM (SELECT Num, 
              (CASE WHEN @Record = Num THEN @Count := @Count + 1 
                    WHEN @Record <> @Record := Num THEN @Count := 1 END) AS n 
       FROM Logs, 
            (SELECT @Count := 0, @Record := (SELECT Num FROM Logs LIMIT 1)) AS tmp1 
       ) AS tmp2 
 WHERE tmp2.n >= 3;`

<a id='181'></a>
## 181. Employees Earning More Than Their Managers (Easy)

The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id. 

| Id | Name | Salary | ManagerId |
|----|------|--------|-----------|
| 1 | Joe | 70000 | 3 | 
| 2 | Henry | 80000 | 4 | 
| 3 | Sam | 60000 | NULL | 
| 4 | Max | 90000 | NULL | 

Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager. 

| Employee | 
|----------|
| Joe |

<br>

**<font size="3" color='blue'>Answer</font>**

There are 2 types of answers: one using JOIN and the other not. The one not using JOIN is faster.

1. The one answer not using `JOIN`

`SELECT E.Name As Employee FROM Employee E, Employee M 
 WHERE E.Salary > M.Salary AND E.ManagerId = M.Id;`

2. The other answer using `JOIN` 

`SELECT E.Name As Employee FROM Employee E 
 INNER JOIN Employee M 
 ON E.ManagerID = M.Id WHERE E.Salary > M.Salary;`

<a id='182'></a>
## 182. Duplicate Emails (Easy)

Write a SQL query to find all duplicate emails in a table named Person. 

| Id | Email | 
|----|-------|
| 1 | a@b.com | 
| 2 | c@d.com | 
| 3 | a@b.com | 

For example, your query should return the following for the above table: 

| Email | 
|-------|
| a@b.com | 

Note: All emails are in lowercase.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT Email FROM (SELECT Email, COUNT(*) AS num FROM Person GROUP BY EMAIL) tbl 
 WHERE num > 1;`

<a id='175'></a>
## 183. Customers Who Never Order (Easy)

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything. 
Table: Customers. 

| Id | Name | 
|----|------|
| 1 | Joe |
| 2 | Henry | 
| 3 | Sam |
| 4 | Max |

Table: Orders. 

| Id | CustomerId | 
|----|------------|
| 1 | 3 | 
| 2 | 1 | 

Using the above tables as example, return the following: 

| Customers | 
|-----------|
| Henry | 
| Max | 

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT Name AS Customers FROM Customers WHERE Id NOT IN (SELECT DISTINCT CustomerId FROM Orders);`

<a id='184'></a>
## 184. Department Highest Salary (Hard)

The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id. 

| Id | Name | Salary | DepartmentId | 
|----|------|--------|--------------|
| 1 | Joe | 70000 | 1 | 
| 2 | Jim | 90000 | 1 | 
| 3 | Henry | 80000 | 2 | 
| 4 | Sam | 60000 | 2 | 
| 5 | Max | 90000 | 1 | 

The Department table holds all departments of the company. 

| Id | Name | 
|----|------|
| 1 | IT |
| 2 | Sales |

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, your SQL query should return the following rows (order of rows does not matter). 

| Department | Employee | Salary |
|------------|----------|--------|
| IT | Max | 90000 | 
| IT | Jim | 90000 | 
| Sales | Henry | 80000 | 

Explanation: Max and Jim both have the highest salary in the IT department and Henry has the highest salary in the Sales department.

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part**: `GROUP BY` must exist after `FROM` and `WHERE`, but before `HAVING`

`SELECT D.Name AS Department, E.Name AS Employee, E.Salary 
 FROM Employee E 
 LEFT JOIN (SELECT DepartmentId, MAX(Salary) AS Max_salary 
            FROM Employee GROUP BY DepartmentId ) M 
 USING(DepartmentId) 
 INNER JOIN Department D 
 ON E.DepartmentId = D.Id WHERE Salary = Max_salary;`


<a id='185'></a>
## 185. Department Top Three Salaries (Hard)

The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id. 

| Id | Name | Salary | DepartmentId | 
|----|------|--------|--------------|
| 1 | Joe | 85000 | 1 | 
| 2 | Henry | 80000 | 2 | 
| 3 | Sam | 60000 | 2 | 
| 4 | Max | 90000 | 1 | 
| 5 | Janet | 69000 | 1 | 
| 6 | Randy | 85000 | 1 | 
| 7 | Will | 70000 | 1 |

The Department table holds all departments of the company. 

| Id | Name | 
|----|------|
| 1 | IT | 
| 2 | Sales | 

Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows (order of rows does not matter). 

|Department | Employee | Salary | 
|-----------|----------|--------| 
| IT | Max | 90000 | 
| IT | Randy | 85000 | 
| IT | Joe | 85000 | 
| IT | Will | 70000 | 
| Sales | Henry | 80000 | 
| Sales | Sam | 60000 |

Explanation: In IT department, Max earns the highest salary, both Randy and Joe earn the second highest salary, and Will earns the third highest salary. There are only two employees in the Sales department, Henry earns the highest salary while Sam earns the second highest salary.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT D.Name AS Department, E.Name AS Employee, E.Salary 
 FROM Employee E 
 JOIN Department D 
 ON E.DepartmentId = D.Id 
 WHERE (SELECT COUNT(DISTINCT E2.Salary) FROM Employee E2 
        WHERE E2.Salary > E.Salary 
        AND E2.DepartmentId = E.DepartmentId) < 3;`

<a id='196'></a>
## 196. Delete Duplicate Emails (Easy)
Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

|Id | Email | 
|---|-------|
| 1 | john@example.com | 
| 2 | bob@example.com | 
| 3 | john@example.com | 

Id is the primary key column for this table. For example, after running your query, the above Person table should have the following rows: 

| Id | Email |
| 1 | john@example.com | 
| 2 | bob@example.com |

Note: Your output is the whole Person table after executing your sql. Use delete statement.

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is we cannot not use `SELECT Email, MIN(Id) FROM ... GROUP BY Email`, because it does not delete the duplicate records, it just selects something to show.

`DELETE t1 FROM Person t1, Person t2 
 WHERE t1.Email = t2.Email AND t1.Id > t2.Id;`

<a id='197'></a>
## 197. Rising Temperature (Easy)

Given a Weather table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates. 

| Id(INT) | RecordDate(DATE) | Temperature(INT) | 
|---------|------------------|------------------| 
| 1 | 2015-01-01 | 10 | 
| 2 | 2015-01-02 | 25 | 
| 3 | 2015-01-03 | 20 | 
| 4 | 2015-01-04 | 30 | 

For example, return the following Ids for the above Weather table: 

| Id | 
|----|
| 2 |
| 4 |


<br>

**<font size="3" color='blue'>Answer</font>**

`ON` in `JOIN` operation can be done on a condition. Here the condition has 2 parts: one is DATEDIFF, and the other part is temperature. There are two answers: one is slow, and the other is fast.

1. Slow

`SELECT t1.Id FROM Weather t1, Weather t2 
 WHERE t1.Temperature > t2.Temperature 
 AND DATEDIFF(t1.RecordDate, t2.RecordDate) = 1;`

2. Fast

`SELECT t1.Id FROM Weather t1 
 JOIN Weather t2 
 ON DATEDIFF(t1.RecorDate, t2.RecorDate) = 1 
 AND t1.Temperature > t2.Temperature;`

<a id='262'></a>
## 262. Trips and Users (Hard)

The Trips table holds all taxi trips. Each trip has a unique Id, while Client_Id and Driver_Id are both foreign keys to the Users_Id at the Users table. Status is an ENUM type of (‘completed’, ‘cancelled_by_driver’, ‘cancelled_by_client’). 

| Id | Client_Id | Driver_Id | City_Id | Status |Request_at|
|----|-----------|-----------|---------|--------|----------|
| 1 | 1 | 10 | 1 | completed |2013-10-01| 
| 2 | 2 | 11 | 1 | cancelled_by_driver|2013-10-01| 
| 3 | 3 | 12 | 6 | completed |2013-10-01| 
| 4 | 4 | 13 | 6 | cancelled_by_client|2013-10-01| 
| 5 | 1 | 10 | 1 | completed |2013-10-02| 
| 6 | 2 | 11 | 6 | completed |2013-10-02| 
| 7 | 3 | 12 | 6 | completed |2013-10-02| 
| 8 | 2 | 12 | 12 | completed |2013-10-03| 
| 9 | 3 | 10 | 12 | completed |2013-10-03| 
| 10 | 4 | 13 | 12 | cancelled_by_driver|2013-10-03| 

The Users table holds all users. Each user has an unique Users_Id, and Role is an ENUM type of (‘client’, ‘driver’, ‘partner’). 

| Users_Id | Banned | Role | 
|----------|--------|------|
| 1 | No | client |
| 2 | Yes | client | 
| 3 | No | client | 
| 4 | No | client | 
| 10 | No | driver | 
| 11 | No | driver | 
| 12 | No | driver |
| 13 | No | driver | 

Write a SQL query to find the cancellation rate of requests made by unbanned users between Oct 1, 2013 and Oct 3, 2013. For the above tables, your SQL query should return the following rows with the cancellation rate being rounded to two decimal places. 

| Day | Cancellation Rate | 
|-----|-------------------|
| 2013-10-01 | 0.33 | 
| 2013-10-02 | 0.00 | 
| 2013-10-03 | 0.50 | 

Credits: Special thanks to @cak1erlizhou for contributing this question, writing the problem description and adding part of the test cases.


<br>

**<font size="3" color='blue'>Answer</font>**

The most straightforward answer is:

`SELECT A.Request_at AS Day, IFNULL(ROUND(B.cancel/A.tot, 2), 0.00) AS "Cancellation Rate" 
 FROM (SELECT Request_at, COUNT(*) AS tot 
       FROM Trips 
       WHERE Client_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = "Yes") 
       AND Driver_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = "Yes")
       AND Request_at BETWEEN "2013-10-01" AND "2013-10-03" 
       GROUP BY Request_at) A 
 LEFT JOIN (SELECT Request_at, COUNT(*) AS cancel 
            FROM Trips 
            WHERE Client_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = "Yes") 
            AND Driver_Id NOT IN (SELECT Users_Id FROM Users WHERE Banned = "Yes") 
            AND Status LIKE "cancelled_by_%" GROUP BY Request_at) B 
 ON A.Request_at = B.Request_at`
 
Another more efficient answer is:

`SELECT Trips.Request_at AS Day, 
        CONVERT ( SUM( CASE WHEN Trips.STATUS LIKE 'cancelled_by_%' THEN 1 ELSE 0 END ) / COUNT( * ), 
                  DECIMAL ( 10, 2 ) ) AS Cancellation_Rate 
 FROM Trips 
 WHERE Trips.Client_Id NOT IN ( SELECT Users_Id FROM Users WHERE Banned = 'Yes' AND Role = 'client' ) 
 AND Trips.Driver_Id NOT IN ( SELECT Users_Id FROM Users WHERE Banned = 'Yes' AND Role = 'driver' ) 
 AND Trips.Request_at BETWEEN '2013-10-01' AND '2013-10-03' 
 GROUP BY Request_at`


<a id='569'></a>
## 569. Median Employee Salary (Hard)
The Employee table holds all employees. The employee table has three columns: Employee Id, Company Name, and Salary. 

|Id | Company | Salary | 
|---|---------|--------|
|1 | A | 2341 | 
|2 | A | 341 | 
|3 | A | 15 | 
|4 | A | 15314 | 
|5 | A | 451 | 
|6 | A | 513 | 
|7 | B | 15 | 
|8 | B | 13 | 
|9 | B | 1154 | 
|10 | B | 1345 | 
|11 | B | 1221 | 
|12 | B | 234 | 
|13 | C | 2345 | 
|14 | C | 2645 | 
|15 | C | 2645 | 
|16 | C | 2652 | 
|17 | C | 65 |

Write a SQL query to find the median salary of each company. Bonus points if you can solve it without using any built-in SQL functions.

|Id | Company | Salary | 
|---|---------|--------|
|5 | A | 451 | 
|6 | A | 513 | 
|12 | B | 234 | 
|9 | B | 1154 |
|14 | C | 2645 | 

<br>

**<font size="3" color='blue'>Answer</font>**

**The Tricky Part** is:
+ Use IF(COND, YES, NO) to define and update variable
+ <span style = "color:red"> When same variables need to be used/called for multiple times, we need to use alias for table and call these variables with table alias </span>
+ The second method is based on the property of median: <span style = "color:red"> the median's frequency should be equal or greater than the absolute difference of its bigger elements and small ones in an array </span>. 
    + `SELECT t1.col1, t2.col1 FROM t1, t2`: returns a table where each row of t1 (col1) matches with ALL rows of t2 (col1)
    + `SUM(CASE...END)` computes the frequency of a number
    + `ABS(SIGN(...))` computes the difference in the frequencies of bigger and smaller numbers
    + MySQL default setting is "ONLY_FULL_GROUP_BY", so for those variables which are not unique (value) within a group, it will report errors. In this case, we remove it from global setting (in creating a table) and also from session setting (in existing table).
    
There are two methods:

1. Method 1: Ranking

`SELECT t1.Id, t1.Company, t1.Salary 
 FROM (SELECT E.Id, E.Company, E.Salary, 
              IF(@prev = E.Company, @count := @count + 1, @count := 1) AS loc, 
              @prev := E.Company 
       FROM Employee E, (SELECT @count := 0, @prev := 0) AS tmp 
       ORDER BY E.Company, E.Salary) AS t1 
 INNER JOIN (SELECT Company, COUNT(*) AS m_loc 
             FROM Employee 
             GROUP BY Company) AS t2 
 ON t1.Company = t2.Company 
 WHERE t1.loc = FLOOR((m_loc + 1)/2) OR t1.loc = FLOOR((m_loc + 2)/2)`

2. Method 2: Property 

`set global sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,
                      NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'; 
 set session sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,
                       NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'; 
 SELECT Employee.Id, Employee.Company, Employee.Salary 
 FROM Employee, Employee B 
 WHERE Employee.Company = B.Company 
 GROUP BY Employee.Company , Employee.Salary 
 HAVING SUM(CASE WHEN Employee.Salary = alias.Salary THEN 1 ELSE 0 END) >= ABS(SUM(SIGN(Employee.Salary - 
        alias.Salary))) 
 ORDER BY Employee.Id;`    

<a id='570'></a>
## 570. Managers with at Least 5 Direct Reports (Medium)
The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id. 

|Id |Name |Department |ManagerId | 
|---|-----|-----------|----------|
|101 |John |A |null | 
|102 |Dan |A |101 | 
|103 |James |A |101 | 
|104 |Amy |A |101 | 
|105 |Anne |A |101 |
|106 |Ron |B |101 | 

Given the Employee table, write a SQL query that finds out managers with at least 5 direct report. For the above table, your SQL query should return:

| Name | 
|------|
| John |

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT t1.Name FROM Employee t1 
 JOIN (SELECT ManagerId, COUNT(*) AS dir_num 
       FROM Employee 
       GROUP BY ManagerId) t2 
 ON t1.Id = t2.ManagerId 
 WHERE t2.dir_num >= 5;`

<a id='571'></a>
## 571. Find Median Given Frequency of Numbers (Hard)

The Numbers table keeps the value of number and its frequency.

| Number | Frequency | 
|--------|-----------| 
| 0 | 7 | 
| 1 | 1 | 
| 2 | 3 | 
| 3 | 1 |

In this table, the numbers are 0, 0, 0, 0, 0, 0, 0, 1, 2, 2, 2, 3, so the median is (0 + 0) / 2 = 0. 

| median | 
|--------| 
| 0.0000 | 

Write a query to find the median of all numbers and name the result as median.

<br>

**<font size="3" color='blue'>Answer</font>**
**The tricky part** is:
+ Use `AVG()` in case it returns multiple values
+ Use Number <= A.Number rather than `Number < A.Number`: because the former will always return a record, while the later may return null record. Similary for Number >= A.Number.
+ property of median: <span style = "color:red"> the median's frequency should be equal or grater than the absolute difference of its bigger elements and small ones in an array </span>.

`SELECT AVG(A.Number) AS median FROM Numbers A 
 WHERE A.Frequency >= ABS((SELECT SUM(Frequency) FROM Numbers WHERE Number <= A.Number) - 
                          (SELECT SUM(Frequency) FROM Numbers WHERE Number >= A.Number));`

<a id='574'></a>
## 574. Winning Candidate (Medium)

Table: Candidate 

| id | Name | 
|----|------|
| 1 | A | 
| 2 | B | 
| 3 | C | 
| 4 | D | 
| 5 | E | 

Table: Vote 

| id | CandidateId | 
|----|-------------|
| 1 | 2 | 
| 2 | 4 | 
| 3 | 3 |
| 4 | 2 | 
| 5 | 5 | 

id is the auto-increment primary key, CandidateId is the id appeared in Candidate table. Write a sql to find the name of the winning candidate, the above example will return the winner B. 

| Name | 
|------|
| B | 

Notes: You may assume there is no tie, in other words there will be at most one winning candidate.

<br>

**<font size="3" color='blue'>Answer</font>**

Notice this is the way how to choose the Max: Use ORDER BY and then LIMIT

`SELECT name AS 'Name' FROM Candidate 
 JOIN (SELECT Candidateid FROM Vote 
       GROUP BY Candidateid 
       ORDER BY COUNT(*) DESC LIMIT 1) AS winner 
 ON Candidate.id = winner.Candidateid;`

<a id='577'></a>
## 577. Employee Bonus (Easy)
Select all employee's name and bonus whose bonus is < 1000. 

Table:Employee 

| empId | name | supervisor| salary | 
|-------|------|-----------|--------|
| 1 | John | 3 | 1000 | 
| 2 | Dan | 3 | 2000 | 
| 3 | Brad | null | 4000 | 
| 4 | Thomas | 3 | 4000 | 

empId is the primary key column for this table. 

Table: Bonus

| empId | bonus | 
|-------|-------|
| 2 | 500 | 
| 4 | 2000 | 

empId is the primary key column for this table. Example ouput:

| name | bonus | 
|------|-------|
| John | null | 
| Dan | 500 | 
| Brad | null | 

<br>

**<font size="3" color='blue'>Answer</font>**
`SELECT A.name, B.bonus FROM Employee A 
 LEFT JOIN Bonus B 
 USING (empId) 
 WHERE B.bonus < 1000 OR B.bonus IS NULL;`

<a id='578'></a>
## 578. Get Highest Answer Rate Question (Medium)

Get the highest answer rate question from a table survey_log with these columns: uid, action, question_id, answer_id, q_num, timestamp. uid means user id; action has these kind of values: "show", "answer", "skip"; answer_id is not null when action column is "answer", while is null for "show" and "skip"; q_num is the numeral order of the question in current session. Write a sql query to identify the question which has the highest answer rate. 

Example: Input: 
| uid | action | question_id | answer_id | q_num | timestamp | 
|-----|--------|-------------|-----------|-------|-----------|
| 5 | show | 285 | null | 1 | 123 | 
| 5 | answer | 285 | 124124 | 1 | 124 | 
| 5 | show | 369 | null | 2 | 125 | 
| 5 | skip | 369 | null | 2 | 126 | 

Output: 

| survey_log | 
|------------| 
| 285 |

Explanation: question 285 has answer rate 1/1, while question 369 has 0/1 answer rate, so output 285. Note: The highest answer rate meaning is: answer number's ratio in show number in the same question.b

<br>

**<font size="3" color='blue'>Answer</font>**

**The common mistake** is:
<span style = "color:red"> You can't use the column aliases you defined in a query in the same query. </span> For example, in the query to create table alias t1, we cannot use num_answer or num_show. The following code will report error: (You need to write down the whole formula for it: i.e. `ORDER BY SUM(CASE WHEN action = "answer" THEN 1 ELSE 0 END) / SUM(CASE WHEN action = "show" THEN 1 ELSE 0 END)`.)

`FROM (SELECT question_id AS survey_log, SUM(CASE WHEN action = "answer" THEN 1 ELSE 0 END) AS num_answer, 
              SUM(CASE WHEN action = "show" THEN 1 ELSE 0 END) AS num_show 
       FROM survey_log 
       GROUP BY question_id 
       ORDER BY (num_answer / num_show) DESC) t1`

Here is the answer:

`SELECT survey_log 
 FROM (SELECT question_id AS survey_log, SUM(CASE WHEN action = "answer" THEN 1 ELSE 0 END) AS num_answer, 
              SUM(CASE WHEN action = "show" THEN 1 ELSE 0 END) AS num_show 
       FROM survey_log 
       GROUP BY question_id) t1 
 ORDER BY (t1.num_answer / t1.num_show) DESC LIMIT 1;`

<a id='579'></a>
## 579. Find Cumulative Salary of an Employee (Hard)
The Employee table holds the salary information in a year. Write a SQL to get the cumulative sum of an employee's salary over a period of 3 months but exclude the most recent month. The result should be displayed by 'Id' ascending, and then by 'Month' descending. 

Example Input 

| Id | Month | Salary | 
|----|-------|--------| 
| 1 | 1 | 20 | 
| 2 | 1 | 20 | 
| 1 | 2 | 30 | 
| 2 | 2 | 30 | 
| 3 | 2 | 40 | 
| 1 | 3 | 40 | 
| 3 | 3 | 60 | 
| 1 | 4 | 60 | 
| 3 | 4 | 70 | 

Output 

| Id | Month | Salary |
|----|-------|--------| 
| 1 | 3 | 90 | 
| 1 | 2 | 50 | 
| 1 | 1 | 20 | 
| 2 | 1 | 20 | 
| 3 | 3 | 100 | 
| 3 | 2 | 40 | 

Explanation: Employee '1' has 3 salary records for the following 3 months except the most recent month '4': salary 40 for month '3', 30 for month '2' and 20 for month '1' So the cumulative sum of salary of this employee over 3 months is 90(40+30+20), 50(30+20) and 20 respectively. 

| Id | Month | Salary | 
|----|-------|--------| 
| 1 | 3 | 90 | 
| 1 | 2 | 50 | 
| 1 | 1 | 20 | 

Employee '2' only has one salary record (month '1') except its most recent month '2'. 

| Id | Month | Salary | 
|----|-------|--------| 
| 2 | 1 | 20 | 

Employ '3' has two salary records except its most recent pay month '4': month '3' with 60 and month '2' with 40. So the cumulative salary is as following. 

| Id | Month | Salary |
|----|-------|--------| 
| 3 | 3 | 100 | 
| 3 | 2 | 40 |

<br>

**<font size="3" color='blue'>Answer</font>**

<span style = "color:red"> 'WHERE' cannot use the column alias defined in the same query. The basic logic to get cumulative sum is to use JOIN .. ON t1.key = t2.key - 1. </span>

+ table `maxmonth` joins `Employee E1` ON (maxmonth.id = E1.id AND maxmonth.month > E1.month) is to get all months without max_month;
+ then join Employee E2 ON (E2.id = E1.id AND E2.month = E1.month - 1) is to get a table like (similarly for E3):

|id | month | E1.Salary | E2.Salary|
|---|-------|-----------|----------|
|1 | 1 | 20 | null |

`SELECT E1.id, E1.month, (IFNULL(E1.salary, 0) + IFNULL(E2.salary, 0) + IFNULL(E3.salary, 0)) AS Salary 
 FROM (SELECT id, MAX(month) AS month 
       FROM Employee 
       GROUP BY id 
       HAVING COUNT(*) > 1) AS maxmonth ---- table maxmonth 
 LEFT JOIN Employee E1 
 ON (maxmonth.id = E1.id AND maxmonth.month > E1.month)
 LEFT JOIN Employee E2 
 ON (E2.id = E1.id AND E2.month = E1.month - 1) 
 LEFT JOIN Employee E3 
 ON (E3.id = E1.id AND E3.month = E1.month - 2) 
 ORDER BY id ASC , month DESC;` 
 
Another answer is a bit more complicated:

`SELECT Id, Month, Cum_Salary AS Salary 
 FROM (SELECT Id, Month, Salary, 
             (CASE WHEN @record = Id THEN @cum_salary := @cum_salary + Salary 
                   WHEN @record <> @record := Id THEN @cum_salary := Salary END) AS Cum_Salary 
       FROM (SELECT Id, Month, Salary, max_month 
             FROM Employee 
             LEFT JOIN (SELECT Id, MAX(Month) AS max_month 
                        FROM Employee 
                        GROUP BY Id) t1 
             USING (Id) 
             WHERE Month < max_month 
             ORDER BY Id, Month) t2, 
             (SELECT @record := 1, @cum_salary := 0) tmp2
             ) t3 
 ORDER BY Id, Month DESC;`

<a id='580'></a>
## 580. Count Student Number in Departments (Medium)
A university uses 2 data tables, student and department, to store data about its students and the departments associated with each major. Write a query to print the respective department name and number of students majoring in each department for all departments in the department table (even ones with no current students). Sort your results by descending number of students; if two or more departments have the same number of students, then sort those departments alphabetically by department name. 

The student is described as follow: 

| Column Name | Type | 
|-------------|------| 
| student_id | Integer | 
| student_name | String | 
| gender | Character | 
| dept_id | Integer | 

where student_id is the student's ID number, student_name is the student's name, gender is their gender, and dept_id is the department ID associated with their declared major. And the department table is described as below: 

| Column Name | Type | 
|-------------|---------|
| dept_id | Integer | 
| dept_name | String | 

where dept_id is the department's ID number and dept_name is the department name. 

Here is an example input: student table: 

| student_id | student_name | gender | dept_id | 
|------------|--------------|--------|---------|
| 1 | Jack | M | 1 | 
| 2 | Jane | F | 1 | 
| 3 | Mark | M | 2 | 

department table: 

| dept_id | dept_name | 
|---------|-------------| 
| 1 | Engineering | 
| 2 | Science | 
| 3 | Law |

The Output should be: 

| dept_name | student_number | 
|-------------|----------------|
| Engineering | 2 | 
| Science | 1 | 
| Law | 0 |

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT dept_name, COUNT(student_id) AS student_number 
 FROM department 
 LEFT JOIN student 
 USING (dept_id) 
 GROUP BY dept_id 
 ORDER BY student_number DESC, dept_name;`

<a id='584'></a>
## 584. Find Customer Referee (Easy)
Given a table customer holding customers information and the referee. 

| id | name | referee_id| 
|----|------|-----------|
| 1 | Will | NULL | 
| 2 | Jane | NULL | 
| 3 | Alex | 2 | 
| 4 | Bill | NULL | 
| 5 | Zack | 1 | 
| 6 | Mark | 2 | 

Write a query to return the list of customers NOT referred by the person with id '2'. For the sample data above, the result is: 

| name | 
|------|
| Will |
| Jane |
| Bill |
| Zack |

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT name FROM customer WHERE referee_id != 2 OR referee_id IS NULL;`

<a id='585'></a>
## 585. Investments in 2016 (Medium)
Write a query to print the sum of all total investment values in 2016 (TIV_2016), to a scale of 2 decimal places, for all policy holders who meet the following criteria: Have the same TIV_2015 value as one or more other policyholders. Are not located in the same city as any other policyholder (i.e.: the (latitude, longitude) attribute pairs must be unique). 

Input Format: The insurance table is described as follows: 

| Column Name | Type | 
|-------------|------|
| PID | INTEGER(11) | 
| TIV_2015 | NUMERIC(15,2) |
| TIV_2016 | NUMERIC(15,2) |
| LAT | NUMERIC(5,2) |
| LON | NUMERIC(5,2) | 

where PID is the policyholder's policy ID, TIV_2015 is the total investment value in 2015, TIV_2016 is the total investment value in 2016, LAT is the latitude of the policy holder's city, and LON is the longitude of the policy holder's city. 

Sample Input 

| PID | TIV_2015 | TIV_2016 | LAT | LON | 
|-----|----------|----------|-----|-----| 
| 1 | 10 | 5 | 10 | 10 | 
| 2 | 20 | 20 | 20 | 20 | 
| 3 | 10 | 30 | 20 | 20 | 
| 4 | 10 | 40 | 40 | 40 | 

Sample Output 

| TIV_2016 | 
|----------| 
| 45.00 | 

Explanation The first record in the table, like the last record, meets both of the two criteria. The TIV_2015 value '10' is as the same as the third and forth record, and its location unique. The second record does not meet any of the two criteria. Its TIV_2015 is not like any other policyholders. And its location is the same with the third record, which makes the third record fail, too. So, the result is the sum of TIV_2016 of the first and last record, which is 45.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT SUM(insurance.TIV_2016) AS TIV_2016
 FROM insurance 
 WHERE insurance.TIV_2015 IN (SELECT TIV_2015 FROM insurance 
                              GROUP BY TIV_2015 
                              HAVING COUNT(*) > 1 ) 
 AND CONCAT(LAT, LON) IN (SELECT CONCAT(LAT, LON) 
                          FROM insurance 
                          GROUP BY LAT , LON 
                          HAVING COUNT(*) = 1 );`

<a id='586'></a>
## 586. Customer Placing the Largest Number of Orders (Easy)
Query the customer_number from the orders table for the customer who has placed the largest number of orders. It is guaranteed that exactly one customer will have placed more orders than any other customer. The orders table is defined as follows: 

| Column | Type | 
|--------|------| 
| order_number (PK) | int |
| customer_number | int | 
| order_date | date | 
| required_date | date |
| shipped_date | date | 
| status | char(15) |
| comment | char(200) |

Sample Input

| order_number | customer_number | order_date | required_date | shipped_date | status | comment | 
|--------------|-----------------|------------|---------------|--------------|--------|---------| 
| 1 | 1 | 2017-04-09 | 2017-04-13 | 2017-04-12 | Closed | |
| 2 | 2 | 2017-04-15 | 2017-04-20 | 2017-04-18 | Closed | | 
| 3 | 3 | 2017-04-16 | 2017-04-25 | 2017-04-20 | Closed | | 
| 4 | 3 | 2017-04-18 | 2017-04-28 | 2017-04-25 | Closed | | 

Sample Output 

| customer_number |
|-----------------| 
| 3 | 

Explanation The customer with number '3' has two orders, which is greater than either customer '1' or '2' because each of them only has one order. So the result is customer_number '3'. Follow up: What if more than one customer have the largest number of orders, can you find all the customer_number in this case?

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT Customer_number FROM orders 
 GROUP BY Customer_number 
 ORDER BY COUNT(*) DESC LIMIT 1;`

<a id='595'></a>
## 595. Big Countries (Easy)
There is a table World 

| name | continent | area | population | gdp | 
|------|-----------|------|------------|-----|
| Afghanistan | Asia | 652230 | 25500100 | 20343000 |
| Albania | Europe | 28748 | 2831741 | 12960000 | 
| Algeria | Africa | 2381741 | 37100000 | 188681000 | 
| Andorra | Europe | 468 | 78115 | 3712000 | 
| Angola | Africa | 1246700 | 20609294 | 100990000 | 

A country is big if it has an area of bigger than 3 million square km or a population of more than 25 million. Write a SQL solution to output big countries' name, population and area. 

For example, according to the above table, we should output:

| name | population | area | 
|------|------------|------|
| Afghanistan | 25500100 | 652230 | 
| Algeria | 37100000 | 2381741 | 

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT name, population, area FROM World
 WHERE area > 3000000 
 OR population > 25000000;`

<a id='596'></a>
## 596. Classes More Than 5 Students (Easy)
There is a table courses with columns: student and class Please list out all classes which have more than or equal to 5 students. 

For example, the table: 

| student | class | 
|---------|-------|
| A | Math |
| B | English |
| C | Math |
| D | Biology |
| E | Math | 
| F | Computer |
| G | Math |
| H | Math | 
| I | Math | 

Should output: 

| class | 
|-------|
| Math | 

Note: The students should not be counted duplicate in each course.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT class FROM courses 
 GROUP BY class
 HAVING COUNT(DISTINCT student) >= 5;`

<a id='597'></a>
## 597. Friend Requests I: Overall Acceptance Rate (Easy)

In social network like Facebook or Twitter, people send friend requests and accept others’ requests as well. Now given two tables as below: 

Table: friend_request

| sender_id | send_to_id |request_date| 
|-----------|------------|------------|
| 1 | 2 | 2016_06-01 |
| 1 | 3 | 2016_06-01 | 
| 1 | 4 | 2016_06-01 | 
| 2 | 3 | 2016_06-02 | 
| 3 | 4 | 2016-06-09 | 

Table: request_accepted

| requester_id | accepter_id |accept_date | 
|--------------|-------------|------------| 
| 1 | 2 | 2016_06-03 |
| 1 | 3 | 2016-06-08 | 
| 2 | 3 | 2016-06-08 | 
| 3 | 4 | 2016-06-09 | 
| 3 | 4 | 2016-06-10 | 

Write a query to find the overall acceptance rate of requests rounded to 2 decimals, which is the number of acceptance divide the number of requests. 

For the sample data above, your query should return the following result. 

|accept_rate| 
|-----------| 
| 0.80|

Note: The accepted requests are not necessarily from the table friend_request. In this case, you just need to simply count the total accepted requests (no matter whether they are in the original requests), and divide it by the number of requests to get the acceptance rate. It is possible that a sender sends multiple requests to the same receiver, and a request could be accepted more than once. In this case, the ‘duplicated’ requests or acceptances are only counted once. If there is no requests at all, you should return 0.00 as the accept_rate. 

Explanation: There are 4 unique accepted requests, and there are 5 requests in total. So the rate is 0.80. 

Follow-up: Can you write a query to return the accept rate but for every month? How about the cumulative accept rate for every day?

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is that request_accepted table has duplicate (requester_id, accepter_id)

`SELECT ROUND(IFNULL((SELECT COUNT(*) 
                      FROM (SELECT DISTINCT requester_id, accepter_id 
                            FROM request_accepted) AS A) / (
                      SELECT COUNT(*) 
                      FROM (SELECT DISTINCT sender_id, send_to_id 
                            FROM friend_request) AS B), 0), 2) AS accept_rate --- Method 2: SELECT ROUND(SUM(CASE WHEN accepter_id IS NULL THEN 0 ELSE 1 END)/ SUM(CASE WHEN sender_id IS NULL THEN 0 ELSE 1 END), 2) AS accept_rate FROM (SELECT DISTINCT t1.sender_id, t2.accepter_id FROM friend_request t1 LEFT JOIN request_accepted t2 ON t1.sender_id = t2.requester_id AND t1.send_to_id = t2.accepter_id) TMP;`

<a id='601'></a>
## 601. Human Traffic of Stadium (Hard)

X city built a new stadium, each day many people visit it and the stats are saved as these columns: id, visit_date, people Please write a query to display the records which have 3 or more consecutive rows and the amount of people more than 100(inclusive). 

For example, the table stadium: 

| id | visit_date | people | 
|----|------------|--------|
| 1 | 2017-01-01 | 10 | 
| 2 | 2017-01-02 | 109 | 
| 3 | 2017-01-03 | 150 | 
| 4 | 2017-01-04 | 99 | 
| 5 | 2017-01-05 | 145 | 
| 6 | 2017-01-06 | 1455 | 
| 7 | 2017-01-07 | 199 | 
| 8 | 2017-01-08 | 188 | 

For the sample data above, the output is: 

| id | visit_date | people | 
|----|------------|--------|
| 5 | 2017-01-05 | 145 | 
| 6 | 2017-01-06 | 1455 | 
| 7 | 2017-01-07 | 199 | 
| 8 | 2017-01-08 | 188 |

Note: Each day only have one row record, and the dates are increasing with id increasing.

<br>

**<font size="3" color='blue'>Answer</font>**

There are 3 answers:

1. Method 1: union 3 tables and list each condition where t1.id occurs in the beginning, middle or end of the sequence.

`SELECT DISTINCT t1.* FROM stadium t1, stadium t2, stadium t3 
 WHERE t1.people >= 100 
 AND t2.people >= 100 
 AND t3.people >= 100 
 AND ((t1.id - t2.id = 1 and t1.id - t3.id = 2 and t2.id - t3.id =1) -- t1, t2, t3 
       OR (t2.id - t1.id = 1 and t2.id - t3.id = 2 and t1.id - t3.id =1) -- t2, t1, t3 
       OR (t3.id - t2.id = 1 and t2.id - t1.id =1 and t3.id - t1.id = 2) -- t3, t2, t1 ) 
 ORDER BY t1.id;`

2. Method 2: window function using lead and lag, still need to discuss different combinations.

`SELECT s1.id, s1.visit_date, s1.people 
 FROM (SELECT s.id, s.visit_date, s.people, 
              lead(people) OVER (ORDER BY id ASC) as next1, 
              lead(people,2) OVER (ORDER BY id ASC ) as next2, 
              lag(people) OVER (ORDER BY id ASC) as prev1, 
              lag(people,2) OVER (ORDER BY id ASC ) as prev2
       FROM stadium as s) AS s1 
 WHERE (people >=100 
        AND ((next1>=100 and next2>=100) 
             OR (prev1>=100 and prev2>=100) 
             OR (prev1>=100 and next1>=100)));`

3. <span style = "color:red"> Method 3 </span>: create two variables to flag the beginning and the end of the sequence:
    + Num_end flags the end of the sequence where 1 means the last part of the sequence, and 2 means the second last part
    + Num_begin flags the beginning of the sequence where 1 means the first part of the sequence, and 2 means the second part
    + Therefore, to select consective 3 parts we just need to ensure that Num_end + Num_begin >= 3.

`SELECT id, visit_date, people 
 FROM ( SELECT *, @b := (@b + 1) * (people >= 100) AS Num_begin --- beginning of the sequence 
        FROM ( SELECT *, @a := (@a + 1) * (people >= 100) AS Num_end --- end of the sequence 
               FROM stadium, (SELECT @a := 0) tmp1 
               ORDER BY id desc) t1, 
             (SELECT @b := 0) tmp2 
        ORDER BY id) t2 
 WHERE Num_end + Num_begin > 3;`

<a id='607'></a>
## 607. Sales Person (Easy)

Description Given three tables: salesperson, company, orders. Output all the names in the table salesperson, who didn’t have sales to company 'RED'. 

Example Input Table: salesperson

| sales_id | name | salary | commission_rate | hire_date | 
|----------|------|--------|-----------------|-----------|
| 1 | John | 100000 | 6 | 4/1/2006 | 
| 2 | Amy | 120000 | 5 | 5/1/2010 | 
| 3 | Mark | 65000 | 12 | 12/25/2008|
| 4 | Pam | 25000 | 25 | 1/1/2005 |
| 5 | Alex | 50000 | 10 | 2/3/2007 | 

The table salesperson holds the salesperson information. Every salesperson has a sales_id and a name. 

Table: company 

| com_id | name | city | 
|--------|------|------|
| 1 | RED | Boston | 
| 2 | ORANGE | New York | 
| 3 | YELLOW | Boston | 
| 4 | GREEN | Austin | 

The table company holds the company information. Every company has a com_id and a name. 

Table: orders

| order_id | order_date | com_id | sales_id | amount | 
|----------|------------|--------|----------|--------|
| 1 | 1/1/2014 | 3 | 4 | 100000 | 
| 2 | 2/1/2014 | 4 | 5 | 5000 | 
| 3 | 3/1/2014 | 1 | 1 | 50000 | 
| 4 | 4/1/2014 | 1 | 4 | 25000 | 

The table orders holds the sales record information, salesperson and customer company are represented by sales_id and com_id. 

output 

| name | 
|------|
| Amy |
| Mark |
| Alex | 

Explanation According to order '3' and '4' in table orders, it is easy to tell only salesperson 'John' and 'Alex' have sales to company 'RED', so we need to output all the other names in table salesperson.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT name FROM salesperson 
 WHERE sales_id NOT IN (SELECT DISTINCT sales_id FROM orders 
                        WHERE com_id = (SELECT com_id FROM company 
                                        WHERE name = "RED"));`

<a id='602'></a>
## 602. Friend Requests II: Who Has the Most Friends (Medium)
In social network like Facebook or Twitter, people send friend requests and accept others' requests as well. Table request_accepted holds the data of friend acceptance, while requester_id and accepter_id both are the id of a person.

| requester_id | accepter_id | accept_date| 
|--------------|-------------|------------| 
| 1 | 2 | 2016_06-03 | 
| 1 | 3 | 2016-06-08 | 
| 2 | 3 | 2016-06-08 | 
| 3 | 4 | 2016-06-09 |

Write a query to find the the people who has most friends and the most friends number. For the sample data above, the result is: 

| id | num |
|----|-----|
| 3 | 3 | 

Note: It is guaranteed there is only 1 people having the most friends. The friend request could only been accepted once, which mean there is no multiple records with the same requester_id and accepter_id value. Explanation: The person with id '3' is a friend of people '1', '2' and '4', so he has 3 friends in total, which is the most number than any others. Follow-up: In the real world, multiple people could have the same most number of friends, can you find all these people in this case?

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is the friends of a person could be the one who requests and the one who accepts.

`SELECT ids AS id, COUNT(*) AS num 
 FROM ( SELECT requester_id AS ids FROM request_accepted 
        UNION ALL 
        SELECT accepter_id AS ids FROM request_accepted) AS t1 
 GROUP BY ids 
 ORDER BY num DESC LIMIT 1;`

<a id='175'></a>
## 603. Consecutive Available Seats (Easy)
Several friends at a cinema ticket office would like to reserve consecutive available seats. Can you help to query all the consecutive available seats order by the seat_id using the following cinema table?

| seat_id | free |
|---------|------| 
| 1 | 1 | 
| 2 | 0 |
| 3 | 1 | 
| 4 | 1 | 
| 5 | 1 | 

Your query should return the following result for the sample case above. 

| seat_id | 
|---------| 
| 3 | 
| 4 |
| 5 | 

Note: The seat_id is an auto increment int, and free is bool ('1' means free, and '0' means occupied.). Consecutive available seats are more than 2(inclusive) seats consecutively available.

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is: The consective seats or neighboring seats are obtained by the absolute value of the distance of seats: `ABS(t1.seat_id - t2.seat_id) = 1`

Need to use `DISTINCT seat_id` as we may select multiple seat_ids!

`SELECT DISTINCT t1.seat_id FROM cinema t1 
 JOIN cinema t2 
 ON (ABS(t1.seat_id - t2.seat_id) = 1
     AND t1.free = 1 
     AND t2.free = 1) 
 ORDER BY t1.seat_id;`

<a id='608'></a>
## 608. Tree Node (Medium)

Given a table tree, id is identifier of the tree node and p_id is its parent node's id. 

| id | p_id | 
|----|------| 
| 1 | null | 
| 2 | 1 | 
| 3 | 1 | 
| 4 | 2 | 
| 5 | 2 | 

Each node in the tree can be one of three types: Leaf: if the node is a leaf node. Root: if the node is the root of the tree. Inner: If the node is neither a leaf node nor a root node. Write a query to print the node id and the type of the node. Sort your output by the node id. 

The result for the above sample is: 

| id | Type | 
|----|------|
| 1 | Root |
| 2 | Inner|
| 3 | Leaf |
| 4 | Leaf |
| 5 | Leaf | 

Explanation Node '1' is root node, because its parent node is NULL and it has child node '2' and '3'. Node '2' is inner node, because it has parent node '1' and child node '4' and '5'. Node '3', '4' and '5' is Leaf node, because they have parent node and they don't have child node. And here is the image of the sample tree as below: 1 / \ 2 3 / \ 4 5 Note If there is only one node on the tree, you only need to output its root attributes.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT id, (CASE WHEN p_id IS NULL THEN "Root" 
                  WHEN id IN (SELECT DISTINCT p_id FROM tree WHERE p_id IS NOT NULL) 
                       AND p_id IS NOT NULL THEN "Inner" 
                  WHEN id NOT IN (SELECT DISTINCT p_id FROM tree WHERE p_id IS NOT NULL) THEN "Leaf" END) AS Type FROM tree ORDER BY id;`

<a id='610'></a>
## 610. Triangle Judgement (Easy)
A pupil Tim gets homework to identify whether three line segments could possibly form a triangle. However, this assignment is very heavy because there are hundreds of records to calculate. Could you help Tim by writing a query to judge whether these three sides can form a triangle, assuming table triangle holds the length of the three sides x, y and z. 

| x | y | z |
|----|----|----| 
| 13 | 15 | 30 | 
| 10 | 20 | 15 | 

For the sample data above, your query should return the follow result: 

| x | y | z | triangle |
|----|----|----|----------| 
| 13 | 15 | 30 | No |
| 10 | 20 | 15 | Yes |

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT x, y, z, (CASE WHEN x + y <= z OR x + z <= y OR y + z <= x THEN "No" ELSE "Yes" END) AS triangle 
 FROM triangle;`

<a id='612'></a>
## 612. Shortest Distance in a Plane (Medium)

Table point_2d holds the coordinates (x,y) of some unique points (more than two) in a plane. Write a query to find the shortest distance between these points rounded to 2 decimals. 

| x | y | 
|----|----| 
| -1 | -1 | 
| 0 | 0 | 
| -1 | -2 | 

The shortest distance is 1.00 from point (-1,-1) to (-1,2). So the output should be:

| shortest |
|----------| 
| 1.00 | 

Note: The longest distance among all the points are less than 10000.

<br>

**<font size="3" color='blue'>Answer</font>**
Squared uses POW()

`SELECT ROUND(SQRT(MIN((POW(p1.x - p2.x, 2) + POW(p1.y - p2.y, 2)))), 2) AS shortest 
 FROM point_2d p1 
 JOIN point_2d p2 
 ON p1.x != p2.x 
 OR p1.y != p2.y ;`

<a id='613'></a>
## 613. Shortest Distance in a Line (Easy)
Table point holds the x coordinate of some points on x-axis in a plane, which are all integers. Write a query to find the shortest distance between two points in these points. 

| x |
|-----| 
| -1 | 
| 0 | 
| 2 | 

The shortest distance is '1' obviously, which is from point '-1' to '0'. So the output is as below: 

| shortest| 
|---------| 
| 1 | 

Note: Every point is unique, which means there is no duplicates in table point. 

Follow-up: What if all these points have an id and are arranged from the left most to the right most of x axis?

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT MIN(ABS(t1.x - t2.x)) AS shortest 
 FROM point t1 
 JOIN point t2 
 ON t1.x != t2.x;`

<a id='614'></a>
## 614. Second Degree Follower (Medium)

In facebook, there is a follow table with two columns: followee, follower. Please write a sql query to get the amount 
of each follower’s follower if he/she has one. 

For example: 

| followee | follower | 
|----------|----------|
| A | B | 
| B | C | 
| B | D | 
| D | E | 

should output: 

| follower | num | 
|----------|-----|
| B | 2 | 
| D | 1 | 

Explaination: Both B and D exist in the follower list, when as a followee, B's follower is C and D, and D's follower is E. A does not exist in follower list. Note: Followee would not follow himself/herself in all cases. Please display the result in follower's alphabet order.

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is: Follower and follwee are not identical, they may be different in terms of lowercase or uppercase. However, lower and upper case refer to the same person, so we cannot use WHERE follwer IN follwee (as it is case-sensitive);

WE NEED TO DISPLAY Follower in the case-sensitive format!

`SELECT f1.follower, COUNT(DISTINCT f2.follower) as num
 FROM follow f1
 JOIN follow f2 
 ON f1.follower = f2.followee
 GROUP BY f1.follower
 ORDER BY f1.follower;`

<a id='615'></a>
## 615. Average Salary: Departments VS Company (Hard)

Given two tables as below, write a query to display the comparison result (higher/lower/same) of the average salary of employees in a department to the company's average salary. 

Table: salary 

| id | employee_id | amount | pay_date | 
|----|-------------|--------|----------|
| 1 | 1 | 9000 | 2017-03-31 | 
| 2 | 2 | 6000 | 2017-03-31 |
| 3 | 3 | 10000 | 2017-03-31 |
| 4 | 1 | 7000 | 2017-02-28 | 
| 5 | 2 | 6000 | 2017-02-28 |
| 6 | 3 | 8000 | 2017-02-28 | 

The employee_id column refers to the employee_id in the following table employee. 

| employee_id | department_id | 
|-------------|---------------|
| 1 | 1 |
| 2 | 2 | 
| 3 | 2 | 

So for the sample data above, the result is: 

| pay_month | department_id | comparison | 
|-----------|---------------|------------| 
| 2017-03 | 1 | higher | 
| 2017-03 | 2 | lower | 
| 2017-02 | 1 | same | 
| 2017-02 | 2 | same | 

Explanation In March, the company's average salary is (9000+6000+10000)/3 = 8333.33... The average salary for department '1' is 9000, which is the salary of employee_id '1' since there is only one employee in this department. So the comparison result is 'higher' since 9000 > 8333.33 obviously. The average salary of department '2' is (6000 + 10000)/2 = 8000, which is the average of employee_id '2' and '3'. So the comparison result is 'lower' since 8000 < 8333.33. With he same formula for the average salary comparison in February, the result is 'same' since both the department '1' and '2' have the same average salary with the company, which is 7000.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT t1.pay_month, t1.department_id, 
        (CASE WHEN avg_department > avg_company THEN "higher"
              WHEN avg_department < avg_company THEN "lower" 
              ELSE "same" END) AS comparison 
 FROM ( SELECT department_id, DATE_FORMAT(pay_date,'%Y-%m') AS pay_month, 
               AVG(amount) AS avg_department 
        FROM salary 
        JOIN employee 
        USING (employee_id) 
        GROUP BY department_id, pay_month) t1 
 JOIN ( SELECT DATE_FORMAT(pay_date,'%Y-%m') AS pay_month, AVG(amount) AS avg_company 
        FROM salary 
        GROUP BY pay_month) t2 
 USING (pay_month);`

<a id='618'></a>
## 618. Students Report By Geography (Hard)
A U.S graduate school has students from Asia, Europe and America. The students' location information are stored in table student as below. 

| name | continent | 
|------|-----------| 
| Jack | America | 
| Pascal | Europe | 
| Xi | Asia | 
| Jane | America |

Pivot the continent column in this table so that each name is sorted alphabetically and displayed underneath its corresponding continent. The output headers should be America, Asia and Europe respectively. It is guaranteed that the student number from America is no less than either Asia or Europe. 

For the sample input, the output is: 

| America | Asia | Europe |
|---------|------|--------| 
| Jack | Xi | Pascal |
| Jane | | |

Follow-up: If it is unknown which continent has the most students, can you write a query to generate the student report?

<br>

**<font size="3" color='blue'>Answer</font>**

**The tricky part** is <span style = "color:red">We need to use MAX(America) to select the meaningful string, because the derived table contains NULL </span>

`SELECT MAX(America) AS America, MAX(Asia) as Asia, MAX(Europe) AS Europe 
 FROM ( SELECT (CASE WHEN continent = 'America' THEN @r1 := @r1 + 1
                    WHEN continent = 'Asia' THEN @r2 := @r2 + 1 
                    WHEN continent = 'Europe' THEN @r3 := @r3 + 1 END) row_id, 
               (CASE WHEN continent = 'America' THEN name END) America, 
               (CASE WHEN continent = 'Asia' THEN name END) Asia, 
               (CASE WHEN continent = 'Europe' THEN name END) Europe 
        FROM student, (SELECT @r1 := 0, @r2 := 0, @r3 := 0) AS row_id 
        ORDER BY name ) t 
 GROUP BY row_id;`

<a id='619'></a>
## 619. Biggest Single Number (Easy)

Table my_numbers contains many numbers in column num including duplicated ones. Can you write a SQL query to find the biggest number, which only appears once. 

|num| 
|---|
| 8 | 
| 8 |
| 3 |
| 3 | 
| 1 | 
| 4 |
| 5 |
| 6 | 

For the sample data above, your query should return the following result: 

|num| 
|---| 
| 6 | 

Note: If there is no such number, just output null.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT MAX(single_num) AS num 
 FROM (SELECT num AS single_num FROM my_numbers 
       GROUP BY num
       HAVING COUNT(*) = 1) tmp;`

<a id='620'></a>
## 620. Not Boring Movies (Easy)

X city opened a new cinema, many people would like to go to this cinema. The cinema also gives out a poster indicating the movies’ ratings and descriptions. Please write a SQL query to output movies with an odd numbered ID and a description that is not 'boring'. Order the result by rating. 

For example, table cinema: 

| id | movie | description | rating | 
|----|-------|-------------|--------|
| 1 | War | great 3D | 8.9 |
| 2 | Science | fiction | 8.5 |
| 3 | irish | boring | 6.2 | 
| 4 | Ice song | Fantacy | 8.6 |
| 5 | House card| Interesting| 9.1 |

For the example above, the output should be: 

| id | movie | description | rating |
|----|-------|-------------|--------|
| 5 | House card| Interesting| 9.1 | 
| 1 | War | great 3D | 8.9 |

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT * FROM cinema
 WHERE description != "boring" 
 AND MOD(id, 2) = 1 
 ORDER BY rating DESC;`

<a id='626'></a>
## 626. Exchange Seats (Medium)

Mary is a teacher in a middle school and she has a table seat storing students' names and their corresponding seat ids. The column id is continuous increment. Mary wants to change seats for the adjacent students. Can you write a SQL query to output the result for Mary? 

| id | student | 
|----|---------|
| 1 | Abbot | 
| 2 | Doris |
| 3 | Emerson | 
| 4 | Green | 
| 5 | Jeames |

For the sample input, the output is: 

| id | student |
|----|---------|
| 1 | Doris | 
| 2 | Abbot | 
| 3 | Green | 
| 4 | Emerson | 
| 5 | Jeames |

Note: If the number of students is odd, there is no need to change the last one's seat.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT (CASE WHEN MOD(id, 2) = 1 AND id != @max_id THEN id + 1
              WHEN MOD(id, 2) = 0 THEN id - 1 
              WHEN MOD(id, 2) = 1 AND id = @max_id THEN id END) AS id, 
         student
 FROM seat, (SELECT @max_id := (SELECT MAX(id) FROM seat)) tmp 
 ORDER BY id;`

<a id='627'></a>
## 627. Swap Salary (Easy)

Given a table salary, such as the one below, that has m=male and f=female values. Swap all f and m values (i.e., change all f values to m and vice versa) with a single update statement and no intermediate temp table. Note that you must write a single update statement, DO NOT write any select statement for this problem. 

Example: 

| id | name | sex | salary |
|----|------|-----|--------|
| 1 | A | m | 2500 |
| 2 | B | f | 1500 | 
| 3 | C | m | 5500 | 
| 4 | D | f | 500 | 

After running your update statement, the above salary table should have the following rows: 

| id | name | sex | salary | 
|----|------|-----|--------|
| 1 | A | f | 2500 |
| 2 | B | m | 1500 | 
| 3 | C | f | 5500 | 
| 4 | D | m | 500 |

<br>

**<font size="3" color='blue'>Answer</font>**

`UPDATE salary SET sex = IF (sex = "m", "f", "m");`

<a id='1045'></a>
## 1045. Customers Who Bought All Products (Medium)

Table: Customer 

| Column Name | Type | 
|-------------|------|
| customer_id | int |
| product_key | int | 

product_key is a foreign key to Product table.

Table: Product 

| Column Name | Type  |
|-------------|-------|
| product_key | int | 

product_key is the primary key column for this table. 

Write an SQL query for a report that provides the customer ids from the Customer table that bought all the products in the Product table. 

For example: 

Customer table:

| customer_id | product_key | 
|-------------|-------------|
| 1 | 5 | 
| 2 | 6 | 
| 3 | 5 | 
| 3 | 6 |
| 1 | 6 |

Product table:

| product_key | 
|-------------|
| 5 |
| 6 | 

Result table: 

| customer_id | 
|-------------| 
| 1 |
| 3 |

The customers who bought all the products (5 and 6) are customers with id 1 and 3.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT customer_id 
 FROM (SELECT DISTINCT customer_id, product_key FROM Customer) tmp 
 GROUP BY customer_id 
 HAVING SUM(product_key) = (SELECT SUM(product_key) FROM Product);`

<a id='1050'></a>
## 1050. Actors and Directors Who Cooperated At Least Three Times (Easy)

Table: ActorDirector 

| Column Name | Type |
|-------------|------|
| actor_id | int |
| director_id | int |
| timestamp | int | 

timestamp is the primary key column for this table. 

Write a SQL query for a report that provides the pairs (actor_id, director_id) where the actor have cooperated with the director at least 3 times. 

Example: ActorDirector table:

| actor_id | director_id | timestamp |
|----------|-------------|-----------|
| 1 | 1 | 0 | 
| 1 | 1 | 1 | 
| 1 | 1 | 2 | 
| 1 | 2 | 3 | 
| 1 | 2 | 4 | 
| 2 | 1 | 5 | 
| 2 | 1 | 6 |

Result table: 

| actor_id | director_id | 
|----------|-------------|
| 1 | 1 | 

The only pair is (1, 1) where they cooperated exactly 3 times.

<br>

**<font size="3" color='blue'>Answer</font>**

`SELECT actor_id, director_id 
 FROM ActorDirector 
 GROUP BY actor_id, director_id 
 HAVING COUNT(*) >= 3;`
