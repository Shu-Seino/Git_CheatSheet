# Git_CheatSheet
# GitHubコマンド
## イメージ図
![](/img/github.png)
## ローカルリポジトリの新規作成

```bash
git init
```

## Gitリポジトリのコピーを作成する

リモートリポジトリからローカルへ

```bash
git clone <リポジトリ名>
```

## 変更をステージに追加

```bash
git add <ファイル名>
git add <ディレクトリ名>
git add .
```

## 変更を記録する（コミット）

ステージからリモートリポジトリへスナップショットを記録

```bash
git commit
git commit -m "<メッセージ>"
git commit -v
#空のコミット
git commit --allow-empty -m  "<メッセージ>" 
```

| | |
| --- | --- |
| -m | CLI上でコミットメッセージを書ける。 |
| -v | 変更内容の差分を表示 |

## 現在の変更状況を確認する。

```bash
git status
```

## 変更差分を確認する

```bash
# git addする前の変更分
git diff
git diff <ファイル名>

# git addした後の変更分
git diff --staged
```

## 変更履歴を確認する

```bash
git log

# 一行で表示する
git log --oneline

# ファイルの変更差分を表示する
git log -p index.html

# 表示するコミット数を制限する
git log -n <コミット数>

# グラフにして表示する
git log --graph
```

## ファイルの削除を記録する

```bash
# ファイルごと削除
git rm <ファイル>
git rm -r <ディレクトリ>

# ファイルを残したいとき
git rm --cached <ファイル>
```

## ファイルの移動を記録する

```bash
git mv <旧ファイル> <新ファイル>

# 以下のコマンドと同じ
mv <旧ファイル> <新ファイル>
git rm <旧ファイル>
git add <新ファイル>
```

## リモートリポジトリ（GitHub）を新規追加する

```bash
git remote add origin https://github.com/<ユーザ名>/<リポジトリ名>.git
```

## リモートリポジトリ（GitHub）へ送信する

ローカルリポジトリからリモートリポジトリへ

```bash
git push <リモート名> <ブランチ名>
git push origin main
```

## コマンドにエイリアスを付ける

```bash
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co commit
```

## 管理しないファイルをGitの管理から外す

```bash
.gitignoreファイル
# 指定したファイルを除外
index.html
# ルートディレクトリを指定
/root.html
# ディレクトリ以下を除外
dir/
# /以外の文字列にマッチ「*」
/*/*.css
```

## ファイルへの変更を取り消す

ローカル環境のワークツリー内の変更を取り消す。

```bash
git checkout -- <ファイル名>
git checkout -- <ディレクトリ名>

#全変更を取り消す
git checkout -- .
```

## ステージした変更を取り消す

ステージした状態を消すだけなので、ワークツリー内の変更はない。

```bash
git reset HEAD <ファイル名>
git reset HEAD <ディレクトリ名>

# 全変更を取り消す
git reset HEAD .
```

## 直前のコミットをやり直す

リモートリポジトリにpushしたコミットはやり直してはいけない。

```bash
git commit --amend 
```

## リモートを表示する

```bash
git remote
# 対応するURLを表示
git remote -v
```

## リモートリポジトリを新規追加する

```bash
git remote add <リモート名> <リモートURL>

git remote add hoge https://github.com/<ユーザ名>/<リポジトリ名>.git
```

## リモートから情報を取得する（フェッチ）

fetch→ローカルリポジトリ→merge→ワークツリー

```bash
git fetch <リモート名>
git fetch origin
```

## リモートから情報を取得してマージする（プル）

```bash
git pull <リモート名> <ブランチ名>
git pull origin main
# 上記コマンドは、省略可能
git pull

#同じ
git fetch origin main
git merge orgin/main

```

## リモートの詳細情報を表示する

```bash
git remote show <リモート名>
git remote show origin
```

## リモートを変更・削除する

```bash
# 変更する
git remote rename <旧リモート名> <新リモート名>
git remote rename hoge new_hoge

# 削除する
git remote rm <旧リモート名> <新リモート名>
git remote rename new_hoge
```

## ブランチを追加する

```bash
git branch <ブランチ名>
git branch feature
```

## ブランチの一覧を表示する

```bash
git branch

# 全てのブランチを表示する
git branch -a
```

## ブランチを切り替える

```bash
git checkout <既存のブランチ名>
git checkout feature

#ブランチを新規作成して切り替える
git checkout -b <新ブランチ名>
```

## 変更履歴をマージする

```bash
git merge <ブランチ名>
git merge <リモート名/ブランチ名>
git merge origin/main
```

