@[toc]
## 一、数据库的备份
#### 1.数据的介绍：

在操作数据库时,难免会发生一些意外造成数据丢失。例如,突然停电、管理员的操作失误都可能导致数据的丢失。为了确保数据的安全,需要定期对数据库进行备份,这样,当遇到数据库中数据丢失或者出错的情况,就可以将数据进行怀原,从而最大限度地降低损失。这段话是课本上说的，而我想说特别是银行、企业数据、等等吧都用备份这个玩意，关键太强大了，虚拟机我都备份一个，怕坏了重头配置耽搁事情。

#### 2.备份：
	MySQL提供了一个mysqldump命令，它可以实现数据的备份。 mysqldump命令可以备份单个数据库、多个数据库和所有数据库.
备份单个数据库: 这里已经配置完成path路径了，接下来就可以在命令窗口运行mysql的备份命令了，然后选择备份到那个地方。如下图所示：
哈哈，上图，图片才能真正展示我们所表达的。
（1）总：
>Cmd,命令启动数据库
Mysql –u root –proot
输入密码root,进入mysql环境
Show databases;
Quit 先退出在cmd下才可以
Mysqldump -u root –proot db11> e:/db11   （注意密码前、指向符号前后无空格）
到E盘使用记事本查看备份。

（2）先进入数据库：
		看下这是在dos命令窗口下。使用命令看图干就完了：
		
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624104805356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)
（3）确定数据，然后导出，命令看图，干。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624105001910.png#pic_center)

（4）查看看导出的数据：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624105206338.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062410521665.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)

## 二、还原数据库

#### 1.删除数据库
为了演示数据库还原，还得将数据库删除。
（1）总:
>Mysql –u root –p，启动数据库
Show databases;
Use hxc;
Show tables;
Select * from book;
Drop database db11;

如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624105835845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)

#### 2.恢复数据库
1.方法一：（在DOS窗口下运行命令）
（1）了解：
>mysql –uusername –ppassword [dbname] <filename.sql 

上述语法格式中，username表示登录的用户名，password表示用户的密码，dbname表示要还原的数据库名称，如果使用mysqldump命令备份的filename.sql文件中包含创建数据库的语句，则不需要指定数据库。 

（2）步骤：
 
 这里需要重新建立空数据库，然后进入数据库
>Create database hxc;
Use hxc;

然后再退出数据库到cmd页面进行恢复,命令如下：

>Mysql –u root –p hxc<D:\Mysql\导出数据\hxc

创建数据库，然后退出到DOS窗口。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624110358688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)
进行数据导入，箭头朝里的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624110407568.png#pic_center)
查看数据库是否恢复：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624110416126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)

2.方法二 （这种方式在MYSQL数据库环境下）
>Drop database db11;    #删除
Create database db11;   #创建
Use db11;				       #进入
Source D:\Mysql\导出数据\hxc   #注意没有分号，导入数据

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624142219599.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624142235925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200624142247237.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzYxMzU5,size_16,color_FFFFFF,t_70#pic_center)


OK，还原完成！！！



