
 实验2：用户及权限管理

## 实验目的：

掌握用户管理、角色管理、权根维护与分配的能力，掌握用户之间共享对象的操作技能。

## 实验内容：
Oracle有一个开发者角色resource，可以创建表、过程、触发器等对象，但是不能创建视图。本训练要求：
- 在pdborcl插接式数据中创建一个新的本地角色con_res_view，该角色包含connect和resource角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view的用户就同时拥有这三种权限。
- 创建角色之后，再创建用户new_user，给用户分配表空间，设置限额为50M，授予con_res_view角色。
- 最后测试：用新用户new_user连接数据库、创建表，插入数据，创建视图，查询表和视图的数据。

## 实验步骤



- 第1步：以system登录到pdborcl，创建角色con_res_view和用户new_user，并授权和分配空间：
CREATE ROLE CON_RES_VIEW_LMQ;   //创建角色
GRANT CONNECT, RESOURCE, CREATE VIEW TO CON_RES_VIEW_LMQ;  //授予角色权限
CREATE USER NEW_USER_LMQ IDENTIFIED BY 123 DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;	//创建用户
ALTER USER NEW_USER_LMQ QUOTA 50M ON USERS;	//授权用户访问用户表空间，空间限额是50M
GRANT CON_RES_VIEW_LMQ TO NEW_USER_LMQ;	    //将角色权限授予用户



![运行结果](https://github.com/liumengqi77/oracle/blob/master/test2/1.png)


- 第2步：新用户new_user连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。

GRANT SELECT ON MYVIEW_WTS TO hr;    //将MYVIEW_WTS的SELECT对象权限授予hr用户

![运行结果](https://github.com/liumengqi77/oracle/blob/master/test2/2.png)


- 第3步：用户hr连接到pdborcl，查询new_user授予它的视图myview

SELECT * FROM NEW_USER_WTS.MYVIEW_LMQ;  //登录HR用户查询MYVIEW_LMQ视图


![运行结果](https://github.com/liumengqi77/oracle/blob/master/test2/3.png)

实验分析
 对象，拥有者（即创建者）拥有所有权限，Oracle允许将对象的某些权限授予其他用户，以此能实现用户之间共享对象的权限。 
在创建用户后需要给用户分配角色，以此来授予用户权限，其他的用户若想要访问这个用户的表，需要被该用户授予相应的权限才能做到





