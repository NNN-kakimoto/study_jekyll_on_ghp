--- 
title: normal_mode
permalink: /normal_mode
---

# 2.割としっかり目にCSSとか当てて公開したい場合
ドヤりたいときです

## 前提条件
- ブラウザでGitHubが開けること。https接続できること。
- GitHubアカウントがあること。当然、ローカルでGitを使用できる状態であること。
ここまでは1の前提条件と同じ。加えて、
- rubyの実行環境があること。このページではvagrantって仮想マシン上にCentOSを入れて、その上で実行する方法を載せます。
- カレントディレクトリの概念の理解。(知らない人もこの際覚えましょう)
- 多少のHTML/CSSの知識があること。フィーリングでかけるレベルなら問題ないです。

## 推奨条件
- マークダウン記法をある程度使えること。見ながら書いても良い。
- .mdファイルのシンタックスハイライトが効くエディタ。流石にメモ帳やGitHub画面上のコーディングはしんどい。
ここまでは1の推奨条件と同じ。加えて、
- Git bashの導入(Windowsの場合)
- ポート番号って概念が何となくわかること。ローカル開発時にブラウザで確認するとき、ちょっと手こずった(僕の場合)ので。

---
前置きについてはこんな感じです。

## やり方
以下はWindows環境の場合です。Macは持ってないので知らないですが、デフォルトでRubyが動くはずなので「Mac Ruby hello world」とかで検索したら3分で終わると思います。

大まかな流れはこんな感じ。
1. VM virtualboxを入れる ー仮想マシン(以下VM)導入用です。基本的に触らない。
2. Vagrantを入れる ーVMの上に乗っける感じです。エクスプローラーとかWin上からVM内のファイルを普通のファイルと同様にイジれるようにしてくれます。
3. Vagrantを使ってCentOSを入れる
4. CentOSに新しいRuby, jekyllを入れる ーデフォルトのRubyはバージョンが古いという情報を観測しました。
5. jekyll プロジェクトを創る。
6. いい感じにサイトをつくる。
7. ホストブラウザで確認して、`git push`する。 ーこのとき、ポート番号の関係でホスト側から見れなかったりするのでなんやかんやします。
8. 楽しい！✌('ω'✌ )三✌('ω')✌三( ✌'ω')✌

### 1. VM virturlboxを入れる
これは簡単。

[virtualboxのサイト](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html?ssSourceSiteId=otnjp)から適当なのをダウンロードして、インストールします。

### 2. Vagrantを入れる
このへんあまり覚えてないので、適当にググりつつやってもらえると非常に助かります。

