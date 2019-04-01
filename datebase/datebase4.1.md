7. 权限管理
  * 系统权限:对各种特性的访问 或许可oracle特殊任务
    1. 只要DBA才应该拥有ALTER DATEBASE系统权限<br>
      `grant 权限 to 用户列表|角色列表 (public)[with admin option]`<br>
      权限有：create session create table create view<br>
    2. 系统权限的回收<br>
    ```sql
      revoke 权限 from 用户列表|角色列表 (public) --只收回这一层权限 他授予别人的不收回
      revoke create table,create view from use1;
    ```
  * 对象权限:增删改查<br>
    1. 授予
      ```sql
      grant 权限/all on 对象 to 用户列表|角色列表 (public)[with admin option]
      grant select,update,insert on Scott.emp to use1
      ```
    2. 回收
    ```sql
    revoke 对象权限/all on 对象 from 用户列表|角色列表 --逐层全部收回
    ```
  * 查询授权信息
    * DBA_TAB_PRIVS
    * ALL_TAB_PRIVS
    * USER_TAB_PRIVS
    * DBA_COL_PRIVS
    * ALL_COL_PRIVS
    * USER_COL_PRIVS
    * DBA_SYS_PRIVS 包含授予用户或角色的系统权限信息
    * USER_SYS_PRIVS 包含授予当前用户的系统权限信息
8. 角色管理
  * 角色分类：系统预定义角色、用户自定义角色<br>
    `create role 角色名称[not identified]|[identified by password]`
  * 修改角色(必须具有alter any role系统权限,以及with admin option权限 角色创建者自动具有该修改权限)
    ```sql
    alter role 角色名称 [not identified][identified by 密码]
    alter role user identified by password --设置密码
    alter role user identified --取消密码
    ```
  * 所有角色失效
    set role none;
    set role high_tiger_role identified by highrole;
    set role all except low_tiger;
  * 删除角色
    drop role low_tiger;
  * 利用角色进行授权管理
    1. 从用户或角色授予角色
      grant 角色 to 用户列表|角色列表;
    2. 从用户或角色回收角色
      revoke 权限 from 用户列表|角色列表
    3. 用户角色的激活或屏蔽
      alter user 角色名 default role [角色] [all][except 角色名称](激活)[none](屏蔽)
9. 系统权限<br>
  在给用户授予系统权限是，需要注意4个问题：
    1. 只有DBA才应该拥有ALTER DATABASE 系统权限
    2. 应用程序开发者一般需要给它的系统权限是create table,create view,create index
    3.
### 概要文件
1. 介绍
  1. 是数据库和系统资源限制的集合，是oracle数据库安全策略的重要组成部分
  2. 每个数据库都必须有一个概要文件。通常DBA将用户分为几种类型，每一种类型对应一个概要文件，然后将概要文件分配给用户。
  3. 概要文件的限制类型可以：
    * CPU的使用时间
    * 每个用户的并发会话数
    * 每个连接数据库的时间
    * 用户连接数据库的空闲时间
    * 私有SQL区
2. 创建概要文件
```
  create profile 概要文件名称 limit 资源参数 口令参数
  创建一个名为pwd_profile的概要文件 4次连续登陆失败则锁定账号 15天解锁
  create profile pwd_profile limit failed_login attemptes 4 password password_lock_time 10;
  create profile res_profile limit session pre_user 4(4个用户)connect_time 60(连60分钟) idle 20(20分中无操作断开) private_sga 100K cpu_per_call 100;
```
