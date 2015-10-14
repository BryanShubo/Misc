What is performance testing?

Performance testing is the testing, which is performed, to ascertain how the components of a system are performing, given a particular situation. Resource usage, scalability and reliability of the product are also validated under this testing. This testing is the subset of performance engineering, which is focused on addressing performance issues in the design and architecture of software product.

Performance Testing Goal:

The primary goal of performance testing includes establishing the benchmark behaviour of the system. There are a number of industry-defined benchmarks, which should be met during performance testing.

Performance testing does not aim to find defects in the application, it address a little more critical task of testing the benchmark and standard set for the application. Accuracy and close monitoring of the performance and results of the test is the primary characteristic of performance testing.

Example:

For instance, you can test the application network performance on Connection Speed vs. Latency chart. Latency is the time difference between the data to reach from source to destination. Thus, a 70kb page would take not more than 15 seconds to load for a worst connection of 28.8kbps modem (latency=1000 milliseconds), while the page of same size would appear within 5 seconds, for the average connection of 256kbps DSL (latency=100 milliseconds). 1.5mbps T1 connection (latency=50 milliseconds) would have the performance benchmark set within 1 second to achieve this target.

For example, the time difference between the generation of request and acknowledgement of response should be in the range of x ms (milliseconds) and y ms, where x and y are standard digits. A successful performance testing should project most of the performance issues, which could be related to database, network, software, hardware etc…

===================================
2) Load Testing:

Load testing is meant to test the system by constantly and steadily increasing the load on the system till the time it reaches the threshold limit. It is the simplest form of testing which employs the use of automation tools such as LoadRunner or any other good tools, which are available. Load testing is also famous by the names like volume testing and endurance testing.

The sole purpose of load testing is to assign the system the largest job it could possible handle to test the endurance and monitoring the results. An interesting fact is that sometimes the system is fed with empty task to determine the behaviour of system in zero-load situation.

Load Testing Goal:

The goals of load testing are to expose the defects in application related to buffer overflow, memory leaks and mismanagement of memory. Another target of load testing is to determine the upper limit of all the components of application like database, hardware and network etc… so that it could manage the anticipated load in future. The issues that would eventually come out as the result of load testing may include load balancing problems, bandwidth issues, capacity of the existing system etc…

Example:

For example, to check the email functionality of an application, it could be flooded with 1000 users at a time. Now, 1000 users can fire the email transactions (read, send, delete, forward, reply) in many different ways. If we take one transaction per user per hour, then it would be 1000 transactions per hour. By simulating 10 transactions/user, we could load test the email server by occupying it with 10000 transactions/hour.
================================================
3) Stress testing

Under stress testing, various activities to overload the existing resources with excess jobs are carried out in an attempt to break the system down. Negative testing, which includes removal of the components from the system is also done as a part of stress testing. Also known as fatigue testing, this testing should capture the stability of the application by testing it beyond its bandwidth capacity.

The purpose behind stress testing is to ascertain the failure of system and to monitor how the system recovers back gracefully. The challenge here is to set up a controlled environment before launching the test so that you could precisely capture the behaviour of system repeatedly, under the most unpredictable scenarios.

Stress Testing Goal:

The goal of the stress testing is to analyse post-crash reports to define the behaviour of application after failure. The biggest issue is to ensure that the system does not compromise with the security of sensitive data after the failure. In a successful stress testing, the system will come back to normality along with all its components, after even the most terrible break down.

Example:

As an example, a word processor like Writer1.1.0 by OpenOffice.org is utilized in development of letters, presentations, spread sheets etc… Purpose of our stress testing is to load it with the excess of characters.

To do this, we will repeatedly paste a line of data, till it reaches its threshold limit of handling large volume of text. As soon as the character size reaches 65,535 characters, it would simply refuse to accept more data. The result of stress testing on Writer 1.1.0 produces the result that, it does not crash under the stress and that it handle the situation gracefully, which make sure that application is working correctly even under rigorous stress conditions.











Setup content assist in Eclipse:
go to, Window >> Preferences >> Java >> Editor >> Content Assist >> Auto activation triggers for java, and enter .abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ , this will trigger the auto activation for class names, methods, etc...


how to escape & from xml:
```
'&' --> '&amp';

'<' --> '&lt';

'>' --> '&gt';

```




If a property’s name has two characters,  it should be  either defined as “a-b” in schema file and “aB” in Java file, or “aB” in schema file and “ab” in Java file. Otherwise, reflection cannot find the property.
 
4. how to print something using dbms_output.put_line()message 
 
set serveroutput on 
 
select * from user_procedures 
select * from user_triggers 
select * from user_tables; 
 
 
6. To open file on console in linux 
cat file 
less file // for long name 
 
