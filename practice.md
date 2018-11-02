# Git 练习

## 提交流程  
1. 在本地安装 git 工具， 配置 git 客户端的用户名和邮箱

2. 登录 http://192.168.1.9/ ， 每个开发的账户已经分配好，用户名 姓名拼音小写，密码 nugget2008，选择性重置密码， 查看自己所在的小组， 和自己所在的项目， 以及自己的账号所拥有的权限  

3. 生成 ssh key 并保存到自己 gitlab 所在的账户  

4. 使用 ssh 的方式将 http://192.168.1.9/panqiang/gitpractice 克隆到本地  

5. 使用 `git checkout -b branch-1` 在 gitpractice 仓库中切一个新分支， branch-1 是分支的名字， 完成后使用 `git branch` 查看本地存在的分支， 使用 `git branch -d branch-1` 删掉刚才新建的分支 branch-1， 删除成功后使用 `git checkout -b branch-xxxx` 再次新建一个分支， xxxx 为个人姓名拼音小写

6. 用 `branch-xxxx` 分支在仓库 `/folder` 文件夹下新建一个文件, 命名格式为 `file-xxxx.txt`, xxxx xxxx 为姓名拼音小写, 同时用自己喜欢的编辑器修改 `/folder/file.text` 文件， 在其中加上三行文字， 文字格式不限， 更改后使用 git status 查看仓库状态  

7. 使用 `git add .` 将上一条的两个改动（新增一个文件，改动一个已存在的文件）加到暂存区， 用 `git commit -m '提交信息'` 写上提交信息，提交到本地仓库  

8. 使用 `git log` 查看提交的日志, 记录上一次的提交 id `<sha>`， 按下 `q` 或 `shift + 两次 z` 退出 log 页面， 使用 `git show <sha>` 查看提交的内容  

9. 使用 `git reset <sha>` 撤回上一条的提交， 将上一次的提交从本地仓库撤回工作空间， 使用 `git status` 查看此时仓库状态， 查看后再次操作第 7 条，将改动提交到本地仓库  

10. 使用 `git push` 将该分支和分支内的改动提交到远程仓库（当远程没有本地对应的分支时， git 会提示使用 git push --set-upstream， 根据提示将该分支提交到远程仓库） 保证远程仓库可以看到自己提交的分支   

11. 在 gitlab 上发起一次 merge request， 填上 merge 描述， 将自己切出的分支 `branch-xxxx` 请求合并到主干（master）上， 并 assign 给潘强  

## 解决冲突流程  

12. 在本地仓库中， 从分支 `master` 切出两个分支 `branch-2` 和 `branch-3`, 具体操作为，先 `git checkout master` , 再使用 `git branch branch-2`, 接着使用 `git branch branch-3`  

13. 在分支 `branch-2` 上修改 `/folder/file.text`， 修改后提交到本地仓库。 同样的，在分支 `branch-3` 上修改 `/folder/file.text`， 修改后提交到本地仓库， 修改内容与 `branch-2` 避免相同, 以此来制造代码冲突  

14. 第13题的准备工作做完后， `git merge branch-2` , 会提示有冲突， 查看冲突的内容后， 使用 `git merge --abort` 撤销本次 merge。 再次使用 `git merge branch-2`， 解决冲突后，使用 `git commit -am '解决冲突'` 将解决冲突的代码进行提交    

15. 重复执行一次第13题， 在分支 `branch-3` 上使用 `git rebase branch-2`, 提示冲突， 使用 `git rebase --abort` 撤销变基， 撤销后再次使用 `git rebase branch-2` ，解决冲突后使用 `git add .` 和 `git rebase --continue` 结束变基  

