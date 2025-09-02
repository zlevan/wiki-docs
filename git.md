> 常用命令
{ .is-info }

# 回退
```js
// 查看 commit 记录 拿到 hash
git log

// 回退指定版本
git reset <hash>
```

# 查看全局配置 
```js
git config --global --list

// 查看指定属性
git config --global user.name
```

# 仓库地址配置
```js
// 添加远程仓库
git remote add origin <地址>

// 修改远程仓库
git remote set-utl origin <地址>

// 删除远程仓库地址
git remote remove origin
```

# 分支
```js
// 查看所有分支
git branch -a

// 查看当前使用分支
git branch

// 删除本地分支
git branch -d <分支名称>
  
// 删除远程分支
git push origin -delete <分支名称>

// 切换分支
git checkout <分支名称>
  
// 创建并切换到新分支
git checkout -b <分支名称>
  
// 修改本地分支名称
git branch -m <旧分支名称> <新分支名称>
  
// 合并分支
git merge --on-ff <需要合并分支名称>
```

# 更新
```js
// 同步远程仓库
git fetch

// 远程更新分支，并删除本地仓库中不存在余远程仓库的分支
git remote update origin --prune

// 强制覆盖远程仓库
git push -f origin <分支名称>
  
// 更改提交信息或者添加更多
git commit -amend -m '修改信息'

// 强制合并（需注意：没有冲突，且备份）
git pull origin <分支名称> --allow-unrelated-histories
```
















