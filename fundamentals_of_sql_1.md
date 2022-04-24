# SQL基礎
  
## 目次
1. SQL言語とは
2. SQLの基本構文
  
### 1. SQL言語とは
  
RDBMS(リレーショナルデータベースマネジメントシステム)で利用されるDB(データベース)操作言語のこと。  
  
#### 代表的なRDBMS
- MySQL  
- PostgreSQL  
- SQLite  
- Oracle  
  
#### そもそもデータベースってなに？
データベースとは、データを永続化させる仕組み。  
データを効率的かつ汎用的に利用できるようにする。  
  
テーブルで管理できる情報をデータベースを利用してデータを保存すること。  
  
#### DBMS(データベースマネジメントシステム)ってなに？
- ユーザとDBの仲介となって、DBを管理するためのソフト
- データを保存・変更・参照...etc
- 同時接続・同時処理(データの一貫性)をサポートし、データの一貫性を保持する
- ユーザ管理(ロール)をサポートし、データの機密性を保持する
- トランザクションログをサポートし、障害復旧を行える
  
#### RDB(リレーショナルデータベース)ってなに？
データベースにおける、データモデルのひとつ。  
データモデルとは、データベースをどのような構成にするかというもの。  
他には、「階層型」と「ネットワーク型」などがある。  
「リレーショナル型」は、表形式で複数の表を関係づけてデータを構成するモデル。  
  
#### SQLとRDB
改めて、SQLはRDBに登録されている情報をRDBMSを介して操作するための言語。  

できること(=CRUD)  
- 情報の取得(Read)  
- 情報の挿入(Create)  
- 情報の更新(Update)  
- 情報の削除(Delete)  
  
#### SQLの操作対象
- テーブル 
- フィールド, セル 
- 列, カラム 
- 行, レコード  

### SQLの基本構文
#### 情報の取得(SELECT)  
- SELECT <列名> FROM テーブル名  
  
[w3shcools SQL SELECT Statement](https://www.w3schools.com/sql/sql_select.asp)
```
The SELECT statement is used to select data from a database.

The data returned is stored in a result table, called the result-set.

SELECT Syntax

SELECT column1, column2, ...
FROM table_name;
```  
  
- SELECT <列名> FROM <テーブル名> WHERE <条件1> (AND <条件2> AND ...<条件N>)
- SELECT <列名> FROM <テーブル名> WHERE <条件1> (OR <条件2> OR ...<条件N>)

[w3shcools SQL WHERE Clause](https://www.w3schools.com/sql/sql_where.asp)
```
The WHERE clause is used to filter records.

It is used to extract only those records that fulfill a specified condition.

WHERE Syntax
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```  

##### アスタリスク(\*)を使わないこと
カラム名を「\*」で指定することで処理が重くなる。  
- カラム名を格納するメモリ領域が必要になる
- カラム名をメモリに格納する処理が必要になる
- カラム名をメモリから取り出す処理が必要になる
以上から、アスタリスクを業務コードで使用するのはNG。  
  
#### 情報の挿入(INSERT INTO)  
- INSERT INTO <テーブル名> (<列名1>, <列名2>, ...<列名N>) VALUES (<列名に対応するデータ>)  

[w3shcools SQL INSERT INTO Statement](https://www.w3schools.com/sql/sql_insert.asp)
```
The INSERT INTO statement is used to insert new records in a table.

INSERT INTO Syntax
It is possible to write the INSERT INTO statement in two ways:

1. Specify both the column names and the values to be inserted:

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

2. If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. 
However, make sure the order of the values is in the same order as the columns in the table. Here, the INSERT INTO syntax would be as follows:

INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```  
##### 補足: 複数のレコードを登録する
VALUES以降の()をカンマ区切りで指定してあげること  
  
  
#### 情報の削除(DELETE FROM)
- DELETE FROM テーブル名 (WHERE <条件>)  
  
[w3shcools SQL DELETE Statement](https://www.w3schools.com/sql/sql_delete.asp)
```
The DELETE statement is used to delete existing records in a table.

DELETE Syntax
DELETE FROM table_name WHERE condition;

Note: Be careful when deleting records in a table! Notice the WHERE clause in the DELETE statement. 
      The WHERE clause specifies which record(s) should be deleted. 
      If you omit the WHERE clause, all records in the table will be deleted!
```  

##### 論理削除と物理削除
- 論理削除： 有効か無効かを判定するフィールドを用意して、その値によって削除したとみなす方法
- 物理削除： DELETEにより、レコードにある行そのものを削除する方法(一般的には使用しない)

#### 情報の更新(UPDATE)  
- UPDATE <テーブル名> SET (<フィールド1>, <フィールド2>, ...<フィールドN>) (WHERE <条件>)  

[w3shcools SQL UPDATE Statement](https://www.w3schools.com/sql/sql_update.asp)
```
The UPDATE statement is used to modify the existing records in a table.

UPDATE Syntax
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

Note: Be careful when updating records in a table! 
      Notice the WHERE clause in the UPDATE statement. 
      The WHERE clause specifies which record(s) that should be updated. 
      If you omit the WHERE clause, all records in the table will be updated!
```  
