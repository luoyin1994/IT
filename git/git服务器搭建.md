# git 服务器搭建

## 搭建 git 服务 
### 实现免密登录
```bash
    # git用户下
    cd .ssh
    # chmod修改权限,保证在服务器.ssh/authorized_keys中添加了用户的公钥,可以实现免密登录
    mkdir .ssh && chmod 700 .ssh
    touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
```
### 批量导入公钥
```bash
    # user_keys/xxx/*_rsa.pub 存放的为每一个加在本linux用户下authorized_keys中的公钥
    cat user_keys/*/* > authorized_keys  # 批量写入保存的*_rsa.pub 
```
### 禁用shell登录（[git-shell为仅限Git-SSH访问的受限登录shell](https://git-scm.com/docs/git-shell)）
```git
    # /etc/passwd文件中
    # git:x:1001:1001:,,,:/home/git:/bin/bash
    # 改为
    # git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

## 参考文档
* [git官网 - 4.4 Git on the Server - Setting Up the Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)
* [廖雪峰 - 搭建Git服务器](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)