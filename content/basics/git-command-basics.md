---
title: "Git の基本コマンド"
date: 2022-03-16T07:42:16+09:00
weight: 2
---

## Git の基本コマンド
Git の操作方法は GUI と CUI に分けられます。  
Git の GUI を利用すれば、マウスを使って画面上のアイコンやウィンドウを使用すると簡単に Git を操作することができます。  
しかし、以下の理由からコマンドで Git を操作する CUI で学習をすることをお勧めします。  
- つまづいたとき、実行したコマンドと表示されたエラーを元にネットで検索をすることで原因が特定しやすい
- Git に関する記事は GUI よりも CUI の方が圧倒的に多い
- 実行した内容がログとして残るため、自分がどのような操作をしたのかという証跡が残る

そのため、ある程度慣れたのであれば GUI で Git を操作してもよいと思いますが、この教育コンテンツでは CUI（コマンド）で操作を行います。  
ここからは基本的な Git コマンドを紹介します。実際に Git コマンドを実行しながら確認をしていきましょう。  

Git コマンドを実行するにはまずローカル（皆さんのPC内）に Git で管理されているディレクトリを用意する必要があります。
Git で管理されているディレクトリを作成する方法は `git init` と `git clone` の２種類があります。  
それぞれの違いを確認していきましょう。

---
### 既存ディレクトリを Git 管理する
`git init` コマンドにより既に作成済みのディレクトリ（フォルダ）をローカルの Git リポジトリにすることができます。  
同コマンドを実行すると、指定したディレクトリに **「.git」** という隠しディレクトリが作成されます。  
この「.git」ディレクトリが配下にあるディレクトリは Git リポジトリとして扱われます。  
```
git init [Gitリポジトリにしたいディレクトリのパス（省略可）]
```
[Gitリポジトリにしたいディレクトリのパス]は省略することもでき、その場合はカレントディレクトリ（cdコマンド等で移動した現在のディレクトリ）が Git リポジトリとなります。

**DEMO**  
今回はデスクトップ上に git-tutorial ディレクトリを作成して、作成した同ディレクトリを Git リポジトリにしてみましょう。
```
cd /Users/UserName/Desktop
mkdir git-tutorial
git init git-tutorial
```
コマンド実行時に `Initialized empty Git repository in /Users/UserName/Desktop/git-tutorial/.git/`と表示されれば成功です。
※上記のメッセージのうち、UserNameにはOSにログインしているユーザー名が表示されます。  
git-tutorial フォルダを Git リポジトリにすることができたら、git-tutorial フォルダの配下に「.git」ディレクトリがあることを確認しましょう。  
```
cd git-tutorial
ls -al
```
これで Git リポジトリを作ることができました。この **「.git」** の中に過去のファイル・ディレクトリの状態が蓄積されていきます。

---
### リモートリポジトリをクローンする
GitHubなどに存在するリモートリポジトリをローカルにクローン（コピー）して開発を始めることもできます。  
実際の開発ではチームで１つのリポジトリを共有して利用するため、チームメンバーのひとりがリモートリポジトリを作成して、  
残りのメンバーはそのリポジトリをクローンするところから開発が始まることが一般的です。  
これを実現するのが `git clone` コマンドで、コマンドの後ろにはクローンしたいリポジトリのURLを指定します。
```
git clone [リモートリポジトリのURL] [クローン先のディレクトリのパス（省略可）]
```
[クローン先のディレクトリのパス（省略可）]は省略することもでき、  
その場合はカレントディレクトリ（cdコマンド等で移動した現在のディレクトリ）の配下にクローンした Git リポジトリが生成されます。

