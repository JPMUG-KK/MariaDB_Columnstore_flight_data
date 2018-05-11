# MariaDB Columnstore & InnoDB用 全米フライトデータ

全米フライトデータ（2013〜2017年）インポート用ファイル
簡単に各エンジン毎のパフォーマンス検証をするためのデータベース作成支援を目的に公開
ColumnStore及びInnoDBエンジン用の２パターンを用意

## Usage

### ファイルのダウンロード
下記GoogleDriveよりファイルをダウンロード

<https://drive.google.com/open?id=1cUOynhQIAKnhF5GRv42LaheDGzydDtgu>

|file|size|desc|
|:---|---:|:---|
|flights_idb_table.sql|3.78GB|InnoDBテーブル作成&データロード用|
|flights_mcs_table.sql|3KB|Columnstoreテーブル作成用|
|airlines.txt|0.3KB|Columnstore airlinesテーブルデータロード用|
|airports.txt|24KB|Columnstore airportsテーブルデータロード用|
|flights.txt|2.96GB|Columnstore flightsテーブルデータロード用|

### ColumnStore データベース作成

データベース `flights` を作成後にテーブル定義をロード
```sql
create database flights;
use flights;
source flights_mcs_table.sql;
```

`cpimport` コマンドでデータをインポート

```terminal
cpimport flights airlines airlines.txt
cpimport flights airports airports.txt
cpimport flights flights flights.txt
```
### InnoDB データベース作成

データベース `flights_idb` 作成後にデータをロード

```sql
create database flights_idb;
use flights_idb;
source flights_idb_table.sql;
```
