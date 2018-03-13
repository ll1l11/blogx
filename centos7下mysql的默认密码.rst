可以在日志中找到

/var/log/mysqld.log::

    [Note] A temporary password is generated for root@localhost:YourPassword

修改默认密码后才能使用一些功能，可以使用下面命令修改::

    mysql_secure_installation
    
    
使用yum安装文档 `Installing MySQL on Linux Using the MySQL Yum Repository`_.
 
 .. _Installing MySQL on Linux Using the MySQL Yum Repository: https://dev.mysql.com/doc/mysql-repo-excerpt/5.6/en/linux-installation-yum-repo.html
