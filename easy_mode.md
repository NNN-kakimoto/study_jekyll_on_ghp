---
title: easy_mode
permalink: /easy_mode
---
# 1. サクッとページ公開してドヤりたい場合 
ドヤりたいときです 

ちなみにこのサイトに載ってる程度のことならQiitaで書いたほうが早いです。

## 前提条件
- ブラウザでGitHubが開けること。https接続できること。
- GitHubアカウントがあること。当然、ローカルでGitを使用できる状態であること。

## 推奨条件
- マークダウン記法をある程度使えること。見ながら書いても良い。
- .mdファイルのシンタックスハイライトが効くエディタ。流石にメモ帳やGitHub画面上のコーディングはしんどい。

---

## やり方
### 1.GitHubのリポジトリを作る
GitHubの自分のページから`Repositoryes`へ移動して、`New`します。リポジトリの名前はあとから変えられますが、後述の理由からオススメできないです。 

ある程度わかりやすくて短いリポジトリ名にしましょう。 
__https://<自分のGitHub_ID>/github.io/リポジトリ名__ がサイトのURLになります。 

□`Initialize this repository with a README` 

にチェックを入れておくと、あとあと楽かもしれません。特にどっちでもいいです。

### 2.リポジトリのSettingsを編集
GitHubリポジトリの`Settings`(Code, Issues, Pull requests...と並んでいるとこの右端)へ移動。 

`GitHub Pages`というところがあるので、その中の
###### Source
Your GitHub Pages ... 

`None` ←ここ 

を __master branch__ に変更。 

このとき、全くファイルの存在しない空のリポジトリの場合、 __切り替えれません。__ 

逆に上でチェックを入れておくと、すでに`README.md`というファイルが作成されているので切り替えれます。(内容はあとで書き直す必要がある) 

masterとかはブランチに対応していて、デフォルトのブランチであるmasterブランチに最初設定しておくと楽かと思います。 

参考にするjekyll情報によっては「gh-pages」みたいなブランチを用意する場合もあります。(ローカルでのジェネレートをしない場合はmasterで十分です。)


ごちゃごちゃ書きましたが、プルダウンリストを切り替えたら横の`Save`ボタンを押します。ページがロードされて一番上にスクロールが戻ったりしますがさっきの`GitHub Pages`のとこの戻ると緑の通知領域に
```
✔ Your site is published at https://<GitHub_ID>.github.io/<リポジトリ名>/
```
みたいになってるはずです。そこのリンクを踏むと(今のタブで)公開ページに遷移します。 

。。。そう、リポジトリトップに出てくる変なテキストが公開されています。急いで適当な文章に変更しましょう(しろめ) 


ちなみに消す前にブランチ切り替えの下、
###### Theme Chooser
`Change theme`
からテーマを選んで緑のボタン`Select theme`で決定すると、公開されているページのデザインをガラっと変えれます。 

テスト表示にいい感じです。 


気に入ったデザインがあれば変更して、公開したい内容に`README.md`ファイルを変更していきましょう。 

心配しなくても、レスポンシブ対応デザイン(のはず)です。

---

### リポジトリ名について
リポジトリ名は、公開設定をしたのと同じSettingsのページから変更できますが、実際に変更すると反映済みのテーマが死にます。 

公開済みソースを見ると書いているんですが、CSSのパスが変更前のリポジトリ名のままになっています。その証拠にに新しいリポジトリ名を含むパスに書き換えるとデザインが復活するのがわかります。 

##### てっとり早く解決するには
もう一度Settingsのページを開いて、`Change theme`からもう一度 __Select theme__ すると変更できます。多分ですがこのタイミングでGitHub側のレイアウトファイルを更新しているはずです。

実際、このリポジトリ名のstudyを __sutudy__ って書いててこれに陥りました。
###### 余談終わり
---

### ローカルで編集する
前述の通り、極論ブラウザ上ですべての作業はできるのですが、Gitの勉強だと思ってローカルで開発→GitHubへpush→自動で公開という流れをやりましょう。 

以降の内容はローカル環境での開発について書きます。 

