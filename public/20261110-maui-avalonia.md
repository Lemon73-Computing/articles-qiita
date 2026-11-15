---
title: "[.NET MAUI] Avalonia MAUI が登場!?試してみた!"
tags:
  - Linux
  - C#
  - .NET
  - Avalonia
  - MAUI
private: true
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---

[.NET MAUI Advent Calendar 2026](https://qiita.com/advent-calendar/2026/dotnetmaui) 1日目の記事です。

## TL;DR

.NET MAUI を Linux、WebAssembly 上で動かせる[^maui-avalonia-support]、Avalonia Backend が発表。試してみました!

[^maui-avalonia-support]: Windows や macOS でも動かせます。しかも、macOS ではパフォーマンスが約2倍になるらしい…。(.NET MAUI では Catalyst 経由だが、Avalonia Backend で直接実行になるからかな?)

## .NET MAUI + Avalonia Backend とは

(経緯とかについて記載します。興味ない方は、[実際に動かすところ](#実際に触ってみる)まで飛ばしてくださいね)

<!-- ちなみにですが、.NET MAUI + Avalonia Backend は Avalonia 公式から、MAUI Avalonia とも、Avalonia MAUI とも、Avalonia MAUI Backend とも、いろいろな名前で呼ばれています。 -->

### .NET のクロスプラットフォーム環境について

まず、.NET を取り巻くクロスプラットフォーム環境についてですが、知っての通り

| フレームワーク | 開発元 |
| -- | -- |
| Xamarin → .NET MAUI | Microsoft / .NET Foundation / コミュニティー |
| Avalonia | Avalonia / コミュニティー |
| Uno | Uno Platform / コミュニティー |

- Xamarin → .NET MAUI (Microsoft / .NET Foundation / コミュニティー)
- Avalonia (Avalonia / コミュニティー)
- Uno Platform (Uno Platform / コミュニティー)

の3勢力が主流となっています。(Unity, Godot などのゲーム向けは除く)

この中では、Microsoft が開発し、Xamarin の技術を継承している .NET MAUI が圧倒的トップ!?

…かと思いきや、対応プラットフォームや言語の差[^avalonia-uno-support][^avalonia-langs-support]によって、Avalonia や Uno の存在感もかなり感じられている状態です。実際、Avalonia のほうが GitHub の Stars 数は多いです。[^github-stars-status]

[^avalonia-uno-support]: Avalonia や Uno は、.NET MAUI が"公式"サポートしていない Linux や WebAssembly をサポートしています。あとは旧バージョン OS とかも条件ありでサポート。
[^avalonia-langs-support]: また、Avalonia については F#、VB.NET といった、C# 以外の言語も"正式"対応しています。.NET MAUI の F# サポートがあるようですが、コミュニティーサポートのようです
[^github-stars-status]: .NET MAUI: 23.3k, Avalonia: 31.8k, Uno: 10.1k (2026/11/16時点)

### Linux サポートについて

そして、2026年初頭の Linux のサポート状況は以下のようになっていました。

| プラットフォーム | 公式 | 非公式 |
| -- | -- | -- |
| .NET MAUI | x | maui-linux が成長中 |
| Avalonia | o | - |
| Uno Platform | o | - |

ということで、.NET MAUI の Linux サポートは以前から強く望まれていました。

### Avalonia がサポートを表明

2025年11月11日、Avalonia から次の記事が投稿されました。

https://avaloniaui.net/blog/net-maui-is-coming-to-linux-and-the-browser-powered-by-avalonia

2025年12月10日には進捗が投稿。

https://avaloniaui.net/blog/avalonia-maui-progress-update

2026年3月16日には、Preview 1 を投稿されました。

https://avaloniaui.net/blog/maui-avalonia-preview-1

### 現在の状況

現在は Preview 版ではありますが、.NET MAUI から Avalonia へ移植する際の選択肢としても提示されています。

https://docs.avaloniaui.net/docs/migration/maui/#option-1-avalonia-maui-backend

正式公開は .NET 11 頃に予定しているようです。[^pre1]

[^pre1]: [Preview 1](https://avaloniaui.net/blog/maui-avalonia-preview-1) にて記載されています

## 実際に触ってみる

### .NET MAUI プロジェクトを作成

### Avalonia Backend を追加

### Linux で動かしてみる

## 結論

そもそも描画に関する設計思想として、

- .NET MAUI: ネイティブ描画
- Avalonia: 統一描画 (Skia)

のため、MAUI-Avalonia Backend を使うと、Windows、macOS、Android、iOS はネイティブ描画なのに、Linux だけ Skia 経由となってしまいます。

<!-- ↑もしかして、全部の描画が Skia になる?それならなおさら Avalonia に全部変えたほうがよくね? -->

また実用的には、.NET MAUI (Microsoft) と Avalonia の両方のサポートを受ける必要があり (?)[^avalonia-support-scope]、また設計も両方の仕様がまたがるため複雑になります。

[^avalonia-support-scope]: 現時点では、Avalonia MAUI のサポート範囲は不明ですが、Avalonia 社と契約したら、MAUI 部分もサポートしてくれますかね?

以上より Linux 対応したい場合は、新規では Avalonia を、既存のプロジェクトについても Avalonia へ移行したほうが、開発が楽になると考えられ、暫定的なサポート以外、使う場面がない気がしています。(それが、シェア拡大したい、Avalonia 社の作戦なのかもしれませんが)

<!-- Linux や WebAssembly が対応できるようになったことで、.NET MAUI に僅かな追い風、ライバルの Avalonia に強い追い風となっています。(つまり、相対的に負けてる) -->

ということで、.NET MAUI 側も、その後に試験的な機能として Linux ネイティブ描画の技術を開発はじめたので、それについて次の記事では触れたいと思っております。

## その他

ということで、発表からしばらく経ってしまいましたが、Avalonia Backend を試してみました。

実際に試してみましたが、予想通り .NET MAUI 単独か、Avalonia 単独でいい感じしますよね…。組み合わせると、技術的にも、非個人開発の際のサポート的にも、多重で複雑になるのが微妙かと思われます。

本命は、次回の記事で書く maui-labs だと思います。お楽しみに!(記事は明日までに間に合うかな?)
