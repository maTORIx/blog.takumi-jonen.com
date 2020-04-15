---
title: "takumi.jonenのブログ実装備忘録"
date: 2020-04-14T13:59:18+09:00
draft: false
hideLastModified: true
summaryImage: "images/blog.png" 
keepImageRatio: true
tags: ["programming", "blog"]
showInMenu: false
summary: "takumi.jonenのブログを作成するにあたって、利用した技術などについての解説。"
---

{{< analytics >}}

{{< container "header-image" >}}
![header-image](images/blog.png)
{{< /container >}}

この記事では、このブログ「blog.takumi-jonen.com」を作成するに当たって利用したものや、作成手順について解説します。

# 概要

このブログの主な構成要素は、下記の３つです。

- GitHub Pages
- Hugo
- Google Domains

この記事では、これらを利用して個人ブログを立ち上げるまでの手順を紹介します。

# 利用したサービスの概要

## GitHub Pages

プログラマー全員が利用すると言っても過言ではない、GitHub。

そのサービスの一部には、「GitHub Pages」 という機能があることを知っている人は多いと思います。

この「GitHub Pages」は単純に、GitHubにアップロードした静的ファイルをホスティングしてくれる機能です。

最初からドメインの用意もしてくれますし、GitHubでPostすれば反映されるので、簡単かつ便利に静的ファイルを管理し公開することができます。

そして、こんなに便利なGitHub Pagesですが、なんとお値段無料！。

小さな個人ブログの運営用ホスティングサーバとしては、ダントツで便利な部類だと思われます。

オススメです。

## Hugo

これは、ブログの中身部分を、簡単に実装するためのツールです。

Go言語製で速く動作するという特徴もありますが、それ以上に簡単かつ効率的に記事を書くことができる部分が非常に良いと思います。

テーマの種類も多く、楽しいです。

詳しくは、本家のサイトを見た方が良いので、下記のサイトを参照してください。

https://gohugo.io/

## Google Domains

Google社の運営するドメイン管理サービスです。

他のさくらのドメインや、お名前.comとできることは大して変わらないと思います。

詳しくは、下記を参照してください。

https://domains.google.com

# サイト構築の手順

## 1. Hugoの初期設定

まずはじめに、Hugoをインストールします。

インストール方法については、下記のサイトを参考にしてください。

https://gohugo.io/getting-started/installing/

その後、下記のように実行します。

{{< codeWide language="shell" >}}
    $ hugo new site blog.hogehoge.com
    $ cd blog.hogehoge.com
{{< /codeWide >}}

これで、ベースは作成できました。

## 2. Hugoのテーマ設定

初期設定を終えたら、次にテーマを設定します。

https://themes.gohugo.io/

上記のサイトにアクセスすると、様々なHugoのテーマを選び、利用することができます。

スマートフォンに対応しているかどうかや、表示速度、ライセンスなどに留意して、好きなテーマを選びましょう。

