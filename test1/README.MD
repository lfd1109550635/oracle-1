# oracle 实验一
## 1.查询语句一
```java
SELECT d.department_name ,count(e.job_id)as "部门总人数" ,
avg(e.salary)as "平均工资"
from hr.departments d ,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT' ,'Sales')
GROUP BY department_name;
```
### 1.1查询结果
![blockchain](https://github.com/DevinChenPeng/oracle/blob/master/N29Z%T_PO8@2_N4UQ4S12%P.png "区块链")
### 1.2优化指导
为数据库创建一个或多个索引来改进当前语句的执行计划。

## 2.查询语句二
```java
SELECT d.department_name ,count(e.job_id)as "部门总人数" ,
avg(e.salary)as "平均工资"
FROM hr.departments d ,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT' ,'Sales');
```
### 2.1查询结果
![blockchain](https://github.com/DevinChenPeng/oracle/blob/master/N29Z%T_PO8@2_N4UQ4S12%P.png "区块链")
### 2.2优化指导
无

## 3.自定义语句
```java
SELECT d.department_name ,count(e.job_id)as "部门总人数" ,
avg(e.salary)as "平均工资"
FROM hr.departments d, hr.employees e
WHERE d.department_id = e.department_id
and d.department_name = 'IT' or d.department_name = 'Sales'
GROUP BY department_name 
```
### 3.1查询结果
![blockchain](https://github.com/DevinChenPeng/oracle/blob/master/UD4K3WWOLD_O%5B8_S0CO60%5DI.png "区块链")

### 3.2优化指导
取消where语句处大量的笛卡尔积操作

## 4.总结
教材的第二条查询语句最好，oracle没有给出优化指导，查询语句一需要添加一个或多个索引增加查询约束，自定义查询语句需要减少语句查询时产生的大量的笛卡尔积。
![blockchain]()
