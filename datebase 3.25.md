#修改约束
主键约束：表示唯一的，不能为空
唯一约束：表示唯一的
非空约束：表示不能为空
检查约束：检查一个列的内容是否合法
外键约束：

建立主键约束：
create table person(
  pid number(5) primary key,(列级别约束)
  pname number(3) unique not null,
  page number(3) not null foreign key(page) reference department(page),
  psex varchar(4) check(psex in ('男','女')),
  constraint person_pid_pk(自定义错误名) primary key (pid)(放在后面表级别约束)
)
#删除约束
alter table 表名 drop 约束
#查看约束
select * from user_constraints where table_name = 'emp';
alter table 表名 disable/enable constraint 约束名
#视图:获取一个或多个表中的数据集合
    create view 视图名
    as
    select 语句
    creat view [or replace] [force/unforce] 视图名
    as
    select[with check option] [with read only]
  删除视图
  dropview 视图名
#序列：按照一定规则自动增加减少数字的这一种数据库对象
    create sequences 序列名
    increnment by n
    (start with n)
    maxvalue n
    minvalue n
    cycle nocycle
