# dubbo
dubbo官网--
#在线文档：https://www.gitbook.com/
#代码相关：https://github.com/topsale/code-java-cloud-dubbo

**1.微服务：**
    
    1.简介：
        单体应用-->拆分为多个服务(微服务-即解耦过程)
        每一个服务都有自己的数据库--分库（会出现数据冗余，此时就不遵守数据库的三大范式了）
    2.优点：
        --1.解决复杂问题，解耦单体服务，模块化，提高开发效率，服务与服务之间的相互调用方式：rpc-远程调用|消息驱动api
        --2.每个服务均可以被独立开发，易维护，利于协同开发
        --3.可实现每个微服务独立部署-持续集成部署成为可能
        --4.每个服务都可以进行独立拓展：针对不同的需求部署不同的服务：
            --1.要求计算能力的--可部署在cpu处理能力强的服务器
            --2.要是数据存储的--可部署在内存强大的服务器
            --3.可根据实际情况购置相匹配的云服务器：路由网关，应用，数据库服务器...
    3.缺点：
        --1.分布式系统服务之间调用麻烦
        --2.分布式事物问题：每个服务对应一个数据库
            -->导致分布式事务处理问题
            -->尽力保证数据一致性即可
            -->后果：会造成脏数据，冗余数据较多，此种忽略不计，保证数据一致即可
        --3.测试问题：
            -->一个普通的测试需要启动该服务及其所有依赖的服务
        --4.服务依赖问题：
            -->A依赖B，B依赖C，C依赖D
            -->若改变D，则需要一次更新DCBA
        --5.部署问题：每个文件都会有自己不同的配置，要成功部署，则需要高度掌控部署方式和高度自动化
            -->一种自动化方式是使用线程的平台即服务：PaaS 如 Cloud Founday --使用阿里云的产品服务--价格昂贵成本高
            -->或自己开发PaaS：普遍使用集群方案+kubernetes+docker容器相结合--主流方案
