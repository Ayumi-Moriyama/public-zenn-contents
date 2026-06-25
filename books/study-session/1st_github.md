---
title: "【第一回】後半：GitHub & Soursetreeでの操作"
---
## 【後半：GitHubとSoursetree】
## Gitの基本
下記サイトがわかりやすいのでおすすめ
https://backlog.com/ja/git-tutorial/

## Gitコマンドの例

### 初期化

#### git init
隠しフォルダ（.git）が作られ、自分のプロジェクトがGitリポジトリになる

http://frkz.jp/study/git/init

### 状態確認

#### git status
現在の状態を表示する

#### git log
コミット履歴を表示する

### ローカルからリモートへ

#### git add
新たに追加/変更/削除したファイルをインデックスに追加
- コミット前の準備

#### git commit
インデックスに存在するファイルをローカルリポジトリに反映する
- **git commit -m** でコミットにメッセージを付けられる

#### git push
ローカルの変更をリモートに送る
- プッシュすることで、リモートリポジトリに変更が反映される
- 変更されたリモートリポジトリをチームメンバーが見ることができる

:::details インデックスとは？
手元のローカルリポジトリ、GitHubで確認できるリモートリポジトリの他に、見えないですがインデックス（ステージングエリア）というものがあります。
https://qiita.com/sparklingbaby/items/e749249d366c7487bbbf
:::

### リモートからローカルへ

#### git clone
既存のリモートリポジトリをローカル環境に複製する
- .gitも複製されるため、Gitのリポジトリとして機能する
:::details ダウンロード・クローン・フォークの違い
ダウンロードはソースコードの配布、クローンは共同開発、フォークは別バージョン開発時に使うイメージ
https://docs.github.com/ja/get-started/start-your-journey/downloading-files-from-github
:::

#### git pull
リモートの変更をローカルに取り込む
- 他のメンバーが加えた変更を自分の環境に取り込むことができる
:::message
pullは、実はfetchとmargeをまとめて行っています
:::

:::details fetchとmarge
git fetchは情報を取ってくる。
（犬に投げた棒などを取って来させる遊びをFetchと言いますが、そのイメージ）
margeは取ってきた情報を更新する。
https://zenn.dev/atsushi101011/articles/f66617b53f71ea
:::

### Gitの管理はツールを使おう
上記のようなコマンドで操作はできるのですが、これだと今どういう状態なのかを把握するのは困難です。
VS Codeの拡張機能を入れるという方法もありますが、私のおすすめは**Sourcetree**です。

#### Sourcetreeの特徴
- WindowsとMac両方で使える。無料。
- 日本語化されている
- 今どんな操作をしようとしているのかがわかりやすい。こまめにダイアログで確認してくれる親切仕様。

## ブランチ戦略
デフォルトのmainブランチ1つで開発を進めていくのは難しいです。
そこで、チームごとにブランチの管理方法を決めておくことになります。

ブランチモデルという管理方法があり、中でも有名なの**Git-flow**。5~6種類のブランチを切り替えながら開発を進めるやり方です。
[Git-flowの概要](https://tracpath.com/bootcamp/learning_git_git_flow.html)

個人〜小規模開発なら、3つのブランチで管理でもいいかと思います。
- mainブランチ（本番リリース可能な状態を維持）
- developブランチ（開発の基本となる。ここを常に最新に保つ）
- featureブランチ（各機能ごとにdevelopから切り出す）

この場合、
1. developからfeatureブランチを切り出して機能を作る
2. 機能が完成したらdevelopに取り込む
3. リリース可能な状態になったらdevelopからmainブランチに取り込む

という流れになります。
