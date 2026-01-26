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

# Day 2

## 打标签

`git tag (-l/-list)` -> 列出当前已有的标签列表
`git tag -l/-list <通配符查找>` -> 列出符合查找结果的标签列表
`git show <tagname>` -> 展示tag的信息

### git的标签类型：
- lightweight 轻量标签：只提供标签的信息。
- annotated 附注标签： 附注标签是存储在 Git 数据库中的一个完整对象， 它们是可以被校验的，其中包含打标签者的名字、电子邮件地址、日期时间， 此外还有一个标签信息，并且可以使用 GNU Privacy Guard （GPG）签名并验证。
- 通常会建议创建附注标签，这样你可以拥有以上所有信息。

#### 轻量标签
`git tag <tagname>` -> 给当前节点打上标签
#### 附注标签
`git tag -a <tagname> -m <message>` -> 给当前节点打附注标签，且附上一段信息。（若不加-m，git也会启动编辑器让你输入message

`git tag <tagname> <commit>` -> 给指定提交打标签

### 推送标签
git在推送时不会把标签自动push。需要显式地推送。
`git push <remote> <tagname>` -> 把标签推送到远程仓库
`git push <remote> --tags` -> 推送所有不在远程仓库的标签

### 删除标签
`git tag -d <tagname>` -> 删除本地标签
`git push origin --delete <tagname>` -> 删除远程仓库中的某个标签

## 命令的别名
`git config --global alias.<aliname> <command>` -> 给command设置一个别名
- git的别名是简单的命令替换，用aliname替代后面的command
- 可以用来给旧命令起别名，也可以用来给组合命令形成新命令：使用`git config --global alias.<aliname> '<commands>'`
- 对于外部命令的别名，在命令前加入'!'符号，例如`git config --global alias.visual '!gitk'`,这样就可以用`git visual`来执行`gitk`命令了。

# Day 3
## 分支
- 分支的本质： 一个指向“commit”对象的指针
`git branch <name>` -> 创建一个分支
`git checkout <name>` -> 切换到某个分支



`git log --oneline --decorate --graph --all` -> 输出你的提交历史、各个分支的指向以及项目的分支分叉情况。
`git checkout -b <newbranch>` -> 创建并转到新的分支

`git branch -d <branch>` -> 删除分支
`git merge <branch>` -> 将目标分支与现有分支合并

### 合并的冲突处理
`git status` -> 可以查看处于“未合并”(unmerged)状态的文件

出现冲突的文件会包含一些特殊区段，看起来像下面这个样子：
```
    <<<<<<< HEAD:index.html
    <div id="footer">contact : email.support@github.com</div>
    =======
    <div id="footer">
     please contact us at support@github.com
    </div>
    >>>>>>> iss53:index.html
```
这表示 HEAD 所指示的版本（也就是你的 master 分支所在的位置，因为你在运行 merge 命令的时候已经检出到了这个分支）在这个区段的上半部分（======= 的上半部分），而 iss53 分支所指示的版本在 ======= 的下半部分。 为了解决冲突，你必须选择使用由 ======= 分割的两部分中的一个，或者你也可以自行合并这些内容。
例如，你可以通过把这段内容换成下面的样子来解决冲突：
```
<div id="footer">
please contact us at email.support@github.com
</div>
```
上述的冲突解决方案仅保留了其中一个分支的修改，并且 <<<<<<< , ======= , 和 >>>>>>> 这些行被完全删除了。 在你解决了所有文件里的冲突之后，对每个文件使用 git add 命令来将其标记为冲突已解决。 一旦暂存这些原本有冲突的文件，Git 就会将它们标记为冲突已解决。