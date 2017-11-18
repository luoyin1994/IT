# git配置别名
## st标识status，ck表示checkout，cm表示commit，br表示branch等
```
    git config --global alias.st status
    git config --global alias.ck checkout
    git config --global alias.cm commit
    git config --global alias.br branch
    //撤销暂存区的修改
    git config --global alias.unstage "reset HEAD"  
    // 显示最近一次的提交
    git config --global alias.last "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit -1" 
    git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

## 参考文档
* [配置别名 - 廖雪峰](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375234012342f90be1fc4d81446c967bbdc19e7c03d3000)