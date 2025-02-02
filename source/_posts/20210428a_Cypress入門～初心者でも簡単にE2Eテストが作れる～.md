---
title: "Cypress入門～初心者でも簡単にE2Eテストが作れる～"
date: 2021/04/28 00:00:01
postid: a
tag:
  - JavaScript
  - Cypress
  - TechNight
  - 登壇レポート
  - E2Eテスト
category:
  - Infrastructure
thumbnail: /images/20210428a/thumbnail.png
author: 木戸俊輔
featured: false
lede: "皆さんは普段どのようにE2Eテストを行っていますか？忍耐強く手動でポチポチ画面を触って...というのはなかなかにしんどいですよね。自動化ツールを使って楽したいけど難しくてよくわからない、という方もいらっしゃると思います。本記事では、テスト自動化ツールを全く使ったことのなかった私が、テスト自動化ツールである[Cypress]の導入から基本的な使い方までをご紹介していきます。"
---
# はじめに
こんにちは。踊るエンジニア、木戸俊輔です。

2021年4月で社会人2年目になりましたが、総出社回数は3回です。コロナで外出できないのは残念ですが、自宅で安全に業務に取り組むことができる現代の環境には感謝ですね。

さて、皆さんは普段どのようにE2Eテストを行っていますか？忍耐強く手動でポチポチ画面を触って...というのはなかなかにしんどいですよね。自動化ツールを使って楽したいけど難しくてよくわからない、という方もいらっしゃると思います。

本記事では、テスト自動化ツールを全く使ったことのなかった私が、テスト自動化ツールである[Cypress](https://www.cypress.io/)の導入から基本的な使い方までをご紹介していきます。

対象：

- Webサービスのテスト自動化に興味がある人
- 自動テスト初心者
- Cypressを触ってみたい人

## テストは大事

当たり前ですが、システムを納品/リリースする際、動作や性能のテストは必須です。もしテストが不十分だと、バグや想定外の挙動が発生し、

- システム納品先からの信頼消失
- 再開発のためにコスト増加
- サービスの廃止

などなど、恐ろしい事態に繋がる可能性があります。

## E2Eテストとは

E2Eテストとは、「End To Endテスト」の略であり、ユーザが利用するのと同じようにシステム全体をテストします。

抜け漏れなくテストする必要があるため、かかる労力は膨大です。また、テスト者の未成熟などによりテストが正しく行われない可能性もあります。

Cypressを用いて自動化することで、コスト削減＆品質向上を狙います。

# Cypressとは

[Cypress](https://www.cypress.io/)とはWebテスト用に構築されたJava Scriptライブラリです。

<img src="/images/20210428a/image.png" alt="Cypressロゴ" loading="lazy">

特徴として、以下のができます。

- 単体テストからE2Eテストまで広く使える
- テスト構築、実行、バグ検知まで全て行える
- コマンドごとに画面のスナップショットを見返せる
- テスト一連の様子をビデオとして保存できる
- 各種CIとの連携が可能である

## インストール

Cypressによるテストを構築したいディレクトリ下で、以下のコマンドを実行します。

```bash
npm install cypress
```

これだけです。5~10分くらいで簡単にインストールできます。
（Java Scriptライブラリなので、node.jsはいれておいてください。）

## 実行してみよう

とりあえず実行してみましょう。

```bash
npx cypress open
```

を実行すると、Cypressの管理画面が開きます。また、インストールしてから1回目の実行時には、いくつかのサンプルテストを生成してくれます。

<img src="/images/20210428a/image_2.png" alt="サンプルテスト" loading="lazy">

管理画面ではspecファイルごとにテストが並んでおり、実行したいファイルをクリックすると、記述されたテストが自動で実行されていきます。

試しに、サンプルテストの1つ、`actions.spec.js`を実行してみましょう。

<img src="/images/20210428a/image_3.png" alt="actions.spec.jsの実行例" loading="lazy">

画面右側で、Cypressが実際にどのようなWeb上操作を行っているかが確認できます。また、画面左側では、記述したテストの進行状況やチェック項目の可否が表示されています。失敗したテストがあれば、該当箇所をアラートで教えてくれます。


## Cypressの基本的な使い方

Cypressではspecファイルにテストを記述していきます。

```javascript
context('カテゴリ名', () => {
  it('シナリオ名1', () => {
    Cypressコマンドによる処理入力
             ┋
  })
  it('シナリオ名2', () => {
    Cypressコマンドによる処理入力
             ┋
  })
             ┋
})
```

CypressではWeb上でのアクションに相当する様々なコマンドが用意されています。

ここでは、よく使う基本的なコマンドをいくつか紹介します。

### Webサイトを訪れる


```javascript
cy.visit('URL')
```

### DOMを取得する

```javascript
cy.get('DOMのタグ')

cy.contains('探したい文字列')
```

`get()`と`contains()`どちらを使ってもDOMを取得することができます。

`contains()`は、引数として与えた文字列を探してくれるので、非常に簡単に記述することができます。しかし、同画面上に対象の文字列が複数存在する場合や、表示される文字列が変更されうる場合には注意が必要です。

### DOMを操作する
`get()`や`contains()`でDOMを取得し、DOMに対してコマンドを実行します。

```javascript
cy.click()   // クリック

cy.type('入力')    // 文字入力
```

例えば、「検索フォームに文字を打ち込んで検索する」操作は、

```javascript
cy.get('input[title="検索"]').type('Cypressの使い方');
cy.contains('Google 検索').click();
```

などといった記述で実行することができます。

### チェックする

画面の表示は適切か、ボタンはクリックできるか、といったテスト項目をCypressに確認させましょう。

```javascript
cy.should('テストタイプ')
cy.should('テストタイプ', 比較値)
```

例：指定の文字列が表示されていることをチェックする

```javascript
cy.contains('Gogle').should('exist');
```

テストが失敗していた場合はCypressが教えてくれます。
<img src="/images/20210428a/image_4.png" alt="エラーログ" loading="lazy">

## テストの動画を保存する
CYpressでは、テスト実行中の画面の様子を動画として保存できます。

ユーザ登録を行うことで、過去の動画の見返しや他者との共有が可能です。

1. Cypressを実行し、開いた管理画面の`Runs`タブからユーザ登録を行う。
2. Record Keyが発行される。表示されたコマンドでCypressを実行する。
<img src="/images/20210428a/image_5.png" alt="動画保存コマンド" loading="lazy">
3. 管理画面の`Runs`タブに、テストシナリオごとの実行ビデオが表示される。各ビデオファイルごとに保存や共有が可能である。

# おわりに

Cypressを用いたE2Eテストの基本的な実行&管理方法を紹介しました。

画面操作を自動化するだけでなく、バグフィクス、エビデンスとしても役立てることができる優れものですが、私のような初心者でも簡単に構築出来ちゃいます。まだまだ紹介しきれていない機能もありますので、本記事の紹介で気軽にチャレンジしていただければ幸いです。

ぜひ快適なテストライフを！

# 補足

本記事は、[Future Tech Night #8](https://future.connpass.com/event/208056/presentation/)というイベントでお話した内容を記事化したものです。
同イベントの他の発表も記事として投稿されてますので、ぜひご覧ください！

- Cypress入門～初心者でも簡単にE2Eテストが作れる～（この記事です）
- [Cypress - 設定編](/articles/20210428b/)
- [保守・拡張をしやすいカプセル化したCypress](/articles/20210428c/)
- [Cypress - 書きやすいテストの秘密と独自コマンドの実装](/articles/20210428d/)
