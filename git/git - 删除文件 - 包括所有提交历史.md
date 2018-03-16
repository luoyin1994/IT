# git 删除文件 - 包括所有提交历史
```
# 删除包括历史
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch 文件相对路径' --prune-empty --tag-name-filter cat -- --all
# 同步到远程
git push origin master --force
```

## 参考文档
- http://www.cnblogs.com/shines77/p/3460274.html
- [fatal: bad revision rm](https://mfreidge.wordpress.com/2016/04/25/bad-revision-rm-error-when-using-git-filter-branch-index-filter-if-called-from-batch-file/)
- [https://www.jianshu.com/p/58fef32a15bb](https://www.jianshu.com/p/58fef32a15bb)
- [git-filter-branch](https://git-scm.com/docs/git-filter-branch)
- [Git-工具-重写历史](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2)
