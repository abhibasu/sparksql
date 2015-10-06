# sparksql


This Wiki explains how to configure Cloudera Hadoop Distribution (CDH 5.3) to enable SparkSQL with Hive Metastore access.

CDH 5.3 ships with Spark 1.2.0 which also includes SparkSQL - the in-memory SQL-on-Hadoop engine. However, SparkSQL is not enabled for interacting with Hive metastore, which is a mystery to me, as Hive metastore is the most common Hadoop data warehouse in use today. 

**After CDH 5.3 is installed and Spark is enabled through Cloudera Manager, follow these steps to enable Hive access:**  
1. Ensure hive is working from Hive CLI and JDBC through HiveServer2 (Should be working by default).  
2. Copy hive-site.xml to your SPARK_HOME/conf folder.  
3. Add Hive libraries to Spark classpath -> edit the SPARK_HOME/bin/compute-classpath.sh file and add the following:  
    CLASSPATH="$CLASSPATH:/opt/cloudera/parcels/CDH-5.3.0-1.cdh5.3.0.p0.30/lib/hive/lib/*"   (CDH specific example, use your hive lib location).  
4. Restart the Spark cluster for everything to take effect.

**TESTING:**    
1. Run Hive CLI and create a table:    
       CREATE TABLE TEST(id int, desc string);    
       SHOW TABLES; (to verify)  
2. Run SparkSQL CLI (SPARK_HOME/bin/spark-sql):  
       SHOW TABLES;  
       SELECT COUNT(*) from TEST;

Now you are setup to use SparkSQL through the CLI or from spark shells (Python and Scala). See here for more documentation on SparkSQL - http://spark.apache.org/docs/1.2.1/sql-programming-guide.html





 
