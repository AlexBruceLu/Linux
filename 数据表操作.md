###1 在mydb2数据库中创建表tb1，要求字段id( int类型 ，自动增长,主键，) user （varchar(30)，不可以为空），password（varchar(30),不能为空），create(datetime类型)

 create table tb1 (id int auto_increment primary key,user varchar(30) not null,password varchar(30) not null, createtime datetime);
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/1.png)  

###2 查看表tb1的结构

 show columns from tb1 from mydb2;
 show columns from mydb2.tb1;
 describe tb1;
 desc tb1;
  ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/21.png)
  ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/22.png)
  ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/23.png)
  ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/24.png)

###3 在tb1表中 添加新字段email，类型为varchar(50),not null,将字段user的类型由varchar(30)改为varchar(40)。

 alter table tb1 add email varchar(50) not null , modify user varchar(40) not null;(modify修改时不加not null，默认为yes可以为空，需要手动添加）
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/25.png)

###4 将数据表tb1的字段名user修改为username

 alter table tb1 change column user username varchar(40);
注：通过ALTER语句修改列，其前提是必须将表中数据全部删除，然后才可以修改表列。
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/26.png)

###5 删除表tb1中的字段 email

 alter table tb1 drop email;
  ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/27.png)

###6 将数据表tb1更名为 table1

 alter table tb1 rename as table1;
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/28.png)

###7 利用rename重命名表table1为tb1

 rename table table1 to tb1;
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/29.png)

###8 通过tb1 复制出 表 tb2 准备数据：insert into tb1 values(1,'Tom','123','2018-08-01 11:11:11');    

 insert into tb1 values(1,'Tom','123','2018-08-01 11:11:11');
 create table tb2 like tb1;   //复制了表结构，并没有复制数据，因此是一个空表
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/291.png)

###9 通过tb1复制出 表 tb3 并且将数据也复制到tb3中。

 create table tb3 as select * from tb1;
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/292.png)

###10 删除表 tb2 和 表 tb3;

 drop table tb2 , tb3;
 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/293.png)

###11 查询数据库中所有表名

 select table_name from information_schema.tables where table_schema='huoying' and table_type='base table';

###12 查询指定数据库中指定表的所有字段名column_name

 select column_name from information_schema.columns where table_schema='name' and table_name='users';
