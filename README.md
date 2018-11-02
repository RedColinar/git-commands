# Git 工作流程及常用操作  

## [习题](practice.md)  

## [Markdown 语法](markdown-grammar.md)

## 工作流程  
`git clone username@host:/path/to/repository`  
`git branch`  
`git checkout -b <新的分支名>`  
`git add <filename>`  
`git commit -m "代码提交信息"`  
`git push origin <分支名>`  
`git pull`  
`git merge <分支名>`  
`git diff <source_branch> <target_branch>`  
`git branch -d <分支名>`  
`git log`

## 进阶
`git cherry-pick <sha>` 拣选， 从其他分支拣选一个提交，生成一个新的提交，提交到当前分支  
`git rebase <branch>`  
`git revert <sha>`  

## 常用操作详解  

### 在所有操作之前，要添加SSH key到gitlab  
SSH是一种非对称加密的网络协议，用于计算机之间的加密登录。  

```ssh-keygen -t rsa -C "你的email地址"```  

将 `.ssh/id_rsa.pub` 内容复制到 gitlab  

代码参数含义：  
-t 指定密钥类型，默认是rsa，可以省略。  
-C 设置注释文字，比如邮箱。  
-f 指定密钥文件存储文件名。  

### 添加用户信息  

`git config --global user.name "John Doe"`  
`git config --global user.email johndoe@example.com`  
`git config --global core.editor code`  

`--global` 参数可选  

### 检查当前文件状态  
```git status```  
要查看哪些文件处于什么状态，可以用 `git status` 命令
### 暂存已修改文件  
```git add```  
这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。  
将这个命令理解为“添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。  

```git add <file>```  
将指定的文件`<file>`加入暂存区。  

```git add .```  
用一个点`.`作为参数将所有的的修改加入暂存区。  
### 查看文件更改差异  
``` git diff```  
`git diff` 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。 所以有时候你一下子暂存了所有更新过的文件后，运行 `git diff` 后却什么也没有。  

```git diff --staged```  
如果要查看暂存过的文件差异,需要加上参数`--staged`。  
### 提交更新  
```git commit -m <commit message>```  
`<commit message>`填写提交的内容。在提交之前，请一定要确认还有什么修改过的或新建的文件还没有 `git add` 过，否则提交的时候不会记录这些还没暂存起来的变化。  
这些修改过的文件只保留在本地磁盘。 所以，每次准备提交前，先用 `git status` 看下，是不是都已暂存起来了， 然后再运行提交命令 `git commit`。  
### 查看提交历史  
```git log```  
默认不用任何参数的话，git log 会按提交时间列出所有的更新，最近的更新排在最上面。  

```git log -p -2```  
一个常用的选项是 `-p`，用来显示每次提交的内容差异。 你也可以加上 `-2` 来仅显示最近两次提交。  
### 撤销操作  
```git commit --amend```  
有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 --amend 选项的提交命令尝试重新提交，即修改上一次的提交信息。  
使用 `git commit --amend` 后需要用`git push -f` 来推送到远程仓库。  

```git reset HEAD <file>```  
假如你修改了两个文件并且想要将它们作为两次独立的修改提交，但是却意外地输 入了 ```git add .``` 暂存了它们两个，此时取消一个文件`<file>`的暂存用`git reset HEAD <file>`。  

```git checkout -- <file>```  
如果你并不想保留对文件`<file>`的修改，你可以将它还原成上次提交时的样子，即撤销对`<file>`的更改（不可恢复）。  

```git revert <sha>```  
还原，用一次新的commit来回滚之前的commit, 已经merge的分支，无法在merge到该分支  

### 从远程仓库中拉取  
```git fetch <remote-name>```  
此命令会将远程索引拉取到你的本地仓库,它并不会自动合并或修改你当前的工作。  

