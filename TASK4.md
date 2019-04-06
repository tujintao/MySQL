4.1 MySQL 实战
#学习内容#
数据导入导出
将之前创建的任意一张MySQL表导出,且是CSV格式
再将CSV表导入数据库

项目七: 各部门工资最高的员工（难度：中等）  
创建Employee 表，包含所有员工信息，每个员工有其对应的 Id, salary 和 department Id。  
CREATE TABLE Employee(
	Id int(10) NOT NULL,
	Name VARCHAR(10) NOT NULL,
	Salary int(10) NOT NULL,
	DepartmentId int(4) NOT NULL,
  PRIMARY KEY (Id)
)ENGINE=InnoDB;  

+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
|  1 | Joe   |  70000 |            1 |
|  2 | Henry |  80000 |            2 |
|  3 | Sam   |  60000 |            2 |
|  4 | Max   |  90000 |            1 |
+----+-------+--------+--------------+


CREATE TABLE Department(
	Id int(10) NOT NULL,
	Name VARCHAR(10) NOT NULL,
  PRIMARY KEY (Id)
)ENGINE=InnoDB;

+----+-------+
| Id | Name  |
+----+-------+
|  1 | IT    |
|  2 | Sales |
+----+-------+

SELECT Department,Employee,MAX(Salary) FROM
(SELECT d.Name as Department,e.Name as Employee,e.Salary FROM Employee e join Department d
on e.DepartmentId=d.Id) t
GROUP BY Department;

+------------+----------+-------------+
| Department | Employee | MAX(Salary) |
+------------+----------+-------------+
| IT         | Joe      |       90000 |
| Sales      | Henry    |       80000 |
+------------+----------+-------------+


项目八: 换座位（难度：中等）
小美是一所中学的信息科技老师，她有一张 seat 座位表，平时用来储存学生名字和与他们相对应的座位 id。
其中纵列的 id 是连续递增的
小美想改变相邻俩学生的座位。
你能不能帮她写一个 SQL query 来输出小美想要的结果呢？
CREATE TABLE seat(
	id int(10) NOT NULL,
	student VARCHAR(10) NOT NULL,
  PRIMARY KEY (id)
)ENGINE=InnoDB;

+----+---------+
| id | student |
+----+---------+
|  1 | Abbot   |
|  2 | Doris   |
|  3 | Emerson |
|  4 | Green   |
|  5 | Jeames  |
+----+---------+

SELECT (CASE
	WHEN id%2<>0 AND id<>(SELECT COUNT(*) FROM seat)  THEN id+1
	WHEN id%2<>0 AND id=(SELECT COUNT(*) FROM seat) THEN id
	ELSE id-1
	END) 
	AS id,student FROM seat ORDER BY id ASC;

+----+---------+
| id | student |
+----+---------+
|  1 | Doris   |
|  2 | Abbot   |
|  3 | Green   |
|  4 | Emerson |
|  5 | Jeames  |
+----+---------+


项目九:  分数排名（难度：中等）
编写一个 SQL 查询来实现分数排名。如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。
CREATE TABLE score(
	Id int(10) NOT NULL,
	Score FLOAT(4) NOT NULL,
  PRIMARY KEY (Id)
)ENGINE=InnoDB;

+----+-------+
| Id | Score |
+----+-------+
|  1 |   3.5 |
|  2 |  3.65 |
|  3 |     4 |
|  4 |  3.85 |
|  5 |     4 |
|  6 |  3.65 |
+----+-------+

select Score,
(select count(distinct Score) from Score as s2 where s2.Score >= s1.Score) Rank 
from Score as s1
order by Score DESC;

+-------+------+
| Score | Rank |
+-------+------+
|     4 |    1 |
|     4 |    1 |
|  3.85 |    2 |
|  3.65 |    3 |
|  3.65 |    3 |
|   3.5 |    4 |
+-------+------+

