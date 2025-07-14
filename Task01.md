本学习笔记为阿里云天池龙珠计划sql训练营的学习内容，学习链接为：https://tianchi.aliyun.com/specials/promotion/aicampsql

一、学习知识点概要 

数据库与DBMS基本概念

DBMS的5种类型及RDBMS代表产品

RDBMS的C/S系统结构 

MySQL环境搭建（云服务器/本地）

SQL语句分类（DDL/DML/DCL）

SQL基本书写规则

数据库和表的创建与管理

数据类型与约束设置 
表结构的修改与数据操作 

二、学习内容

2.1 DBMS类型对比

类型	                       	        代表

关系数据库(RDBMS)，表结构存储，使用SQL操作，如	MySQL, PostgreSQL 

键值存储(KVS)，灵活键值对存储，如MongoDB

2.2 SQL语句分类
DDL	  定义数据库/表结构	   CREATE, DROP, ALTER

DML	  操作数据（90%常用）	 SELECT, INSERT, UPDATE, DELETE

DCL	  权限控制与事务管理	   COMMIT, ROLLBACK, GRANT

2.3 关键语法规则

语句末尾必须加 ;

语句以分号;结尾

关键字不区分大小写，但数据区分大小写

Windows不区分表名字段名大小写，Linux/Mac严格区分

使用半角空格或换行分隔单词

常数书写方式固定：'abc', 1234, '2023-01-01'


2.4 表操作示例

sql
-- 创建表（含主键约束）
CREATE TABLE product (
    product_id CHAR(4) NOT NULL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    sale_price INTEGER
);

-- 添加列
ALTER TABLE product ADD COLUMN regist_date DATE;

-- 删除列
ALTER TABLE product DROP COLUMN regist_date;

2.5 数据插入的两种方式
sql
-- 单行插入

INSERT INTO product VALUES ('0001', 'T恤', '衣服', 1000);

-- 多行插入（MySQL/PG支持）

INSERT INTO product 
VALUES ('0002', '打孔器', '办公用品', 500),
       ('0003', '菜刀', '厨房用具', 3000);
       
-- 更新数据

-- 更新特定记录

UPDATE product
   SET sale_price = sale_price * 10
 WHERE product_type = '厨房用具';

-- 多列更新

UPDATE product
   SET sale_price = sale_price * 10,
       purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';

-- 清空为NULL

UPDATE product
   SET regist_date = NULL
 WHERE product_id = '0008';
 
2.6 重要注意事项

约束冲突：

设置了 NOT NULL 的列不可插入 NULL

主键列的值必须唯一

UPDATE：UPDATE语句必须使用WHERE条件，否则会更新全部数据

数据类型选择：

INTEGER 整数型

CHAR 型 存储定长字符串，由于会浪费存储空间，所以一般不使用。

VARCHAR 型存储可变长度字符串，即使字符数未达到最大长度，也不会用半角空格补足。

DATE 型用来指定存储日期（年月日）的列的数据类型（日期型）。

三、学习问题与解答

问题：我使用了postgresql 数据库进行创建表失败

解决：在postgresql中不使用将字段的注释直接在建表语句中直接注释，而是在建表后使用语句
comment on
column <模式.表名.字段> is '注释内容';

  注：表名唯一时或者使用数据库工具时在sql编辑器指定好了模式可以省略

高效清空使用

  TRUNCATE TABLE product; -- 高效清空

  
四、学习思考与总结

知识

SQL本质：接近自然语言的数据库操作指令，重点在于精准描述需求（如 WHERE 条件）。
约束的意义：PRIMARY KEY 保证数据可定位，NOT NULL 强制数据完整性。

方法

所有数据操作前先写 WHERE 子句
生产环境禁用 DROP / TRUNCATE

总结

数据库是"数据的仓库"，SQL是"仓库管理手册"。初学需严格遵循语法规范，避免因大小写/空格导致的隐性错误。实操中宜采用"最小化操作原则"——每次只修改必要数据，并通过事务(COMMIT/ROLLBACK)控制风险。





附：练习题sql(该sql语句是使用postgresql数据库而不是mysql)

--3.1

create table public.addressbook (

	regist_no integer not null,
 
	"name" varchar(128) not null,
 
     address varchar(128) not null,
     
     tel_no varchar(10) null,
     
     mail_address varchar(20) null,
     
	constraint addressbook_pkey primary key (regist_no)
 
);

comment on
table public.addressbook is '地址薄';

comment on
column public.addressbook.regist_no is '注册编号';

comment on
column public.addressbook."name" is '姓名';

comment on
column public.addressbook.address is '住址';

comment on
column public.addressbook.tel_no is '电话号码';

comment on
column public.addressbook.mail_address is '邮箱地址';

--3.2

alter table addressbook add column postal_code varchar(8) not null; 

comment on column  addressbook.postal_code is '邮政编码';

--3.3
drop table addressbook;

-- 3.4 
--drop 后的表无法恢复，所以在实际应用中除非确定该表已经完全不可用或是测试表，需要提前备份，若是有数据存在也应该提前备份

以下是我提前备份的语句(用dbeaver工具生成)

-- public.addressbook definition

-- Drop table

-- DROP TABLE public.addressbook;

CREATE TABLE public.addressbook (

	regist_no int4 NOT NULL, -- 注册编号
 
	"name" varchar(128) NOT NULL, -- 姓名
 
	address varchar(128) NOT NULL, -- 住址
 
	tel_no varchar(10) NULL, -- 电话号码
 
	mail_address varchar(20) NULL, -- 邮箱地址
 
	postal_code varchar(8) NOT NULL -- 邮政编码
 
);
-- 表注释

COMMENT ON TABLE public.addressbook IS '地址薄';


-- 添加字段注释

COMMENT ON COLUMN public.addressbook.regist_no IS '注册编号';

COMMENT ON COLUMN public.addressbook."name" IS '姓名';

COMMENT ON COLUMN public.addressbook.address IS '住址';

COMMENT ON COLUMN public.addressbook.tel_no IS '电话号码';

COMMENT ON COLUMN public.addressbook.mail_address IS '邮箱地址';

COMMENT ON COLUMN public.addressbook.postal_code IS '邮政编码';



















  
