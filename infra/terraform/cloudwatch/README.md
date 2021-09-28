
# cloudwatch

---

## aws_cloudwatch_metric_alarm のリファレンスめも

- alarm_name
  - (必須) アラームの説明的な名前です。この名前は、ユーザーのAWSアカウント内で一意である必要があります。

- comparison_operator
  - (必須) 指定されたStatisticとThresholdを比較する際に使用する算術演算です。
  - 指定されたStatisticの値が第1オペランドとして使用されます。
  - 以下のいずれかがサポートされています。
    - GreaterThanOrEqualToThreshold: `＞＝`
    - GreaterThanThreshold: `＞`
    - LessThanThreshold: `＜`
    - LessThanOrEqualToThreshold: `＜＝`
  - さらに、LessThanLowerOrGreaterThanUpperThreshold、LessThanLowerThreshold、GreaterThanUpperThresholdの値は、異常検知モデルに基づくアラームにのみ使用されます。

- evaluation_periods
  - (必須) データを指定した閾値と比較する期間の数です。
  - 「統計」として使用する「期間」を継続する評価回数を設定します。

- metric_name
  - （オプション）アラームに関連するメトリックの名前。
  - サポートされているメトリックについては、docsを参照してください。
    - [AWS services that publish CloudWatch metrics \- Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/aws-services-cloudwatch-metrics.html)

      | 項目 | 設定値 |
      | :-- | :-- |
      | CPU使用率 | CPUUtilization |
      | ディスク使用率 | DiskSpaceUtilization |
      | バースト使用量 | BurstBalance |
      | メモリ使用率 | MemoryUtilization |
      | ステータスチェック | StatusCheckFailed |
      | ファイル数 | NumberOfObjects |
      | データサイズ | BucketSizeBytes |
      | ストレージ残量(Byte) | FreeStorageSpace |
      | 空きメモリ残量(Byte) | FreeableMemory |
      | 読み込みレイテンシ | ReadLatency |
      | 書き込みレイテンシ | WriteLatency |
      | SWAP利用量(Byte) | SwapUsage |
      | DBコネクション数 | DatabaseConnections |
      | レスポンスタイム | TargetResponseTime |
      | 読み込みIOPS | ReadIOPS |
      | 書き込みIOPS | WriteIOPS |
      | 書き込みOps | VolumeWriteOps |
      | 読み込みOps | VolumeReadOps |


- namespace
  - (オプション) アラームの関連メトリックのネームスペース。
  - 名前空間のリストについては、docsを参照してください。
  - サポートされているメトリックについては、docs を参照してください。
    - [AWS services that publish CloudWatch metrics \- Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/aws-services-cloudwatch-metrics.html)

- period
  - (オプション) 指定した統計を適用する期間を秒単位で指定します。

    | 項目 | 設定値 |
    | :-- | :-- |
    | 1分 | 60 |
    | 5分 | 300 |
    | 15分 | 900 |
    | 1時間 | 3600 |
    | 6時間 | 21600 |
    | 1日 | 86400 |


- statistic
  - (オプション) アラームの関連メトリックに適用する統計値。
  - 以下のいずれかがサポートされます。
    - SampleCount
    - Average
    - Sum
    - Minimum
    - Maximum

- threshold
  - (オプション) 指定された統計値を比較する値です。
  - しきい値となる値
  - このパラメータは、静的しきい値に基づくアラームには必要ですが、異常検知モデルに基づくアラームには使用しないでください。

- threshold_metric_id
  - (オプション) これが異常検知モデルに基づくアラームの場合、この値をANOMALY_DETECTION_BAND関数のIDと一致させます。

- actions_enabled
  - (オプション) アラームの状態が変化したときにアクションを実行するかどうかを示します。
  - デフォルトはtrueです。

- alarm_actions
  - (オプション) このアラームが他の状態からALARM状態に遷移したときに実行するアクションのリストです。
  - 各アクションは、Amazonリソース名(ARN)として指定されます。

- alarm_description
  - (オプション) アラームの説明です。

- datapoints_to_alarm
  - (オプション) アラームを作動させるために違反しなければならないデータポイントの数です。

- dimensions
  - (オプション) アラームの関連メトリックの寸法。
  - 利用可能な寸法のリストについては、こちらのAWSドキュメントを参照してください。
    - [AWS services that publish CloudWatch metrics \- Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/aws-services-cloudwatch-metrics.html)

- insufficient_data_actions
  - (オプション) このアラームが他の状態からINSUFFICIENT_DATA状態に遷移したときに実行するアクションのリストです。
  - 各アクションは、Amazon Resource Name (ARN)として指定されます。

