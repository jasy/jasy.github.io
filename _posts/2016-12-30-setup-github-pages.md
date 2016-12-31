---
layout: post
title:  "Setup GitHub Pages with Jekyll"
date:   2016-12-30 22:30:00 +0900
categories: github pages
---
[GitHub Pages](https://pages.github.com/)で標準サポートの
[Jekyll](https://jekyllrb.com/)を使ってみたので設定方法だけ残しておく。

## GitHub Pagesのローカル環境
必須ではないがローカルでも扱えた方が便利だろうと以下を参考に環境を整えた。

* [Setting up your GitHub Pages site locally with Jekyll - User Documentation](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)

macOS Sierra標準のRubyが
[GitHub Pages Ruby Gem](https://github.com/github/pages-gem)の要求より古かったので
[rbenv](https://github.com/rbenv/rbenv)で新しいの入れることにした。

```shell
brew install rbenv
echo 'eval "$(rbenv init -)"' >> ~/.profile
```

```shell
rbenv install 2.3.3
rbenv local 2.3.3
```

依存するGemの[Nokogiri](https://github.com/sparklemotion/nokogiri)のビルドが遅いのでGemfileに若干工夫を入れる

```
source 'https://rubygems.org'
ENV['NOKOGIRI_USE_SYSTEM_LIBRARIES'] = 'YES'
gem 'github-pages', group: :jekyll_plugins
```

```shell
brew install libxml2 libxslt
gem install bundler
bundle install
```

とりあえずローカル環境完成

## themeのカスタマイズ
↓作ったもののthemeが[Minima](https://github.com/jekyll/minima)。
全部自分で作るのは面倒なのでこれをベースにする。

```shell
jekyll new /path/to/mypage
```

表示したいもので設定になさそうなのが以下だったのでピンポイントでカスタマイズすることにした。

* `favicon.ico`
* `apple-touch-icon`

Jekyllの説明(↓)によると、同じファイルは選択したthemeより先に読むらしい。

* [Themes - Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/themes/)

ということで`_includes/head.html`をコピーして↓を追記した。

```html
  <link rel="shortcut icon" href="/favicon.ico">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

この後のこのファイルのアップデートに自動追従できなくなるのと、
決まった分割があるわけでもなさそうなので全然違う構成になったりすると面倒だなぁ
と思いつつとりあえずこのまま行くことにする。

## Syntax highlighting
[Rouge](https://github.com/jneen/rouge)が標準で入っているのはありがたいと説明だけ見てこの記事書いた。

* [Using syntax highlighting on GitHub Pages - User Documentation](https://help.github.com/articles/using-syntax-highlighting-on-github-pages/)
* [List of supported languages and lexers · jneen/rouge Wiki · GitHub](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers)

## 制御構文や変数
[Liquid](https://shopify.github.io/liquid/)がベース。
`site.github`変数が使える。

* [Repository metadata on GitHub Pages - User Documentation](https://help.github.com/articles/repository-metadata-on-github-pages/)
