# CentOS7 安装mysql（YUM源方式）

**1.下载mysql源安装包**

    $ wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm

 
**2.安装mysql源**

    $ yum localinstall mysql57-community-release-el7-8.noarch.rpm 

 
**3.检查mysql源是否安装成功**

    $ yum repolist enabled | grep "mysql.*-community.*"

 
**4.修改yum源 【可跳过】**

    $ vim /etc/yum.repos.d/mysql-community.repo
    
![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWFnZXMyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQ0Mzc0OS8yMDE4MDgvMTQ0Mzc0OS0yMDE4MDgwMjA5NTA1MTE4My0yMDUzNDI1MjEyLnBuZw)
改变默认安装的mysql版本。比如要安装5.6版本，将5.7源的enabled=1改成enabled=0。然后再将5.6源的enabled=0改成enabled=1即可。
备注：enabled=1表示即将要安装的mysql版本，这个文件也可以不修改，默认安装mysql最高版本

 

**5.安装MySQL** 
这一步才是真正安装mysql

    $ yum install mysql-community-server

 
**6.启动MySQL服务并设置开机启动**

    $ systemctl start mysqld
    $ systemctl enable mysqld
    $ systemctl daemon-reload

 
**7.端口开放**

    $ firewall-cmd --zone=public --add-port=3306/tcp --permanent
    $ firewall-cmd --reload

 
**8.修改root本地登录密码**
 1）查看mysql密码

    $ grep 'temporary password' /var/log/mysqld.log
![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWFnZXMyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQ0Mzc0OS8yMDE4MDgvMTQ0Mzc0OS0yMDE4MDgwMjA5NDg0MTkwMi0xMjEyMzM5NTQ5LnBuZw)
2）连接mysql

    $ mysql -uroot -p

3）修改密码【注意：后面的分号一定要跟上】

    mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';

或者：

    mysql> set password for 'root'@'localhost'=password('MyNewPass4!'); 
    mysql> show variables like '%password%';

 **9.修改密码复杂度**
 我们可以通过改变MySQL的默认密码校验规则，修改密码为简单的密码
1. 修改校验策略：

    set global validate_password_policy=0;
2. 设置密码长度：

    set global validate_password_length=6;

**10.添加远程登录用户**

    mysql> GRANT ALL PRIVILEGES ON *.* TO 'lhn'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;

 ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQ0Mzc0OS8yMDE5MDgvMTQ0Mzc0OS0yMDE5MDgxMTAwMzQzMDgwMS04NjM1MzQ4NTEucG5n)
**11.使用客户端连接测试**
备注：这里的用户名是第9步设置的lhn，密码为：123456
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190821171654522.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
 