**DEMO**
今回は GitHub 上にある [git_tutorial](https://github.com/a-nakamura1015/git_tutorial.git) リポジトリをローカルのデスクトップにクローンしてみましょう。
```
cd /Users/UserName/Desktop
git clone https://github.com/a-nakamura1015/git_tutorial.git
```
コマンド実行後にデスクトップ上に git_tutorial ディレクトリがあることと、その配下に **「.git」** があることを確認してみましょう。  
そのため、クローンするだけでそのディレクトリ配下で Git の操作をすることができます。 

---
### ローカルリポジトリにリモートリポジトリを追加する
ローカルリポジトリとリモートリポジトリを紐づけるコマンドもあるので紹介します。   
 `git remote add`コマンドでリモートリポジトリの名前（**origin**）とリモートリポジトリのURLを設定することで実現できます。  
```
git remote add [リモートリポジトリの名前] [リモートリポジトリのURL]
```
リモートリポジトリにはデフォルトで**origin**という名前がついているので、この名前とリモートリポジトリのURLを紐付けるのが一般的です。  
また、ローカルリポジトリが現在どのリモートリポジトリと紐づいているかは以下のコマンドで確認をすることができます。
```
git remote -v
```
一方で一度紐づけたリモートリポジトリとの紐付けを解除することもできます。
```
git remote rm [リモートリポジトリの名前]
```

**DEMO**  
今回はデスクトップ上に remote ディレクトリを作成して、[git_tutorial](https://github.com/a-nakamura1015/git_tutorial.git) リポジトリをリモートリポジトリとなるように設定してみましょう。
まずは以下のコマンドでデスクトップ上に remote ディレクトリを作成して、remote ディレクトリをカレントディレクトリにしましょう。
```
cd /Users/UserName/Desktop
mkdir remote
cd remote
```
remote ディレクトリに移動ができたら、`git init`で remote ディレクトリを Git リポジトリにしましょう。
```
git init
```
続いて、以下のコマンドでリモートリポジトリを紐付けましょう。
```
git remote add origin https://github.com/a-nakamura1015/git_tutorial.git
```
以下のコマンドで火もづいているリモートリポジトリを確認してみましょう。
```
git remote -v
```
以下のような結果が表示されれば成功です。
```
origin	/Users/UserName/Desktop/remote/ (fetch)
origin	/Users/UserName/Desktop/remote/ (push)
```
最後にリモートリポジトリとの紐付けを解除してみましょう。  
先ほどリモートリポジトリのURLを設定した際に指定したリモートリポジトリの名前は **origin** なので以下のコマンドを実行しましょう。
```
git remote rm origin
```
これでリモートリポジトリの紐付けがなくなりました。試しに`git remote -v`を実行してみても結果は何も表示されません。

ここまではローカルに Git リポジトリを作成するコマンドを紹介してきました。  
ここからは本命のファイルの変更履歴を残す・確認するコマンドを紹介しますが、
「既存ディレクトリを Git 管理する」で作成した git-tutorial ディレクトリでコマンドの動作を確認していきます。  
以下のコマンドを実行した上で次に進みましょう。
```
cd /Users/UserName/Desktop/git-tutorial
```

---
### 現在のステータスを確認する
まずはGitリポジトリ内の状態を確認する `git status` コマンドを紹介します。  
後ほどファイルの状態をご紹介しますが、**編集したファイルがどのような状態であるかを確認することができる** コマンドです。
```
git status
```
git-tutorial ディレクトリでこのコマンドを実行すると、以下の内容が表示されます。
```
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

`On branch master` はカレントブランチ(※1)が master であることを意味します。
`No commits yet`はコミット(※2)がまだないことを意味します。  
※1 ブランチは、同じプロジェクトで同時変更で作業を進めるための仕組みです。ブランチは応用編で解説します。
※2 コミットは Git が管理しているリポジトリ内のログに変更履歴を残す操作のことです。 本編で解説します。 
まだコミットをしていないので画面上には`No commits yet`と表示されています。  

この後いくつかの Git コマンドを実行してステータスを変えていくので、その際にこのコマンドで状態を確認していきましょう。

---
### ３つのエリア
Git でファイルの変更履歴を登録する過程には３つのエリアがあります。  
Git の操作の流れを理解をする上でとても重要な観点ですので、しっかり押さえておきましょう。  
Git はファイルを変更してもその内容がローカルリポジトリに反映されることはありません。  
変更したファイルを指定して、その変更内容をまとめて変更履歴に残すという流れになります。  
わかりやすく言い換えると、変更内容を記録に残したいファイルを撮影台（ステージングエリア）にあげて、  
撮影台に乗っている記録のキャプチャショットを撮るというイメージです。

1. 作業ディレクトリ  
ファイルの作成、更新、削除といった作業を行うエリアです。Gitリポジトリ内で何らかの変化があると Git はそれを検知してくれます。
1. ステージングエリア  
Git が検知した変化のうち、Gitの変更履歴に残したいものが置かれているエリアです。  
`git add`コマンドで記録したい変更履歴を撮影台（ステージングエリア）に上げることができます。
1. ローカルリポジトリ  
ファイルの変更履歴が蓄積されているエリアです。  
`git commit`コマンドで撮影台に乗っている乗っている残したい記録のキャプチャショットを撮ることができます。

![git-command-basics-1.png](../img/git-command-basics-1.png)

イメージだけではなかなか理解には至らないと思うので、実際に Git を操作して確認をしていきましょう。

---
### 変更内容をステージングエリアに追加する
新規追加・変更したファイルは `git add` コマンドでステージングエリアに追加することができます。  
コマンドの後ろにはステージングエリアに追加したいファイルのパスを指定します。
```
git add [編集したファイルのパス]
```

**DEMO**  
今回は sample.txt を新規で作成して、同ファイルをステージングエリアに追加してみましょう。
①ファイルを新規で作成してみよう
まずは以下のコマンドで sample.txt を作成します。  
```
touch sample.txt
```
続いて、作成したファイルに hello と書き込みます。
```
echo hello > sample.txt
```
`cat` コマンドで sample.txt に hello と書き込みができているかを確認してみましょう。
```
cat sample.txt
```
ここで一旦ステータスを確認してみましょう。
```
git status
```
`git status`コマンドを実行すると以下の結果が表示されます。
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	sample.txt

nothing added to commit but untracked files present (use "git add" to track)
```
着目する点は `Untracked files` です。  
これはまだ Git の管理下に置かれていないファイルがあることを意味します。  
 `Untracked files`の後ろに sample.txt があるので、このファイルがまだ Git の管理下に置かれていないということです。  
![git-command-basics-2.png](../img/git-command-basics-2.png)
Git の管理下に置かれるようにするには `git add` コマンドを実行する必要があります。

②ファイルのステータスを修正済にする
それでは、`git add` コマンドを実行してみましょう。
```
git add sample.txt
```
`git add` コマンドを実行すると、以下の内容が表示されます。
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   sample.txt
```
`git add` コマンドの実行前は **Untracked files** でしたが、実行後は **Changes to be committed** に変わりました。
これはファイルのステータスが修正済に変わり、コミットの対象になっていることを意味します。
今回は新しいファイルを Git に追加しようとしているため **new file:   sample.txt**と表示されています。
![git-command-basics-3.png](../img/git-command-basics-3.png)

---
### 変更内容をコミットする  
変更内容をステージングエリアに追加されていると、その変更内容を Git の履歴に追加できるようになります。  
この Git の履歴に追加する操作を**コミット**といいますが、コミットは以下のコマンドで実行することができます。
```
git commit
```
このコマンドはファイルそのものを保存しているのではなく、ファイルの変更履歴を保存することができるというところがポイントです。  
コミット時のスナップショットを撮って、その記録をローカルリポジトリに保存をするというイメージです。
![git-command-basics-6.png](../img/git-command-basics-6.png)

また、コミットの際に任意のメッセージを残すことができます。  
以下のコマンドのように、コマンドの後ろにオプション（`-m`）を指定して、その後に登録したいメッセージを入力します。  
実際の開発プロジェクトでは「このコミットでどのような対応を行なったか」をメッセージに残すことになります。  
なぜなら、大量のコミットのログの中から特定のコミットを探す作業が容易になり、
またチームメンバーにもどのような対応をしたのかを共有することもできるからです。
```
git commit -m "message"
```
{{% notice warning %}}
メッセージはクォーテーションで囲う必要があります。
{{% /notice %}}

**DEMO**  
今回は先ほど修正済（`git add` コマンドを実施済）となった sample.txt の新規追加する内容を Git の変更履歴に登録しましょう。  
コミットのメッセージには`first commit` と入力しましょう。（今回のメッセージは英語でしたが、日本語を入力することも可能です。）
```
git commit -m "first commit"
```
コマンドを実行すると以下のメッセージが画面に表示されます。
```
[master (root-commit) 5c670db] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 sample.txt
```
それでは、再度ステータスを確認してみましょう。
```
git status
```
コマンドを実行すると以下のメッセージが画面に表示されます。
```
On branch master
nothing to commit, working tree clean
```
コミットを行なったことにより修正済のファイルがコミット済となったため、`nothing to commit, working tree clean` と表示されます。

**DEMO**  
では、もう一つデモを試してみましょう。  
先ほどは新規ファイルを Git に登録して、そのファイルの内容を Git に登録しました。  
今度は既存ファイルの変更内容を Git に登録してみましょう。

まずは既存のファイル（sample.txt）に good と追記しましょう。
```
echo good >> sample.txt
```
`cat` コマンドで sample.txt に good と追記ができているかを確認してみましょう。
```
cat sample.txt
```
ここで一旦ステータスを確認してみましょう。
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sample.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
2行目の**Changes not staged for commit**はコミット対象の変更がステージングエリアにはないという意味です。  
5行目の**modified:   sample.txt**は sample.txt に変更があったことを意味します。  
最後の**no changes added to commit**は2行目と同じ意味で、コミットするものがないことを意味します。  
![git-command-basics-4.png](../img/git-command-basics-4.png)

それでは、`git add`コマンドで sample.txt の変更内容がコミット対象となるようにしましょう。
```
git add sample.txt
```
もう一度ステータスを確認してみましょう。
```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   sample.txt
```
![git-command-basics-5.png](../img/git-command-basics-5.png)
2行目が**Changes to be committed**に変わりました。これはステージングエリアにある変更がコミットできるようになっていることを意味します。

最後にコミットができるかを試してみましょう。  
先ほどのコミットと区別がつくようにコミットメッセージを `second commit` に変えておきましょう。
```
git commit -m "second commit"
```

---
### コミットログを確認する
Git はコミットした履歴（コミットログ）を以下のコマンドで確認することができます。  
```
git log
```
コマンドを実行すると以下のようなログが表示されます。
```
commit 0336368ff10d1f69849cd5beeda1cf1ed274bb6d (HEAD -> master)
Author: corgi9n <arapon1015@gmail.com>
Date:   Fri Mar 11 03:54:55 2022 +0900

    second commit

commit 5c670db6fc4a8d109a5e2724c421cd8105c2598f
Author: corgi9n <arapon@gmail.com>
Date:   Fri Mar 11 03:44:55 2022 +0900

    first commit
```
`commit 0336368ff10d1f69849cd5beeda1cf1ed274bb6d (HEAD -> master)`のうち、
`0336368ff10d1f69849cd5beeda1cf1ed274bb6d` はコミットのハッシュ値で、このハッシュ値で一意のコミットを特定することができます。
` (HEAD -> master)`は HEAD の内容を master ブランチに履歴を残したということを意味します。（この内容については応用編で解説します。）
`Author`は Git のコミットを残した Git アカウントが表示され、`Date`はコミットした日時が表示されます。  
さらに下にはコミットの際に残したメッセージが表示されます。

{{% notice info %}}
もし、`git log` コマンドを実行した後、表示されたログの下に `:` が表示されている場合は、
続けてコマンドを実行することができません。  
この場合は `q` を入力して Enter キーを押すことで再度コマンドが実行できるようになります。
{{% /notice %}}

---
### 変更内容をリモートリポジトリに反映する
先ほどはコミットを完了して、ファイルの変更内容を無事コミットログに残すことができました。  
これでやりたいことが終わったように感じますが、まだやらなければならないことが残っています。  
チーム開発している場合はリモートリポジトリでソースコードを共有しているため、  
**ファイルを編集した場合はリモートリポジトリにアップロードして、チームメンバーと共有できるようにする** 必要があります。  
![git-command-basics-7.png](../img/git-command-basics-7.png)

変更内容（コミットログ）をリモートリポジトリにアップロードするには、  
`git push` コマンドを実行します。
```
git push origin [リモートリポジトリの名前] [リモートリポジトリのブランチ名]
```
**DEMO**
今回は以下のコマンドを実行して、リモートリポジトリの main ブランチにアップロードをしてみましょう。
```
git push origin main
```
コマンドを実行するとパスワードの入力を求められます。  
これは GitHub アカウントに対して2段階認証を設定したため GitHub アカウントのパスワードを求められています。  
GitHub アカウントのパスワードを入力して Enter キーを押しましょう。  
(入力したパスワードは目視で確認ができないため、誤入力に気をつけましょう。)

無事コマンドを完了できたら、GitHub上でアップロードされたファイルを確認してみましょう。

---
### リモートリポジトリから最新の履歴を取得する
先ほどは `git push` コマンドでリモートリポジトリに変更内容を反映いたしました。  
リモートリポジトリが更新されると、他のメンバーはリモートリポジトリから最新のソースコードをダウンロードすることになります。  
(もちろん、他のメンバーがリモートリポジトリを更新したら、あなたも最新のソースコードをダウンロードすることになります。)
![git-command-basics-8.png](../img/git-command-basics-8.png)
リモートリポジトリからソースコードをダウンロードする場合は、`git pull` コマンドを実行します。
```
git pull [リモートリポジトリの名前] [リモートリポジトリのブランチ名]
```
**DEMO**  
今回はリモートリポジトリ上に main ブランチしかないため、以下のコマンドを実行しましょう。  
ただ今回はローカルリポジトリの内容をアップロードしたばかりのため、`git pull` コマンドを実行してもローカルリポジトリに変化はありません。
```
git pull origin main
```
`git pull` コマンドを実行することでローカルリポジトリが変わる内容は、応用編で登場しますので楽しみにしてください！
