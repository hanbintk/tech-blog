---
title: "Engineer Camp 2021（IoTプラットフォーム）に参加しました！"
date: 2021/09/22 00:00:00
postid: a
tag:
  - インターン
  - インターン2021
  - IoTプラットフォーム
category:
  - Culture
thumbnail: /images/20210922a/thumbnail.png
author: 山本雄樹
featured: false
lede: "こんにちは。2021年のフューチャーのサマーインターン「Engineer Camp」に参加いたしました、山本雄樹です。インターンの振り返りも兼ねて、このブログを読んだ方にインターンの内容や雰囲気を伝えられたらと考えています。インターン参加前のスキルセットとしては以下の通りです。バックエンドの技術を中心に学習していたのですが、めぼしい成果物などもなく、実務経験が一切ありませんでした。"
---
# 始めに
こんにちは。2021年のフューチャーのサマーインターン「[Engineer Camp](https://note.com/future_event/n/n76e7e7d4beef)」に参加いたしました、山本雄樹です。

インターンの振り返りも兼ねて、このブログを読んだ方にインターンの内容や雰囲気を伝えられたらと考えています。

<img src="/images/20210922a/profile.jpeg" alt="profile.jpeg" width="460" height="460" loading="lazy">

# インターン参加前
インターン参加前のスキルセットとしては以下の通りです。バックエンドの技術を中心に学習していたのですが、めぼしい成果物などもなく、実務経験が一切ありませんでした。

- Go言語やGitを日常的に使用している
- Linuxの簡単なコマンドであれば知っている
- GCPとDockerを使用したことがある

そのため、Go言語を使用した実務経験を積めるようなインターン先を探していました。

# 参加したコース
私が参加した2021年のフューチャーのインターンではコースが合計11コースあり、その中から私は③の「[大規模IoTプラットフォームのバックエンド開発](https://note.com/future_event/n/n76e7e7d4beef#bJRgs)」を選んで応募しました。Go言語を使用する開発の中で、一番自分の技術スタックとあっているものを選びました。

実際の業務では以下の技術を使用しました。

- 言語: Go言語
- インフラ系: Terraform, AWS
- エディタ: GoLand, VSCode
- その他: Git, Docker, Google Chat API

# インターン内容
インターンには週5日、四週間参加しました。

稼働時間は10:00~19:00で、始めの時間を早める場合は終わりの時間を早めます。昼休憩の１時間とインターン生の集まり、インターン生用講義、採用チームとの面談（週一、各30分）以外は全てお仕事の時間です。受け入れ先プロジェクトの方からタスクをもらって、調べたり質問したりしながらタスクを進め、終わったら新しいタスクをもらう、というサイクルを回していました。

## インターンの雰囲気
### インターン生同士の関わり

週に一度、インターン生の集まりがあり、そこでお互いが行っているタスクの内容を話したります。お互い異なるコースに参加しているため聞ける話もバラバラで面白いです。

話し足りなかったという方もいらっしゃるかと思いますが、個人的にはその分タスクに集中できたので良かったかなと考えています。


### 社員の方との関わり

受け入れ先のプロジェクトの方がインターン生の面倒を見てくれます。基本的には一人でタスクを進めていくのですが、行き詰まった際にはSlackで質問します。困っているときには声を上げることが大切です。

また、技術ブログを執筆した際にはたくさんのレビューをいただきました。

<img src="/images/20210922a/スクリーンショット_2021-09-17_13.40.38.png" alt="スクリーンショット_2021-09-17_13.40.38.png" width="918" height="444" loading="lazy">


## インターンでの成果
### 技術力の向上

Go言語やGitは日常的に使用しておりキャッチアップの必要性がなかった分、インターン期間中は以下のようなAWSやTerraformといったインフラ寄りの技術について多く触れることができ、バックエンドエンジニアとして扱うことのできる技術領域を広げることができました。

<img src="/images/20210922a/スクリーンショット_2021-09-16_18.56.07.png" alt="スクリーンショット_2021-09-16_18.56.07.png" width="1200" height="563" loading="lazy">

### 「IoTデバイスのエラー通知を集計して日毎に通知するシステム」の実装
期間中にこなしたタスクの中で一番粒度の大きかったものが**「IoTデバイスのエラー通知を集計して日毎に通知するシステム」**の実装です。

AWS LambdaではGo言語を使用して以下の処理を実装しました。

- DynamoDBから昨日のデータを取得する
- 取得したデータを集計する
- Amazon KMSで暗号化されたGoogle Chatの送信先URLを復号する
- Google Chat APIで指定されたJSON形式にして送信する

<img src="/images/20210922a/スクリーンショット_2021-09-16_14.39.51.png" alt="スクリーンショット_2021-09-16_14.39.51.png" width="1017" height="485" loading="lazy">

実装はアサインしたプロジェクトのコーディング規則やコードを参照しながら進めました。行き詰まった際にはメンターの方に質問をすることができますし、実務レベルのコードレビューをしていただけます。おかげさまでインターンを通して、実務レベルのGo言語のコーディング能力と自信をつけることができたと考えています。

### Future Tech Blogへの投稿
フューチャーは学びや経験をブログ化する文化が強く、私もその文化に乗じてインターン期間中にブログを２本投稿いたしました。[こちらの記事にもあるとおり](/articles/20200530/#%E3%82%A2%E3%83%AB%E3%83%90%E3%82%A4%E3%83%88er%E3%82%84%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%B3%E7%94%9F%E3%81%AB%E5%B0%B1%E8%81%B7%E6%B4%BB%E5%8B%95%E3%83%8D%E3%82%BF%E3%81%A8%E3%81%97%E3%81%A6%E6%9B%B8%E3%81%84%E3%81%A6%E3%82%82%E3%82%89%E3%81%86)、フューチャーではブログの執筆が歓迎されます。書きたい欲があるのであればメンターの方にチラッと伺ってみると良いと思います。きっと背中を押してくれます。
<img src="/images/20210922a/スクリーンショット_2021-09-17_11.32.42.png" alt="スクリーンショット_2021-09-17_11.32.42.png" width="789" height="492" loading="lazy">

投稿記事:
* [GoLand Tips 7選](/articles/20210902b/)
* [【Google Chat API】Incoming Webhook を Go で触ってみる](/articles/20210913a/)

## インターンでの学び
### リモート環境でのコミューニケーション

リモートでは自分が何をしていて、どんなことを考えているかが相手に伝わりにくいです。そのため常に自分が何をしていて、どんなことを考えているかを文字としてSlackの個人用スレッドにぶら下げていました。そうすることで自分の作業内容を相手が理解、管理しやすくなります。

### 質問のテクニック

私はインターンの始めは、問題について15分は必ず考え、解決の糸口が見つからなそうな場合は質問するようにしていました。しかし実際には質問がまとまっていなかったり、どのように質問するか整理して考えている間に解決したりと、うまくいかない場面が何度かありました。これらは自分で解決ができないと分かったタイミングですぐに質問をしているために起こっており、質問をする前に自分の中で一旦整理する時間が必要だと反省しました。

今後は以下のような手順で質問することを心がけたいと考えています。

- 問題について15分考える
- 解決できない場合はさらに15分かけて問題を整理し、相手にうまく伝える準備をする
- 問題を文字に起こして質問する

### ブログ化のメリット
インターン参加前はFuture Tech Blogについて、採用活動の一環として行っているのかな程度に思っていたのですが（実際私はフューチャーを認知したのはFuture Tech Blogがきっかけでした）、社内での使われ方を見てブログ化することのメリットを感じました。

以下は成果発表会で使用したスライドです。

<img src="/images/20210922a/スクリーンショット_2021-09-17_13.12.41.png" alt="スクリーンショット_2021-09-17_13.12.41.png" width="1194" height="684" loading="lazy">

# まとめ
フューチャーのインターンに参加したことにより以下のような経験を積むことができました。

- 実務でのGoの開発経験を得ることができた
- AWSを中心とした現場で使われているインフラに関しての知識を得ることができた
- リモートワークの雰囲気を知れた
- フューチャーのブログ文化に触れることができた

インターンを通して社員の方と同じように扱っていただきながらも、インターン生としてしっかりと面倒を見ていただきました。おかげさまで実際の仕事の雰囲気を感じながら、楽しく４週間を過ごすことができました。

インターンの企画をしてくださった採用の方々、面倒を見ていただいた受け入れ先プロジェクトの皆様、ありがとうございました！
<img src="/images/20210922a/集合写真.png" alt="集合写真.png" width="1200" height="620" loading="lazy">
