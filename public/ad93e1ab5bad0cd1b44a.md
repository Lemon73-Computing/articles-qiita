---
title: KDEの翻訳について-ソフト系
tags:
  - Subversion
  - メモ
  - KDE
  - 日本語化
  - Lokalize
private: false
updated_at: '2023-08-12T22:43:38+09:00'
id: ad93e1ab5bad0cd1b44a
organization_url_name: null
slide: false
ignorePublish: false
---
## 文章について
本文章は、以下の投稿の続編となっていますが、以下の文章を読んでいなくても全く問題ありません。

https://qiita.com/Lemon73/items/768215973076938c86a2

::: note warn
注意点:本文章は、**KDE本部や日本KDEユーザ会とは関係のない文章です。**
そのため、この文章について質問や間違えの訂正に関してはこちらのコメント欄以外の利用はお控えください。
:::

## 雑談
KDEのソフトウェアはどれもとても素晴らしいものですが、日本語化があまり進んでいません。
国内で人気の高い[Krita](https://krita.org)や、[Kdenlive](https://kdenlive.org)などは翻訳が進んでいるほうですが、それでも細かい部分は英語が多く残っています。

そのため、翻訳の手順がかなり複雑なので翻訳協力したくても難しくてあきらめる人が多く出てしまうかも…と思って文章にまとめてわかりやすくしました。
是非こちらの文章を読み、翻訳作業を手伝ってくれる人が増えることを切に望みます。

この文章が誰かの役に立ったら幸いです。

## ソフトウェアの翻訳

#### 目次
KDEのソフトウェア翻訳方法を簡単に表しますと、以下のようになります。
- [SVN](https://subversion.apache.org)で翻訳データの入手(.poファイル)
- 翻訳(gettext)
- メールで送信
- 適応(日本KDEユーザ会の翻訳担当の方がやってくれます。)

### 翻訳の前に必要な事前準備
#### 翻訳元データの入手のためのソフトウェア

KDEの翻訳ではsummitという技術が使われています。
[TechBase PO_Summit](https://techbase.kde.org/Localization/Workflows/PO_Summit)によると、正規リリース版と非正規リリース版で翻訳内容を共有するシステム?なのかと思います。
KDE独自のシステムだそうです。

ファイルの管理自体はSVNが使われているので、SVNでファイルの入手を行います。

<details>
<summary><a href="https://subversion.apache.org">SVN</a>ってなに？</summary>

SVNとはSubversionの略で、バージョン管理システムです。
[Git](https://git-scm.com)と似たものですが、[Git](https://git-scm.com)は分散型、[SVN](https://subversion.apache.org)は集中型を採用しているなどの若干の違いがあります。
(Gitのほうが新しい方式です)
</details>


今回の説明では[Git](https://git-scm.com)でいう[GitHub Desktop](https://docs.github.com/ja/desktop/installing-and-configuring-github-desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop)のようにコマンドなしで進められる方法を利用します。
(Gitのようにコマンドの操作も可能ですが、GUIのほうが直感的でわかりやすいと思います。
今回行うのはファイルの入手だけで、コミットなどほかの操作は行いませんのでコマンドを使う必要はないでしょう。)

[GitHub Desktop](https://docs.github.com/ja/desktop/installing-and-configuring-github-desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop)代わりになるのがこちら、[TortoiseSVN](https://tortoisesvn.net)です。

(追記:[TortoiseSVN](https://tortoisesvn.net)はWindowsOS専用らしいです。
OSが[Windows](https://www.microsoft.com/ja-jp/windows)の方は情報が多い[TortoiseSVN](https://tortoisesvn.net)の利用を推奨しますが、[Windows](https://www.microsoft.com/ja-jp/windows)以外のOSを利用の方は[別のSVNソフト](https://ja.wikipedia.org/wiki/Apache_Subversion#クライアント)をご利用ください。
KDEでも[KDESVN](https://apps.kde.org/kdesvn/)というソフトウェアを開発しているそうです。(日本語情報が少なそうですが…))

[こちら](https://tortoisesvn.net/downloads.html)からダウンロードしましょう。
日本語化をお勧めします。
(ダウンロード方法や日本語化の方法は調べれば出てくるので今回は説明を割愛します。)

#### 翻訳に使用するソフトウェアのダウンロード

翻訳ファイルは.poや.pot、.moという形式のファイルを使います。
この翻訳形式はgettextと言って、WordPressなどでも使われています。
Windowsのメモ帳などのテキストエディタでも翻訳作業はできますが、作業効率的に専用ソフトを入れるのを推奨します。

今回紹介するのはKDEが開発している[Lokalize](https://userbase.kde.org/Lokalize)です。
※KDE4ベースなので少しソフトウェアの古いです。
十分使えますが文献がやや少なめだったりするので、他の文献の多いソフトウェアを選択するのもありです。
[こちら](https://binary-factory.kde.org/job/Lokalize_Release_win64/)からダウンロードできます。

### 翻訳作業開始
- ファイルの適当なところ(デスクトップ画面とか)で右クリックする
- TortoiseSVN→リポジトリブラウザをクリック
- svn://anonsvn.kde.org/home/kde/trunk/l10n-support/ja/summit/messagesを入力
[こちら](https://websvn.kde.org/trunk/l10n-support/ja/summit/messages/)につながっています。
- 翻訳したいソフトの.poファイルをダブルクリックでダウンロード。
- 「ソフトを選択してください」と出るので、Lokalizeを選択。
- 翻訳開始。
(ファイルの場所がよくわからないところにあるので、名前を付けて保存を推奨)
- 翻訳した文章をまとめてZIPに圧縮
(ZIPファイルの名前は何でもいいです)
- KDEのメール(kde-jp@kde.org)へZIPファイルを送信
(クラウドドライブも対応していますが、スパムとしてはじかれる可能性があります。
以前にOneDriveで送った人がずっとスパムとして翻訳データをはじかれていたことがあったらしいです。)

広い範囲の翻訳をする際も、翻訳はこまめに提出してくれると助かります。

数日たったら翻訳を反映してくれます。
(Kritaなどは毎晩ソフトウェアがビルドされているので、最新のKrita+を入れると自分の翻訳が反映された状態で見れます。
逆に、メインリリース版で翻訳が反映された状態のものを見たい場合は、(当たり前ですが)次のメインリリースを待つ必要があります。)

翻訳状況については[こちら](https://l10n.kde.org/stats/gui/stable-kf5/team/ja/)(自分が翻訳したソフトウェアを選択すると翻訳割合が見れます。)が役立つかと思います。

(追記:詳しくはわかりませんが、[こちら](https://identity.kde.org/index.php?r=developerApplication)でDeveloperアカウントを取っているとsvnのコミットが自分でできるようになるらしいです。
KDEの翻訳をちょくちょくやっている方は、取っておくと楽になるかもしれません。)

## なんでこんな面倒な方法取るの？
ブラウザやGitLabから翻訳データをダウンロードする方法では、KDEの翻訳で使用しているsummitが使えないため、あまり良くないようです。
初期設定はかなり面倒ですが、設定さえできたらあとは楽なのでこの方法でやってください。

## 翻訳の参考になりそうな場所まとめ
- [翻訳について](https://jp.kde.org/community/getinvolved/translation/)
[日本KDEユーザー会](https://jp.kde.org)が発行している資料です。

- [日本KDEのメール購読](https://jp.kde.org/community/whatiskdejp/communicate/)
登録:[メール登録](https://mail.kde.org/mailman/listinfo/kde-jp)
- [メールのアーカイブ](https://mail.kde.org/pipermail/kde-jp/)
こちらはメールを購読していない人でも見ることができます。
(内容はメール購読と同じです。)
- [Matrix](https://app.element.io/#/room/#jp:kde.org)
昔のやり取りで役に立つものがあるかもしれません。
- [KDE 日本語フォーラム](https://discuss.kde.org/c/local-communities/kde/21)
近日開始しました。
- IRC
私自身IRCをやっていないので、どのくらい人がいるのか、どのような内容が話し合われているのかはわかりません。

#### 個人的に思うこと
KDE、翻訳をGitで管理するのはだめなの…？
(KDEは開発ではGitlabを使用しています。)

### 最後に
これ、写真入れないとわかりにくいですね…
今度気が向いたら写真も入れておきます。

そろそろKDE6出そうですね。
KritaとかKdenliveも新バージョンになるのでしょうか？楽しみです。

## 追記
- 2022/5/19
KDE日本ユーザ会の[小川さん](https://qiita.com/phanect)がこちらの記事に反応と指摘をしてくださったので、文章の間違っている点を修正しました。ありがとうございます。
