---
title: "GitHub の基本"
date: 2022-03-16T07:38:25+09:00
weight: 3
---

### GitHub とは
ソフトウェア開発のプラットフォームであり、ソースコードを共有するためのホスティングサービス（サーバーの領域を貸し出すサービス）です。  
先述したリモートリポジトリはこのサービスが提供してくれます。

GitHub のサーバー上にソースコードを格納することで、チームメンバーとソースコードを共有してコードレビューを行ったり、プロジェクトの管理を行ったりすることができます。  
使用用途も様々で、チームメンバーのみがアクセスできるようにすることもできれば、オープンソースとして提供するために世界中のエンジニアにアクセスしてもらえるようにすることもできます。  
名称に Git が含まれている通り、GitHub のバージョン管理システムには Git が使用されています。

### GitHub を始めてみよう
#### GitHub アカウントを作成しよう
GitHubを利用するためにはアカウントを作成する必要があります。  
以下の手順に沿って GitHub アカウントを作成しましょう。  
`注意：GitHub アカウントを作成するにはメールアカウントが必要になります。`  
1. GitHub の公式サイトにアクセスしましょう。  
https://github.com/  
2. 画面右上の Sign up をクリックしましょう。
![github-basics-1.png](../img/github-basics-1.png)
3. メールアドレスを入力後、Continue ボタンをクリックしましょう。
![github-basics-2.png](../img/github-basics-2.png)
4. パスワードを入力後、Continue ボタンをクリックしましょう。  
※パスワードは任意の内容でOKです！
![github-basics-3.png](../img/github-basics-3.png)
5. ユーザーネームを入力後、Continue ボタンをクリックしましょう。
![github-basics-4.png](../img/github-basics-4.png)
6. 入力したメールアドレス宛に GitHub から認証コードが送られます。  
届いた認証コードを画面に入力しましょう。  
![github-basics-5.png](../img/github-basics-5.png)
7. ここからは個人設定となりますが、必須事項ではないので割愛します。  
画面下部の Skip personnnaization をクリックしましょう。  
![github-basics-6.png](../img/github-basics-6.png)
8. 以下の画面が表示されればアカウントの作成は完了です！
![github-basics-7.png](../img/github-basics-7.png)

#### リモートリポジトリを作成しよう
GitHub アカウントがあれば GitHub 上にリモートリポジトリを作成することができます。  
次の手順に沿って作成してみましょう。  
1. GitHubにログイン後、Create repository ボタンをクリックしましょう。
![github-basics-8.png](../img/github-basics-8.png)
2. 以下の画面が表示されましたら、以下の手順でリモートリポジトリを作成しましょう。  
    1. リポジトリの名前を設定しましょう。今回は `tutorial` としましょう。 
    2. 他のユーザーがリポジトリにアクセスできないように非公開にしましょう。  
       `Public` を選択すると世界中の GitHub ユーザーがアクセスすることができます。  
       `Private` を選択するとリポジトリを作成したアカウントのみがアクセスすることができます。  

![github-basics-9.png](../img/github-basics-9.png)
3. 以下の画面が表示されればリモートリポジトリの作成は完了です！
![github-basics-10.png](../img/github-basics-10.png)

**Point: チームメンバーのみにリモートリポジトリを共有したい場合**  
`Private` を選択することで他の GitHub ユーザーはアクセスできなくなりますが、チームメンバーにはアクセスできるようにしたいですよね。  
このようなときは GitHub のリポジトリへ招待する機能を使いましょう。  
1. 招待したいリモートリポジトリの画面で Setting を選択しましょう。
2. Settings 画面の左側に表示されているメニューから Collaborators を選択しましょう。
3. Add people ボタンをクリックしましょう。  
4. 入力欄に GitHub のユーザーネーム（またはメールアドレス）を入力して、招待したいユーザーを選択しましょう。

#### ファイルをアップロードできるようにしよう
GitHub上にリモートリポジトリを用意できましたら、次はファイルをアップロードができるようにしましょう。  
GitHub にファイルをアップロードするための通信手段として、HTTPSとSSHの2種類から選ぶことができます。
HTTPSはデータをそのまま送っているのに対し、SSHは暗号化した上で送るためセキュリティの観点からSSHで通信を行うことを推奨します。  
また、HTTPSとSSHとではそれぞれ設定の手順が異なりますので注意しましょう。  

