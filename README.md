# GitHubを使ってみよう
# はじめに
### 今回行うこと
Gitを用いたファイル管理を行うための準備を行います。
# Gitの環境構築
はじめにリモートリポジトリを作成し，ローカルリポジトリにコピー(クローン)する作業を実施します。
Gitを扱うための環境構築を実施します。  
以下の作業を行ってください。  
- Git for Windowsのインストール  
https://gitforwindows.org/  
- Visual Studio Codeのインストール  
https://azure.microsoft.com/ja-jp/products/visual-studio-code  
上記の作業が終わったら，次の工程に進んでください。  
# Visual Studio Code拡張機能のインストール
![](https://storage.googleapis.com/zenn-user-upload/4c3e993a97cc-20230623.png)  
写真の箇所で拡張機能を追加できます。  
GitGraphを検索し，インストールしましょう。  
日本語化を行いたい人は，Japanese Language Pack for Visual Studio Codeをインストールしましょう。(コチラは必須ではありません。本記事では，英語を前提として勧めます。)  
# GitHubへの登録
https://github.com/ へアクセスし，ユーザ登録を行ってください。  
入力したメールアドレスとユーザ名は次で使うので覚えておきましょう。  
# Gitの初期設定
GitBashを起動し，ユーザ情報の入力を行います。  
はじめに以下のコードを入力して自分がいるディレクトリを確認しましょう。  
($は入力しなくても良いです。)  
```
$ pwd
```
ファイルをクローンするディレクトリを変更したい場合は，GitBashのあるファイルにアクセスし，GitBashのプロパティを開きます。  
作業フォルダを任意のディレクトリに変更し，リンク先にある–cd-to-homeも消去してください。(これがあると，強制的に作業フォルダがhomeフォルダになってしまいます。)  

ここでは，プロキシ環境下にいる人のためにプロキシの設定も行います。(不要な方は読み飛ばしてもらって結構です。)  
ここで入力するuser.nameとuser.emailはGitHubに登録した情報，http.proxyとhttps.proxyは使用しているプロキシサーバを入力してください。  
```
$ git config --global user.name "NihonTaro"
$ git config --global user.email "hoge@example.com"
$ git config --global http.proxy "http://proxy.japan.com:8080"
$ git config --global https.proxy "https://proxy.japan.com:8080"
$ git config --global init.defaultbranch main
```
以下のコマンドより，設定が入力されているか確認することができます。  
```
$ git config --global --list
```
# 【Git】プロキシの外し方
プロキシ環境で設定していたものを解除するには，プロキシ設定の各コマンドに  
```
--unset
```
を入力します。  
使用例は，以下の通り。  
```
$ git config --global --unset http.proxy "http:proxy.japan.com:8080"
```
# GitHubでリモートリポジトリ作成・クローン
## リモートリポジトリ作成
GitHub上でリモートリポジトリを作成します。  
リモートリポジトリとは，インターネット上に存在するファイルや履歴を記録するプロジェクトのことです。  
リポジトリ内のファイルを更新する際には，自身のPCへリポジトリをコピー(クローン)します。  

GitHubへアクセスし，リモートリポジトリを作成します。  
GitHub右上のプロフィールアイコンから"your repositories"→"New"でリポジトリを作成します。  
![](https://storage.googleapis.com/zenn-user-upload/9abf836f98b3-20230623.png)  
Repository name:リポジトリ名(英字表記)  
Public / Private: インターネットへの公開有無  
→Publicを選択すると全世界に公開することができます。今回はPrivateを選択します。  
Initialize this repository with: リポジトリ作生成するファイル  
→今回は「Add a AREADME file」にチェックを入れます。  
  
最後にCreate repositoryボタンで作成されます。  
なお，README.mdがあるとGitHubのWeb上で閲覧できる部分が追加されます。  
(概要を説明できる)  
## クローン
リポジトリが作成されたので，自身のPCにクローンします。  
GitHub右上のプロフィールアイコンから「your repositories」→作成したリポジトリを選択します。  
緑色のボタン「Code」を選択すると，クローン用のURLが表示されます。設定がHTTPSいなっているか確認し，URLをコピーします。  
![](https://storage.googleapis.com/zenn-user-upload/17f1d5f1d26b-20230623.png)  

GitBashを起動し，以下のコマンドでクローンを行います。  
```
$ git clone コピーしたURL
```
なお，GitBashでペーストをする場合は，Shift+Insertで行います。(Windows標準と違って難しい)  
GitBashの設定が正しく出来ていればGitHubアカウント連動のポップアップが表示され，GitHubのアカウント名，パスワードの入力を求められるので，指示に従って作業してください。  
  
ここからはVisual Studio Code を用いてGit操作を行う。  
Visual Studio Codeで開く際は，ファイル→フォルダ を開くからクローンしたフォルダを選択してください。  
ファイルを開くから取り組むと、この後の作業が失敗します。  
## ファイルの追加・修正
リポジトリにファイルを追加する場合，下の図にあるようにVS Codeの左側(アクティビティバー)にある"EXPLORER"を選択し，右クリック→New Fileを選択します。  
ファイル名が指定できるので，任意に決めてファイルの種類を指定するために拡張子も記述します。  
![](https://storage.googleapis.com/zenn-user-upload/84a65f649527-20230623.png)  
下の図のようにソースを選択し，追加・編集したいファイルが"Changes"に存在するか確認します。  
リポジトリを更新するためには，Stage→Commitの手順が必要です。  
はじめに，ステージを行うファイルを選択します。  
"Changes"内にマウスポインタをかさねると"+"マークが表示されます。クリックすると"Staged Changes"へ移動します。  
次に上部にあるMessageに任意のコメントを入力します。  
ここでコメントした内容は，後でバージョン履歴一覧を確認する際に，コメントとして表示されるため，今回の更新で何を行ったかわかりやすいコメントを書きましょう。  
コメント入力後，右上のチェックマークを押すとコミットが完了します。  
![](https://storage.googleapis.com/zenn-user-upload/7d4f691824dc-20230623.png)  
チェックマークの右側"View Git Graph"を確認すれば，今回コミットした内容が表示されます。  
![](https://storage.googleapis.com/zenn-user-upload/23255fa55580-20230623.png)  
このように，ファイルの編集を行った際には，ステージ→コミットの手順を踏みましょう。  
## リモートリポジトリに反映・リモートリポジトリからデータ取得
ステージ→コミットで編集された内容は，PC内部のローカルリポジトリのみに反映されるため，GitHub上のリモートリポジトリはクローンされる前の状態になっています。  
これから，ローカルリポジトリの状態をリモートリポジトリに反映させます。  
(これから行うことをプッシュと言います。気になったら調べてみよう)  
下のいずれかでプッシュを行うことができます。  
![](https://storage.googleapis.com/zenn-user-upload/fec25e80ad94-20230623.png)  
![](https://storage.googleapis.com/zenn-user-upload/8d772517ec65-20230623.png)  
GitHubにアクセスし，反映されたか確認しましょう。  


## Pushできない場合
```shell
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
などのエラーが出た場合は，  
```shell
git remote add origin https://github.com/s-hirata0831/WebApp.git
```

これで今回の作業は完了です。  
