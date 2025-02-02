---
title: "新人研修有志が初心者向けにバーチャルコンテストを実施しました & Tips"
date: 2020/07/15 10:51:27
postid: ""
tag:
  - 競技プログラミング
  - 新人研修
  - 社内勉強会
category:
  - Culture
thumbnail: /images/20200715/thumbnail.png
author: 佐藤尭彰
featured: false
lede: "皆さんは競技プログラミングをやったことはありますか？　聞いたことがあるけれど参加したことがない……そんな人も多いのではないでしょうか。そんな新人向けに向けて、新人研修で同期の運営チームメンバーとともにバーチャルコンテストを開催しました！　現在 6 回開催して、4 月入社の新人だけにとどまらず、キャリア入社の方や 7, 10 月入社予定の同期（現在アルバイト）まで参加しています。"
---

# はじめに

こんにちは。現在 SAIG に所属しております、2020 年 4 月入社新人の佐藤と申します。現在競技プログラミング部に所属しており、[HTTF 2019 2 位](https://atcoder.jp/contests/future-contest-2019-final/standings) の [omi](https://atcoder.jp/users/omi) とも申します。

皆さんは競技プログラミングをやったことはありますか？　聞いたことがあるけれど参加したことがない……そんな人も多いのではないでしょうか。

そんな新人向けに向けて、新人研修で同期の運営チームメンバーとともに**バーチャルコンテスト**を開催しました！　現在（2020/07/15時点） 6 回開催して、4 月入社の新人だけにとどまらず、キャリア入社の方や 7, 10 月入社予定の同期（現在アルバイト）まで参加しています。

詳しい経緯については未来報で仁木さんが [記事を書いています](https://note.future.co.jp/n/nda51c959f75a) ので割愛します。
本記事は自分たちで未経験者を巻き込んでバーチャルコンテストを開催しようと考えている人たちや、あるいはバーチャルコンテストに参加してみたいけどどんな活動をしているのか知りたいという人に向けた内容となっています。具体的には

- 使用しているツールと使い方の紹介
- コンテスト中の運営対応
- コンテスト後の解説について

となっています。読んでくれた方々の参考になったり、私達の活動を知ってもらえたら幸いです。

# AtCoder と AtCoder Problems

[AtCoder](https://atcoder.jp/home) は日本の競技プログラミング運営サイトです。ほぼ毎週末に開催される ABC(AtCoder Beginner Contest) をはじめとして、多種多様なコンテストが無料で受けられます。さらにオープンなコンテストの過去問は **すべて無償公開** されています。

[AtCoder Problems](https://kenkoooo.com/atcoder/#/table/) は AtCoder の過去問を集めて、ユーザごとの提出・解答状況の管理や難易度推定を行っているサードパーティーのサイトです。ここにバーチャルコンテスト開催機能があり、今回はこちらを利用しました。

バーチャルコンテスト参加にあたっては双方にアカウントを作成して AtCoder Problems 側での連携設定が必要となります。 AtCoder Problems は GitHub アカウント連携でしかアカウントを生成できず、GitHub アカウントがない人は GitHub アカウントの新規作成が必要になります。運営だけでなく、**参加者も全員必要なのでアカウントを作成してもらいましょう。**
双方にログインできたら、AtCoder Problems 側で Account → Account Info に AtCoder User ID を入力して Update すれば連携設定完了です。念のため、過去のコンテストから任意の過去問に提出してしばらく待ち、結果が反映されていることを確認すると完璧です。

# コンテストの作成

AtCoder 右上の Virtual Contest からコンテストを作成できます。

部外者が、乱立するバーチャルコンテストの中からわざわざ知らない名前を選んで入ってくることは滅多にないのですが、念のため Description に何か書いておくべきかもしれません。私は「身内用」などと記載しておくことにしました。

次に、その編集画面の下半分で問題を選んでいきます。留意すべきことは大きく 3 点あります。

- ターゲットを明確にすること。
  - 第3回 PAST 直前に PAST 過去問演習回を設定して、初心者からは大変不評だった
  - 初心者向けセットなのか、経験者向けセットなのかは事前に決定し、明確にアナウンスすべき
- difficulty に頼り過ぎないこと。
  - 特に ABC-B, C あたりは体感難易度のブレが大きく感じる
  - 純粋な知識問や [ABC169B](https://atcoder.jp/contests/abc169/tasks/abc169_b), [ABC169C](https://atcoder.jp/contests/abc169/tasks/abc169_c) のように言語仕様上の罠がある問題は不親切
    - 事前に解いてみて想定以上に難しくないかチェックしたほうがよい
- 初心者向けセットに水 diff (令和 ABC-E) 以上を出さないこと。
  - ABC-C あたりから手も足も出なくなる人が多いため、出すならやりたい人がやる枠として隔離しておく

最後にコンテスト時間を設定します。時間設定は問題数・難易度勾配よりも大切です。
長すぎると座っているだけの時間を作ってしまうことになるので、はじめのうちは長くても 1 時間に留めたほうが良いでしょう。我々は終業 30 分後から 50 分間のコンテストを設定しています。

# コンテスト実施

コンテスト自体は時間になったら自動的に開始するので、その間運営としてやるべきことは **質問対応** です。各種チャットツールは色々なアナウンスが行われると質問が流れていきやすく、どうしても見逃してしまいます。そこで解説用のGoogle Meetのビデオ会議を早めに準備しておき、困ったらそちらで口頭で質問してもらうようにしています。

質問は設問そのものに対してよりも、提出ができない、うまく動かないという大雑把な質問が飛んできがちです。適宜ヒアリングを行い、最終的には大体の勘で対応します。

実施してみて、事前にやっておいたほうが良かったことが 2 点あります。

- 入出力、提出のチュートリアルを事前に行うこと。
  - AtCoder 側での提出が出来ることを確かめてもらう
  - 当社新人研修では Java を用いていたため、新人向けに Java の入出力テンプレートを作成して事前に共有した
    - それでも言語選択欄を見逃して提出できない人が出たのでチュートリアルは必須
- コードテストの存在を周知すること。
  - 悪意のない提出デバッグをしてしまうことがある
  - `WA` はともかく `CE` はコードテストでサンプルを実行するだけでも回避可能
    - `RE` , `TLE` も ABC-A,B なら大体は回避可能

どうしても解決できない質問については、全員の提出から本人の提出コードをチェックして回答しても良いかもしれません。

# コンテスト終了後

ちゃんと解説をしましょう。その際に一度問題文を読み上げて問題設定を全員に伝えると、後ろの方の問題まで手がつけられなかった人にとって親切です。

運営側で画面共有をして、 `AC` できた参加者のコードを数人分映しながら各自のコードを解説してもらうと多くの人がコミットできます。どうしても書いてあることと言っていることが食い違うケースがありますので、経験者が質問したり指摘したりして認識を合わせると全員の成長につながると思います。

解説のメモとして Google Slides の空スライドを予め用意しておき、書ける人が協力して解説中に書きこんでいます。現在は参加者が 20 名程度なのでうまくいく手法ですが、50-60 名が一斉に開いて編集を試みるとスライドがとてつもなく重くなるため、人数が増えてきたら再考の余地があります。

<img src="/images/20200715/photo_20200715_01.png" loading="lazy">

# コンテストを実施してみて

参加した同期からは概ね良好なフィードバックを頂くことが出来ました！　新人の中にはコーディング未経験者も多い中で、入社後すぐに綺麗な、効率の良いコードを書くことはなかなか不可能です。それでも競技プログラミングの経験を通して「綺麗な、効率の良いコード」の威力、大切さを知ってもらうことが出来たと考えています。

具体的に同期の提出コードを見ていても、はじめ A 問題の $N= 10^9$ 制約に対して、全整数を for loop するコードを書いて `TLE` していた人が B, C 問題まで解けるようになるまで成長しています。毎回問題を選定していた側としても自分のことのように嬉しくなりました。

# おわりに

本企画は多くの運営によって支えられています。しかし運営全員が新人同期の有志であり、今もなお発展途上の企画です。是非参加したい！　という人は一緒にブラッシュアップしていきましょう。よろしくおねがいします。

当社では AtCoderJobs 経由で [競技プログラミング経験者の採用を行っています](https://jobs.atcoder.jp/offers/list?f.CompanyScreenName=future)。新卒・中途・アルバイトすべての求人がございますので、気になった方は一度ご覧になってください。