**HTTPS通信の場合**  
HTTPS通信でファイルをアップロードするには**アクセストークン**が必要になります。  
このアクセストークンは GitHub の設定画面で発行することができます。
次の手順に沿って作成してみましょう。
1. 画面右上のアイコンをクリックしてしてメニューを表示します。
2. メニュー内の「Settings」を選択します。  
![github-basics-11.png](../img/github-basics-11.png)
3. 「Settings」画面のメニュー内の「Developer settings」を選択する。
![github-basics-12.png](../img/github-basics-12.png)
4. 「Developer settings」画面のメニュー内の「Personal accesstoken」を選択する。
![github-basics-13.png](../img/github-basics-13.png)
5. 「Personal accesstoken」画面内の「Generate new token」ボタンをクリックします。
![github-basics-14.png](../img/github-basics-14.png)
6. Note に任意の文字列を入力し、画面最下部にある「Generate token」ボタンをクリックします。
![github-basics-15.png](../img/github-basics-15.png)
7. 発行されたアクセストークンをコピーしましょう。
![github-basics-16.png](../img/github-basics-16.png)
8. ファイルをプッシュする際にコピーしたアクセストークンをペーストして実行しましょう。

**SSH通信の場合**  
SSH（Secure SHell）通信は送信しているデータを暗号化していることが特徴です。  
クライアントマシン（例えば、皆さんのPC）で秘密鍵と公開鍵を生成し、公開鍵を送信先の GitHub に設定することでSSH通信を行うことができます。  
そして、GitHub 側は設定したアカウントと公開鍵を紐づけて管理することになります。
次の手順に沿って作成しましょう。
1. 秘密鍵と公開鍵を格納するフォルダに移動しましょう。
ホームディレクトリの直下にある`.sshフォルダ`の直下に秘密鍵と公開鍵を置くことができます。  
以下のコマンドで`.sshフォルダ`に移動しましょう。
    ```
    cd ~/.ssh
    ```
    `.sshフォルダ`がない場合は以下のコマンドで削除した上で移動しましょう。  
   ```
   mkdir ~/.ssh
   ```
2. 秘密鍵と公開鍵を生成しましょう。
以下のコマンドで秘密鍵と公開鍵を生成することができます。
   ```
   ssh-keygen -t rsa
   ```
   コマンドを実行すると以下の３点を確認されます。
   ①秘密鍵と公開鍵のファイルの名前
   ②秘密鍵と公開鍵のパスフレーズ
   ③秘密鍵と公開鍵のパスフレーズの再確認  
   以下のメッセージが表示されますが、必須の設定ではないためEnterキーをクリックすることでスキップすることができます。
   ```
   Generating public/private rsa key pair.
   Enter file in which to save the key (/Users/(username)/.ssh/id_rsa):
   Enter passphrase (empty for no passphrase):
   Enter same passphrase again:
   ```
3. 秘密鍵と公開鍵が生成されたことを確認しましょう。
lsコマンドで以下の２ファイルが生成されていることを確認しましょう。  
   - id_rsa
   - id_rsa.pub

   生成されたファイルのうち、id_rsa が秘密鍵、id_rsa.pub が公開鍵になります。  
   公開鍵である id_rsa.pub の内容を GitHub に設定することになります。
4. 公開鍵を GitHub に設定しましょう。
    1. 「Settings」画面のメニュー内の「SSH and GPG keys」を選択しましょう。
    2. 「SSH and GPG keys」画面内の「New SSH key」ボタンをクリックしましょう。
    3. コマンドで公開鍵の内容をコピーしましょう。  
        【Macの場合のコマンド】
        ```
        pbcopy < ~/.ssh/id_rsa.pub
        ```
        【Windowsの場合のコマンド】
        ```
        clip < ~/.ssh/id_rsa.pub
        ```
    4. 2. で表示した画面の Title に秘密鍵のファイル名を入力し、Key に 3. でコピーした内容を貼り付けましょう。
    5. 「Add SSH key」ボタンをクリックしましょう。
5. SSH接続ができているかを確認しましょう。
  次のコマンドでSSH接続ができているかを確認することができます。
  ```
  ssh -T git@github.com
  ```
  以下のメッセージが表示されれば接続は成功しています。
  ```
  Hi (account名)! You've successfully authenticated, but GitHub does not provide shell access.
  ```
  接続がうまくいかなかった場合は手順通りに行えていないところがある可能性があるので、もう一度見直してみましょう。