7. How to increase output buffer size in Oracle 
PL/SQL: DBMS_OUTPUT.ENABLE (buffer_size => NULL); 
SQL*Plus: set serveroutput on size unlimited 
 
 
8. how to add quote for cell in excel 
·         High­light the cells you want to add the quotes. 
·         Go to For­mat –> Cells –> Custom 
·         Paste the fol­low­ing into the “Type” field: ”””@””” (see blow up below) 
·         Click “okay” 
  
JUnit, Mockito, powermock, easymock 
 
 
** Apache POI 
9. Iterate over cells, with control of missing / blank cells 
Use for loop instead of cell.hasNext() 
 
 
10. how to comment or uncomment in sql developer 
control + / 
 
 
 
11. how to find corrupt index in DB 
 select object_name, object_type from dba_objects where object_id=8831; 
   
  select partition_name from dba_segments where TABLESPACE_NAME = (select tablespace_name from dba_data_files where file_id=26) and SEGMENT_NAME='APPLICANT_BENEFIT_XREF_IDX05'; 
   
12. where is the tnsnames.ora file 
/network/admin/tnsnames.ora  
 
13. DB link does not work: 
```
 CREATE DATABASE LINK QDSMISC1 
  CONNECT TO research IDENTIFIED BY research_qdsmisc1 USING 
 '(DESCRIPTION = 
   (ADDRESS_LIST = 
     (ADDRESS = (PROTOCOL = TCP)(HOST = usvcltmiscqds1.reinscloud.local)(PORT = 1521)) 
   ) 
   (CONNECT_DATA = 
     (SERVICE_NAME = qdsmisc1) 
   ) 
 )'; 
  
 ```
  
 INSERT INTO DMF_EXTRACT 
    select * from dmf_extract@QDSMISC1; 
    commit; 
 
 
 
14. Grant user select privilege 
 
BEGIN 
    FOR t IN (SELECT * FROM user_tables)  
    LOOP    
        EXECUTE IMMEDIATE 'GRANT SELECT ON ' || t.table_name || ' TO U000010,VELOGICA_SERVICE,USUNODA,USUTHOP,USUCUHA,USUFIJA,USUMCIA,USUMEAF,USUMCKE,USUMCBR,U000488';     
    END LOOP; 
END; 
 
 
Alter table column size 
alter table RESCORE_RX_GROUP_DETAIL 
 MODIFY RX_GROUP varchar2(30) 
 
 
Oracle alter table modify column Syntax example 
 
Oracle Tips by Burleson Consulting 
For complete tips on Oracle alter table syntax, see the book "Easy Oracle Jumpstart".  Oracle provides "alter table" syntax to modify data columns in-place in this form: 
alter table 
   table_name 
modify 
   column_name  datatype; 
If you are brave you can use a single "alter table" syntax to modify multiple columns: 
alter table 
   table_name 
modify 
   ( 
   column1_name  column1_datatype, 
   column2_name  column2_datatype, 
   column3_name  column3_datatype, 
   column4_name  column4_datatype 
   ); 
Here are some examples of Oracle "alter table" syntax to modify data columns and note that you can add constraints like NOT NULL: 
ALTER TABLE  
   customer  
MODIFY  
   (  
   cust_name varchar2(100) not null, 
   cust_hair_color  varchar2(20) 
   ) 
; 
We can also use Oracle "alter table" syntax in dynamic PL/SQL to modify data columns 
BEGIN  
SQL_STRING := 'ALTER TABLE '||:TABLE_NAME||' MODIFY '||:COLUMN_NAME||' VARCHAR2(100)'; . . .  
END;  
 
 
 
 
 
Start–>cmd–>netstat -a -o -n 
 
 
taskkill /F /PID <pid> 
 
 
 
Solve printer issue (Splwow64.exe error)
'''
Please follow the steps below to sort out the issue:

Click Start and type in regedit and press Enter. Alternatively press Windows button and R key at the same time and this opens the Run command. Type in regedit and press Enter.
Scroll down to HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Environments\Windows x64\Drivers
When we expand the Drivers key, we should find the key Version-3.
The sub-keys after this should contain the printer driver configuration information. Delete all the sub-keys that comes under it. At least delete the key that contains the name of the Printer model that is causing issues.
Press Windows button and R key and press Enter. Type in “cmd” and press enter. This would open the command prompt window.
Type in the command net stop spooler . Please note that this is equal to going to Service from Control Panel and stopping the print spooler service.
Navigate to “C:\WINDOWS\system32\spool\printers\” and delete files in this folder, if there are any. Normally you might not find files in there, but if there are any, delete them. The folder is so significant because this is where the print spooler stores print files.
Navigate to “C:\WINDOWS\system32\spool\drivers\x64\3″ and delete all the files and sub-folders in here.
Go to the command prompt window again and type in the command net start spooler or just right click on Print Spooler and press Start.
'''
 
```
site:mitbbs.com linkedin
```
