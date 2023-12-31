---
title: 様々なSNSのRSSを取得しよう!
tags:
  - ATOM
  - RSS
  - SNS
  - feed
private: false
updated_at: '2023-09-29T00:30:44+09:00'
id: 8af0f6f1dce25efdb533
organization_url_name: null
slide: false
ignorePublish: false
---
:::note
こちらの文章は、昔に[別のサイト](https://lemon73.qlog.dev/items/3c2056c0df6f459591a252bd7e70c558/)で公開した内容のミラーです。
:::

# RSSとは
>RSSは、ニュースやブログなど各種のウェブサイトの更新情報を配信するための文書フォーマットの総称である。
(参考:https://ja.wikipedia.org/wiki/RSS)

<img src="https://stat.qlog.app/media/article/image/7949071a72dc40fb87fb6dce1d3f1b7d.jpg" width=10%>

↑ブログやSNSなどでこのマークを見たことはありますか?

こちらは、好きなニュースやブログ、SNSの人のコメントだけを集めて通知してほしい場合などで使います。
様々なSNSがこのRSSに対応しているのですが、これの入手方法がSNSによって異なるので、この文章ではそれをまとめていきます。
ブログ系などは全体のRSSなどもありますが、今回は特定のユーザーのRSS取得に着目します。
(RSSの利用方法については他の方の文章をご利用ください。)

## Blog系
### Qiita
バージョン:Atom
![qlog](https://stat.qlog.app/media/article/image/58cc317556a246ab864e56ccfa913acb.png)
または
```
https://qiita.com/ユーザ名/feed
```
(ユーザ名…@xxxxのxxxxの部分)

### Zenn
バージョン:RSS2.0/(Atom?)
![qlog](https://stat.qlog.app/media/article/image/e66a34ecd4ea4c00962e387518d913f8.png)
または
```
https://zenn.dev/ユーザ名/feed
```
(ユーザ名…@xxxxのxxxxの部分)

### Note
バージョン:RSS2.0/(Atom?)
![qlog](https://stat.qlog.app/media/article/image/7a160a1cfe724d7e9031c6479ccb1db7.png)
または
```
https://note.com/ユーザ名/rss
```
(ユーザ名…@xxxxのxxxxの部分)

## Git系
(SNSじゃないw)
コミットごとに通知が来るのでうざいです。
登録しないほうがいいです。
### GitHub
バージョン:Atom
```
https://github.com/ユーザ名.atom
```
(ユーザ名…@xxxxのxxxxの部分)

### GitLab
バージョン:Atom
![qlog](https://stat.qlog.app/media/article/image/2362b99fbd6e4d6aa03194bfb5a72fd4.png)
または
```
https://gitlab.com/ユーザ名.atom
```
(ユーザ名…@xxxxのxxxxの部分)

## 動画系SNS
### YouTube
バージョン:Atom
YouTubeは若干面倒です。

https://www.youtube.com/channel/UCNiEtjncyYOxSsZ-6BFCNUA
https://www.youtube.com/@lemon73
両方とも同じチャンネルを指していて、上が昔からのチャンネル表記、下が近年追加された新しいチャンネル表記です。
昔からの古いチャンネル表記でのリンクが分かる場合はRSSの取得が可能です。
([こちら](https://ilr.jp/tech/485/)を利用すると新しいチャンネル表記から昔のチャンネル表記に変換できます。)

```
https://www.youtube.com/feeds/videos.xml?channel_id=チャンネルID
```
例)
https://www.youtube.com/channel/UCNiEtjncyYOxSsZ-6BFCNUA
このチャンネルのRSSを取得する場合、
UCNiEtjncyYOxSsZ-6BFCNUAの部分がチャンネルIDになります。
なので、
https://www.youtube.com/feeds/videos.xml?channel_id=UCNiEtjncyYOxSsZ-6BFCNUA
がこのチャンネルのRSSのリンクです。

### ニコニコ
バージョン:RSS2.0/Atom
![qlog](https://stat.qlog.app/media/article/image/212ba37412014b958f7800cdcf80a240.png)
ユーザーのIDを記録します。

RSS2.0
```
https://www.nicovideo.jp/user/ユーザーID/video?rss=2.0
```
Atom
```
https://www.nicovideo.jp/user/ユーザーID/video?rss=atom
```

## チャット系
### mstdn.jp(Mastodon)
バージョン:RSS2.0
```
https://mstdn.jp/@ユーザー名.rss
```
(ユーザー名…@xxxx)

### Fedibird(Mastodon)
バージョン:RSS2.0
```
https://fedibird.com/@ユーザー名.rss
```
(ユーザー名…@xxxx)

### Misskey(Misskey.io)
バージョン:Atom
![qlog](https://stat.qlog.app/media/article/image/aa91906c61a249038be9c9ddd14a1d4c.png)
または
```
https://misskey.io/@ユーザー名.atom
```
(ユーザー名…@xxxx)

## その他
### Reddit
バージョン:Atom
```
https://www.reddit.com/user/ユーザー名.rss
```
(ユーザ名…@xxxxのxxxxの部分)

### Pinterest
バージョン:RSS2.0
```
https://www.pinterest.jp/ユーザー名/feed.rss/
```
(ユーザ名…@xxxxのxxxxの部分)

## 最後に
RSSのバージョン問題が結構面倒…
ソフトウェアとか自作サイトでこのRSSデータを使おうとすると、RSS2.0とAtomで別の処理にしなきゃいけないので、若干面倒ですねw
RSSリーダーとかを使う際はバージョン関係なく読み取れると思うので、ぜひ気軽に利用してみてください。

他のSNSは気が向いたら追加します。
