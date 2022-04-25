# SQL基礎2

## 目次
1. MySQLとはなにか
2. MySQLのインストール
3. テーブルの作成
4. テーブルの確認
5. テーブルをJOINしてみる

### 1. MySQLとはなにか
- 現在はOracleのオープンソースソフトウェアのRDBMS
- SQLが利用できる
- 1995年に生まれる(RDBMSでは比較的新しい)  
  [MySQLの歴史が面白い](https://qiita.com/nom_bom/items/75d409b303f4814143c8)

#### RDBMSのメリット
1. トランザクションによりデータの一貫性・整合性を保証
2. ユーザ管理により、データの機密性を担保
3. トランザクションログにより、障害からの復旧

### 2. MySQLのインストール
```
$ uname -a
Linux ubuntu 5.4.0-107-generic #121-Ubuntu SMP Thu Mar 24 16:04:27 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux

$ sudo apt update
...(略)

$ sudo apt install mysql-server
...(略)
Do you want to continue? [Y/n] Y
...(略)

$ systemctl status mysqld
● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-04-25 23:50:24 JST; 21s ago
...(略)

$ sudo mysql_secure_installation
...(略)
Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0
Please set the password for root here.

New password: // 好きなパスワード
Re-enter new password: // 上記と同じパスワード

Estimated strength of the password: 0 // 0 - 100まででパスワードの強度を表示してくれます
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
...(以降のプロンプトはすべて「Y」)

$ mysql -V
mysql  Ver 8.0.28-0ubuntu0.20.04.3 for Linux on x86_64 ((Ubuntu))
$ sudo mysql -u root
...(略)
mysql>

```  

### 3. テーブルの作成
```
$ sudo mysql -u root < sql2.sql
$ 
```  

- sql2.sql
```
DROP DATABASE IF EXISTS app_db; # もしapp_dbデータベースがあれば削除する
CREATE DATABASE app_db; # app_dbデータベースを作成
USE app_db; # app_dbへ接続

CREATE TABLE prefectures (
    prefecture_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(6)
); # prefecturesテーブルを作成して、prefecture_id, nameカラムを作成

CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    prefecture_id INT,
    name VARCHAR(18)
); # usersテーブルを作成して、user_id, prefecture_id, nanmeカラムを作成

INSERT INTO prefectures (name) VALUES
('北海道'),
('青森'),
('岩手'),
('宮城'),
('秋田'),
('山形'),
('福島'),
('茨城'),
('栃木'),
('群馬'),
('埼玉'),
('千葉'),
('東京'),
('神奈川'),
('新潟'),
('富山'),
('石川'),
('福井'),
('山梨'),
('長野'),
('岐阜'),
('静岡'),
('愛知'),
('三重'),
('滋賀'),
('京都'),
('大阪'),
('兵庫'),
('奈良'),
('和歌山'),
('鳥取'),
('島根'),
('岡山'),
('広島'),
('山口'),
('徳島'),
('香川'),
('愛媛'),
('高知'),
('福岡'),
('佐賀'),
('長崎'),
('熊本'),
('大分'),
('宮崎'),
('鹿児島'),
('沖縄');
# prefecturesテーブルのnameカラムに、各都道府県(値)を挿入する

INSERT INTO users (prefecture_id, name) VALUES
(14, 'mike'),
(10, 'david'),
(1, 'karen'),
(3, 'emma'),
(null, 'ava');
# usersテーブルにprefecture_idとnameカラムに値を挿入

```  

### 4. テーブルの確認
```
$ sudo mysql -u root

mysql> show database;
+--------------------+
| Database           |
+--------------------+
| app_db             |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

mysql> show tables;
+------------------+
| Tables_in_app_db |
+------------------+
| prefectures      |
| users            |
+------------------+
2 rows in set (0.00 sec)

mysql> USE app_db;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select * from users
+---------+---------------+-------+
| user_id | prefecture_id | name  |
+---------+---------------+-------+
|       1 |            14 | mike  |
|       2 |            10 | david |
|       3 |             1 | karen |
|       4 |             3 | emma  |
|       5 |          NULL | ava   |
+---------+---------------+-------+
5 rows in set (0.00 sec)

mysql> select * from prefectures;
+---------------+-----------+
| prefecture_id | name      |
+---------------+-----------+
|             1 | 北海道    |
|             2 | 青森      |
|             3 | 岩手      |
|             4 | 宮城      |
|             5 | 秋田      |
|             6 | 山形      |
|             7 | 福島      |
|             8 | 茨城      |
|             9 | 栃木      |
|            10 | 群馬      |
|            11 | 埼玉      |
|            12 | 千葉      |
|            13 | 東京      |
|            14 | 神奈川    |
|            15 | 新潟      |
|            16 | 富山      |
|            17 | 石川      |
|            18 | 福井      |
|            19 | 山梨      |
|            20 | 長野      |
|            21 | 岐阜      |
|            22 | 静岡      |
|            23 | 愛知      |
|            24 | 三重      |
|            25 | 滋賀      |
|            26 | 京都      |
|            27 | 大阪      |
|            28 | 兵庫      |
|            29 | 奈良      |
|            30 | 和歌山    |
|            31 | 鳥取      |
|            32 | 島根      |
|            33 | 岡山      |
|            34 | 広島      |
|            35 | 山口      |
|            36 | 徳島      |
|            37 | 香川      |
|            38 | 愛媛      |
|            39 | 高知      |
|            40 | 福岡      |
|            41 | 佐賀      |
|            42 | 長崎      |
|            43 | 熊本      |
|            44 | 大分      |
|            45 | 宮崎      |
|            46 | 鹿児島    |
|            47 | 沖縄      |
+---------------+-----------+
47 rows in set (0.01 sec)

```  

### 5. テーブルをJOINしてみる
```
mysql> SELECT * FROM users INNER JOIN prefectures ON users.prefecture_id = prefectures.prefecture_id;
+---------+---------------+-------+---------------+-----------+
| user_id | prefecture_id | name  | prefecture_id | name      |
+---------+---------------+-------+---------------+-----------+
|       1 |            14 | mike  |            14 | 神奈川    |
|       2 |            10 | david |            13 | 群馬      |
|       3 |             1 | karen |             1 | 北海道    |
|       4 |             3 | emma  |             3 | 岩手      |
+---------+---------------+-------+---------------+-----------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM users LEFT OUTER JOIN prefectures ON users.prefecture_id = prefectures.prefecture_id;
+---------+---------------+-------+---------------+-----------+
| user_id | prefecture_id | name  | prefecture_id | name      |
+---------+---------------+-------+---------------+-----------+
|       1 |            14 | mike  |            14 | 神奈川    |
|       2 |            10 | david |            13 | 群馬      |
|       3 |             1 | karen |             1 | 北海道    |
|       4 |             3 | emma  |             3 | 岩手      |
|       5 |          NULL | ava   |          NULL | NULL      |
+---------+---------------+-------+---------------+-----------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM users RIGHT OUTER JOIN prefectures ON users.prefecture_id = prefectures.prefecture_id;
+---------+---------------+-------+---------------+-----------+
| user_id | prefecture_id | name  | prefecture_id | name      |
+---------+---------------+-------+---------------+-----------+
|       3 |             1 | karen |             1 | 北海道    |
|    NULL |          NULL | NULL  |             2 | 青森      |
|       4 |             3 | emma  |             3 | 岩手      |
|    NULL |          NULL | NULL  |             4 | 宮城      |
|    NULL |          NULL | NULL  |             5 | 秋田      |
|    NULL |          NULL | NULL  |             6 | 山形      |
|    NULL |          NULL | NULL  |             7 | 福島      |
|    NULL |          NULL | NULL  |             8 | 茨城      |
|    NULL |          NULL | NULL  |             9 | 栃木      |
|       2 |            10 | david |            10 | 群馬      |
|    NULL |          NULL | NULL  |            11 | 埼玉      |
|    NULL |          NULL | NULL  |            12 | 千葉      |
|    NULL |          NULL | NULL  |            13 | 東京      |
|       1 |            14 | mike  |            14 | 神奈川    |
|    NULL |          NULL | NULL  |            15 | 新潟      |
|    NULL |          NULL | NULL  |            16 | 富山      |
|    NULL |          NULL | NULL  |            17 | 石川      |
|    NULL |          NULL | NULL  |            18 | 福井      |
|    NULL |          NULL | NULL  |            19 | 山梨      |
|    NULL |          NULL | NULL  |            20 | 長野      |
|    NULL |          NULL | NULL  |            21 | 岐阜      |
|    NULL |          NULL | NULL  |            22 | 静岡      |
|    NULL |          NULL | NULL  |            23 | 愛知      |
|    NULL |          NULL | NULL  |            24 | 三重      |
|    NULL |          NULL | NULL  |            25 | 滋賀      |
|    NULL |          NULL | NULL  |            26 | 京都      |
|    NULL |          NULL | NULL  |            27 | 大阪      |
|    NULL |          NULL | NULL  |            28 | 兵庫      |
|    NULL |          NULL | NULL  |            29 | 奈良      |
|    NULL |          NULL | NULL  |            30 | 和歌山    |
|    NULL |          NULL | NULL  |            31 | 鳥取      |
|    NULL |          NULL | NULL  |            32 | 島根      |
|    NULL |          NULL | NULL  |            33 | 岡山      |
|    NULL |          NULL | NULL  |            34 | 広島      |
|    NULL |          NULL | NULL  |            35 | 山口      |
|    NULL |          NULL | NULL  |            36 | 徳島      |
|    NULL |          NULL | NULL  |            37 | 香川      |
|    NULL |          NULL | NULL  |            38 | 愛媛      |
|    NULL |          NULL | NULL  |            39 | 高知      |
|    NULL |          NULL | NULL  |            40 | 福岡      |
|    NULL |          NULL | NULL  |            41 | 佐賀      |
|    NULL |          NULL | NULL  |            42 | 長崎      |
|    NULL |          NULL | NULL  |            43 | 熊本      |
|    NULL |          NULL | NULL  |            44 | 大分      |
|    NULL |          NULL | NULL  |            45 | 宮崎      |
|    NULL |          NULL | NULL  |            46 | 鹿児島    |
|    NULL |          NULL | NULL  |            47 | 沖縄      |
+---------+---------------+-------+---------------+-----------+
47 rows in set (0.00 sec)

```  

#### JOINの仕組み
MySQLでは、Nested Loop JOINを実行している。
```
app_db データベース
+------------------+
| Tables_in_app_db |
+------------------+
| prefectures      |
| users            |
+------------------+

users テーブル
+---------+---------------+-------+
| user_id | prefecture_id | name  |
+---------+---------------+-------+
|       1 |            14 | mike  |
|       2 |            10 | david |
|       3 |             1 | karen |
|       4 |             3 | emma  |
|       5 |          NULL | ava   |
+---------+---------------+-------+

prefectures テーブル
+---------------+-----------+
| prefecture_id | name      |
+---------------+-----------+
|             1 | 北海道    |
|             2 | 青森      |
|             3 | 岩手      |
|             4 | 宮城      |
|             5 | 秋田      |
|             6 | 山形      |
|             7 | 福島      |
|             8 | 茨城      |
|             9 | 栃木      |
|            10 | 群馬      |
|            11 | 埼玉      |
|            12 | 千葉      |
|            13 | 東京      |
|            14 | 神奈川    |
|            15 | 新潟      |
|            16 | 富山      |
|            17 | 石川      |
|            18 | 福井      |
|            19 | 山梨      |
|            20 | 長野      |
|            21 | 岐阜      |
|            22 | 静岡      |
|            23 | 愛知      |
|            24 | 三重      |
|            25 | 滋賀      |
|            26 | 京都      |
|            27 | 大阪      |
|            28 | 兵庫      |
|            29 | 奈良      |
|            30 | 和歌山    |
|            31 | 鳥取      |
|            32 | 島根      |
|            33 | 岡山      |
|            34 | 広島      |
|            35 | 山口      |
|            36 | 徳島      |
|            37 | 香川      |
|            38 | 愛媛      |
|            39 | 高知      |
|            40 | 福岡      |
|            41 | 佐賀      |
|            42 | 長崎      |
|            43 | 熊本      |
|            44 | 大分      |
|            45 | 宮崎      |
|            46 | 鹿児島    |
|            47 | 沖縄      |
+---------------+-----------+
```  
駆動表と内部表がある。  
駆動表のレコードに対して、すべての内部表のレコードを見る。  
これを駆動表のレコードすべてで実行する。  

駆動表はメモリに格納される。  
もしJOINを実行する場合は、駆動表のレコードを小さくして内部表のレコードを大きくすることで効率的にJOINを実行できる。  
上記のテーブルについては、『users > prefectures』なので、駆動表がusersだと早くなる。  
