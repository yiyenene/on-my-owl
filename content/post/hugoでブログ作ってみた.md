---
title: HUGOでブログ作ってみた
date: 2019-09-22T14:37:25.442Z
author: yiyenene
image: /images/uploads/blog.png
tags:
  - code
draft: false
---
表題の通りブログを作ってみました。  
Static Site Generator の中から圧倒的速さと評判(?)の HUGO を使ってみました。  
テーマは [hugo-swift-theme](https://themes.gohugo.io/hugo-swift-theme/) を使ってみたのですが、いろいろ躓いたところがあったので共有します。  

## docker-image

docker イメージは [klakegg/hugo](https://hub.docker.com/r/klakegg/hugo/) を使いました。HUGO で sass を使う場合は extended バージョンを使う必要があります。最初無印を使っていてハマりました。

## css パス

theme の head.html 内に以下のように書いてあります。

```go
 {{- $options := (dict "targetPath" "css/main.css" "outputStyle" "expanded" "enableSourceMap" "true") -}}
```

この targetPath が曲者で、これだと netlify にデプロイした際のビルドプロセスの中で scss 中の画像や font も css ディレクトリを指してしまって404になってしまっていました。とりあえず `css/` を削除して public ルートに生成されるようにして回避しました。  
あと config に baseURL を追加しておかないと本番環境では相対パスになってしまって死にます。

## data/author.yml の構造とか

exampleSite の中にある yml がわりと適当で実際に html 内で使われている Key が微妙に違っていたりするので html をしっかり眺めるといいです。author は front-matter に author を追加すると表示されるっぽいです。

## 他

にもいろいろあったような気もしますが、netlify へのデプロイも含めて全体的にはかなりお手軽感あります。すごい時代ですね。静的サイトだけど netlify CMS を使うと普通の Blog のように書けます。これもすごいサービスですね…  
気が向いたときにこちらにいろいろ書いていければと思います。  

それではお先に失礼します。
