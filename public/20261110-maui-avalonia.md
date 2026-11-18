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
| Uno Platform | Uno Platform / コミュニティー |

- Xamarin → .NET MAUI (Microsoft / .NET Foundation / コミュニティー)
- Avalonia (Avalonia / コミュニティー)
- Uno Platform (Uno Platform / コミュニティー)

の3勢力が主流となっています。(Unity, Godot などのゲーム向けや、Blazor などのウェブ系を除いた、ネイティブアプリでは)

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

公式リリース当初から2026年初頭に至るまで、.NET MAUI では Linux サポートを強く望まれていました。[^maui-discuss-linux]

[^maui-discuss-linux]: https://github.com/dotnet/maui/discussions/339

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

今回は、.NET CLI + VSCode で開発します。Visual Studio や Rider でも大丈夫です。

```sh
dotnet new maui -n MAUI_Avalonia
```

### Avalonia Backend を追加

### Linux で動かしてみる

## 結論と考察

### どのような場面で使えるか

Avalonia 自体が .NET MAUI から Avalonia への移行の方法の1つとして紹介している通り、Avalonia の描画方法を導入し、プラットフォームの拡大やパフォーマンスの改善を行いたい場合に利用する、というパターンがメインとなりそうです。

### 設計思想との違い

そもそもの話、クロスプラットフォームの開発の際、.NET MAUI か Avalonia の選択肢で考えると、以下の点が考えられます。

1. サポート元 (大企業のサポートが良い場合は .NET MAUI)
2. プラットフォーム (Linux、WebAssembly が欲しい場合は、Avalonia[^support-wasm])
3. 描画方法 (ネイティブがいいなら .NET MAUI、統一 (Skia) がいいなら Avalonia)

[^support-wasm]: とはいえ、WebAssembly については MAUI Blazor Web App があるので、ある程度はなんとかなります。

特に (3) については、.NET MAUI のプロジェクトに Avalonia を混在させると、Windows、macOS、Android、iOS はネイティブ描画なのに、Linux だけ (または、デスクトップの Windows、macOS、Linux だけ) Skia 経由となってしまい、描画方法がバラバラになってしまいます。また、両方の仕様がまたがるため内部が複雑になります。

(1) については、有償サポートの範囲などがあまりわかっていませんが、.NET MAUI (Microsoft) と Avalonia の両方のサポートを受ける必要があるのではないかと考えています。

以上より Linux 対応したい場合は、新規では Avalonia を、既存のプロジェクトについても Avalonia へ移行したほうが、開発が楽になると考えられ、段階的な移行時で、暫定的に Linux サポートを入れたい時以外では使う場面がない気がしています。(それが、シェア拡大したい Avalonia 社の作戦なのかもしれませんが)

## その他

ということで、発表からしばらく経ってしまいましたが、Avalonia Backend を試してみました。

実際に試してみましたが、予想通り .NET MAUI 単独か、Avalonia 単独でいい感じしますよね…。組み合わせると、技術的にも、非個人開発の際のサポート的にも、多重で複雑になるのが微妙かと思われます。

本命は、次回の記事で書く maui-labs だと思います。お楽しみに!(記事は明日までに間に合うかな?)