ブラウザ上だけでの開発というハードモードをしたい人は自力で勉強してください。というかこのページ見なくても書けます。

#### 1. Git clone する
GitHubのリポジトリに移動して、緑色の`Clone or download`→「ファイルに矢印のついた謎なアイコン」をクリックするとアドレスがコピーできます。その状態でコマンド画面を開き
```
> git clone <コピーしたアドレス> ←ここでenter
Cloning into '<リポジトリ名>'...
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.
Checking connectivity... done.
>
```
ってなれば完了です。 

ちなみに僕はGit Bashでやりましたが、コンソールも同時に操作できるエディタ[VS code](https://code.visualstudio.com/)とかでもできます。導入すると良いです。ちなみに、こと開発においてはコマンドプロンプト画面は使わない主義です。 
~~lsすら打てないのはオワコンすぎる~~

クローンしてきたファイルを __VS codeとか__ でファイルごと開いて、ゴリゴリ編集していきましょう。


### ページを増やす
一枚のページならいいんですが、普通のサイトは複数枚のページで構成されています。
[PHP Conference 関西2018のページ](https://2018.kphpug.jp/)なんかがいい例ですね。

ちなみに新しいページを作るのはGitHub Pagesのjekyllだと簡単です。 

__・新しい.mdファイルを作る__ 

これだけです。 

例えば、`sub_page.md`みたいなのを作ると、`https://<GitHub_ID>/github.io/<リポジトリ名>/sub_page`というアドレスで公開されます。
 

ページを作ったあとは、そのページヘのリンクをREADME.mdに追記しましょう。書き方は
```
[表示する文字列](アドレス)
```
なのでこの場合だと、
```
[サブページ](https://<GitHub_ID>.github.io/<リポジトリ名>/sub_page)
```
ってそのまま打てばリンクが形成されます。 

さっきのページへの「戻る」リンクの場合は↑みたいに
```
[戻る](https://<GitHub_ID>.github.io/<リポジトリ名>/)
```
でOK.(README.md はデフォルトでアプリルートのURLに設定されています)


ここまで終わったらコミットとプッシュをしましょう。 

コンソール画面上を開きます。 __ちなみにVS codeならctrl+@でスグに開けるんですが__ 
> git add -A 

> git commit -m "コミットメッセージ" 

> git push origin master

で公開ページに反映されます。 

通常、1～2分ぐらい反映されないので気軽に待ちましょう。 

それと最初のpushのときは
```
> git push origin master
To https://github.com/<リポジトリ情報>
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/<リポジトリ情報>'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
となりました。(僕の環境では) 

なんか失敗してるっぽいのがわかると思いますが、リモートでの状態とローカルでの状態が違うことによるものです。最初のページの記述内容は全く不要なので、 __すべての内容をローカル側の内容で完全に上書きするコマンド__ `git push -f origin master`で対応しました。(乱発は避けたほうが良い)

---

##### ちなみに、
VS Codeなら`git commit`までをマウスでぽちぽち見ながら実行できます。 

その方法をお教えしましょう。 
1. まず、エディタ画面左枠に縦に並んだアイコンのうち、『Y』の先端3つが丸になったようなものを選びます。
2. すると、(変更されたファイルがある場合)リスト上に表示されます。
3. 変更をコミットするファイルの横の『＋』ボタンを押します。これでファイル単位で`git add`したことになります。「ステージング済みの変更」の欄に表示されるのがわかります。
4. その前に変更点がみたいときは単純にファイル名をクリックします。前のコミットとの差分が色分けされて表示されます。
5. 「ステージング済...」の更に上の枠にコミットメッセージを入力します。コミットメッセージのいい感じのサンプル集を見たんですが、見つけられなかったのでそのうち加筆します。
6. 一番上の✔マークを押すか、ctrl+enterします。(git commit) 
7. おわり。 

__やりやす～～～い！__ 

このあとctrl+@のパワーシェル上で`git push origin master`すればOKです。これに慣れすぎて僕のVScodeのパワーシェル履歴がひたすら`git push`になりました。
 

[戻る](https://nnn-kakimoto.github.io/study_jekyll_on_ghp/)
