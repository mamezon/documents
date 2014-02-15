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

環境構築
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
#### 各種設定
##### mysql
######シンボリックリンク作成(Hiveディレクトリの下に作成)
ln -s /usr/share/java/mysql-connector-java.jar /usr/lib/hive/lib/mysql-connector-java.jar
###### サービス起動
インストール直後は起動されていなかったので立ち上げる。また自動で起動するように設定しておく  
service --status-allで確認  
service mysqld start  
chkconfig --listで確認  
chkconfig mysqld on  
###### ログイン＆パスワード設定
mysql -u root -p でログイン  
mysqladmin -u root password "{パスワードを設定※記号を利用する場合にはダブルクォーテーションで囲う必要あり}"  
###### Hiveを利用するためにmetastoreを作成
create database metastore;
###### metastoreの設定
source /usr/lib/hive/scripts/metastore/upgrade/mysql/hive-schema-0.12.0.mysql.sql;（※読み込むファイルは最新版でよい。） 
###### hiveユーザの作成&権限作成
create user hiveuser@localhost identified by '{パスワード}'  
grant all privileges on metastore.* to hiveuser@localhost;
flush privileges;
##### Hiveの設定
/etc/hive/conf/hive-site.xmlを修正  
ConnectionURL,ConnectionDriverNameをデフォルトのDurbyからmysqlに変更  
ユーザ名、パスワードを設定
