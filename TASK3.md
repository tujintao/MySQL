MySQL 基础 （二）- 表操作
1. MySQL表数据类型
2. 用SQL语句创建表
    语句解释
    设定列类型 、大小、约束
    设定主键
3. 用SQL语句向表中添加数据
    语句解释
    多种添加方式（指定列名；不指定列名）
4. 用SQL语句删除表
    语句解释
    DELETE
    DROP
    TRUNCATE
    不同方式的区别
5. 用SQL语句修改表
    修改列名
    修改表中数据
    删除行
    删除列
    新建列
    新建行
    
项目三
1.创建表  
CREATE TABLE email ( 
student char(5) NOT NULL
class char(10) NOT NULL
PRIMARY KEY (student)
)ENGINE=InnoDB;

+---------+----------+
| student | class    |
+---------+----------+
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |
| A       | Math     |
+---------+----------+

2.列出所有超过或等于5名学生的课
select class from courses group by class
having count(distinct student) >= 5

+-------+
| class |
+-------+
| Math  |
+-------+


项目四
1.创建表  
CREATE TABLE email ( 
id int NOT NULL
name char(5) NOT NULL
sex char(5) NOT NULL
salary int NOT NULL
PRIMARY KEY (id)
)ENGINE=InnoDB;
+----+------+------+--------+
| id | name | sex  | salary |
+----+------+------+--------+
|  1 | A    | m    | 2500   |
|  2 | B    | f    | 1500   |
|  3 | C    | m    | 5500   |
|  4 | D    | f    | 500    |
+----+------+------+--------+

2.交换所有的 f 和 m 值(例如，将所有 f 值更改为 m，反之亦然)。要求使用一个更新查询，并且没有中间临时表。
UPDATE salary SET sex= (CASE WHEN sex = 'm' THEN 'f' ELSE 'm' END);
+----+------+------+--------+
| id | name | sex  | salary |
+----+------+------+--------+
|  1 | A    | f    | 2500   |
|  2 | B    | m    | 1500   |
|  3 | C    | f    | 5500   |
|  4 | D    | m    | 500    |
+----+------+------+--------+

项目五

