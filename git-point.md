### ポイント
ローカルの状態と、リモートの状態を把握  
以下がわかると良いかも
#### 1 ローカル作成
githubからクローンしてローカルに持ってくる  
または  
新規フォルダを作成し、git initで.gitファイルを作成する  
※その場合、remoteの場所をaddする必要がある
#### 2 変更してpushする
#### 3 ブランチをマージする
自分は各ローカルフォルダ単位でgit設定されているため、  
フォルダごとにpushする接続先を変更することもできる  
→git remote -vで確認しながら行うと良い

## githubにアップするまでの手順
（参考：https://qiita.com/na4da/items/32c002b10abe5227f49c）
### ①git add .(ALL OR FILE NAME)
 →追加状況はstatusで確認する
### ②git commit -m"(MESSAGE)"
 →コミット時のメッセージ「-m」がないと変なことになる・・・
### ③git push origin HEAD(OR BRANCH NAME)
 →HEADにすると現在のブランチと同じ名前のブランチにpushする  
 →ブランチの確認をしながらpushする  
 →確認時にでてくるブランチ前（remotes/origin/）はつけない
## マージする時の手順

## リモート確認
※SSH接続できる状態で実行
### git remote -v
→リモートの接続先
### git remote set-url origin git@bitbucket.org:~.git
→接続先変更（bitbucket）
### git remote set-url origin git@github.com:~.git
→接続先変更（github）
#### git remote add origin git@github.com:~.git
→No such remote 'origin'の場合にaddする

## gitの現状確認
git config -l  
→ギットの設定状況確認  
git clone (SSH等のgitHubからもってきたURL)  
→ギットからローカルに取得する場合

# 以下、対象フォルダに移動してからコマンドを打つ
→lsコマンドでファイルの確認、cdコマンドで対象フォルダまで移動
## 困った時の対処法
### gitがロックされてしまった
同じリポジトリ内で同時に複数の操作が行われないようにするために作られる排他制御用のロックファイル  
がgit操作中にできる時がある。問題なければ消してしまう  
①対象のファイルを確認して  
ls .git/index.lock  
②ある場合は削除  
rm .git/index.lock
### gitでこんなエラーが出たら
nothing to commit, working tree clean  
→コミット済みで作業するものがない  
（コミットまで終わってて、pushだけが残っている場合もある）

## ブランチ
### git branch -a(-r)
→全部のブランチを確認
### git branch
→現在のブランチを確認　✳️が現在の状況  
```
例）  
$ cd hello-santaclaus  
$ git branch  
* (HEAD detached at origin/develop)  
  develop  
  main  
```
### git checkout origin/develop
→ブランチからチェックアウト（切り替え）
### git branch -d (btanch.name)
→ブランチの削除  
　（参考：https://qiita.com/mather314/items/a1536c52a2eb0426b2b5）
### git push --delete origin branch_name
→リモートブランチの削除

## bitbucktのSSH鍵登録
久しぶりにbitbucktさわったら、SSH鍵が前の端末（Air）だったので登録し直した  
①ssh-keygen  
②ファイルの保存先を指定（bitbucketって打ったつもりが  gitbucketになってて死んだ）  
③catで対象ファイルを開いて、SSH鍵をbitbucket側に登録  
④ssh -T git@bitbucket.org やったらつながってなくて  
```
(RSA) to the list of known hosts.  
git@bitbucket.org: Permission denied (publickey).  
```
⑤vi ~/.ssh/config　やって追記したらいけた
### ２つ目のGithubアカウントに対する設定
（参考：https://qiita.com/Mikenerian/items/481587d4e8d8db9c0382）  
①SSH鍵作ってGithubに登録  
②SSHが繋がらなくて、configに設定追加  
```
vim ~/.ssh/config  
Host github-sub.com  
  HostName github.com  
  IdentityFile ~/.ssh/github_private  
  User git  
```
③SSH接続を確認  
ssh -T git@github-sub.com  
④リモートの設定を変更でOK!!  
git remote set-url origin git@github-sub.com:~.git

## 除外ファイルを追加する
### gitignore
（参考：https://codeaid.jp/blog/gitignore/）