---
layout: post
title:  "Jekyllのエントリに画像を貼る"
date: 2014-06-08 13:45:00
categories: jekyll
---
まず、適当なディレクトリを作成して画像ファイルを入れておきます。たとえば`/images/sample.png`という画像ファイルを配置したとします。
エントリにはこんな感じの記述で画像を貼ることができます。

```
![キャプション]({{site.baseurl}}/images/sample.png)
```

ただし、このままだと巨大な画像ファイルの場合もそのままのサイズで表示されてしまうため、レイアウトの横幅からはみ出てしまいます。

そこで、`css/main.css`に以下のようなスタイルを追加します。

```css
img {
  max-width: 100%;
  border: 1px solid #eee;
}
```

これで画像は最大でもブログエントリのレイアウトの横幅いっぱいに表示されるようになります。

Jekyllには画像サイズを指定するプラグインなどもあるようですが、Github PagesではJekyllのプラグインは使えないようです。ローカルでHTMLを生成してpushするようにすればできますが、それはそれで面倒ですよね…。
