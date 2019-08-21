title: "Google Cloud Next '19 in Tokyo Day3 セッションレポート"
date: 2019/08/09 08:29:54
tags:
  - GCP
category:
  - Infrastructure
author: "DXチーム統合思念体"
featured: false
lede: "Google Cloud Next ’19 in Tokyo Day3にも少し顔を出していたのでそちらの参加レポートをお送りします。"
---

# はじめに
こんにちは、TIG DXチームの統合思念体です。[Google Cloud Next ’19 in Tokyo Day3](https://cloud.withgoogle.com/next/tokyo/)に少し顔を出していたので参加レポートをお送りします。

* [Day2 の参加レポート](https://future-architect.github.io/articles/20190804/)はこちらです。


# Google Cloud Next ’19 in Tokyoとは
「かつてないクラウドを体験しよう」をテーマに、📍東京プリンスホテル, 📍ザ・プリンス パークタワー東京の2ヶ所で 7/30~8/1の3日間に渡ってクラウドの最新動向や、採用事例を学べるセッションが開催されるカンファレンスです。ハッシュタグは`#GoogleNext2019`。2019年は160ものセッションが開催され年々熱気が増しているように感じます。


# 会場への道のり & 会場の様子
Day2に参加した私はすでに会場への道をマスターしており、道中で「これブログに使えるかな？」などと考えながら写真を撮る余裕がありました。
<img src="/images/20190809/photo_20190809_01.jpeg">
↑行きしなに東京タワーをパシャリ。変わらずの炎天下でしたが会場着後は快適な空調のおかげで穏やかな気持ちでセッション聴講できました！
<img src="/images/20190809/photo_20190809_02.jpeg">
↑こちらはEXPO会場のとある一角。バーコーナー的な感じでしょうか。写真ではお水のみですが、時間帯によってはお菓子も並んでいました。個人的には`揚一番`を陳列してくれていた点に全力で称賛を送りたいと思います!!（何個も食べてすいません...揚一番大好きです！！）



# セッションレポート
さて、本題に入っていきましょう。Day3もコンテナオーケストレーションネタを主軸にいくつかのセッションに参加したのでレポートを書いていきます！


## ☁ハイブリッド マルチクラウド環境下における Kubernetes デザインの勘所 - データ管理の視点から
>本セッションでは、なぜ Kubernetes クラスタがステートレスである必要があるか、アプリケーションから生成されるデータを保管する Kubernetes ストレージのデザインについて、ネットアップのソリューションを使用するとどのような課題を解決できるかをお話します。
>https://cloud.withgoogle.com/next/tokyo/sessions?session=327831-143299

k8s、ハイブリッド・マルチクラウド、という単語に惹かれる形で参加を決定しました。コンテナを使うときに悩みどころのひとつとなる「ステートフルデータの取り扱い方法」について詳しく解説してくれたセッションでした。本セッションはランチセッションだったみたいなのですが、知らずにギリギリで会場イン。係員の方に「お弁当はもう無いです。」と言われ、「ああーー勿体ないことしたぁぁーー」と思いながら着席しました笑

セッションを通じて、k8sひいてはコンテナアプリケーションを扱う際に必ずつきまとう「ステートフルデータどうする問題」に詳しくなりました！クラウドであれば、コンテナはステートレスな状態としステートフルなものはマネージドサービスをフル活用する、というのがコンテナアプリケーション運用時のベストプラクティスと考えていましたが、アプリケーションレベルでの管理に私の意識が寄っていた気がします。ハイブリッド・マルチクラウドが進む世界においては、etcd含め、クラスタレベルでのステートという考えも大事であり、「コンテナを破棄可能な状態に保つ」だけでなく「クラスタを破棄可能な状態に保つ」ことも重要だなと改めて考えさせられました！

以下セッションメモです。

### 複数のk8sクラスタを運用する際の課題 
* クラウドごと、あるいはオンプレでクラスタのオペレーションが微妙に異なる
* 複数クラスタをどうやって接続するか
* ステートフルなデータをどういったストレージで管理するか（本日のメイントピック）

### ハイブリッドクラウドの実現に向けて

#### オペレーションの統合
* 環境ごとにマネージド範囲が異なるので差異を吸収するレイヤが必要
* 統一的に操作できるAPIなどを定義した管理レイヤを設けるのが好ましい

#### k8sクラスタを破棄可能な状態にしておき、クラスタ移動に備える
* ワークロードにはステートフルとステートレスの2種類あるが、ステートフルワークロードの扱い方が重要
* ステートフルデータがあると、クラスタの移動が容易にできなくなってしまうため
* 保存の仕方は主に以下3種
  * マネージドのデータサービス
  * ユーザ管理データサービス
  * ブロック・ファイルストレージ

### コンテナにおけるステートとは？
システム稼働時に必要なデータあるいはコンテナ起動時に必要なデータがそれにあたる

#### k8sにおけるステート
* ステートフルなものは、Podのライフサイクルとは異なるライフサイクルのもので、`PVC`や`PV`など
* 現実的にマニフェスト化できないもの（コードで管理が難しいもの）はSecretなど
* ステートレスなものは、k8sのオブジェクトは基本ステートレス

#### k8sがステートを持たない利点
* ステートを持つ場合は、有事の際に直す必要がでてくる
  * アドホックだし時間がかかる
* ステートを持たなければ、再作成で復旧可能
  * 壊れても良い

### ではそのステートをどうやって管理するか？

#### データ永続化の領域
* マネージドデータサービスとユーザ管理データサービス
  * ベンダーロックイン的な話も出るが、大事なのはデータサービスの抽象化レイヤを配置し、入れ替え可能にしておくこと
* ブロック・ファイルストレージ
  * `Storage in k8s`と`Storage for k8s`。クラスタ上にデータを置くと、再作成など難しい

#### CSIとは(Container Storage Interface)？
* コンテナストレージの共通仕様
* APIは共通化されているため、バックエンドを置き換え可能になる
* ただし、CSI対応を謳っていても実装状況は違うので注意

### ステートフルなデータの取り扱い
Podが動いている間にうまれるデータ、およびetcdのデータがある

#### etcdを保護するために
* etcdは`クラスタのステート`と捉える場合と`クラスタのコンフィグレーション`と捉える場合でアプローチが異なる
* クラスタのステートとして考える場合
  * マネージドなクラスタの場合は、サービス提供側に任せるか、3rdパーティ製ツールを用いる
  * マネージドではないクラスタの場合は、自身で必ず保護し、バックアップのみならずそこからのリストアフローまでしっかり考えておく
* クラスタのコンフィグレーションとして考える場合
  * GitOpsのような状態が理想
  * 管理しているマニフェストを再実行で復旧状態にしておく
  * Secretをどのように考えるかが大事だが、例えばHashicorp Vaultを使うのは1つの解決策となりうる

### まとめ
* 微妙に違うk8sたちを統一的に管理することが必要
* 重要なのはクラスタを破棄可能にするためのステート管理方式の決定


## ☁Kubernetes ソフトウェア サプライチェーンにおけるエンドツーエンドのセキュリティ＆コンプライアンス
>このセッションでは、コンテナがもたらす課題とメリットについて、ANZ のメンバーも参加して意見を交わします。
>https://cloud.withgoogle.com/next/tokyo/sessions?session=302742-140857

k8sにおけるセキュリティに興味があり参加を決めました！スピーカーの方が英語で話されるとのことで入り口では通訳レシーバーが配布されていましたが、良い機会だと思い私はレシーバーを受け取らずにセッション会場へ突入していきました。(わりとなんとかなります。みなさんもぜひチャレンジを！)

ANZ(オーストラリア・ニュージーランド銀行)さんの事例に合わせ、いかにセキュリティを高めるかがテーマのセッションでした。コンテナセキュリティという観点で登場したサービス・ソリューション群はDay2で聞いたものと一緒でしたが、その分洗練されたセキュリティサービスが提供されていると理解しました。緻密なセキュリティ対策が求められる銀行ビジネスの中で、セキュリティを高めつつクラウド・コンテナアプリケーションを導入していくかという話が興味深く、技術ネタそのものよりもそちらに耳を傾けてしまいました。

講演中に手元の端末を使ってDEMOを行う際は、スイッチャーの方に「画面切り替えお願いします」といった形でお願いするのですが、うまく切り替わった後に講演者の方がスマートに発した「Perfect」の一言が最高にCoolでかっこいいなとテンション上がってました！笑

以下、セッションメモです。

### Supply Chain Security
* VM時代のサプライチェーンはToo Human Baseでした
* マイクロサービスであるということは大量のデプロイを何度も行うということである
* 人力ではとても回らないので、CI/CDを適切に整えることが大切

### ANZにおける事例
* ANZ = オーストラリア・ニュージーランド銀行
  * 50thousand employees
  * 10million customers
* New ways of workingを考えている
* Fintechの流れもあり、techにも力を入れている
  * Quick change & Quick feedback
* 素晴らしいエクスペリエンスは顧客の信頼の中で生まれる
  * 「Security is key to gain customers trust.」

### まとめ
* Base image、Image scan、Binary AuthorizationなどのGCPセキュリティサービスを活用してコンテナアプリをセキュアに保つことが大事

## ☁Anthos が変えるハイブリッドクラウドの形
>本セッションでは、Anthos が何を目指しているのか、何が実現できるのかというようなコンセプトから、Kubernetes、Istio などのコンポーネントに触れながら、これを利用することで何が変わるのか、技術者、ビジネス担当者それぞれの立場から見たメリットを合わせ、ご説明します。
>https://cloud.withgoogle.com/next/tokyo/sessions?session=297710-140796

話題のAnthosのセッションなのでぜひ聞きたいと真っ先に参加申し込みをしたのがこのセッションです！やる気出しすぎて最前ど真ん中というベスポジ中のベスポジをゲットしつつ臨みました。

Anthosの具体的なアーキテクチャについての話というよりも、Anthosがどこに向かっているのかを聞けるセッションでした。本セッションで話していたことは、Anthosに閉じず、GCPがどこに向かおうとしているのか、も多分に含んでいるんだろうなーと感じています。OSSに対する強い思いも随所にあふれており、私の大好きなIstioの話も登場し、Google Cloud ソリューションアーキテクト長谷部さんの熱意あふれる大満足な40分間でした！

以下、セッションメモです。

### 日本のエンタープライズITは変革が求められている
* 開発手法・スキル・リソース配分・市場など様々な観点で変化があり、それに追従するためにも変革が求められている
* その一つの解がAnthosであり、本セッションでは技術よりも、Anthosが向かう先を話す

### Anthosが目指すもの

#### ハイブリッド＆マルチクラウド
* 既存リソースの有効活用
  * すべてクラウドに移行しているのは稀。最近の調査では、クラウドからオンプレに戻そうとする動きもある
* レギュレーション・社内ポリシーの対応
  * クラウドに置けないデータはオンプレにおくしかない
* マルチクラウド
  * 他社クラウドもサポート

#### フルマネージド指向
* デファクトとなりつつある3つのOSS、それらをマネージドサービスで提供する
  * k8s --> GKE
  * Istio --> Istio on GKE
  * Knative --> Cloud Run
* 価値のある業務に集中する。プラットフォーム管理はGoogleが、開発者は価値のあるところにフォーカスしてほしい
* マネージドサービスの提供領域についてはGoogleがテスト、監査を行う
* あくまで元々のOSSに準拠し、魔改造はしない

#### オープンテクノロジー with Google
* Goolgeはk8s・Knative・Istio・Tensorflowをはじめ2000を超えるOSSプロジェクトへ貢献してきた
* 昨今のクラウドベンダーとOSSベンダーとの衝突は悲しいものであり、GoogleはOSSを育ててきた企業だからこそ、OSS企業を大事にしたい
* OSS各社と戦略的パートナーシップを結んだ

#### Anthosが支えたい世界
CEOの方々と話す機会があるが、「3年後のIT投資戦略をたてなきゃいけないがそれは可能か？」とよく聞かれる。変化が早く、見通せないのは前提。であれば、変化したらそれに柔軟に合わせられる状態になるような選択をするのが大事。しかし保守的すぎてもだめで、競争力をつけるためにk8sやIstioなどの最新のテクノロジーは使える状態であるべき。それらをマネージドサービスにて利用することで開発者は価値のある箇所に注力することができる。

### Anthosの構成要素
* Anthosはコンテナを基礎としている
* コンテナの特徴は3点
  * 「ファイルサイズが小さい」・「アプリに必要なものがひとまとめ」・「(仮想マシンに比べ）負荷が低い」

#### なぜGoogleがコンテナを使うのか？
* 開発速度をあげて、早くリリースしたい
* サーバリソースを有効活用したい
* 開発者は開発に集中したい

#### コンテナオーケストレーションの重要性
* どのサーバ上につくる？ = スケジューリング
* サーバが落ちたらどうする？ = セルフヒーリング
* 負荷が高くなったらどうする？ = オートスケーリング

#### Anthosのテクノロジースタック
<img src="/images/20190809/photo_20190809_03.jpeg">

* ベースにGKEとIstioがいて、その上にControl Planeがある

### Anthosのもたらす価値・提供機能
<img src="/images/20190809/photo_20190809_04.jpeg">

##### コンテナオーケストレーション - GKE/GKE On-prem
* k8sは宣言型APIで設定する
* 宣言型API = あるべき状態を記述する。手順ではなく、最後の状態を定義する
* k8sは宣言された状態をkeepするように動く

#### サービスメッシュ(の前に...)
なぜマイクロサービス？

* 1つ1つのサービスが小さくシンプル
* 機動的な機能追加
* 個別集中的なセキュリティ
* 個別のテクノロジー採用」

しかし...連携が増え管理が大変

* どのように連携するか？
* どのサービスがどのサービスと連携しているのか？
* サービス間のセキュリティ、認証認可の担保は？


#### サービスメッシュ - Istio on GKE/CSM
* Istioという解決策。間に入り、サービス間の連携を取り持つ
  * つなげる、セキュアに保つ、見える化する

#### 設定、ポリシーの一元管理 - Anthos Config Management
* マルチ、ハイブリッドクラスタの一元管理
* 宣言型モデルと継続的なモニタリング
* シンプルなマイグレーション

#### コンテナへのマイグレーション - Migrate for Anthos
* 仮想マシンで動いているものを簡単にコンテナ化できる

### ユースケース
#### Anthos on Edges
* エッジロケーション(工場など)にAnthosを導入し、集中管理を行う
* GKE On-premはインターネットへの疎通ができれば導入可能

#### Anthos for Hybrid Cloud
* クラウドにおけないものはOn-prem、おけるものはクラウドに

#### Anthos for Multi Cloud
* 複数のクラウドを組み合わせたサービス構成
* 複数クラウドでDRを組むなども可能になる

### まとめ
<img src="/images/20190809/photo_20190809_05.jpeg">

* 2019/09/03にGoogle Cloud Kubernetes Dayやります(私も楽しみです！)


## ☁Istio, Kubernetes, Spinnaker を使ったカナリア デプロイメント
>Istio, Kubernetes, Spinnaker を使うことで、カナリアデプロイメントなど高度なロールアウトパターンをサポートし、アプリケーションを安全かつ簡単にデプロイすることが可能です。本セッションではこれらを如何に GCP 上で実現するか、最新のプロダクト情報も交えながら説明します。
>https://cloud.withgoogle.com/next/tokyo/sessions?session=299647-140817

Istioが好きで最近仕事でCI/CDを設計している私にとってまたとない機会だったので、意気揚々と参加登録しました。本セッションもスピーカーの方が英語ネイティブな方だったのですが、2つ前のセッションを通訳レシーバーなしで過ごした私は、これまた意気揚々と「レシーバー要らないです」と言いながら会場へ足を踏み入れました。

k8sとIstioを使っていかにカナリアデプロイを実現するか、デモを交えて詳しく説明してくれるセッションでした。講演者の方の朗らかな人柄もあいまって、幸せな笑いに満ちたセッションだなーと思いつつ聴講していました！ちなみにセッションタイトルには「Spinnaker」とありますが、本セッションでは代わりに「TEKTON」を利用したカナリアデプロイメントの説明をしてくださっています。「Spinnaker」を利用したのはGoogle Cloud Next '19 in San Franciscoだったようです。(セッションの模様はYouTubeで見られるとのこと！)

[Canary Deployments With Istio and Kubernetes Using Spinnaker (Cloud Next '19)](https://youtu.be/CmZWau04ZS4)

デモアプリで登場した猫のアプリがとても印象的でした！猫！かわいい！！

以下、セッションのメモです。

### k8sにおけるコンテナデプロイ
* 課題は、どうやって安全かつ簡単にコンテナアプリケーションのバージョンを切り替えるか
* ケースとして、アプリバージョンをOldからNewへ切り替えたい時
* k8sではすでに下記に対応可能
  * Rollingアップデート
  * Blue/Greenデプロイ
  * オーバープロビジョニング

### カナリアデプロイメント
徐々に新しいバージョンにアプリケーションを切り替えていく。

* k8sでやるには、Deployment objectを利用する
* よりアドバンスにやるには、Istioを利用してTrafficの分配を行う
  * `Destination Rule`と`Virtual Service`の設定によって実現可能


### TEKTONについて
* カナリアデプロイメントに際し、フェーズごとに設定変更しなければならない箇所がたくさんある
* でも手で全部やるのは大変！！→自動化しよう！！
* TEKTONはIstioを利用してカナリアデプロイメントを自動化してくれるツール
* TEKTONはk8sのCRD(Custom Resource Definition)をラップしており、PipelineとTasksを定義することで動作する​​

### まとめ
* k8sを利用したカナリアデプロイメントにはIstioは絡めてTrafficコントロールを任せよう
* TEKTONやSpinnakerを使って自動化することはとても重要
* Spinnakerを使ったDEMOを行った[サンフランシスコでのセッション動画](https://youtu.be/CmZWau04ZS4)をぜひみてください！

# 最後に
[Day2のレポート](https://future-architect.github.io/articles/20190804/)でも書きましたが、Anthos含めKubernetesに関連するセッションが非常に充実していました。AnthosのセッションはまさにGoogle Cloudがどこに向かっていくかをありのまま伝えてくれたように思います。

Anthosのセッションを担当されていた長谷部さんが「実はGoogleは数年前からコンテナを使っているが、昨今いろいろな所でコンテナという言葉を耳にする。コンテナ技術は今流行っていると言える。」と発言されていました。Kubernetes・Istio・Knativeなどをはじめ、いまデファクトスタンダードになりつつある様々なOSSは例えばBorgなど元々Googleの社内システムにて利用されていたシステムが起源となっています。彼らは数年かけてブラッシュアップさせてきたものをOSSとして公開し、そしてそれを今GCPにてマネージドサービスとして提供しています。

変化の早いテクノロジーの世界において、知見は隠すものではなく皆で共有し・皆で育てていくものとなってきています。GCPを活用するということは言い換えればGoogleが長年培ってきた知見の集大成を一気に享受できるということであり、そのメリットは計り知れないはずです。我々も受け取るだけでなく広く世に発信し続けなければならないなと改めて考えさせられる良い機会にもなりました。

Day2・Day3の2日間だけの参加でしたが、非常に有意義な時間を過ごすことができました！GCPについての学びを惜しみなく発信する機運がマックスに高まってますので本ブログにも引き続きご注目ください！

我ら統合思念体の起源であるDXユニットに興味を持っていただけたら、 [Qiita Jobs](https://jobs.qiita.com/employers/future/development_teams/109)や[このあたりの職種](https://progres12.jposting.net/pgfuture/u/job.phtml?job_code=344) もぜひご覧いただけると幸いです。
