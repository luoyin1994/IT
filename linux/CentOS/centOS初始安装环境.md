# centOS初始安装环境
## centOS 7
### update yum
```
    yum update
```
### vim
```
    yum install vim
```
### git
```bash
    yum install git
```
### [nvm]( https://github.com/creationix/nvm)
```bash
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh| bash
```
```
    # 添加以下到~/.bashrc
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```
### node、npm
```
    nvm install node # install the lastest release of node
```
### 总步骤
```
    yum update
    yum install vim git -y
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh| bash
    nvm install node
```