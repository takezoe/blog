---
layout: post
title:  "はじめてのJekyll on Github Pages"
date: 2014-06-08 11:48:00
categories: jekyll
---
## インストール
今更感がありますが、Githubで[Jekyll](http://jekyllrb.com/)を使ってブログを書けないかなーと思い、試してみました。

まずは`gem`コマンドでJekyllをインストール。

```bash
$ gem install jekyll
```

すると`jekyll`コマンドが使用できるようになるので（使用できない場合はターミナルを再起動します）、ディレクトリを作成。

```bash
$ jekyll new jk
```

生成されたディレクトリに移動して実際に動かしてみます。

```bash
$ cd jk
$ jekyll server
```

すると4000番ポートでサーバが起動するのでブラウザからhttp://localhost:4000/にアクセスすると以下のような画面が表示されるはずです。

![jekyll serverで動作確認]({{site.baseurl}}/images/setup-jekyll1.png)

なお、`jekyll build`コマンドを実行するとサーバで動かすのではなく、`_site`ディレクトリ配下にHTMLを生成することができるようです。

##Github Pagesで動かしてみる

次にGithub Pagesで動かせるかどうかを試してみます。

今回はテスト用にhttps://github.com/takezoe/blog/というリポジトリを作成しました。Github Pagesでコンテンツを公開するには`gh-pages`というブランチにpushします。

```bash
$ git init .
$ git checkout -b gh-pages
$ git add .
$ git commit -m 'first commit'
$ git remote add origin https://github.com/takezoe/blog.git
$ git push origin gh-pages
```

http://takezoe.github.io/blog/にアクセスしてみます。するとこんな感じに…。

![CSSが見えていない]({{site.baseurl}}/images/setup-jekyll2.png)

どうやら`css/main.css`が見えていないようです。デフォルトの状態だとドキュメントルートからのパスでCSSを見に行ってしまうようなので`_config.yml`の`baseurl`を変更します。

```yaml
# Site settings
title: Your awesome title
email: your-email@domain.com
description: "Write an awesome description for your new site here. You can edit this line in _c\
onfig.yml. It will appear in your document head meta (for Google search results) and in your fe\
ed.xml site description."
baseurl: "http://takezoe.github.io/blog"
url: "http://yourdomain.com"
```

この状態でpushするとGithub Pages上でもきちんと表示されるようになります。

しかし困ったことにこの状態だとローカルで`jekyll server`で動かすときにエラーが表示されるようになってしまいます。なので、ローカルで実行するときは

```bash
$ jekyll server --baseurl ''
```

のように`--baseurl`オプションを指定して起動するとよさげです。
