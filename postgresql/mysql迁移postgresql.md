>https://github.com/aliyun/rds_dbsync/blob/master/README.md?spm=a2c6h.13066369.0.0.22d91427UldoTk&file=README.md
>
>���￪Դ rds_dbsync
>
>ʹ��navicatֱ��ͬ������Щ����ĵ����������������ظ������⣬�����½���������

# ֧�ֵĹ��� PostgreSQL -> PostgreSQL pgsql2pgsql
    
    PostgreSQL -> PostgreSQL pgsql2pgsql
        ���� pg->pg ȫ��+��������ͬ��
    MySQL -> PostgreSQL/Greenplum��binlog_minner binlog_loader��
        ���ܣ����� MySQL binlog ��������������ͬ��
    PostgreSQL -> PostgreSQL/Greenplum pgsql2gp
        ���ܣ����� PostgreSQL �߼���־����������ͬ��
    MySQL -> PostgreSQL/Greenplum mysql2pgsql
        ���ܣ��Ա�Ϊ��λ�Ķ��߳�ȫ������Ǩ��
        https://github.com/aliyun/rds_dbsync/blob/master/doc/mysql2pgsql_ch.md
# �����������Թ���

## mysql2pgsql

���� mysql2pgsql ֧�ֲ���صİ� MYSQL �еı�Ǩ�Ƶ� HybridDB/Greenplum Database/PostgreSQL/PPAS���˹��ߵ�ԭ���ǣ�ͬʱ����Դ�� mysql ���ݿ��Ŀ�Ķ����ݿ⣬�� mysql ����ͨ����ѯ�õ�Ҫ���������ݣ�Ȼ��ͨ�� COPY ����뵽Ŀ�Ķˡ��˹���֧�ֶ��̵߳��루ÿ�������̸߳�����һ�������ݿ����

## ��������

�޸������ļ� my.cfg������Դ��Ŀ�Ŀ�������Ϣ��

- Դ�� mysql ��������Ϣ���£�

	**ע�⣺**Դ�� mysql ��������Ϣ�У��û���Ҫ�ж������û���Ķ�Ȩ�ޡ�

```
[src.mysql]
host = "192.168.1.1"
port = "3306"
user = "test"
password = "test"
db = "test"
encodingdir = "share"
encoding = "utf8"
```

- Ŀ�Ŀ� pgsql ������ PostgreSQL��PPAS �� HybridDB for PostgreSQL ����������Ϣ���£�

	**ע�⣺**Ŀ�Ŀ� pgsql ��������Ϣ���û���Ҫ��Ŀ�����д��Ȩ�ޡ�

```
[desc.pgsql]
connect_string = "host=192.168.1.1 dbname=test port=5888  user=test password=pgsql"
```

## mysql2pgsql �÷�

mysql2pgsql ���÷�������ʾ��

```
./mysql2pgsql -l <tables_list_file> -d -n -j <number of threads> -s <schema of target able> 

```

����˵����

- -l����ѡ������ָ��һ���ı��ļ����ļ��к�����Ҫͬ���ı������ָ���˲�������ͬ�������ļ���ָ�����ݿ��µ����б�```<tables_list_file>```Ϊһ���ļ��������溬����Ҫͬ���ı����Լ����ϲ�ѯ�������������ݸ�ʽʾ�����£�

```
table1 : select * from table_big where column1 < '2016-08-05'
table2 : 
table3
table4 : select column1, column2 from tableX where column1 != 10
table5 : select * from table_big where column1 >= '2016-08-05'
```

- -d����ѡ��������ʾֻ����Ŀ�ı�Ľ��� DDL ��䣬��ʵ�ʽ�������ͬ����

- -n����ѡ��������Ҫ��-dһ��ʹ�ã�ָ���� DDL ����в�������������塣

- -j����ѡ������ָ��ʹ�ö����߳̽�������ͬ���������ָ���˲�������ʹ�� 5 ���̲߳�����

- -s����ѡ������ָ��Ŀ����schema��һ������ֻ��ָ��һ��schema�������ָ���˲����������ݻᵼ�뵽public�µı�

### �����÷�

#### ȫ��Ǩ��

ȫ��Ǩ�ƵĲ�������������ʾ��

1\. ͨ�����������ȡĿ�Ķ˶�Ӧ��� DDL��

```
./mysql2pgsql -d
```

2\. ������Щ DDL���ټ��� distribution key ����Ϣ����Ŀ�Ķ˴�����

3\. ִ���������ͬ�����б�

```
./mysql2pgsql
```

�������������ļ�����ָ�����ݿ��е����� mysql ������Ǩ�Ƶ�Ŀ�Ķˡ�������ʹ�� 5 ���̣߳���ȱʡ�߳���Ϊ 5������ȡ�͵��������漰�ı����ݡ�

#### ���ֱ�Ǩ��

1\. �༭һ�����ļ� tab_list.txt�������������ݣ�

```
t1 
t2 : select * from t2 where c1 > 138888
```

2\. ִ���������ͬ��ָ���� t1 �� t2 ��ע�� t2 ��ֻǨ�Ʒ��� c1 > 138888 ���������ݣ���

```
./mysql2pgsql -l tab_list.txt
```

## mysql2pgsql �����ư�װ������

���ص�ַ������[����](https://github.com/aliyun/rds_dbsync/releases)��

## mysql2pgsql Դ�����˵��

�鿴Դ�����˵��������[����](https://github.com/aliyun/rds_dbsync/blob/master/README.md)��

