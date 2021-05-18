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
 
 
 Snowflake Architecture:
 Multi cluster Shared Architecture.
 It has 3 layers :
 1. Data Storage
 2. Virtual Data Warehouse. - this layer holds cache to persist the data.
 3. Cloud Services. This part has Metadata storage, Authentication and access control. And other cloud services such as infrastructure manager, Optimizer, Security.
 
 Shared Nothing Architecture:
 1. Heterogenous workload and homogenous hardware.
 2. Membership Changes
 3. Problem with Software upgrades.
 
 How the Shared Nothing Architecture is revisited using Snowflake Architecture:
 1. Both Compute and Data Storage layer can grow or shrink in parallel.
 2. Cloud services layer can help us to manage all other information such as Metadata layer, Optimizer, Security, Authentication and access control.

Snowflake uses Multi cluster Shared Nothing Architecture.

      https://docs.snowflake.com/en/user-guide/intro-key-concepts.html
      
 
 Snowflake Caching :
    Snowflake Caching is purley dependent on the 3 parts : 1. Remote Disk on data storage layer
                                                           2. Local Disk Cache on VIrtual Warehouse layer
                                                           3. Result Cache on the CLoude services layer.
                                                           
                                                           
   Always use Result cache on teh cloude services layer. If it is not present, then go with Local Disk.
   Otherwise, it will take long time to get the data from Local Disk Cache on Virtual Warehouse layer.
   
   To disable the Cloud services layer Result cahce- we use the command as alter session used_cache_disabled =false
   





