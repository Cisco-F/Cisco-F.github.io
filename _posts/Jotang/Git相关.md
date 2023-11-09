## Git相关

### .gitignore

使用`git config --global core.excludefile`查看全局gitignore文件

使用`git config --global core.excludefile ~/.gitignore`在全局配置中指定gitignore文件

***

在特定项目中，使用`touch .ignore`为其单独指定gitignore文件

文本编辑器打开.gitignore文件编辑：

```
#忽略备份文件
*~

#忽略编译结果
/build

#忽略特定文件
/<文件名>

#忽略特定文件夹（下的所有文件）
<文件夹>/

#忽略后缀
*.txt
```

****

更新规则时输入以下代码

```
#删除本地git仓库所有信息
git rm -r --cached .
#更新忽略规则
git commit -m 'update ignore rule'
#重新提交文件
git add .
```



