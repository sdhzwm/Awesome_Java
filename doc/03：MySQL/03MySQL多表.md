
## 1、表连接查询

### 0. 数据准备
```sql
# 创建部门表
create table dept(
  id int primary key auto_increment,
  name varchar(20)
)
insert into dept (name) values ('开发部'),('市场部'),('财务部'); # 创建员工表
create table emp (
id int primary key auto_increment, 
name varchar(10),
genderchar(1), -- 性别 
salarydouble, --工资
join_date date, -- 入职日期
dept_id int,
foreign key (dept_id) references dept(id) -- 外键，关联部门表(部门表的主键)
)
insert into emp(name,gender,salary,join_date,dept_id) values('孙悟空','男 ',7200,'2013-02-24',1);
insert into emp(name,gender,salary,join_date,dept_id) values('猪八戒','男 ',3600,'2010-12-02',2);
insert into emp(name,gender,salary,join_date,dept_id) values('唐僧','男',9000,'2008-08-08',2);
insert into emp(name,gender,salary,join_date,dept_id) values('白骨精','女 ',5000,'2015-10-07',3);
insert into emp(name,gender,salary,join_date,dept_id) values('蜘蛛精','女 ',4500,'2011-03-14',1);

```

### 1. 多表查询

多表查询的作用

> 比如:我们想查询孙悟空的名字和他所在的部门的名字，则需要使用多表查询。
> 如果一条 SQL 语句查询多张表，因为查询结果在多张不同的表中。每张表取 1 列或多列。

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20190926155729.png)

### 2. 笛卡尔积现象

#### 笛卡尔积现象
> 笛卡尔积是指在数学中，两个集合X和Y的笛卡尓积（Cartesian product），又称直积，表示为X × Y，第一个对象是X的成员而第二个对象是Y的所有可能有序对的其中一个成员。笛卡尔积又叫笛卡尔乘积，是一个叫笛卡尔的人提出来的。 简单的说就是两个集合相乘的结果。假设集合A={a, b}，集合B={0, 1, 2}，则两个集合的笛卡尔积为{(a, 0), (a, 1), (a, 2), (b, 0), (b, 1), (b, 2)}。

####  笛卡尔积在sql中

我们对数据库表进行操作时，经常会对多张表进行关联，但是一不小心很容易出来庞大冗余的数据。

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20190926160240.png)

####  如何清除笛卡尔积现象的影响

> 我们发现不是所有的数据组合都是有用的，只有员工表.dept_id = 部门表.id 的数据才是有用的。所以需要通过条件过滤掉没用的数据。

```sql
-- 设置过滤条件 Column 'id' in where clause is ambiguous select * from emp,dept where id=5;
select * from emp,dept where emp.`dept_id` = dept.`id`;
-- 查询员工和部门的名字
select emp.`name`, dept.`name` from emp,dept where emp.`dept_id` = dept.`id`;
```

### 3. 内连接

用左边表的记录去匹配右边表的记录，如果符合条件的则显示。如:从表.外键=主表.主键

#### 隐式内连接

- 隐式内连接:看不到 JOIN 关键字，条件使用 WHERE 指定

```sql
 select * from emp,dept where emp.`dept_id` = dept.`id`;
 
```
#### 显式内连接

- 显示内连接:使用 INNER JOIN ... ON 语句, 可以省略 INNER

```sql
SELECT 字段名 FROM 左表 [INNER] JOIN 右表 ON 条件

```
> 查询唐僧的信息，显示员工 id，姓名，性别，工资和所在的部门名称，我们发现需要联合 2 张表同时才能 查询出需要的数据，使用内连接

```sql
# 确定查询哪些表
select * from emp inner join dept;
# 确定表连接条件，员工表.dept_id = 部门表.id 的数据才是有效的
select * from emp e inner join dept d on e.`dept_id` = d.`id`;

# 确定查询条件，我们查询的是唐僧的信息，员工表.name='唐僧'

 select * from emp e inner join dept d on e.`dept_id` = d.`id` where e.`name`='唐僧 ';

 # 确定查询字段，查询唐僧的信息，显示员工 id，姓名，性别，工资和所在的部门名称
 select e.`id`,e.`name`,e.`gender`,e.`salary`,d.`name` from emp e inner join dept d on e.`dept_id` = d.`id` where e.`name`='唐僧';
 # 给表取别名，显示的字段名也使用别名

  select e.`id` 编号,e.`name` 姓名,e.`gender` 性别,e.`salary` 工资,d.`name` 部门名字 from emp e inner join dept d on e.`dept_id` = d.`id` where e.`name`='唐僧';


```
#### 总结内连接查询步骤

