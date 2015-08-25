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
