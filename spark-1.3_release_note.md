# Apache Spark 1.3.0 リリースノート

日本語訳: [@data_sciesotist](https://twitter.com/data_sciesotist)

## Spark 1.3.0
Spark 1.3.0は1.x系の4つ目のリリースです。本リリースでは、Spark SQLのアルファ版プロジェクトから、DataFrame APIが正式に取り込まれました。

また、Spark CoreやMLlib、Spark Streamingについても改良が加えられました。

Spark 1.3は60以上の組織、174名のコントリビューターからの、1000以上のパッチによる成果です。

Spark 1.3は、[ダウンロードページ](https://spark.apache.org/downloads.html) から入手できます。

## Spark Core
Spark 1.3では、Spark Coreに対していくつかの改良を行いました。

Core APIでは、複雑なReduce処理を高速化するために["multi level aggregation trees"](https://issues.apache.org/jira/browse/SPARK-5430) をサポートしました。

[エラーレポートの改良](https://issues.apache.org/jira/browse/SPARK-5063) により、的確に処理の過程、結果を把握できるようになりました。

SparkのJettyアプリケーションサーバへの依存性により、ユーザープログラムと衝突していた[問題が解消されました](https://issues.apache.org/jira/browse/SPARK-3996) 。

Sparkは、いくつかの通信機能において、[SSL encryptionをサポートしました](https://issues.apache.org/jira/browse/SPARK-3883) 。

また、[リアルタイムにガベージコレクションのメトリクスを行う機能](https://issues.apache.org/jira/browse/SPARK-3428) 、[タスク内のI/Oを計測する機能](https://issues.apache.org/jira/browse/SPARK-4874) を新たにUIに追加しました。

## DataFrame API
Spark 1.3では、新たに[DataFrame API](https://spark.apache.org/docs/1.3.0/sql-programming-guide.html#dataframes) が導入されました。

DataFrame APIは、構造化されたデータセットに対する強力で簡便な操作を実現します。DataFrame APIは、スキーマ情報と紐付いた名前付きフィールドを保有しており、基本的なRDD APIの発展形と言えます。

DataFrame APIはHiveテーブルやJSONデータ、JDBCで接続したデータベース、その他Sparkの新しいデータソースAPIを経由したさまざまなデータから、データフレームを作成できます。

データフレームは、今後Sparkとその他システムとの間での標準的なデータ交換フォーマットになる予定です。データフレームは、Python、Scala、Javaでサポートされています。

## Spark SQL
本リリースにおいて、Spark SQLはアルファプロジェクトを[卒業](https://issues.apache.org/jira/browse/SPARK-5166) しました。

また、HiveQLの"方言"への後方互換性を保証し、安定したプログラミングAPIを提供することになりました。

Spark SQLは、各データソースAPIに対する[テーブルの書き込み機能をサポートしました](https://issues.apache.org/jira/browse/SPARK-5658) 。

新しい[JDBCデータソースAPI](https://issues.apache.org/jira/browse/SPARK-5472) はMySQL、PostgreSQL、その他のRDBMSとの間のインポート、エクスポートに対応しました。

HiveQLとの互換性を向上するため、多岐にわたる小さな機能追加が行われています。

また、[Parquetと互換性のあるスキーマ構造を取り入れた](https://issues.apache.org/jira/browse/SPARK-3851) ことにより、機能が向上しています。

## Spark ML / MLlib
本リリースにおいて、Spark MLlibにいくつかの新しいアルゴリズムが実装されました。

1. トピックモデルのための["Latent Dirichlet Allocation (LDA)"](https://issues.apache.org/jira/browse/SPARK-1405)
1. 多値分類のための[多項ロジスティック回帰](https://issues.apache.org/jira/browse/SPARK-2309)
1. クラスタリングのための[ガウス混合分布モデル](https://issues.apache.org/jira/browse/SPARK-5012)
1. [べき乗法クラスタリング](https://issues.apache.org/jira/browse/SPARK-4259)
1. 頻出パターンマイニングのための[頻出パターン成長 (FP-growth) モデル](https://issues.apache.org/jira/browse/SPARK-4001)
1. 分散環境における線形代数処理のための ["block matrix abstraction"](https://issues.apache.org/jira/browse/SPARK-4409)

また、交換可能なフォーマットによる[モデルのインポート、エクスポートのサポートを開始しました](https://issues.apache.org/jira/browse/SPARK-4587) 。今後、Java / Python / Scalaにおいてさらに交換可能なモデルを追加していきます。

k-means法とALSの実装を改良し、[パフォーマンスが向上しました](https://issues.apache.org/jira/browse/SPARK-3424,%20https://issues.apache.org/jira/browse/SPARK-3541) 。

PySparkにおいて、Spark 1.2で追加された[ML pipeline API](https://issues.apache.org/jira/browse/SPARK-4586) と、[勾配ブースティング木 (gradient boosted trees)](https://issues.apache.org/jira/browse/SPARK-5094) および[ガウス混合分布モデル](https://issues.apache.org/jira/browse/SPARK-5012) をサポートしました。

ML pipeline APIは、新しいDataFrame構造をサポートします。

## Spark Streaming
Spark 1.3では、["direct Kafka API"を提供します](https://issues.apache.org/jira/browse/SPARK-4964) [（ドキュメント）](http://spark.apache.org/docs/1.3.0/streaming-kafka-integration.html) 。これにより、ログ先行書き込みを必要とせず、重複を排除したデータ入出力が可能になりました。

PythonのためのKafka APIも、将来的な拡張を念頭に[実装されました](https://issues.apache.org/jira/browse/SPARK-5047) 。

[ロジスティック回帰のオンライン (リアルタイム) 処理](https://issues.apache.org/jira/browse/SPARK-4979) を実装し、[バイナリデータ (2値データ) を処理することが可能になりました](https://issues.apache.org/jira/browse/SPARK-4969) 。

ステートフルな処理を実現するため、["initial state RDD"がサポートされました](https://issues.apache.org/jira/browse/SPARK-3660) 。

ドキュメントを更新し、ストリーミング処理におけるSQLやDataFrameの扱いに関する情報を追加しました。また、Sparkにおける「フォールトトレランス」の意味を明確化しました。

## GraphX
グラフにおける ["canonical edge" のサポート](https://issues.apache.org/jira/browse/SPARK-4917) をはじめとした、いくつかの改良、拡張を行いました。

## Spark 1.3へのアップグレード
Spark 1.3は過去の1.x系とバイナリ互換性があります。そのため、自作アプリケーションのコードなどを書き換える必要はありません。ただし、unstable扱いであったAPIは除きます。

例えば、Spark SQL APIが安定化したことにより、SchemaRDDクラスはDataFrameクラスに拡張、改名されました。詳細は、[Spark SQLの移行ガイド](http://spark.apache.org/docs/1.3.0/sql-programming-guide.html#migration-guide) を参照してください。

Spark SQLは、列識別子を必要とします。予約語 ("string"や"table"など) を識別子に用いることもできますが、その場合はバッククォート (` `) によりエスケープします。

## 既知の問題点
1. [SPARK-6194](https://issues.apache.org/jira/browse/SPARK-6194) : PySparkのcollect()関数におけるメモリリーク
1. [SPARK-6222](https://issues.apache.org/jira/browse/SPARK-6222) : Spark Streamingにおけるリカバリ処理に関する問題
1. [SAPRK-6315](https://issues.apache.org/jira/browse/SPARK-6315) : Spark SQLにおいて、Spark 1.1で生成されたParquet形式のデータが読み込めない問題
1. [SPARK-6247](https://issues.apache.org/jira/browse/SPARK-6247) : Spark SQLにおいて、いくつかのjoin構文の処理がエラーになる問題

クレジットは省略
