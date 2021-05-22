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
   
   Cluster is a most important part of the snowflake to group the data and create micropartitions.
   Also, its costly too. Including Manual clustering
   Also, instead of clustering, we can go with order by or group by.
   
   Virtual warehouse :
   Virtual warehouse is a kind of servers running backend which automatically spins up or spins down based on the number of users.
  Auto Sized cluster : The cluster automatically spins up whenever they are needed.
  Maximized Mode : when both maximum and minimum mode are same, then automatically it clusters to the maximum mode.
  
Scaling Policy - Standara, Economy are performed.
If standard is there, then the cluster scales up automatically
If economy is there, it checks for 5-6 minutes and then scales up.


Performance Tuning in Snowflake is the cost reduction:
1. Processing cost : By sharing the clusters, Use order by instaed of Cluster by, FIlter on the max rows, Use Multi cluster option instead of spinning up the same cluster.
2. Storage cost :

No Indexing, constraints in the Snowflake.
DataSkipping - Create a metadata out of the partitions and check if the metadata has relevant data. If so, it will pick up the partition, else it will be skipped.
Pruning - Based on the where clause, it eliminates the major partitions and load the data into the system.
ACID Transactions: Atomicity, Consistency, Isolated, Durability guarantee a successfule transaction.

Update and another Update- second update will be blocked
Update and next drop - Update will be aborted 
Insert and drop - insert will run
2 updates on different columns on same table also result in block of second update statement.

Update Transaction in Snowflake : COmbination of Insert & delete.
In Snowflake - all the data is stored as BLOB storage in S3. Here, if we want to update, we have to delete that whole file and recreate with updated data.
If the updated records are less - we can go with recreating the table, instead of deleting and updating.

No Constraints. Only active Constraint is Not Null
Definitaly we need to run the SCD2 or SCd1 to merge the data to maintain the Referential Integrity.


Storage Metircs table in Snowflake:
select *
from snowflake.information_schema.table_storage_metrics
where table_name = 'LINEITEM';

Information_schema.table_storage_metrics - this view stores the information about the storage cost of current table & deleted table.
Deleted table comes under 3 options :
                               1. Time travel - when the table is deleted but it is still within the retention period.
                               2. Fail Safe - Fail Safe is the table is not within the retention period, but within the fail
                               3. result of cloning - Not in time travel or fail safe, but the new table refers the deleted table as a result of cloning.
                               






