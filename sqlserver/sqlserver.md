
###�ο���https://www.w3cschool.cn/sqlserver/

**1.sqlserver��飺**
    
    SQL Server����Microsoft�������ƹ�Ĺ�ϵ���ݿ����ϵͳ(DBMS)��
    SQL Serverʹ�÷��㣬�����Ժ�������������ɳ̶ȸߣ�
    SQL Server ���ݿ�����Ϊ��ϵ�����ݺͽṹ�������ṩ�˸���ȫ�ɿ��Ĵ洢����

**2.sqlserver�������ü�飺**

    1.SQL Server(MSSQLSERVER)�Ǳ���Ҫ�����ģ���������ݿ�������������������ķ�����һ����ȱ������
    2.SQL Server����(MSSQLSERVER)�Ǵ������񣬱�������һЩ�Զ����еģ���ʱ��ҵ��������һЩά���ƻ������綨ʱ�������ݿ�Ȳ�������ô��Ҫ�򿪣����򣬾Ͳ��ᱸ�����ݿ���
    3.SQL Server Analysis Services (MSSQLSERVER)�Ƿ�������һ�㲻�ÿ���������������λ�������������ھ򣬲���Ҫ����
    4.SQL Full-text Filter Daemon Launcher (MSSQLSERVER)��ȫ�ļ������������û��ʹ��ȫ�ļ�����������ôҲ����Ҫ����
    5.SQL Server VSS Writer MicrosoftSQLServer��SQL��д�������������ݺͻ�ԭӦ�ó����Ա���VolumeShadowCopyService(VSS)����н��в���
    6.Sql Browser ���� һ����Ҫ����Զ�̷��ʣ�����Ҫ����sql browser����sql browser��ͨ����������ip,�˿� ���ַ�ʽ�Ϳ��Է���Զ�̵ķ�����

**3.Sql Server���ݿ���SQL����ѯ�������£�**
    
    select name from sysobjects where xtype='TR' --���д�����
    select name from sysobjects where xtype='P' --���д洢����
    select name from sysobjects where xtype='V' --������ͼ
    select name from sysobjects where xtype='U' --���б�
    
    select * into ��tablename�� from ��viewName��;--����ͼ��Ϊ������
    sp_help  v_BOM_01;--��ѯ��������
    sp_columns   v_BOM_01;--��ѯ�����ֶ���Ϣ
    select * from information_schema.columns where table_name='v_BOM_01';--��ѯ�����ֶ���Ϣ

**4.**