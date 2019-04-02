#任务二#
MySQL 基础 （一）- 查询语句

#学习内容#
1. 导入示例数据库，教程 https://www.yiibai.com/mysql/how-to-load-sample-database-into-mysql-database-server.html
2. SQL是什么？MySQL是什么？
3. 查询语句 SELECT FROM 
    语句解释
    去重语句
    前N个语句
    CASE...END判断语句
4. 筛选语句 WHERE 
    语句解释
    运算符/通配符/操作符
5. 分组语句 GROUP BY
    聚集函数
    语句解释
    HAVING子句
6. 排序语句 ORDER BY 
    语句解释
    正序、逆序
7. 函数
    时间函数
    数值函数
    字符串函数
8. SQL注释
9. SQL代码规范
    [SQL编程格式的优化建议] https://zhuanlan.zhihu.com/p/27466166
    [SQL Style Guide] https://www.sqlstyle.guide/



项目一：查找重复的电子邮箱
CREATE TABLE email
(
    id int NOT NULL AUTO_INCREMENT
    c char(50) NOT NULL
    PRIMARY KEY (id)
)ENGINE=InnoDB;


select c,count(*) as count  
from email group by c having count>1;  

项目二：查找大国
CREATE TABLE email
(
    cname char(20) NOT NULL  
    continent char(20) NOT NULL  
    area int NOT NULL  
    population int NOT NULL  
    gdp int NOT NULL  
    PRIMARY KEY (cname)  
)ENGINE=InnoDB;  
  
+-----------------+------------+------------+--------------+---------------+  
| name            | continent  | area       | population   | gdp           |  
+-----------------+------------+------------+--------------+---------------+  
| Afghanistan     | Asia       | 652230     | 25500100     | 20343000      |  
| Albania         | Europe     | 28748      | 2831741      | 12960000      |  
| Algeria         | Africa     | 2381741    | 37100000     | 188681000     |  
| Andorra         | Europe     | 468        | 78115        | 3712000       |  
| Angola          | Africa     | 1246700    | 20609294     | 100990000     |  
+-----------------+------------+------------+--------------+---------------+  
  
  
SELECT cname,population,area  
FROM world where area>3000000 or (population>25000 and gdp>20000000)  
  
+--------------+-------------+--------------+  
| name         | population  | area         |  
+--------------+-------------+--------------+  
| Afghanistan  | 25500100    | 652230       |  
| Algeria      | 37100000    | 2381741      |  
+--------------+-------------+--------------+  
