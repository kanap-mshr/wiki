
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


## 元ネタ

- [aws\_cloudwatch\_metric\_alarm \| Resources \| hashicorp/aws \| Terraform Registry](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm)
- [AWS CloudWatch – アラーム設定 – IT Knowledge 109](https://www.itc109.com/knowledge/aws/aws-cloudwatch-alarm-setting)