**2.linux：**
    
    1.linux内核常用：ubuntu，centos
        --1.www.ubuntu.com/download/server  -->长使用不带界面版本的，生产环境必须使用以LTS结尾的
    2.linux系统运算速度快，常被用于服务器
    3.linux命令：
        --1.关机命令：
            1、halt   立刻关机 
            2、poweroff  立刻关机 
            3、shutdown -h now 立刻关机(root用户使用) 
            4、shutdown -h 10 10分钟后自动关机 
        --2.重启命令：
            1、reboot 
            2、shutdown -r now 立刻重启(root用户使用) 
            3、shutdown -r 10 过10分钟自动重启(root用户使用)  
            4、shutdown -r 20:35 在时间为20:35时候重启(root用户使用) 
               如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启
        --3.查看目录文件命令：
            1.ls
            2.ll
            3.ls -a --显示隐藏文件
        --4.创建目录：
            1.mkdir 
            2.mkdir -p 递归创建目录
        --5.创建文件;
            1.touch a.txt
        --6.将打印内容写入文件
            1.echo "hello" > test.txt
            2.echo "hello" >> test.txt      --在原文件上追加文本hello（会换行）
        --7.查看文件：
            1.cat test.txt  --全部
            2.more test.txt --分页显示文件
            3.head test,txt --显示文件开头
            4.tail test.txt --显示文件结尾
            5.tail -f       --显示实时日志
            6.stat test.txt --显示文件详细信息：大小，类型等
        --8.复制，移动(也可重命名)，删除
            1.cp
            2.mv
            3.rm 
        --9.查找文件：
            1.find -m "*test"   --查看当前文件夹下以test结尾的文件
        --10.查找某文件中某内容：
            1.cat test.txt | grep linux     --在test.txt文件中查找含linux的字符串
        --11.显示当前路径
            1.pwd
        --12.显示主机名称：
            1.hostname
        --13.显示当前登录用户
            1.who
        --14.显示系统信息
            1.uname
        --15.显示当前系统中耗费资源最多的进程--等同于windows的任务管理器
            1.top
        --16.显示瞬间进程状态：
            1.ps  
        --17.显示指定文件或所在目录已经使用的磁盘空间的总量
            1.du -h
        --18.显示文件系统磁盘的空间使用情况
            1.df -h
        --19.显示当前内存和交换空间的使用情况：
            1.free -h
        --20.显示网络接口信息;
            1.ifconfig
        --21.显示网络状态信息
            1.netstat
        --22.测试网络畅通性
            1.ping 网址
        --23.清屏
            1.clear
        --24.杀死进程：
            1.kill  -9 pid
        --25.文件夹压缩:
            1.tar -zcvf yasuo.tar.gz download/  将download文件夹压缩为yasuo.tar.gz包
        --26.文件解压：
            1..tar -zxvf yasuo.tar.gz
        --27.文件编辑：vim file
            1.:q            直接退出
            2.:q!           强制退出
            3.:wq           保存后退出
            4.:set number   在编辑文件显示行号
            5.:set nonumber 在编辑文件不显示行号
            6.:w file       将当前内容保存成某个文件
        --28.修改数据源：--
        --29.安装软件：
            1.yum install tree -y   --安装：-y表示yes
            2.tree                  --显示当前结构目录树
        --30.软链接：类似于快捷方式
            1.ln /test/t.txt mm.txt --当前目录下mm.txt文件是/test/t.txt文件的软链接，修改软链接内容，原t.txt文件也会被修改
        --31.卸载软件：
            1.yum erase nginx -y 
        --32.linux用户及用户组管理：linux支持多用户登录使用资源
            1.passwd root           --给root用户设置密码包含修密码
            2.exit(或者ctrl+d)      --推出root用户登录
            3.cat /etc/passwd       --查看系统用户信息；每行代表一个账号
            4.userdel -r 用户名      --删除用户
            5.id 用户名              --查看用户信息
        --33.更改权限操作：
            1.rwx：分别代表读，写，可执行权限
            2.测试：
                vi test.sh 添加
                    #!/bin/bash        --选择执行器
                    echo "hello"    --打印hello
                :wq
                chmod +x test.sh    --给此文件添加x权限--可执行
                ./test.sh           --执行文件
            3.chown -R root:root jdk1.8/    --将jdk1.8这个文件夹的用户归属改为root用户组下的root用户
            
    3.VM上安装centos:
        1.创建虚拟机：
            文件--新建虚拟机--自定义--下一步--稍后安装操作系统--linux & centos64
            --虚拟机名称 & 安装位置 -- 处理器数量1 &内核数量2 --虚拟机内存1G 
            --使用网络地址转换(NET)(E) --I/O控制器类型：推荐 
            --虚拟磁盘类型：推荐 --创建新的虚拟磁盘 --指定磁盘容量：默认下一步--指定磁盘文件存储位置
            --创建虚拟机完成    
        2.安装centos：
            --参考位置：https://www.cnblogs.com/mosson0816/p/5416376.html
            编辑虚拟机设置--CD/DVD--使用ios镜像文件--选择ios文件位置--启动虚拟机--SKIP--
            --生产环境选择磁盘分区时一定要选择带LVM的--即磁盘扩容技术
            --注意不配置自动更新
            --只安装openssh server
            --安装完成后克隆虚拟机做备份--将干净的虚拟机备份--操作克隆机器
            --shutdown -h now
            --备份
        3.开启远程连接：--安装完成后默认是开着的，若没有则参见linux仓库下的相关文件进行配置
            --安装openssh：
                基于口令的安全验证：账号+密码可远程登录，口令和数据在传输过程中会被加密
                基于秘钥的安全验证：需要创建一对秘钥，将公有秘钥放在远程服务器自己的宿主目录中，四有迷药自己保存
                --1.检查是否安装：
                    apt-cache policy openssh-client openssh-server
                --2.安装服务端和客户端：
                    apt-get install openssh-server
                    apt-get install openssh-client
            --配置修改：主要是/etc/ssh/sshd\_config
        4.xshell连接：--
**3.安装jdk：**       
        
        1.检索1.8的列表
          yum list java-1.8*   
        2.安装1.8.0的所有文件
          yum install java-1.8.0-openjdk* -y
        3.使用命令检查是否安装成功
          java -version
        （系统环境变量文件：/etc/environment）
        （用户环境变量文件：/etc/profile）
