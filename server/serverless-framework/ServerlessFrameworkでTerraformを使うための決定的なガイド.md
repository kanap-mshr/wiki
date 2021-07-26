
# The definitive guide to using Terraform with the Serverless Framework (DeepL翻訳)

クラウドインフラの管理に自動化を使用している組織であれば、Terraformについて聞いたことがあるはずです。そして、もしあなたが何かサーバーレスなものを作ったことがあれば、Serverless FrameworkでデプロイすることがTerraformを実行することとよく似ていることに気付いたかもしれません。

その通りだと思います。Serverlessを使っている企業の多くは、すでにTerraformを使っていますし、Serverless Frameworkの機能の中には、特にクラウドリソースのプロビジョニングに関して、Terraformでできることと似ているものがあります。

では、TerraformとServerlessの両方でインフラ自動化のニーズを解決できる場合、どちらを使うべきでしょうか？また、すべての目的のために1つだけを使うべきでしょうか？

私たちはその答えを持っています。

この記事では、TerraformとServerlessの両方を使用する場合のインフラ管理の正しい方法について説明し、TerraformとServerlessをプロジェクトに統合する実例を確認します。

## インフラ管理を自動化する理由

IaC（Infrastructure as Code）は、開発者が増大するクラウドインフラを整理し、チーム間でコラボレーションする方法を必要とする場合に、非常に重要になります。

最も重要なことは、IaCツールによってプロセスと規律が必要になり、偶発的または予期せぬ変更の可能性が減り、インフラの異なる部分間で構成を共有することが容易になることです。

## 共有インフラとアプリケーション固有のインフラの管理

すべてのインフラをIaCオートメーションで管理すべきだと考えていますが、1つのアプリケーションに特化したインフラと、スタック内の複数のアプリケーションで共有されているインフラを区別したいと考えています。これらはそれぞれ異なる方法で管理する必要があります。

アプリケーション固有のインフラは、アプリケーションのデプロイ時に作成され、削除されます。アプリケーション固有のインフラストラクチャの一部を変更することはほとんどありません。アプリが開発されると、それをサポートするインフラも変更する必要があり、時にはデプロイのたびに大幅に変更されることもあります。

一方、共有インフラは、ゼロから作り直すことはほとんどなく、よりステートフルなものです。コアとなるインフラ（セキュリティグループやVPC IDなど）は、スタック内の多くのアプリケーションから参照されているため、アプリケーションのデプロイの間で変更されることはありません。このような永続的なインフラは、通常、デプロイパイプラインの外部で管理されます。

このように、アプリケーション固有のインフラと共有インフラは、それぞれ別のツールで管理する必要があります。

## Serverless vs Terraform：いつどちらを使うか

TerraformとServerlessの両方を使用している組織のために、それぞれの利点と、どのような場合にどちらを選択すべきかを説明します。

アプリケーションに特化したインフラにはサーバーレス
アプリケーション固有のインフラについては、いくつかの理由から、Serverless Frameworkですべてのピースを管理することをお勧めします。

まず、このインフラをアプリケーション自体に結合することができます。第二に、Postgresデータベースのテーブルのように、アプリケーションが物事を「所有」していると考えたいのです。アプリケーションのコンテキストの外（例えばTerraform）でテーブル名を管理する価値はほとんどありません。

3つ目は、共有インフラに触れることなく、アプリケーションのリリースを繰り返すことができることです。ソフトウェアリリースは共有インフラから切り離されているため、インフラの変更を気にすることなく、アプリケーション自体に集中することができます。

共有インフラのためのTerraform
しかし、共有インフラを特定のアプリケーションに結びつけることは正しくありません。共有インフラは通常、ゼロから再作成されるのではなく、更新されます。

このため、Terraformは共有インフラの管理に適しています。Terraformは永続的なクラウドインフラの中央情報源となり、既存のインフラの更新をうまく管理できます。

## 例えば

共有データベースがあり、そこにテーブルを作成する2つのServerlessアプリケーションがある場合、データベースはTerraformで管理する必要があります。特定のテーブルは、アプリのデプロイとティアダウンのプロセス中に、Serverless Frameworkによって作成および破棄されるべきです。

## どこで線を引くか

データベースとそのテーブルがあれば、アプリ固有のインフラと共有インフラの区別は明確です。

しかし、データベース全体が1つのアプリでしか使用されない場合はどうなるでしょうか？キューやキューのサブスクリプションはどうでしょうか。2つのServerlessマイクロサービスの間に契約があり、それらがインターフェースとしてキューを使用している場合はどうでしょうか？

これらの項目はすべて、アプリ固有のものと共有のものとの間のどこかに該当します。

このようなケースでは、どちらの選択肢でも構わないと考えています。それよりも、インフラ全体で一貫した判断をすることで混乱を避けることが重要です。

## SSMでTerraformとServerlessの間でデータを共有する

TerraformとServerlessを使ってインフラの異なる部分を管理している場合、最終的にはTerraformとServerlessのプロジェクト間でデータを共有する必要があります。VPC ID、セキュリティグループID、RDSインスタンスのデータベース名など、Terraformで作成され、Serverlessで消費されるすべてのものを考えてみましょう。

SSMパラメータストアは、2つのシステム間で値を共有するのに最適な方法です。TerraformにはSSMパラメータリソースが用意されており、これを使って任意のSSMキーを書き込むことができます。そして、それらのキーをserverless.ymlの中で${ssm:...}の参照を介して消費することができます。

## TerraformとServerlessでSSMを使う例

SSMによるパラメータの受け渡しを説明するために、例を作ってみました!

