---
title: Mysql max_allowed_packet
date: 2017-04-23 11:48:49
tags: mysql
---

**Mysql的max_allowed_packet问题**
---
&emsp;&emsp;在初学mysql时我们可能不会遇到max_allowed_packet的问题，但当你需要一次写入大量的数据时，就可能会遇到mysql提示写入的数据过大问题。

1.什么是max_allowed_packet：
---
&emsp;&emsp;max_allowed_packet是mysql允许插入一条数据的大小

2.查看max_allowed_packe：
---
&emsp;&emsp;在mysql的命令行模式中使用

	  show VARIABLES like 	'%max_allowed_packet%’;


![@查看结果如下](http://img.blog.csdn.net/20170419133351579?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvTV9BTEw=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/
gravity/SouthEast )
3.解决的办法：(对mysql的max_allowed_packet的修改。（3种方式）)
---
- 修改my.cnf文件，设置max_allowed_packet=16M，该方法简单并且永久的生效。完成这些以后必须做的就是对mysql的重启和项目中对数据库要重新连接，也就是说重启你的服务（以spring boot来说，其他类似）。

- 进入mysql的命令行模式，使用set global max_allowed_packet = 2 \* 1024 \* 1024 \* 10;来进行设置大小，可以根据你项目的需求来进行调整，在出错误时mysql是会提示你插入的数据包的大小和你当前允许的数据包的大小的。这是不需要对musql进行重启的，重启后会恢复到以前的设置，所以切记不要重启。当然和上一个相同你的服务还是要重启的。

- 在终端 使用mysql --max_allowed_packet=32M 来进行设置。（没有试过，有兴趣的可以试试。然后记得回复我）
