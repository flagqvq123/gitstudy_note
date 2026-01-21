# Day 1

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
[当前提交分支 完整SHA-1校验和]
n file changed, m insertions(+/-)
```