[こんな感じのサイト](https://qiita.com/TakashiOshikawa/items/d2fb48d59e9e316af9a2)が参考になる気がします。このページの __VM立ち上げ__ まで行けたら大丈夫のはずです。

詰まったら[僕のTwitter](https://twitter.com/kakimoto_itc)まで画像つけてリプライしてください。

__以降、コンソールとは基本的にVM側のものを指します。VM側のコンソールに入るには、VMがをインストールした場所で、__ `vagrant ssh` __すれば良いです。__

上のリンクとか見ながらインスコもろもろ終わったらポート設定しておいたほうがいいかもです。


Vagrantにはポートフォワードとかいう~~よくわからない~~機能があって、すっげー簡単に言うと、
1. ホストブラウザから`http://localhost:4200/`にアクセスしても動かない
2. なんかいろいろと衝突してるらしい
3. ホスト側からアクセスするポート番号とVM側でそれぞれ開いてるものに変更する
4. みれるようになる

って感じで、このときの変更する機能がポートフォワードっぽいです。

[これ見て直しました](http://maku77.github.io/vagrant/port-forward.html)。

まあ開けないときに疑ってみるといいと思います。

### 3. Vagrantを使ってCentOSを入れる
上のリンクを参照してほしいです。

### 4. CentOSに新しいRuby, jekyllを入れる
jekyllの最小Rubyバージョンを検索できなかったのでわからないんですが、言語に関して古いものを使う理由はほぼないので、新しいのを入れておきましょう。

あとRubygemがほぼ必要です。あらゆるインスコが楽になります。

ただ僕はあんまり詳しく知らないので、知りたい方にはRubyの人を紹介します。

jekyllはRubyとgemがインストール完了したら、そこからは日本語リファレンスを読むと幸せになれます。

[http://jekyllrb-ja.github.io/](http://jekyllrb-ja.github.io/)

真ん中あたりに
```
~ $ gem install jekyll
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~ $jekyll serve
```
ってあると思いますが、これで完結です。5の内容も終わりでええな？

### 6.いい感じにサイトをつくる。
ここからが大変。

例えば[僕のサイト](https://nnn-kakimoto.github.io/mySite/)をご紹介します。

このサイトは、アプリルートにREADME.mdを呼び出していて、そのテンプレートに別のHTMLファイルとCSSを利用している、という形です。

以下に簡単なファイル構造を載せます。

```
/mySite
  └ _includes
  | └ head.html (HTMLの上部分を書きます。最初は無視でOK)
  | └ footer.html (フッター部分の共通化。これも無視)
  | └ css
  |   └ main.scss (CSSファイルだと思ってください)
  └ _layouts
  | └ index.html (ここに枠組みを書く)
  └ _config.yml (サイト共通の設定を書く)
  └ index.md
  └ about.md
```
こんな感じです。実際はもっとごちゃごちゃファイルとディレクトリが存在してます。

とりあえず「無視」と書いているもの以外でないものがあれば作成しましょう。

拡張子がついてないものはディレクトリです。アンダースコアを忘れずに。

このあたりから、公式リファレンスの記事が参照できるようになります。

割と適当に見ながらやっても動いたり動かなかったりするのでいろいろ試してみたら良いと思います。

#### 6-1. とりあえずハローワールド
まずindex.mdに何か打って、コンソールから
```
~/サイト名 $ jekyll serve --host 0.0.0.0
```
と打ってみましょう。その後ブラウザから`http://localhost:4000/`とかにアクセスしても音沙汰ないときは、上のポートフォワードを設定してみてください。 僕は14000番を当てました。(安易に一桁増やす人間)

__ちなみに、GitHub Pagesでの公開を目標としている場合__ は、baseurlの設定をしましょう。

baseurlは、アプリルートの`_config.yml`ファイルから編集できます。baseurlの設定によって、ローカルとGitHub PagesでのURLがほぼ同じになるので、後々悩まなくてすみます。

`_config.yml`ファイルの20行目あたり、
```
baseurl: "" # the subpath of your site, e.g. /blog
```
という一行があるはずです。この行のダブルクウォートの中にGitHubリポジトリの名前を入れましょう。

`jekyll serve`したままの場合は、一度ctrl+cで終了してから、もう一度↑ボタンで同じコマンドを打ちましょう。

以降、`_config.yml`を編集した際などは再ビルドが必要なので連打します。

ブラウザのURLの最後に`/<追記したbaseurl>`をつけてリロードして表示されれば完璧です。 __※スラッシュが必要です。__


#### 6-2. レイアウトの適用
さて、無事に表示されたらほかのファイルについても編集していきましょう。

まずは`_layouts/index.html`から。いわゆるHTMLのおまじないを書いていきます。
```
<html lang="ja">
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<header>
		<h1>header</h1>
	</header>
	<article>
		{{ content}}
	</article>
	<footer>
		<h2>footer</h2>
	</footer>
</body>
</html>
```
`content`の部分にマークダウンが呼び出されます。

で、呼び出し元のマークダウンファイル`index.md`を加筆します。

```
---
layout: index
title: index
permalink: /
---
```
`---`の存在が重要です。これで囲った範囲がページの設定項目となります。

- layout

	→`_layouts`ディレクトリの中にある同名のhtmlファイルを参照します。ちなみにデフォルトがpageだったりします。CSSが元からあたってるのでお試しにはちょうど良いです。

- title

	→その名の通りページタイトルになります。今は反映してないので関係ないですが、今後HTMLヘッド部分のtitleに反映させたり、ページヘッダーに呼び出したりできます。

- permalink

	→今は関係ないです。ここに指定したパスでアクセスできるようになります。書かない場合はマークダウンファイルの名前に設定されます。


このあたりで`jekyll serve`。

表示を確認しましょう。


#### 6-3. 更にレイアウトを分割
いい感じに表示できていれば、よく使う部分を共通化させましょう。

`_includes`ディレクトリの`head.html`(headerじゃなくてhead)にさっきのhtmlの上の部分を移植して、`index.html`側はそれを引っ張ってくる記述をします。

ついでにtitleも設定しましょう。

具体的にはこんな感じです。
`_includes/head.html`
```
<html lang="ja">
<head>
	<meta charset="utf-8">
	<title>{ { include.param } } | { { site.title } }</title>
</head>
```
`_layouts/index.html`
```
{％ include head.html param=page.title ％}
<body>
・・・
</html>
```
__上の例ではincludeの文の’%’を全角文字にしています。__(このサイトもjekyllでビルドされている関係で)

__実行する際は’半角で’%を入力してください。__

__それと`include`とか`site`とかの部分も二重中かっこの外側と内側が半角スペースで開いていますが、これもつめて書いてください。

各ファイルの、二重の`{}`　←で囲った部分に別の場所で設定した文字列が自動挿入されます。

また、`_layout/index.html`の{} ←の中に、`head.html`ファイルが読み込まれます。

同様に、`footer.html`なども作成して、読み込んでみると良いでしょう。

この場合、データの流れとして
1. index.md の`tile`が
2. index.html では`page.title`に入る
3. index.html 一行目、`param`に代入されて
4. head.html では`include.param`に入る
5. head.html で展開される
6. 'index'が出力される

さらに、
1. _config.yml の`title`が
2. head.html では`site.title`に入る
3. head.html で展開される
4. `$ jekyll new` したときの名前が出力される

最後2つが連結されます。

なお、`site`から取り出せる変数はsite変数と呼ばれ、すべてのページから参照可能(のはず)です。例えばサイトタイトル、githubのリポジトリアドレス、あるいは自分の連絡先など、ページを移動しても普遍の情報を入れると良いです。

ほかにもいろいろ展開できる変数はあるんですが、そこまで使いこなせてないので割愛します。[公式リファレンス](http://jekyllrb-ja.github.io/docs/variables/)を参照してほしいです。

#### 6-4. CSSの適用
jekyllはデフォルトでSCSSのコンパイルに対応しているので、利用しましょう。

SCSSはCSSの要コンパイルの完全上位互換といった感じで、使わない理由はないです。

もちろん完全上位互換なのでCSSそのまま書いても大丈夫です。最初CSSで書いておいて、後でSCSSに書き直しても良いと思います。

早速作っていきます。
`_includes`ディレクトリの中に、新たに`css`ディレクトリを作り、その中に`main.scss`というファイルを作ります。

ファイル構造はこんな感じになります。
```
/
  └ _includes
    └ css
    | └ main.scss
    └head.html
  └ _layouts
	・
	・
	・
```
`main.scss`の中身は後ほど自由に変えてもらうとして、仮にこうしておきましょう。うまく行けばページの上部分がグレーに、文字色が白になるはずです。
```
header{
	background-color: gray;
	color: white;
}
```
これを読み込むために`_includes/head.html`に加筆します。
```
<html lang="ja">
<head>
	<meta charset="utf-8">
	<title>{ { include.param } } | { { site.title } }</title>
	<style>
		{％ capture styles ％}
			{％ include css/main.scss ％}
		{％ endcapture ％}
		
	</style>
</head>
```
`<style>`タグ内が反映箇所です。すべてのページにおいて上の方に展開されるのでスマートじゃない気もしますが、気にする人は自力で改善すると成長できると思います。

__例によって’%’は全角文字で入力しています。実行の際は半角への置き換えをしてください。二重中かっこも同じくです。__

同様の理由で、`endcapture`と`</style>`の間の行に` styles | scssify `という文字列を二重中かっこで囲んで入れてください。これについてはどうやってもエスケープできなかった。

#### 6-5. 画像の表示
今更言うのも申し訳ないのですが、基本的にjekyllにおいて、ジェネレートされる`_site`ディレクトリ以下は __触ってはいけません__ 。というか、触っても`jekyll serve`のたびに戻されます。

そのため、画像などのそのまま出力するファイルについても、一度プールする場所を作り、ビルドの後、htmlファイルが開けるようにパスを設定する必要があります。

まず、ルート直下に`images`ディレクトリを作成して、その中に画像を入れます。
```
/
  └ _includes
  └ _layouts
  └
  └
  └ images
  | └ top-image.jpg
  └ index.md
	・
	・
	・
```
`top-image.jpg`を呼び出すには、`_layout/index.html`にて、
```
~省略~
<hrader>
	<h1>header</h1>
	<img src="{ { site.baseurl } }/images/top-image.jpg" alt="top-image">
</header>
~省略~
```
のようにします。

注意点は __パスの最初に`{ { site.baseurl } }`を指定すること__ 。これがないとファイルを見つけられずエラーになります。



#### 終わり。
#### 適宜更新と`jekyll serve`,`git push`をしていい感じのサイトを公開しましょう！
読みながらやったけど動かねぇぞ！みたいなときは自分で調べてください。

嘘です。[僕のTwitter](https://twitter.com/kakimoto_itc)にどうぞ。

#### 追記。
jekyllの二重中かっこ関連のエスケープまじでめんどかった。

なんで解説する言語つかって公開したんだろうとホンキで思った。