## ブランチを変更・削除

```bash
# 作業しているブランチ名を変更
git branch -m <ブランチ名>
git branch -m new_branch

# ブランチを削除する
git branch -d <ブランチ名>
git branch -d feature

#強制削除する
git branch -D <ブランチ名>
```

## リベースで履歴を整えた形で変更を統合する

ブランチの基点となるコミットを別のコミットに移動する。

```bash
git rebase <ブランチ名>
```

## プル型のリベース

mergeのコミットが残らないので、GitHubの内容を取得したいときだけ使う方法。

リモートリポジトリ→fetch→ローカルリポジトリ→rebase→ワークツリー

```bash
git pull --rebase <リモート名> <ブランチ名>
git pull --rebase origin main
```

## プルをリベース型に設定する

```bash
git config --global pull pull.rebase true

# mainブランチでgit pullするときだけ
git config branch.main.rebase true
```

## 複数のコミットをやり直す

```bash
git rebase -i <コミットID>
git rebase -i HEAD~3

pick 3ee3651 add:file
pick 7bbf693 Create README.md
pick 366aa90 add:dir

```

```bash
# やり直したいcommitをeditにする。
edit 3ee9251 add:chapter3.3
pick 7bbe693 Create README.md
pick 366aa32 add:file

# やり直したら実行する
git commit --amend

# 次のコミットへ進む（リベース完了）
git rebase --continue
```

## コミットを並び替える・削除する

```bash
git rebase -i HEAD~3

pick 3ee3651 add:file
pick 7bbf693 Create README.md
pick 366aa90 add:dir

# 削除したり、順番を入れ替えたりできる。
pick 7bbf693 Create README.md
pick 3ee3651 add:file
```

## コミットをまとめる

```bash
git rebase -i HEAD~3

pick 3ee3651 add:file
pick 7bbf693 Create README.md
pick 366aa90 add:dir

# コミットを１つにまとめる。
squash 3ee3651 add:file
squash 7bbf693 Create README.md
pick 366aa90 add:dir
```

## コミットを分割する

```bash
git rebase -i HEAD~3

pick 3ee3651 add:file
pick 366aa90 add:dir
pick 7bbf693 README.mdとindex.htmlを追加

# コミットを１つにまとめる。
pick 3ee3651 add:file
pick 366aa90 add:dir
edit 7bbf693 README.mdとindex.htmlを追加

git reset HEAD^
git add README.me
git commit -m 'READEME.meを追加'
git add index.html
git commit -m 'index.htmlを追加'
git rebase --continue
```

## タグの一覧を表示する

```bash
git tag
```

## タグを作成する

```bash
git tag -a [タグ名] -m "[メッセージ]"
git tag -a 20230704 -m "version 20230704"

# 軽量バージョン
git tag [タグ名]
git tag -a 20230704

# 後からタグ付けをする
git tag [タグ名] [コミット名]
 8a6hd8f
```

## タグのデータを表示する

```bash
git show [タグ名]
git show 20230704
```

## タグをリモートリポジトリに送信する

```bash
git push [リモート名] [タグ名]
git push origin 20230704

# タグを一斉送信
git push origin --tags
```

## 作業を一時避難する

変更分をstashに一時避難する。

```bash
git stash
git stash save
```

## 避難した作業を確認する

```bash
git stash list
```

## 避難した作業を復元する

```bash
# 最新の作業を復元する
git stash apply

# stageの状況も復元する
git stash apply --index

# 特定の作業を復元する
git stash apply [スタッシュ名]
git stash apply stash@{1}
```

## 避難した作業を削除する

```bash
# 最新の作業を削除する
git stash drop

# 特定の作業を削除する
git stash drop [スタッシュ名]
git stash drop stash@{1}

#全作業を削除する
git stash clear
```

## コンピュータにある全てのリポジトリ用にGitユーザ名、メールアドレスを設定する

```bash
# ユーザ名を設定
git config --global user.name "<ユーザ名>"
# メールアドレスを設定
git config --global user.email "<メールアドレス>"

#確認方法
git config --global user.name
git config --global user.email
```
## 単一のリポジトリ用にGitユーザ名、メールアドレスを設定する

```bash
# ユーザ名を設定
git config user.name "<ユーザ名>"
# メールアドレスを設定
git config user.email "<メールアドレス>"

#確認方法
git config user.name
git config user.email
```
## 既存のリモートリポジトリを新しいリモートリポジトリへ変更する。

```bash
git remote set-url origin <新しいリモートリポジトリURL>
```
