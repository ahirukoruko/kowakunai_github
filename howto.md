# セットアップ

## ターミナル

### 秘密鍵、公開鍵の作成と設定

鍵の名前(今回はed25519)を`-t`で指定して`ssh-keygen`を作る
```
$ ssh-keygen -t ed25519
```
~/.sshの中に公開鍵id_ed25519.pub、秘密鍵id_rsa.pubができる


公開鍵の中身を見る
```
$ cat id_ed25519.pub
ssh-ed25519 AAAA(略)
```
公開鍵をコピー

## github
Settings>Access>SSH and GPG keysからNew SSH keyを追加。TitleをつけてKeyのところにさっきコピーした公開鍵をペースト。

`sudo`を使って`vim`でssh_configを編集
```
$ sudo vim /etc/ssh/ssh_config
```
文章を追記

## ターミナル
### 鍵を使えるようにPC側の色々設定
```
$ git config --global user.email"githubメールアドレス"
```
```
$ git config --global user.name"githubユーザー名"
```

`sudo`から`vim`でssh_configを編集。
```
$ sudo vim /etc/ssh/ssh_config
```
下を追記(Personalの部分、及びパスは適宜変更すること)
```
Host github.com
        User git
        HostName github.com
        IdentityFile /Users/Personal/.ssh/id_ed25519
```
ちなみに`vim`の時編集したい時は<esc→i>\
保存して閉じたい時はinsertじゃない状態で<:wqを入力→enter>

完成！

# 2回目以降

## github

新規レポジトリを作成/既存レポジトリを開き、sshのURLを取得(↓みたいなやつ)
```
git@github.com:ユーザー名/レポジトリ名_github.git
```
## ターミナル

`git clone`でレポジトリをgithubから自分のpcに持ってくる
``` 
$ git clone (さっき取得したURL)
```

あげたい文章を書く！拡張子は`.md`\
ここでは例として以下test.mdとして書く。
```
$ touch test.md
```
でファイルができる(今いるディレクトリに注意)


testgit.mdを`git add`でgit管理の対象に
```
$ git add testgit.md
```
更新バージョン名intitという名前を`-m`で指定して`git commit`で追加
```
$ git commit -m "intit"
```
`git push`でアップロード
```
$ git push
```
完成！