**4.tomcat安装配置：**   
    
    1.地址：https://tomcat.apache.org/download-90.cgi
    2.链接地址：http://mirrors.shu.edu.cn/apache/tomcat/tomcat-9/v9.0.10/bin/apache-tomcat-9.0.10.zip
    
    3.安装：
        wget ...    下载
        unzip ...   解压缩
    4.赋予可執行權限
        cd apache-tomcat-9.0.10
        chmod a+x -R *   --給tomcat下所有文件赋予可执行权限
            a+x代表赋予linux登录的所有人
            -R当前路径下及所有子路径
            *代表路径下所有文件名
    5.端口修改：
        vim conf/server.xml
    6.运行测试：
        bin/startup.sh
        ps -ef |grep tomcat
    7.浏览器测试：
        ip+8080  
        如果在windows上无法访问VM中的linux中的tomcat，请尝试关闭防火墙
        
**5.mysql安装配置：**  
        
    1.见其他md
    2.重启：service mysqld restart
    3.登录重置密码：
        $ mysql -u root
        mysql > use mysql;
        mysql > update user set password=password('123456') where user='root';
        mysql > exit;
    4.创建普通用户并授权：
        mysql > use mysql;
        mysql > grant all privileges on *.* to 'root'@'%' identified by '123456';
        mysql > flushn privileges;
    5.重启即可通过navcat连接数据库服务器
    6.远程访问速度慢的问题解决：
        vi  /etc/my.cnf
        添加：--跳过mysql的dns解析
        skip-name-resolve
        重启解决

**6.docker部署微服务：**

    1.克隆一个干净的虚拟机：只安装docker即可
    2.其余参考buildTool仓库

