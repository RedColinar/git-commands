# git-commands
Common git commands  
  
查看文件历史版本
`git log --follow -p file`  
  
文件回退历史版本
`git checkout <hash> <filename>`  

`git reset --hard history_id`  

查看分支关联关系  
`git branch -vv`  
  
将当前分支与远程分支关联  
`git branch --set-upstream-to=origin/expand-view`  
  
安装一个 Debian 软件包，如你手动下载的文件  
`dpkg -i <package.deb>`  
