
# Amazon SNS

## 仕組み

![仕組み](https://www.unitrust.co.jp/wp/wp-content/uploads/2018/05/sns_diagram.png)

## 用語

- Amazon Resource Name（ARN）
  - AWSにおけるリソースのIDです。
  - このARNを参照し、配信対象や配信先の呼び出しを行ないます。
  - SNSにおいては、後述のエンドポイント、トピック、サブスクリプションにこのARNが割り当てられています。
    - 例）arn:aws:sns:us-east-1:123456789012:push_topicname
  - SNSに限らず、AWS全体で使われていますので、覚えておいて損はありません。
  - arn:aws:までは全サービス共通となっており、その後ろにサービス毎に異なる情報が付与されます。
  - 上記例の場合は【arn:aws:サービス:リージョン:アカウントID:トピックの名前】となっています。
  - 下記URLに詳細な説明と、各サービスにおけるARNの例が記載されていますのでこちらも一読してみてください。
    - https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws-arns-and-namespaces.html

- エンドポイント
  - 配信対象端末を識別するためのデータです。
  - 本記事の[1.]にて説明した「デバイストークン」より作成する、端末を識別するためのARNになります。
  - デバイストークンを登録するとこのエンドポイントが作成され、配信を行う際はこのエンドポイントを指定し、配信します。
  - わかりにくければ、メールアドレスのようなものだと考えていただいて構いません。

- アプリケーション
  - アプリごとの、プッシュ通知に利用するプラットフォームを設定しています。
  - iOSアプリなら「Apple Production」か「Apple Development」
  - Androidアプリなら「Google Cloud Messaging（GCM）」
  - をそれぞれ選択します。基本アプリごとに作成するものと思っていただいて問題ありません。
  - 前述のエンドポイントは、このアプリケーションに紐付く形で登録、管理されます。

- トピック
  - 配信対象をグルーピングし、配信対象に一斉に通知を配信するための機能です。
  - このトピックを作成し、エンドポイントを登録したあと、トピックに対し送信したいメッセージを発行すると、トピックに登録されているエンドポイントへ一斉に通知を配信することができます。
  - 個別のエンドポイントへ通知を配信するのは前述のアプリケーションでも行なうことができますが、配信の度に対象を選択するのは手間です。
  - その手間を解消するのがこのトピックです。

- サブスクリプション
  - Amazon SNS用語最大のハードルがこのサブスクリプションです。
  - サブスクリプションとは、作成したトピックと配信対象のエンドポイントを紐づけるデータです。
  - サブスクリプションによってトピックにエンドポイントが紐づけられていることで、トピックに対しメッセージを発行すると、そのトピックに紐づく配信対象のエンドポイントへとメッセージが配信されるようになっています。
  - サブスクリプションは日本語で「購読・予約購読」という意味です。
  - トピックに対しエンドポイントの紐づけを行うことで、「トピックに発行されたメッセージを購読できる」というイメージがあるとよりわかりやすくなるかもしれません。

- パブリッシュ（発行）
  - 通知を配信することです。
  - SNSにおいて通知の配信は、エンドポイントやトピックに対しメッセージを発行するという形をとっています。
  - メッセージの発行はアプリケーション画面、トピック画面より可能です。
  - 用語は以上になります。この6つの用語がわかればSNSの基本的なサービスの理解はできたも同然です。
  - これらを踏まえて、Amazon SNSのプッシュ通知の仕組みについて見てみましょう。

## 参考サイト

- [Amazon SNSを利用してモバイルプッシュ通知を送信するやり方ーコンソール利用 \- Qiita](https://qiita.com/Rei_2020/items/ab1768c1a0191b73492e#%E5%89%8D%E6%BA%96%E5%82%99)
- [Amazon SNSを利用してモバイルプッシュ通知を送信するやり方ー Node\.js \- Qiita](https://qiita.com/Rei_2020/items/fd8c679f697b0e0f5ca7)
- [Amazon SNSでプッシュ通知を送るための基礎知識 \| UNITRUST](https://www.unitrust.co.jp/6182)
- [\[AWS CloudFormation\] Amazon SNS プッシュ通知環境構築 \- Qiita](https://qiita.com/takmot/items/664b57e8be6a41b33ab9)
- [Amazon SNS Mobile Push を使ってみる](https://www.slideshare.net/shimy_net/amazon-sns-mobile-push)

