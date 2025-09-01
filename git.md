> 常用命令
{ .is-info }

# 回退
```git
// 查看 commit 记录 拿到 hash
git log

// 回退指定版本
git reset <hash>
```

# 查看全局配置 
```git
git config --global --list

// 查看指定属性
git config --global user.name
```

# 仓库地址配置
```git
// 添加远程仓库
git remote add origin <地址>

// 修改远程仓库
git remote set-utl origin <地址>

// 删除远程仓库地址
git remote remove origin
```

# 分支
```git
// 查看所有分支
git branch -a

// 查看当前使用分支
git branch

// 切换分支
git checkout <分支名称>
```