1. 确定查询哪些表
2. 确定表连接的条件 
3. 确定查询的条件 
4. 确定查询的字段

### 左外连接

- 左外连接:使用 LEFT OUTER JOIN ... ON，OUTER 可以省略

- 用左边表的记录去匹配右边表的记录，如果符合条件的则显示;否则，显示 NULL 
- 可以理解为:在内连接的基础上保证左表的数据全部显示(左表是部门，右表员工)

```sql
-- 在部门表中增加一个销售部
insert into dept (name) values ('销售部'); 
select * from dept;
-- 使用内连接查询
select * from dept d inner join emp e on d.`id` = e.`dept_id`;
-- 使用左外连接查询
select * from dept d left join emp e on d.`id` = e.`dept_id`;

```

![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20190926161329.png)

### 右外连接
- 右外连接:使用 RIGHT OUTER JOIN ... ON，OUTER 可以省略

- 用右边表的记录去匹配左边表的记录，如果符合条件的则显示;否则，显示 NULL 
- 可以理解为:在内连接的基础上保证右表的数据全部显示

```sql
-- 在员工表中增加一个员工
insert into emp values (null, '沙僧','男',6666,'2013-12-05',null); select * from emp;
-- 使用内连接查询
select * from dept inner join emp on dept.`id` = emp.`dept_id`;
-- 使用右外连接查询
select * from dept right join emp on dept.`id` = emp.`dept_id`;

```
![](https://imagerepos.oss-cn-beijing.aliyuncs.com/images/20190926161449.png)


## 2、子查询

### 子查询的概念

- 一个查询的结果做为另一个查询的条件 
- 有查询的嵌套，内部的查询称为子查询 
- 子查询要使用括号

```sql
select * from emp;
-- 通过两条语句查询
select id from dept where name='开发部' ;
select * from emp where dept_id = 1;
-- 使用子查询
select * from emp where dept_id = (select id from dept where name='市场部');
```
### 子查询结果的三种情况

#### 子查询的结果是单行单列

子查询结果只要是单行单列，肯定在 WHERE 后面作为条件，父查询使用:比较运算符，如:> 、<、<>、=
等

```sql

SELECT 查询字段 FROM 表 WHERE 字段=(子查询);

```
**案例**
```sql

-- 1) 查询最高工资是多少
select max(salary) from emp;
-- 2) 根据最高工资到员工表查询到对应的员工信息
select * from emp where salary = (select max(salary) from emp);

-- 1) 查询平均工资是多少
select avg(salary) from emp;
-- 2) 到员工表查询小于平均的员工信息
select * from emp where salary < (select avg(salary) from emp);

```

#### 子查询结果是多行单列的时候
子查询结果是单例多行，结果集类似于一个数组，父查询使用 IN 运算符

```sql
SELECT 查询字段 FROM 表 WHERE 字段 IN (子查询);
```

```sql
-- 先查询大于 5000 的员工所在的部门 id
select dept_id from emp where salary > 5000;
--再查询在这些部门id中部门的名字 Subqueryreturnsmorethan1row
select name from dept where id = (select dept_id from emp where salary > 5000);
select name from dept where id in (select dept_id from emp where salary > 5000);

-- 先查询开发部与财务部的 id
select id from dept where name in('开发部','财务部');
-- 再查询在这些部门 id 中有哪些员工
select * from emp where dept_id in (select id from dept where name in('开发部','财务 部'));
```

#### 子查询的结果是多行多列

- 子查询结果只要是多列，肯定在 FROM 后面作为表
- 子查询作为表需要取别名,否则这张表没有名称则无法访问表中的字段

```sql
SELECT 查询字段 FROM (子查询) 表别名 WHERE 条件;

```
```sql
-- 查询出 2011 年以后入职的员工信息，包括部门名称
-- 在员工表中查询 2011-1-1 以后入职的员工
select * from emp where join_date >='2011-1-1';
-- 查询所有的部门信息，与上面的虚拟表中的信息组合，找出所有部门 id 等于的 dept_id
select * from dept d, (select * from emp where join_date >='2011-1-1') e where d.`id`= e.dept_id ;

select * from emp inner join dept on emp.`dept_id` = dept.`id` where
join_date >='2011-1-1';
select * from emp inner join dept on emp.`dept_id` = dept.`id` and
join_date >='2011-1-1';
```
#### 子查询小结

- 子查询结果只要是单列，则在 WHERE 后面作为条件
- 子查询结果只要是多列，则在 FROM 后面作为表进行二次查询