---
title: '[NixOS] Raspberry Pi で再現可能なサーバーを作ってみたい'
tags:
  - 'Nix'
  - 'NixOS'
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

[Qiita Tech Festa 2026](https://qiita.com/tech-festa/2026) の投稿記事です。

## TL;DR

1. NixOS のダウンロードと書き込み準備
1. ラズパイ実機に NixOS をインストール
1. NixOS にてユーザーや SSH 設定、メイン PC から SSH 接続

## はじめに

Nix に興味を持ったので、NixOS を使ってみた記録と感想です。

一応目的は、「"**サーバー構築**"、"**再現可能な環境**[^reproducible]" (*Reproducible Environment*) などの**学習**」としますが、正直 Nix を楽しめたらいいかな、と思っています。

[^reproducible]: 再現可能な開発環境というと、Docker もですね

(本記事では NixOS のインストールと SSH 接続まで行います。Web サーバー、Samba などのアプリケーション設定や、外部公開は行いません)

## 準備

今回は、仮想環境ではなく、物理的なハードウェアにインストールして利用してみます。[^phy]

[^phy]: 本記事では触れませんが、将来的にネットワーク系も設定も試してみたいので

今回用意したハードウェアは以下のとおりです:

- サーバー用: Raspberry Pi 3 Model B+
  - MicroSD 16GB
  - MicroSD → SD 変換
  - 電源
  - イーサネット (有線LAN)
- 液晶1台: 初期セットアップ用
- キーボード: 初期セットアップ用
- メイン PC: SSH 設定後の操作用

## インストール

### SD カード用の NixOS をダウンロード

SD カード用・ARM64 用をダウンロードします。

<!-- ここのスクリーンショットは後に撮影したので、実際にインストールした NixOS のバージョンとはわずかに異なります。が、ほとんど影響はないはずです。 -->

#### 1. 配布サイトにアクセス

まずは以下のリンクを開きます。

https://hydra.nixos.org/job/nixos/unstable/nixos.sd_image.aarch64-linux

![画像_2026-06-15_173100025.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/19c0a977-fc82-44cd-b75a-4cbde4914bd0.png)

#### 2. 最新の成功ビルドを開く

一番上のチェックがついているものを開きます。

この時は、上から2番目でした。(一番上は中断しており、ダウンロードできません)

![画像_2026-06-15_173252630.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/0b9c0f0f-d1cf-4644-8e66-bac5fbc26639.png)

#### 3. ダウンロード

最後に中央のリンクを選択すると、ダウンロードが開始します。4GB 程度あり、時間がかかるので、ゆっくり待ちましょう。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/12c1bb32-51b4-4adc-ad7f-6578252509ba.png)

### Rasberry Pi Writer を準備

続いて、Raspberry Pi に書き込むツールを用意します。

### NixOS を SD カードに書き込む

### NixOS を Raspberry Pi で起動

## 設定してみる

### 設定用 Nix ファイルを作成

### 設定用 Nix ファイルを編集

### メイン PC から SSH 接続する

<!--
## 再現可能性を確かめてみる

書くか未定

-->

## 最後に

今回のサーバー構築を通して、Nix の概念や使い方について理解を進めることができたと感じます。

サブ PC にも導入してみたい気持ちになってきました。時間があったら、試してみたいと思います。

## 今後の展望

今後は、サーバーに機能を持たせてみたいと考えています。

具体的には以下の例を考えています。

- ゲームサーバー (テラリア、factorio、Minecraft[^mc]など)
- Web サーバー
- ファイルサーバー
- API サーバー
- 家庭内 DNS サーバー

[^mc]: マイクラに関しては、実は本体を持っていないのですが

が、使用しているハードウェア (Raspberry Pi 3) のスペック的にできることは少ないかもしれません。(`sudo nixos-rebuild switch` 処理ですらやや重い)

厳しそうだったら、別のパソコンに変えてみたいと思います。[^alt-pc]

[^alt-pc]: 別のパソコンに移行するのも、再現可能性があるので、楽にできそうですね。または、WSL で試してみてもいいかも知れません。

また、VPN を通して外部からのアクセスを可能にしたいと考えています。セキュリティー的に難しそうですが、試してみたいですね。

上手くできたら、また記事を作成するかも知れません。お楽しみに!

## 参考

### 記事の参考

- https://debslink.hatenadiary.jp/entry/20260117/1768615582

### 役に立ちそう

- https://mtlynch.io/nixos-pi4/
