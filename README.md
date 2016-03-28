# Apache-Phoenix
This is a basic Apache phoenix Installation and sample run
hduser@Acomp154:~$ start-all.sh

This script is Deprecated. Instead use start-dfs.sh and start-yarn.sh

16/03/18 09:34:48 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

Starting namenodes on [localhost]

hduser@localhost's password: 

localhost: starting namenode, logging to /usr/local/hadoop/logs/hadoop-hduser-namenode-Acomp154.out

localhost: Java HotSpot(TM) Server VM warning: You have loaded library /usr/local/hadoop/lib/native/libhadoop.so.1.0.0 which might have disabled stack guard. The VM will try to fix the stack guard now.

localhost: It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.

hduser@localhost's password: 

localhost: starting datanode, logging to /usr/local/hadoop/logs/hadoop-hduser-datanode-Acomp154.out

localhost: Java HotSpot(TM) Server VM warning: You have loaded library /usr/local/hadoop/lib/native/libhadoop.so.1.0.0 which might have disabled stack guard. The VM will try to fix the stack guard now.

localhost: It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.

Starting secondary namenodes [0.0.0.0]

hduser@0.0.0.0's password: 

0.0.0.0: starting secondarynamenode, logging to /usr/local/hadoop/logs/hadoop-hduser-secondarynamenode-Acomp154.out

0.0.0.0: Java HotSpot(TM) Server VM warning: You have loaded library /usr/local/hadoop/lib/native/libhadoop.so.1.0.0 which might have disabled stack guard. The VM will try to fix the stack guard now.

0.0.0.0: It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.

16/03/18 09:35:19 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

starting yarn daemons

starting resourcemanager, logging to /usr/local/hadoop/logs/yarn-hduser-resourcemanager-Acomp154.out

hduser@localhost's password: 

localhost: starting nodemanager, logging to /usr/local/hadoop/logs/yarn-hduser-nodemanager-Acomp154.out

localhost: Java HotSpot(TM) Server VM warning: You have loaded library /usr/local/hadoop/lib/native/libhadoop.so.1.0.0 which might have disabled stack guard. The VM will try to fix the stack guard now.

localhost: It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.


hduser@Acomp154:~$ start-hbase.sh

hduser@localhost's password: 

localhost: starting zookeeper, logging to /opt/hbase/bin/../logs/hbase-hduser-zookeeper-Acomp154.out

starting master, logging to /opt/hbase/logs/hbase-hduser-master-Acomp154.out

starting regionserver, logging to /opt/hbase/logs/hbase-hduser-1-regionserver-Acomp154.out



hduser@Acomp154:~$ jps

3421 NodeManager

2727 DataNode

2573 NameNode

2923 SecondaryNameNode

3860 HMaster

4108 Jps

3791 HQuorumPeer

3992 HRegionServer

3078 ResourceManager




Setting Up Apache Phoenix Environment:

Download Apache phoenix-4.7.0-Hbase-1.0-bin from phoenix archives

Extract to  /opt/phoenix

Copy the entire Apache Phoenix jar files paste into hbase lib folder.

And simply run ./sqlline.py localhost in phoenix bin 

hduser@Acomp154:/opt/phoneix/bin$ ./sqlline.py localhost
Setting property: [incremental, false]

Setting property: [isolation, TRANSACTION_READ_COMMITTED]

issuing: !connect jdbc:phoenix:localhost none none org.apache.phoenix.jdbc.PhoenixDriver

Connecting to jdbc:phoenix:localhost

SLF4J: Class path contains multiple SLF4J bindings.

SLF4J: Found binding in [jar:file:/opt/phoneix/phoenix-4.7.0-HBase-1.0-client.jar!/org/slf4j/impl/StaticLoggerBinder.class]

SLF4J: Found binding in [jar:file:/usr/local/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]

SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.

16/03/18 09:42:41 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

16/03/18 09:42:42 WARN hbase.HTableDescriptor: Use addCoprocessor* methods to add a coprocessor instead

Connected to: Phoenix (version 4.7)

Driver: PhoenixEmbeddedDriver (version 4.7)

Autocommit status: true

Transaction isolation: TRANSACTION_READ_COMMITTED

Building list of tables and columns for tab-completion (set fastconnect to true to skip)...

128/128 (100%) Done

Done

sqlline version 1.1.8


Create a table for  
0: jdbc:phoenix:localhost> CREATE TABLE IF NOT EXISTS LOAN2 (
AMT INTEGER,

DATE DATE,
LOAN_TIT VARCHAR,
RSK_SCRE INTEGER,
INCME_RTIO VARCHAR NOT NULL,ZIP VARCHAR,
STATE CHAR(2),
EMPL_LNTH VARCHAR,
POL_CODE INTEGER
 CONSTRAINT PK PRIMARY KEY (INCME_RTIO)
 );


No rows affected (0.535 seconds)

Bulk Load CSV File For 

hduser@Acomp154:~$ ./psql.py -t LOAN localhost /home/hduser/Desktop/loan/load.csv

Example for Bulk Load

hduser@Acomp154:/opt/phoneix/bin$ 
                                   ./psql.py -t LOAN2 localhost/home/hduser/Desktop/loan/RejectStatsB.csv


SLF4J: Class path contains multiple SLF4J bindings.

SLF4J: Found binding in [jar:file:/opt/phoneix/phoenix-4.7.0-HBase-1.0-client.jar!/org/slf4j/impl/StaticLoggerBinder.class]

SLF4J: Found binding in [jar:file:/usr/local/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]

SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.

16/03/18 11:06:11 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

16/03/18 11:06:12 WARN hbase.HTableDescriptor: Use addCoprocessor* methods to add a coprocessor instead

16/03/18 11:06:13 WARN hbase.HTableDescriptor: Use addCoprocessor* methods to add a coprocessor instead

csv columns from database.

CSV Upsert complete. 1048574 rows upserted

Time: 71.896 sec(s)




jdbc:phoenix:localhost>select * From loan2;

Output looks like

+---------+--------------------------+--------------------------+-----------+-------------+--------+--------+------------+-----------+

|   AMT   |           DATE           |         LOAN_TIT         | RSK_SCRE  | INCME_RTIO  |  ZIP   | STATE  | EMPL_LNTH  | POL_CODE  |

+---------+--------------------------+--------------------------+-----------+-------------+--------+--------+------------+-----------+

| 5550    | 2014-02-27 00:00:00.000  | debt_consolidation       | 684       | 99.15%      | 726xx  | AR     | < 1 year   | 0         |

| 25000   | 2014-02-18 00:00:00.000  | credit_card              | 626       | 99.16%      | 376xx  | TN     | < 1 year   | 0         |

| 10000   | 2014-02-26 00:00:00.000  | debt_consolidation       | 598       | 99.17%      | 309xx  | GA     | < 1 year   | 0         |


+---------+--------------------------+--------------------------+-----------+-------------+--------+--------+------------+-----------+

25,598 rows selected (17.793 seconds)

0: jdbc:phoenix:localhost> 







Group By loan title

0: jdbc:phoenix:localhost> SELECT  LOAN_TIT as "Loan Title",count(STATE) as "State Count",sum(AMT) as "Amt Sum"
 from loan2
 GROUP BY LOAN_TIT
 ORDER BY sum(AMT) DESC;





Advantages:

Normally Hbase is not support for querying but using apahe phoenix we can easily querying using hbase with efficient than hive.It supports all type of join group by everything.
