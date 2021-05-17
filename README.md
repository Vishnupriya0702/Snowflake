# Snowflake

Snowflake is cloud based data storage system, which can be accessed through AWS & other consoles.

sql queries  in Snowflake :

to change the admin :
 Use role accountadmin

create table statement:
Create table demo_db.public.call_center
AS 
Select * from snowflake_sample_data.TPCDS_SF100TCL.call_center

Select count(*) from demo_db.public.call_center

SELECT * FROM DEMO_DB.PUBLIC.CALL_CENTER limit 10

Create table using Like Statement: But only we can create, we cant copy the data.
 CREATE TABLE DEMO_DB.PUBLIC.CALL_CENTER_TEST LIKE DEMO_DB.PUBLIC.CALL_CENTER
 
SELECT *  FROM DEMO_DB.PUBLIC.CALL_CENTER_TEST2 limit 10

To copy the data from one table to another table:
 CREATE TABLE DEMO_DB.PUBLIC.CALL_CENTER_TEST2 CLONE DEMO_DB.PUBLIC.CALL_CENTER
 
 Show tables:
 Show tables like 'call%'
 Retentions are stored in Show tables.
 
 Partitions are stored in QueryID
