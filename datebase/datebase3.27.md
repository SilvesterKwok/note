### sequence
1. 创建序列
创建一个系列test_seq  ，起始值为10每次增长2，最大值为100，最小值9 的循环序列，每次缓存10<br>
```sql
create sequence test_seq
start with 10
increment by 2
maxvalue 100
minvalue 9
cycle
cache 10; --也可以使用nocache,即无缓冲,缓存中序列值的个数为10
```
```sql
create table stu{
  sid number(3),
  sname varchar2(5),
  }
create sequence student_seq
...
```
nextval伪列：返回下一个值<br>
currval伪列：返回当前值，必须在nextval后使用<br>
2. 修改序列
```
alter sequence test_seq
去掉start with 即可
```
3. 删除序列<br>
`drop sequence 序列名`<br>
rowid: 伪列，系统自动生产，表示的每个数据库中的记录的物理地址，唯一，可以快速定位到记录<br>
由 数据对象编号 相关文件编号 块编号 行编号 组成<br>
   `000000      fff         BBBBBB RRR`

### 索引（提高查询效率）
1. 自动创建：在建表的时候，使用了PRIMARY_KEY或unique约束时，数据库会自动创建一个索引
2. 手动创建
```sql
create index 索引名
on 表名(列...)
```
**命名规范：idx_表名_列名**
3. 删除索引<br>
`drop index 索引名`

### 用户管理
1. oracle 数据库的初始用户<br>
 * sys
 * system
 * scott 表示测试网络连接的用户
 * public 实质上一个用户名，数据库中任何一个用户都属于该组 要为所有人授予某个权限，只需要把权限授予public即可
2. 用户属性
 1. 安全属性：
  1. 身份认证:数据库身份认证、外部身份认证、全局身份认证
  2. 默认表空间
  3. 临时表空间
  4. 表空间配额
  5. 概要文件
  6. 账号状态
3. 创建账号
```sql
create user 用户名  indentified
[by 密码|externally|globally as 'external_name']
```
```sql
default tablespace tablespace_name
temporary tablespace temp_tablespace_name
quota nK|M|unlimited on tablespace_name
profile profile_name
password expire
account look|unlock;
```
4. 修改账号
```
alter user 后边与上面一样
default role_list ALL[EXCEPT role_list][none]
```
5. 删除用户<br>
```sql
drop user 用户名[cascade]--级联删除,子表亦删除
```
6. 查看用户
 * ALL_USERS:包括用户名、id、创建时间
 * DBA_USERS:所有详细信息
 * USER_USERS:包括当前用户详细信息
 * DBA_TS_QUOTAS:包括所有用户的表空间配额信息
 * V$SEEION:
 * V$OPEN_CURSOR:包含用户执行的SQL语句信息
7. 权限管理
 * 对象权限:增删改查
 * 系统权限:对各种特性的访问 或许可oracle特殊任务
  1. 只要DBA才应该拥有ALTER DATEBASE系统权限
