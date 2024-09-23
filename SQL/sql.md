Truncate table table_name;

The TRUNC (date) function returns date with the time portion of the day truncated to the unit specified by the format model fmt . The value returned is always of datatype DATE , even if you specify a different datetime datatype for date . If you omit fmt , then date is truncated to the nearest day.

expression [ NOT ] BETWEEN low AND high
processing_time BETWEEN
TO_TIMESTAMP('10-JUL-2023 15.38','DD-MON-YYYY HH24.MI.SS') --AT TIME ZONE 'Asia/Singapore'
AND
TO_TIMESTAMP('10-JUL-2023 15.43','DD-MON-YYYY HH24.MI.SS') --AT TIME ZONE 'Asia/Singapore' 

To Synchronize the all_tables:
exec dbms_stats.gather_schema_stats('PDBUSER'); 


Get Duplicate counts:
SELECT
col1,count(*)
FROM
table rt
group by col1
having count(*)> 1;

Check Object_type:
select * from all_objects where OBJECT_NAME=UPPER('table');

select text from all_source where owner='PDBUSER' and name=upper('table');

SELECT filename FROM table(rdsadmin.rds_file_util.listdir('DATA_PUMP_DIR')) order by mtime;
select count(*) from all_tables ; -- 3160 rows
select count(*) from ALL_VIEWS; -- 8355  Rows
select count(*) from all_indexes; -- 4452  Rows
select COUNT(*) from all_objects;-- where object_type='INDEX';38733

Get Table size:
SELECT SUM(bytes)/1024/1024 AS "Table Size (MB)" FROM user_segments WHERE segment_name='PDB_DATA_IN_3301';


Triggers:
Create table audit_table(
Audit_id number primary key,
Orignial_table_tow_id number,
Attribute_name varchar2(100),
Old_value varchar2(100),
New_value varchar2(100),
Modified_date timestamp

);

Create or replace trigger table_trigger_name
Before update of attribute1,attribute2,….atttribut10 on "original_table_name"
For each row
BEGIN
    if :old.attribute1<> :NEW.attribute1 then
       insert into audit_table() values ();
   end if;
End;

Hierarchy by child:
select * from table
start with oid=
(select oid  from table where CONNECT_BY_ISLEAF=1 start with oid=52137220
CONNECT BY prev_oid = PRIOR oid)
connect by prior prev_oid=oid;

Execution Time:
    EXPLAIN PLAN FOR
SELECT
    *
FROM
    table where column='1';
    

SELECT 
    PLAN_TABLE_OUTPUT 
FROM 
    TABLE(DBMS_XPLAN.DISPLAY());

1) Syntactic check -> it will check(Syntax check) all the reserved keys like select,from,where..
2) Semantic check -> it will check table,columns,etc..
    a. It will start from right to left check.
3) Full scan -> it scans all the records in the table, so there will be performance issue. Energy -> CPU Cost.
    a. To check CPU Cost -> select * from v$sql_plan;
    b. For particular query, we have to get sql_id, for that we need to get from "select * from v$sql where sql_text like ('query%');
    