- ok_actions
  - (オプション) このアラームが他の状態から OK 状態に遷移したときに実行するアクションのリスト。
  - 各アクションは、Amazon Resource Name (ARN)として指定されます。

- unit
  - (オプション) アラームの関連メトリックの単位。

    | 項目 | 設定値 |
    | :-- | :-- |
    | ％ | Percent |
    | 回 | Count |
    | 秒 | Seconds |
    | マイクロ秒 | Microseconds |
    | ミリ秒 | Milliseconds |
    | バイト | Bytes |
    | KB | Kilobytes |
    | MB | Megabytes |
    | GB | Gigabytes |
    | TB | Terabytes |
    | Bit | Bits |
    | Kbit | Kilobits |
    | Mbit | Megabits |
    | Gbit | Gigabits |
    | Tbit | Terabits |

- extended_statistic
  - (オプション) アラームに関連するメトリックのパーセンタイル統計です。p0.0 ～ p100 の間で指定します。

- treat_missing_data
  - (オプション) このアラームがデータポイントの欠落をどのように処理するかを設定します。
  - 欠損データの処理方法を設定します。
  - 次の値がサポートされています: missing、ignore、breaching、notBreaching。デフォルトは missing です。

    | 項目 | 設定値 |
    | :-- | :-- |
    | 適正(しきい値を超えていない) | notBreaching |
    | 不正(しきい値を超えている) | breaching |
    | 無視(アラート状態を維持する) | ignore |
    | 見つかりません | missing |

- evaluate_low_sample_count_percentiles
  - (オプション) パーセンタイルに基づくアラームにのみ使用されます。
  - ignore を指定すると、統計的に有意であるにはデータ ポイントが少なすぎる期間、アラームの状態は変更されません。
  - evaluate を指定するか、またはこのパラメータを省略した場合、利用可能なデータポイントの数に関わらず、アラームは常に評価され、状態が変化する可能性があります。
  - 次の値がサポートされています： ignore, および evaluate。

- metric_query
  - （オプション） メトリックの数式に基づいてアラームを作成できるようにします。
  - 最大で20個まで指定できます。

- tags
  - (オプション) リソースに割り当てるタグのマップです。
  - プロバイダのdefault_tags構成ブロックが存在するように構成されている場合、一致するキーを持つタグは、プロバイダレベルで定義されたものを上書きします。

- 注：
  - 少なくとも1つのmetric_queryを指定した場合、metric_name、namespace、period、statisticを指定することはできません。
  - metric_queryを指定しない場合は、これらをそれぞれ指定する必要があります
  - （ただし、statisticの代わりにextended_statisticを使用することができます）。

---

## EC2 の metric_name 一覧

- CPUUtilization
  - インスタンスに割り当てられたEC2コンピュートユニットのうち、現在使用されているものの割合。この指標は、選択したインスタンス上でアプリケーションを実行するために必要な処理能力を特定します。
  - インスタンスの種類によっては、インスタンスに完全なプロセッサコアが割り当てられていない場合、OSのツールがCloudWatchよりも低い割合を表示することがあります。
  - 単位は以下の通りです。パーセント

- DiskReadOps
  - 指定された期間に、インスタンスで利用可能なすべてのインスタンスストアボリュームから完了した読み取り操作。
  - 期間中の1秒あたりの平均I/O操作（IOPS）を計算するには、期間中の総操作数をその期間の秒数で割ります。
  - インスタンス・ストア・ボリュームがない場合は、値が0になるか、このメトリックは報告されません。
  - 単位 カウント

- DiskWriteOps
  - 指定された期間に、インスタンスで利用可能なすべてのインスタンスストアボリュームへの書き込み操作が完了したこと。
  - 期間中の1秒あたりの平均I/O操作（IOPS）を計算するには、期間中の総操作数をその期間の秒数で割ります。
  - インスタンス・ストア・ボリュームがない場合は、値が0になるか、このメトリックは報告されません。
  - 単位 カウント

- DiskReadBytes
  - インスタンスで利用可能なすべてのインスタンスストアボリュームからの読み取りバイト数。
  - この指標は、アプリケーションがインスタンスのハードディスクから読み込んだデータのボリュームを判断するために使用されます。これは、アプリケーションの速度を判断するために使用できます。
  - 報告される数値は、その期間に受信したバイト数です。基本的な（5分間）モニタリングを行っている場合は、この数値を300で割ってバイト/秒を求めることができます。詳細（1分）監視の場合は、60で割ってください。
  - インスタンス・ストア・ボリュームがない場合は、値が0になるか、メトリックが報告されません。
  - 単位は バイト数

