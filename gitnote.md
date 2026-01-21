# Day 1

## 一个基础的git仓库

### 创建第一个git仓库！
`git init` -> 在目录下创建.git文件
`git add <file>` -> 将想要添加的文件放入暂存区
`git commit -m <name>` -> 将暂存区文件生成为一个名为\<name>的commit

### 克隆一个仓库！
`git clone <url>` -> 克隆链接地址的仓库
`git clone <url> <filename>` -> 克隆并自定义仓库的名字

### 记录仓库的更新！
git中文件状态有：
- 未追踪，已追踪(**track**)：表示纳入git管理与否
- 未更改，已更改(**modified**)，已暂存：`未更改` ---`修改文件`---> `已更改` ---`暂存文件`---> `已暂存` ---`提交文件`---> `未更改`

`git status` -> 查看所有文件状态
`git status -s(or --short)` -> 简短模式
`git add <file>` -> 追踪一个新文件，或将更改的文件加入暂存区
`git diff` -> 未暂存的文件和已暂存的文件之间的差异
`git diff --staged(or --cached)` -> 已暂存的文件和上一次提交的文件的差异

### Commit!
`git commit` -> 呼出commit面板，填写message
`git commit -m "<message>"` -> 直接填写message并提交
`git commit -a` -> 将所有已追踪文件暂存并提交（省略add）
 
提交成功后会弹出信息：
```
[当前提交分支 完整SHA-1校验和],
n file changed, m insertions(+), k deletion(-)
```

### 移除与重命名文件
`git rm <file>` -> 删除文件
`git rm --cache <file>` -> 将文件移除出git管理，但不删除
`git mv <file_from> <file_to>` -> 将文件重命名

### 查看提交历史
`git log` -> 查看文件的更改历史
- `-p/-patch`：强调每次提交引入的差异
- `-2`：显示最近两次提交
- `--stat`：总结显示
详见：https://git-scm.com/book/zh/v2/Git-%e5%9f%ba%e7%a1%80-%e6%9f%a5%e7%9c%8b%e6%8f%90%e4%ba%a4%e5%8e%86%e5%8f%b2#pretty_format

### 撤销操作
##### 重新提交

`git commit --amend` -> 将暂存区提交，并替代上一次提交
（用于提交后发现有小错误需要更改的情况，能够精简仓库历史）

##### 撤销

`git reset HEAD <file>` -> 取消file的暂存记录
`git checkout -- <file>` -> 将file还原为上次提交的状态

**注意：** git上几乎所有已提交的内容都是可恢复的，然而未提交的内容删除时需要十分谨慎，因为很可能难以恢复！


## 远程仓库的操作

`git remote` -> 查找当前目录的远程仓库服务器
- 选项`-v`：显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。
```
origin https://github.com/flagqvq123/gitstudy_note.git (fetch)
origin https://github.com/flagqvq123/gitstudy_note.git (push)
```

- 简写可以替代url使用

`git remote add <shortname> <url>` -> 添加远程服务器，并且指定一个简写
`git fetch <remote>` -> 访问远程仓库，拉取其中没有的数据
- **注意：** 并不会自动合并或修改当前的工作，需要手动添加合并

`git pull` -> 若当前分支设置了追踪远程分支，则可以自动抓取并合并该远程分支到现有分支。

`git push <remote> <branch>` -> 将某分支推送到指定服务器
- 推送时必须与服务器其他工作相同才能推送。

`git remote show <remote>` -> 列出远程仓库URL、跟踪分支、在本地使用pull、push指令会导致的推送。

`git remote rename <name1> <name2>` -> 改变远程仓库简写名
- 注意这个操作也会改变远程跟踪分支前缀

`git remote remove <name>` -> 移除远程仓库