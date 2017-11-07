* 在git服务器创建git裸仓库。假设创建于git用户的“~/git/”目录下。
```git
    # 仓库名称 storename.git
    git init --bare storename.git
```
* 进入“storename.git”目录， 进入“hooks”目录，githook（git钩子存在于其中，默认有“*.sample”样式的例子。如“update.sample”。）
```git
    cd storename.git
    # 可以看到“*.sample”等例子”
    cd hooks  
``` 
---
* 在开发机上“clone”该裸仓库（未明确指出时，现在及以下出现的“该裸仓库”均表示最开始在git服务器中创建的“storename.git”裸仓库）。
```git
    # git服务器主机地址yourhosturl
    git clone git@yourhosturl:git/storename.git
```

* 进行开发......
* 开发机向该裸仓库进行“push”操作。触发“pre-receive”