- DiskWriteBytes
  - インスタンスで利用可能なすべてのインスタンスストアボリュームに書き込まれたバイト数。
  - この指標は、アプリケーションがインスタンスのハードディスクに書き込んだデータの量を判断するために使用されます。これは、アプリケーションの速度を判断するために使用できます。
  - 報告される数値は、その期間に受信したバイト数です。基本（5分）監視の場合は、この数値を300で割るとバイト/秒となります。詳細（1分）監視の場合は、60で割ってください。
  - インスタンス・ストア・ボリュームが存在しない場合、値はゼロになるか、メトリックは報告されません。
  - 単位はバイト

- MetadataNoToken
  - トークンを使用しない方法で、インスタンス・メタデータ・サービスへのアクセスに成功した回数です。
  - この指標は、トークンを使用しないInstance Metadata Service Version 1を使用してインスタンス・メタデータにアクセスしているプロセスがあるかどうかを判断するために使用されます。
  - すべてのリクエストがトークンを使用するセッション、つまりInstance Metadata Service Version 2を使用している場合、値は0になります。
  - 詳細については、Instance Metadata Service Version 2の使用への移行を参照してください。
  - 単位 カウント

- NetworkIn
  - インスタンスがすべてのネットワーク・インターフェイスで受信したバイト数。この指標は、単一のインスタンスへの受信ネットワークトラフィックの量を特定します。
  - 報告される数値は、その期間に受信したバイト数です。
  - 基本的な（5分）モニタリングを行っており、統計値が「Sum」の場合、この数値を300で割ると「Bytes/second」となります。詳細（1分）監視で、統計値が「Sum」の場合は、60で割ります。
  - 単位は バイト数

- NetworkOut
  - インスタンスがすべてのネットワーク・インターフェイスで送出したバイト数。この指標は、単一のインスタンスから発信されるネットワークトラフィックの量を特定します。
  - 報告される数値は、その期間に送信されたバイト数です。
  - 基本的な（5分）モニタリングを行っており、統計値が「Sum」の場合、この数値を300で割ると「Bytes/second」となります。詳細（1分）監視で、統計値が「Sum」の場合は、60で割ります。
  - 単位は バイト数

- NetworkPacketsIn
  - インスタンスがすべてのネットワーク・インターフェイスで受信したパケット数です。このメトリックは、単一のインスタンスのパケット数で受信トラフィックの量を識別します。
  - このメトリックは、基本的なモニタリング（5分単位）でのみ利用できます。5分間にインスタンスが受信したPPS（Packet per Second）の数を計算するには、Sum統計値を300で割ります。
  - 単位は カウント

- NetworkPacketsOut
  - インスタンスがすべてのネットワーク・インターフェイスで送出したパケット数。このメトリックは、単一のインスタンスのパケット数で発信トラフィックの量を識別します。
  - このメトリックは、基本的なモニタリング（5分単位）でのみ利用できます。5分間にインスタンスが受信したPPS（Packet per Second）の数を計算するには、Sum統計値を300で割ります。
  - 単位は カウント

- StatusCheckFailed
  - インスタンスが過去1分間にインスタンス・ステータス・チェックとシステム・ステータス・チェックの両方に合格したかどうかを報告します。
  - このメトリックは0（合格）または1（失敗）のいずれかです。
  - デフォルトでは、このメトリックは1分ごとの頻度で無料で利用できます。
  - 単位は 回数

- StatusCheckFailed_Instance
  - インスタンスが過去1分間にインスタンス・ステータス・チェックに合格したかどうかを報告します。
  - このメトリックは0（合格）または1（失敗）のいずれかです。
  - デフォルトでは、このメトリックは1分ごとの頻度で無料で利用できます。
  - 単位は カウント

- StatusCheckFailed_System
  - インスタンスが過去1分間にシステム・ステータス・チェックに合格したかどうかを報告します。
  - このメトリックは0（合格）または1（失敗）のいずれかです。
  - デフォルトでは、このメトリックは1分間の頻度で無料で利用できます。
  - 単位は カウント


---

## 元ネタ

- [aws\_cloudwatch\_metric\_alarm \| Resources \| hashicorp/aws \| Terraform Registry](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm)
- [AWS CloudWatch – アラーム設定 – IT Knowledge 109](https://www.itc109.com/knowledge/aws/aws-cloudwatch-alarm-setting)
- [List the available CloudWatch metrics for your instances \- Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html)

