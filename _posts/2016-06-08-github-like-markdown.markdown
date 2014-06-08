---
layout: post
title:  "JekyllでGithub風の記法を使えるようにする"
date: 2014-06-08 23:27:00
categories: jekyll
---

JekyllではMarkdownでエントリを記述することができますが、デフォルトでは[kramdown](http://kramdown.gettalong.org/)というパーサが使用されます。これは皆さん御馴染みのGithubのMarkdownの書式とは若干異なるものです。

[redcarpet](https://github.com/vmg/redcarpet)というパーサを使うとGithubと同じ記法でコードブロックやテーブルなどを記述できるようになるようです。

`_config.yml`を以下のように編集します。

```yaml
# Build settings
#markdown: kramdown
#permalink: prettay

markdown: redcarpet 
redcarpet: 
    extensions: ["no_intra_emphasis", "fenced_code_blocks", "autolink", 
                 "tables", "with_toc_data"] 
```

すると以下のようにGithub風の記法でコードブロックが書けるようになります。

<pre>
```bash
$ jekyll server --baseurl ''
```
</pre>

これならGithubのWebエディタや、その他のMarkdownエディタで編集する場合でもそれなりにプレビューできますね。