**7.mysql服务器优化：-->**
    
    0.TPS与QPS：
        TPS:服务器每秒处理的事务数
        QPS:每秒查询率,对应fetches/sec，即每秒的响应请求数，也即是最大吞吐能力
    1.SQL语言共分为四大类：
        数据查询语言DQL:SELECT子句，FROM子句，WHERE
        数据操纵语言DML:INSERT UPDATE DELETE
        数据定义语言DDL:创建数据库中的各种对象-----表、视图、索引、同义词、聚簇 
                       TABLE/VIEW/INDEX/SYN/CLUSTER DDL操作是隐性提交的！不能rollback
        数据控制语言DCL:数据控制语言DCL用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果，
                       对数据库实行监视等。如：
                       --1.GRANT：授权
                       --2.ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点
                       --1.COMMIT [WORK]：提交
    2.提交数据有三种类型：
        显式提交：SQL>COMMIT；
        隐式提交：用SQL命令间接完成的提交为隐式提交：ALTER，AUDIT，COMMENT，CONNECT，CREATE，DISCONNECT，DROP，
                  EXIT，GRANT，NOAUDIT，QUIT，REVOKE，RENAME。
        自动提交：若把AUTOCOMMIT设置为ON，则在插入、修改、删除语句执行后，
                 系统将自动进行提交，这就是自动提交。其格式为：
                 SQL>SET AUTOCOMMIT ON；
                 select @@autocommit;   //查看一下autocommit的设置  
                 select @@tx_isolation;   //查看事物隔离级别
                 show variables like '%iso%'//查看事物隔离级别
    3.事务：
        --0.事务命令：
            select @@tx_isolation;   //查看事物隔离级别
            show variables like '%iso%'//查看事物隔离级别
            set session tx_isolation = 'read-committed';设置事物的隔离级别为读已提交
        --1.事务的基本要素（ACID）:
            1.原子性：要么全部做完，要么全部不做
            2.一致性：所得结果要一致：A 加， B 减结果一致
            3.隔离性：同一时间，只允许一个事务请求同一数据，不同的事务之间彼此没有任何干扰
            4.持久性：提交事务后，事务对数据库的所有更新将被保存到数据库，不能回滚，级别那系统崩溃，数据也在
        --2.事务的并发问题：
            1.脏读：A读到了B未提交的事物
            2.不可重复读：指读到了已经提交的事务的更改数据（修改或删除）
                A读数据时，B更新数据并提交，若A多次读取，则前后读取的数据不一致
            3.幻读：读到了其他已经提交事务的新增数据
        --3.MySQL事务隔离级别
            事务隔离级别	                脏读	    不可重复读	幻读
            读未提交（read-uncommitted）	是	    是	        是
            读已提交（read-committed）	否	    是	        是
            可重复读（repeatable-read）	否	    否	        是
            串行化（serializable）	    否	    否	        否
            mysql默认的事务隔离级别为repeatable-read innodb
        --注意：
            1、事务隔离级别为读提交时，写数据只会锁住相应的行
            2、事务隔离级别为可重复读时，如果检索条件有索引（包括主键索引）的时候，默认加锁方式是next-key 锁；如果检索条件没有索引，更新数据时会锁住整张表。
                一个间隙被事务加了锁，其他事务是不能在这个间隙插入记录的，这样可以防止幻读。
            3、事务隔离级别为串行化时，读写数据都会锁住整张表
            4、隔离级别越高，越能保证数据的完整性和一致性，但是对并发性能的影响也越大。
    4.以双十一为例：万级到百万级
        1.web服务器的横向拓展
        1.数据库服务器的拓展：
            --1.1主-->15从：弊端-主服务器挂了只能手动选择从服务器
                1主： 
                    CPU:64核
                    内存:512GB
                    ————————
                    qps与tps对比：
                        最高峰-QPS 350000次/S 
                        最高峰-TPS 50000次/S 
                        +++++++++++++++++++++++++++++++++
                        对服务器做的sql性能优化:
                        10ms处理一个sql
                        1s处理100sql
                        QPS<=100 应为cpu也会被其他服务占用
                        +++++++++++++++++++++++++++++++++
                        所有sql性能优化很重要
                    ———————— 
                    并发量与cpu使用率：-->针对数据库服务器
                        并发量：同一时间处理请求的数量，避免与同时连接数混淆
                        并发量：700
                        cpu：100% 
                        +++++++++++++++++++++++++++++++++
                        风险：
                        大量的并发：数据库连接被占满(max_connections默认100，适量改大)
                        超高的cpu使用率：因cpu资源耗尽出现宕机
                        +++++++++++++++++++++++++++++++++
                    ————————
                    io监控：关闭数据备份远程同步计划任务，避免性能损耗
                        +++++++++++++++++++++++++++++++++
                        磁盘io性能下降：使用更快的磁盘设备
                        其他大量消耗磁盘性能的计划任务：调整计划任务
                        +++++++++++++++++++++++++++++++++
                    ————————
                    网卡流量：
                        +++++++++++++++++++++++++++++++++
                        网卡io被占满 1000M
                        如何避免无法连接数据库的情况：
                            --1.减少从服务器数量    从服务器之间要进行日志备份
                            --2.进行分级缓存
                            --3.避免使用select * 查询不必要字段在大促时候也会拉低性能
                            --4.分离业务网络和服务器网络   
                        +++++++++++++++++++++++++++++++++
                    ————————
                    大表带来的影响：
                        大表：相对于业务和存储设备而言，若记录日志，即使超过也没大的影响   
                            --1.记录行数巨大，单表超过千万行
                            --2.表数据文件巨大，超过10GB
                        影响：
                            --1.对查询的影响：产生慢查询，很难在一定时间过滤出所需数据
                                如订单来源日志表：亿条数据，要过滤来源方：京东，淘宝，qq
                                来源少-->来源有3个：京东，淘宝，qq 
                                区分度低
                                消耗大量磁盘io
                                降低磁盘效率
                                产生大量慢查询
                        DDL操作:
                            --1.建立索引需要很长时间
                                风险：
                                    -1.mysql版本<5.5  使用自带的innodb存储引擎 建立索引会锁表
                                    -2.mysql版本>=5.5 不会锁表，但会引起主从延迟
                            --2.修改表结构长时间锁表
                                风险：
                                    -1.会造成长时间主从延迟：主库完成通过日志发送至从库,再从库上完成相同操作，达到表结构复制
                                        主从复制单线程，5.6及之后支持多线程
                                    -2.影响正常数据操作：加字段锁表，导致数据连接池被占满，出现访问失败500错误
                            --3.数据库中大表的处理：
                            
                                1.分库分表：大表分为多个小表
                                    难点：
                                        分表主键的选择
                                        分表后跨分区数据的查询和统计
                                        对web业务的影响  
                                2.大表的历史数据归档：如订单表，日志表
                                    减少对前后端业务的影响
                                    难点：
                                        归档时间点选择 年或月
                                        如何进行归档操作
                    ————————
                    大事务带来的影响：
                        定义：运行时间较长，操作的数据比较多的事物
                        风险：
                            锁定头太多数据，造成大量的阻塞或锁超时
                            回滚所需时间较长
                            容易造成主从延迟
                        处理：
                            避免一次处理太多的数据：批次处理 -增删改查
                            移出不必要在事务中的select操作
                                            
                                    
        
        
               