### 推送到远程仓库  
```git push```  
本地新建一个分支时，此时使用 `git push` ,会提示 `git push --set-upstream origin <branch>` 。  
此时应该使用 `git push --set-upstream origin <branch>` 或者 `git push -u origin <branch>`与远程分支建立追踪并推送，建立推送后就可以直接使用 `git push` 来进行提交。  
另一种方式是先使用 `git branch -u origin/branch ` 与远程分支建立追踪后，再使用 `git push`。  

### 分支与合并  
`git checkout <branch>`  
切换到某个分支。  

`git checkout -b <branch>`  
基于当前分支新建一个分支并切换到这个分支。  

 ```git pull <远程主机名> <远程分支名>:<本地分支名> ```  
 `git pull origin develop:branch` 取回远程 `develop` 分支，与本地`branch` 分支合并。省略`:branch` 默认和当前分支合并。  
 实质上，`git pull` = `git fetch` + `git merge`。  

 `git merge <branch>`  
 与branch分支合并，`git merge origin/<branch>` 与远程分支合并。  

 `git rebase <branch>`  
 rebase 意思为变基。`git rebase origin/<branch>`与远程分支合并。  
 `merge` 和 `rebase` 是合并不同分支代码的两种方式，各有优势。  

 `git rebase -i <sha>`  
 它将罗列出此提交之后的所有提交，然后可以对个个提交做对应的操作.
 `git rebase -i HEAD~2`  
 使用此命令来合并多个提交，`HEAD~2` 中的`2`表示显示将最近的两次，然后对两个提交进行操作，包括提交合并成一个提交。  
 使用后会出现类似如下界面：  
 >pick f7f3f6d changed my name a bit  
 >pick 310154e updated README formatting and added blame  

将第二个 `pick` 改为 `squash ` 或 `s` 后保存退出，即将两次提交合成一个。  
 或者使用 `git reset <sha>` 回退到某一次提交后，重新 `git commit -am <commit message>` 可以实现相同的效果。  

`git branch -vv`  
 查看分支关联关系  

`git branch -u origin/expand-view`  
 将当前分支与远程分支关联  

### 解决合并冲突  

>$ git merge iss53  
>Auto-merging index.html  
>CONFLICT (content): Merge conflict in index.html  
>Automatic merge failed; fix conflicts and then commit the result  

使用merge出现冲突时，会出现 `CONFLICT` ，后面提示冲突的文件，解决所有冲突后，使用`git add .` 将已解决的冲突添加到暂存并提交。  
如有需要，再使用`git commit --amend` 把暂存区的改动提交到上一次提交中。  

使用rebase出现冲突时，解决完冲突后，将冲突文件 `git add .` 到暂存区，需要 `git rebase --continue`。  
如果有了冲突后不想再进行rebase，可以使用`git rebase --abort`回到rebase执行前的状态。  

### Https和SSH互换
```git remote set-url origin <url>```  
`<url>` 填写Https或SSH地址  

### 别名alias  
如果不想每次都输入完整的 Git 命令，可以通过 git config 文件来轻松地为每一个命令设置一个别名。  
这里有一些例子你可以试试：

>$ git config --global alias.co checkout  
>$ git config --global alias.br branch  
>$ git config --global alias.ci commit  
>$ git config --global alias.st status  

  这意味着，当要输入 git commit 时，只需要输入 git ci。  
  随着你继续不断地使用 Git，可能也会经常使用其 他命令，所以创建别名时不要犹豫。  

  一个丧心病狂的别名：  
>git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  

看看效果：  
<img src="./assets/alias.png" align=center />  

### Log  
`git log --follow -p file`  
查看文件历史版本  

文件回退历史版本  
`git checkout <hash> <filename>`  
`git reset --hard history_id`  

### 储藏与清理
`git stash`  
`git apply`  
`git pop`  
`git stash list`  
`git stash apply stash@{1}`  
查看内容  
`git stash show stash@{1}`  
`git stash show -p stash@{1}`  

### gitignore  

通常我们会从gitignore网站上获取一份模板，然后再根据自己的需要进行更改  
[gitignore.io 地址](https://www.gitignore.io/)
  
_更加详细的git使用，[点这里。](https://git-scm.com/book/zh/v2)_

