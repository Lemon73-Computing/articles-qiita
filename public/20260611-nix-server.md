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

[Qiita Tech Festa 2026](https://qiita.com/tech-festa/2026) の記事です。

## はじめに

Nix に興味を持ったので、NixOS を使ってみた記録と感想です。

一応目的は、「"**サーバー構築**"、"**再現可能な環境**[^reproducible]" (*Reproducible Environment*) などの**学習**」としますが、正直 Nix を楽しめたらいいかな、と思っています。

[^reproducible]: 再現可能な開発環境というと、Docker もですね

(結論を言うと、NixOS のインストールと SSH 接続まで行います。Web サーバーなどのアプリケーションインストールや、外部公開は行いません)

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

### Rasberry Pi Writer を準備

### NixOS を SD カードに書き込む

### NixOS を Raspberry Pi で起動

## 設定してみる

### 設定用 Nix ファイルを作成

### 設定用 Nix ファイルを編集

### メイン PC から SSH 接続する

## 再現可能性を確かめてみる



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