このブログの場合は、 [こちら](https://themes.gohugo.io/hugo-refresh/) を利用しています。

設定は、テーマの紹介ページ下部に書かれている説明を見ながら行ってください。

**以降の説明は全て、 `hugo-refresh` を利用した場合を想定します。**


{{< codeWide language="shell" >}}
    $ cd blog.hogehoge.com
    $ git init
    $ git submodule add https://github.com/PippoRJ/hugo-refresh.git themes/hugo-refresh
    $ rm config.toml
    $ curl -O https://raw.githubusercontent.com/PippoRJ/hugo-refresh/master/exampleSite/config.yaml
{{< /codeWide >}}

この状態で、`hugo server` を実行すると、 localhost:1313 にてブログをプレビュー することができます。

## 3. Hugoによるファイル生成場所の変更

今回の記事では、ブログの公開にGitHub Pagesを利用するので、Hugoの設定を一部変更する必要があります。

config.yaml (toml) に下記の欄を追加します。

{{< codeWide language="yaml" >}}
    publishDir: docs
{{< /codeWide >}}

テーマによって、 `toml` を使っていたり、 `yaml` を使っていたりすると思うので適宜読み替えて追記してもらえれば幸いです。

## 4. その他、config.yamlによるHugoの設定

hugoでは、config.yamlを使って、サイトの様々な部分（例えば、文章や画像など）を改変することができます。

どのテーマでもほとんど共通の設定として、 `title`, `publishDir`, `baseURL` などがありますが、大半の設定はテーマによって異なります。

記事以外の大半の情報についてはConfigを用いて変えられるので、自由に変更してください。


## 5. ドメインの取得

ドメインを取得しましょう。筆者のおすすめは domains.google.com です。（他にも、「さくらのドメイン」や「お名前.com」があります）

基本的には、1年間で1500円ほど掛かりますが、インターネットを漁ると無料のドメインも手に入る場合があるので、お金がない人は調べると良いでしょう。

## 6. GitHubへのPush

まずはじめに、GitHubのリポジトリを作成しましょう。この際、名前は好きに決めていただいて構いません。

次に、そのリポジトリのURL(ここでは、 https://github.com/hoge/blog.hogehoge.com とします)を用いて、ターミナルでコマンドを実行します。下記のように実行してください。

{{< codeWide language="shell" >}}
    $ cd blog.hogehoge.com
    $ git iinit
    $ git remote add origin https://github.com/hoge/blog.hogehoge.com
    $ echo resources > .gitignore
    $ git add .
    $ git commit -m "initial commit"
    $ git push origin master
{{< /codeWide >}}

これで、GitHubにサイトの情報を保存することができました。

## 7. GitHub Pages を用いた公開設定

次に、GitHub Pagesの設定をします。

作成したリポジトリのページにアクセスし、ページの右上にある「Settings」をクリックすると設定画面が開きます。

その一番下から2番目のHeaderに「github pages」の設定項目があると思います。ここを、変更します。

まず、sourceを「master branch /docs folder」へ。

custom domain を 購入したドメインに。

Enfoce HTTPS はオンにしましょう。(カスタムドメインを設定してしばらくはオンにできないので、1時間程度待ちましょう。)

下記の画像は、実際に blog.takumi-jonen.com が行っている GitHub Pages の設定です。

{{< figure src="images/gh-pages-settings.png" width="700" >}}

## 8. Hugoで作ったサイトの公開

最後の設定です。ドメインを購入したサイトで、CNAMEの設定を追加しましょう。GoogleDomainsの場合、次のように設定します。

{{< container "gh-pages-settings-image" >}}
|Column|タイプ|TTL|データ|
|---|-----|---|-----|
|blog|CNAME|1h|[github-username].github.io|
{{< /container >}}

ユーザー名は、適宜変更してください。

この設定の反映には10分程度かかるので、しばらく時間を置いてアクセスしましょう。

これで、個人ブログの公開は完了です。

## 新規投稿とアップデート

新規投稿は、とても簡単です。

まず、下記のコマンドで新規投稿を作成します。

{{< codeWide language="shell" >}}
    $ cd blog.hogehoge.com
    $ hugo new posts/[ページの名前]
{{< /codeWide >}}

その後、 `contents/[ページの名前].md` にファイルが生成されますので、編集してください。

編集し終えたら、下記のように実行します。

{{< codeWide language="shell" >}}
    $ hugo
    $ git add .
    $ git commit -m "[コメント]"
{{< /codeWide >}}

以上でアップデートは完了です。

------

以上です。

ブログをゼロから作成するのは、デザインやサーバー管理などで面倒な部分がありますが、外部サービスやHugoのようなツールを用いることで、ここまで簡単に個人ブログを開設することができます。

興味があればぜひ、お試しください。

それでは、今後も takumi.jonen のブログをよろしくお願いします。
