Hadoop環境構築メモ
======================
目的
----------------------
MapReduce2.0とCloudera Impalaを使い倒すための環境構築メモ
注意（免責）
----------------------
お勉強のために試行錯誤して環境構築をおこなうため
記載した内容は必ずしも正しいとは限りません。
また、こちらを参考にインストールされた内容を参考にし
不具合が生じたとしても一切の責任は取りませんのでご注意ください。
環境
----------------------
###サマリ
ResouceManagerのサーバ1台、データNode1台の最小構成で構築する。
#### マスタ
##### virtualhost上にcentos6(64bit)
##### java7(1.7.0_45)
##### mysql-server(5.1)
##### mysql-connector-java
##### Hadoop
###### 　hadoop-hdfs-namenode 
###### 　hadoop-hdfs-secondarynamenode
###### 　hadoop-yarn-resourcemanager
######　 hadoop-mapreduce-historyserver
###### 　hadoop-yarn-proxyserver
###### 　hadoop-client
##### impala-state-store
