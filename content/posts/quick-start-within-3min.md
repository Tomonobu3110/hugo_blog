---
title: "Hugo + GitHub をつかって3分で静的サイトを立ち上げる"
date: 2020-04-02T10:58:52+09:00
draft: false
---
```
  環境：ローカルマシン(Ubuntu 16.04 LTS)
        GitHub

  HUGO使い方
  https://wiki.browniealice.net/technote/hugo/how_to_use_hugo/
  「Hugoは静的Webページ変換ツールの1つ」
  「基本的にはMarkdownで記事を書き, Hugoを起動して変換してもらって所定の静的なWebページを作る.」

  HugoとGitHub Pagesで静的サイトを公開する
  https://qiita.com/satzz/items/e24bd703fc04fb45f7ef

  << Hugoのインストール (Ubuntu 16.04 LTS) >>

  × $ sudo apt-get install hugo --> 古いhugoがインストールされる

  × $ wget https://github.com/gohugoio/hugo/releases/download/v0.40.2/hugo_0.40.2_Linux-64bit.deb
  × $ sudo apt install ./hugo_0.40.2_Linux-64bit.deb
  ※ これでもだいぶ古い

  〇 $ wget https://github.com/gohugoio/hugo/releases/download/v0.68.3/hugo_0.68.3_Linux-64bit.deb
  〇 $ sudo apt install ./hugo_0.68.3_Linux-64bit.deb
  ※ 太田まさんが使っているバージョン

  << サイト(hugo_blog)を作る >>

  $ hugo new site hugo_blog
  Congratulations! Your new Hugo site is created in "/home/tomonobu/git/hugo_blog".

  $ cd hugo_blog

  << gitにコミット >>

  $ git init .
  $ curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/master/Go.gitignore

  $ git add -A
  $ git commit -m "Init Hugo."

  << GitHubにあげる >>

  GitHubでリポジトリ作成 (hugo_blog)
  以下、チュートリアル
  --------------------------------------
  echo "# hugo_blog" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git remote add origin https://github.com/Tomonobu3110/hugo_blog.git
  git push -u origin master
  --------------------------------------

  $ git remote add origin https://github.com/Tomonobu3110/hugo_blog.git
  $ git push -u origin master

 << 設定ファイルいじり >>

  $ vi config.toml
  -----
  baseurl = "https://tomonobu3110.github.io/hugo_blog/"
  languageCode = "ja-JP"
  title = "Tomo3110's New Hugo Site"
  publishDir = "docs"
  copyright = "Copyright; 2020, Tomonobu Saito. All rights reserved."
  theme = "pickles"
  -----

  << 記事追加 >>

  $ hugo new posts/my-first-post.md
  $ vi content/posts/my-first-post.md

  Hugo で使える Markdown の記法
  https://k-kaz-git.github.io/post/hugo-markdown/

  Markdown Cheatsheet
  https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

  $ git submodule add https://github.com/mismith0227/hugo_theme_pickles.git themes/pickles

  << ローカルデバッグ >>

  HugoをWebサーバとして使う
  https://wave.hatenablog.com/entry/2016/05/12/074500

  $ hugo server --bind="43.31.104.100" --port=8080 --baseURL="43.31.104.100"

  ブラウザで http://43.31.104.100:8080/ にアクセスすると
  ホームページが見える！！

  $ hugo -D -t pickles

  ==> "-D" はドラフト版も含める (ドラフト記事は記事の .md のヘッダに draft : true がある)
  ==> "-t" はテーマ指定

  $ git add -A
  $ git commit -m "theme : pickles"
  $ git push origin master

  ==> テーマがあると docs の下に index.html が生成される様子
      ※テーマがないと index.xml だけ...

  << GiuHub側 >>

  リポジトリのページを開いて Settings -> GutHub Pages -> Source -> master branch /docs folder と設定して保存する.
  するとmasterブランチの docs フォルダ 以下がWebページだとみなしてWebサイトにしてくれる.
  -----
  Your site is published at https://tomonobu3110.github.io/hugo_blog/
  -----

  ● テーマについて

  テーマは "Pickles" がいい感じ
  https://themes.gohugo.io/hugo_theme_pickles/

  いろいろ追加...

  $ git submodule add https://github.com/mismith0227/hugo_theme_pickles.git themes/pickles
  $ git submodule add https://github.com/goodroot/hugo-classic.git themes/hugo-classic
  $ git submodule add https://github.com/digitalcraftsman/hugo-artists-theme themes/hugo-artists-theme
```


