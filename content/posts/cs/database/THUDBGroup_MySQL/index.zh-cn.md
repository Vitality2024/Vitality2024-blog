+++
title = '数据库管理系统课程笔记'
date = 2024-10-23T23:01:39+08:00
draft = false
math = true
toc = true
categories = ["数据库"]
tags = ["DataBase", "MySQL"]

+++

## SQL

### 数据定义语言（DDL）

数据定义语言（Data Definition Language）：用于定义和修改数据库结构，提供创建、修改、删除数据库中的各种对象（例如表、索引、视图和约束等）的命令。

|      | 创建          | 修改        | 删除        |
| ---- | ------------- | ----------- | ----------- |
| 模式 | create schema |             | drop scheme |
| 表   | create table  | alter table | drop table  |
| 视图 | create view   | alter view  | drop view   |
| 索引 | create index  | alter index | drop index  |

注意：**在MySQL中模式（SCHEMA）与数据库等价**。

#### 表

**创建表**

- 语法格式为：

  ```sql
  create table <表名> (
      <列名> <数据类型> [列级完整性约束] ... [列级完整性约束]
      [,<列名> <数据类型> [列级完整性约束] ... [列级完整性约束]]
      ...
      [,<列名> <数据类型> [列级完整性约束] ... [列级完整性约束]]
      [,表级完整性约束]
      ...
      [,表级完整性约束]
  );
  ```

- 几种完整性约束：

  - not null：指定某列不可为空。
  - unique：某列或者几列不能重复。
  - primary key：某列或者某几列为主键，主键属性必须非空且唯一。
  - foreign key （A1,A2,...,Am）references s：外键约束表示关系中任意元组在属性（A1,A2,...Am）上的取值必须对应于关系 s 中某元组在**主码属性**上的取值。

- 数据类型

  |            数据类型             |                     含义                     |
  | :-----------------------------: | :------------------------------------------: |
  |      CHAR(n), CHARACTER(n)      |            长度为 n 的定长字符串             |
  | VARCHAR(n)，CHARACTERVARYING(n) |          最大长度为 n 的变长字符串           |
  |          INT, INTEGER           |                整数（4 字节）                |
  |            SMALLINT             |               短整数（2 字节）               |
  |             BIGINT              |               大整数（8 字节）               |
  |            FLOAT(n)             |     可选精度浮点数，精度至少为 n 位数字      |
  |             DOUBLE              |                 双精度浮点数                 |
  |              REAL               |            浮点数，精度依赖于机器            |
  |        DOUBLE PRECISION         |         双精度浮点数，精度依赖于机器         |
  |          NUMERIC（p,d)          | 定点数，由 p 位数字组成，小数点后有 d 位数字 |
  |     DECIMAL(p,d), DEC(p,d)      |                  同NUMERIC                   |
  |             BOOLEAN             |                    布尔型                    |
  |              DATE               |           日期，格式为 YYYY-MM-DD            |
  |              TIME               |            时间，格式为 HH:MM:SS             |
  |            TIMESTAMP            |    时间戳类型，格式为 YYYY-MM-DD HH:MM:SS    |
  |            INTERVAL             |                 时间间隔类型                 |

**修改表**

- 添加列

  ```sql
  alter table <表名> add [column] <列名> <数据类型>;
  ```

- 删除列

  ```sql
  alter table <表名> drop [column] <列名> [restrict | cascade];
  ```

  restrict：如果该列被其他列引用，则无法删除该列。

  cascade：引用该列的其他列会和该列同时被删除。

- 修改列

  ```sql
  alter table <表名> alter column <列名> <数据类型>;
  ```

**删除表**

```sql
drop table <表名> [,<表名>] ... [,<表名>] [restrict | cascade];
```

drop table语句同时删除表中所有元组和该表的关系模式。

当使用级联选项删除表时，引用该表的其他表也会被删除。

#### 视图

**创建视图**

```sql
create view <视图名> [(<列名> [,<列名>, ... , <列名>])] as <子查询>;
```

- 子查询：任何 select 语句。
- 执行 create view 语句时并不执行其中的子查询语句，只把视图的定义存入数据字典。

**修改视图**

```sql
alter view <视图名> as <子查询>;
```

**删除视图**

```sql
drop view <视图名> [cascade];
```

- cascade：该视图和该视图导出的视图都会被删除。

**物化视图**

一些数据库支持物化视图，将视图存储在数据库中。

物化视图的创建、修改和删除相较于视图多了关键字 MATERIALIZED.

例如创建物化视图的命令为：

```sql
create materialized view <物化视图名> [(<列名> [,<列名>, ... , <列名>])] as <子查询>;
```



### 数据操纵语言（DML）

Data Manipulation Language：数据的增删改查。