インフラはTerraformで管理しており、Terraformの操作結果を使ってデータベースに接続するServerlessアプリがあります。アプリケーションはそのデータベース接続を利用して、データベースのテーブルを作成したり、アプリケーション自体の動作に必要なものを作成したりします。

それでは、TerraformとServerlessの両方の設定ファイルを見ながら、簡単なプロジェクトでどのように見えるかを見ていきましょう。

### テラフォーム

Terraformプロジェクトでは、必要なリソースを作成します。ここではMySQL RDSインスタンスを作成します。

```
# main.tf
provider "aws" {
  region = "us-east-1"
}

resource "aws_db_instance" "default" {
  name                   = "${var.name}"
  username               = "${var.user}"
  password               = "${random_string.password.result}"
  parameter_group_name   = "default.mysql5.7"
  # a few more options go here…
}
```
ここでは、aws_db_instance データソースを使用しています（詳細なドキュメントはこちらをご覧ください）。データベース名を直接指定するのではなく、nameとuserという変数を参照し、パスワードとなるランダムな文字列を生成しています。

そして、nameとuserの内容を含むvariables.tfファイルを作成し、ランダムな文字列にいくつかのパラメータを設定します。

```
# variables.tf
variable "name" {
  default = "testdb"
}
variable "user" {
  default = "serverless"
}

resource "random_string" "password" {
  length  = 16
  special = false
}
```


さて、サーバーレスアプリケーションにDB接続文字列の詳細を取得させたい場合は、SSMパラメータストアにDB名とパスワードを暗号化された文字列として保存する必要があります。それには、aws_ssm_parameterリソースを以下のように使用します。

```
# parameters.tf
resource "aws_ssm_parameter" "endpoint" {
  name        = "/database/${var.name}/endpoint"
  description = "Endpoint to connect to the ${var.name} database"
  type        = "SecureString"
  value       = "${aws_db_instance.default.address}"
}
...
```
terraform applyを実行すると、以下のようになります。

var.name}は、variables.tfで定義した名前の値に置き換えられます。 main.tfで指定したデータベースが作成されると、${aws_db_instance.default.address}の値がデータベースインスタンスのIPアドレスに置き換えられます。 SSMパラメータは、/database/tdb/endpointという名前で作成され、データベースインスタンスのIPアドレスが含まれています。 Terraformの設定では、データベースのエンドポイントだけでなく、データベースのユーザー、パスワード、アクセスするデータベースの名前も保存されます。

### サーバーレス

Serverlessの設定ファイルでは、Terraformで管理しているデータベースに接続するための関数を定義します。

関数の定義では、すべてのデータベース接続パラメータを含む環境変数を作成します。各変数では、SSMパラメータを参照します（この点については、こちらのドキュメントを参照してください）。

なお、上記のTerraformファイルではSSMへのパラメータをSecureStringsとして保存しているため、serverless.yml内でこれらの値を取得するには、特別な~true構文を使用する必要があります。

```
# serverless.yml
service: terraform-serverless-integration

provider:
  name: aws
  runtime: nodejs8.10

functions:
  rdsConnector:
    handler: handler.handle
    environment:
      DATABASE_ENDPOINT: ${ssm:/database/testdb/endpoint~true}
      DATABASE_NAME: ${ssm:/database/testdb/name~true}
      DATABASE_USER: ${ssm:/database/testdb/user~true}
      DATABASE_PASSWORD: ${ssm:/database/testdb/password~true}
    events:
      - http:
          method: GET
          path: /
```
環境セクションで指定した変数には、デプロイメントプロセス中にSSMから正しい値が入力され、これらの値は関数の実行環境で利用可能になります。

Serverless関数の本体では、これらの値を使ってMySQLの接続を設定することができます。

```
# handler.js

const mysql = require("serverless-mysql")({
  config: {
    host: process.env.DATABASE_ENDPOINT,
    database: process.env.DATABASE_NAME,
    user: process.env.DATABASE_USER,
    password: process.env.DATABASE_PASSWORD
  }
});
...
```

これで、Terraformで管理されているMySQLデータベースに、サーバーレスアプリケーションでアクセスできるようになりました!

## データベース接続データの変更

Terraformでデータベースの設定を変更する必要がある場合、terraformの実行時にSSMのパラメータを適用すると、サーバーレスアプリの参照先が更新されます。しかし、実行中のアプリでこれらを更新するには、サーバーレスアプリを再デプロイする必要があります。

## SSMの限界

SSMは、ServerlessプロジェクトでTerraformからパラメータを参照するための便利な方法を提供します。しかし、注意しなければならないのは、SSMはAmazon Web Servicesでしか利用できないということです。

また、SSMからの値がビルドログやCloudFormationのテンプレートに入ってしまう可能性があるため、最も安全なソリューションとは言えません。(このドキュメントセクションの免責事項を参照）。)

これらの制限にもかかわらず、SSMを使用してTerraformからServerlessにデータを渡すというオプションは、共有およびアプリ固有のインフラを管理するほとんどのケースで機能します。


## 結論

Terraformはより永続的な共有インフラを管理するのに適しており、Serverlessはアプリケーション固有のインフラを管理するのに適しています。

TerraformとServerlessの間で情報を共有する例は上記を確認してください。また、完全な例はこちらのGitHub repoにあります。

あなたは現在、TerraformとServerlessを併用していますか？あなたのアプローチを以下のコメント欄またはフォーラムで共有してください。


## 元ネタ

- [The definitive guide to using Terraform with the Serverless Framework](https://www.serverless.com/blog/definitive-guide-terraform-serverless)
