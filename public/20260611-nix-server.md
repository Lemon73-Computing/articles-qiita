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

[^reproducible]: 再現可能な開発環境で有名なのは、コンテナ化技術 (Docker、Podman) ですね

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

Raspberry Pi だったら、バージョンにかかわらず参考になると思います。普通のパソコンに入れる場合は、SD カードではなく USB に書き込むほうが一般的なので、他の資料のほうが参考になるかも知れません。

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

最後に中央のリンクを選択すると、ダウンロードが開始します。4GB 程度あり、時間がかかるのでゆっくり待ちましょう。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/12c1bb32-51b4-4adc-ad7f-6578252509ba.png)

### Rasberry Pi Writer を準備

続いて、Raspberry Pi に書き込むツールを用意します。

https://www.raspberrypi.com/software/

Raspberry Pi Imager を利用します。ウェブサイトから、アプリケーションをインストールしてください。(インストールは簡単なので説明を省略)

### NixOS を SD カードに書き込む

#### バージョン選択

Raspberry Pi Imager を開くと、以下の画面が表示されます。

![スクリーンショット 2026-06-06 133106.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/7b6a5a2e-b2ea-4e60-8efd-4a09fd5fd45c.png)

利用するバージョンを選択してください。今回は Raspberry Pi 3 です。

#### OS 選択

続いて、OS 選択画面です。

![スクリーンショット 2026-06-06 133128.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/ca130f49-3071-4bc4-88b4-6a51e5dd8231.png)

一般的に利用される Raspberry Pi OS を利用する場合は、それを選択します。

![スクリーンショット 2026-06-06 133143.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/be2c3678-11c6-4598-b162-1c04c1c4d312.png)

が、今回は Nix OS を入れたいので、下にスクロールし、カスタムイメージを選択します。フォルダーが表示されるので、先程インストールした Nix OS を選択してください。

#### ストレージ選択

![スクリーンショット 2026-06-06 133158.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/67aee880-da9f-4cd6-8acf-3d018201b279.png)

書き込み先を選択してください。書き込みを行うと、データが消えるので、間違えないように!

#### 確認画面

![スクリーンショット 2026-06-06 133202.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/742e4d2e-10ef-4f48-9803-656834be88a2.png)

間違いないか確認し、<kbd>Write</kbd> を教えてください。

![スクリーンショット 2026-06-06 133207.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/0f98d6b0-c897-441f-a5a3-daeb1e2d3f2d.png)

大丈夫でしたら、<kbd>I understand, erase and write</kbd> で。

#### 書き込み中

![スクリーンショット 2026-06-06 133220.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/2ede8de5-a334-451d-85af-5c0aa574eabc.png)

書き込みが開始します。

#### 書き込み終了

![スクリーンショット 2026-06-06 134927.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2769460/4f96a587-6908-4f16-b04b-4739c600d329.png)

書き込みが終了しました。<kbd>Finish</kdb> で終了し、SD カードを取り出してください。

### NixOS を Raspberry Pi で起動

SD カードを Raspberry Pi に入れ、電源を差し込むと自動起動します。

なにか表示されますが、キーボードの何か (<kbd>Enter</kbd> とか) を打ち込んだら起動すると思います。[^no-photo]

[^no-photo]: すいません、写真取れませんでした

これで、Nix OS を使うための準備は終了です。SD カードに書き込むのが少し特殊ですが、USB 書き込みとそれほど変わらない手順なので、経験者は直ぐにできると思います。

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
