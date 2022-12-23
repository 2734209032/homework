#### 1. git

```js
VCS  version  control system 版本控制系统
git 开源的分布式版本控制系统

// 作用： 版本控制，存档
```

#### 2. 配置用户名和邮箱

```js
git config --global user.name "用户名"
git config --global user.email "邮箱"

查看配置
git config --list 
查看全局配置
git config --list --global
```

#### 3. 初始化仓库

```js
1. 新建一个空文件夹，  右键 git bash here 
2. ===>  git init 
```

#### 4. 查看文件的状态

```bash
git status  
# 简写 
git status --short 
git status -s

红色： 工作区     绿色： 暂存区

?? 文件未跟踪
A  文件刚纳入跟踪
M  表示文件已经修改了

```

#### 5. git add 

```js
// 1. 将未纳入跟踪（管理）的文件，纳入管理
git add 文件名 
git add .

// 2. 将修改后的文件，（工作区中），添加到暂存区 
git add .

// ==> git add . 
```

#### 6. 提交更新（存档，记录一个版本）

```js
只要commit之后，这次版本就永久的记录下来了 

git commit -m "本次提交的信息"

// 每次提交的时候 

工作区  --->  暂存区  ---> git仓库
git add . 
git commit -m "update"

===> 跳过暂存区， 前提是文件已经被git纳入跟踪管理
git commit -am "跳过暂存区" 


// 修改最近一次提交说明 amend修正
git commit --amend -m "修改最近一次提交信息"

// 1. 先修改文件 
// 2. git add .  / git commit -m "提交信息"
// 3. git commit --amend -m "修改提交信息"
// 4. git log --oneline 查看
```

#### 7. 查看历史提交记录

```js
git log  详细信息
git log -2 查看两条
git log --oneline  简洁的查看  ==> 推荐

// 如果回退到某个版本之后，还想切换另一个版本 查看所有的提交记录
git reflog 
```

#### 8. 回退指定版本

```js
1. 回退
git reset --hard 版本id   

2. 将暂存区的文件 移动到 工作区
git reset HEAD .  （所有的文件）
```

#### 9. 撤销对文件的修改

```js
// 用的很少 
// 就是将工作区的文件，用仓库中当前版本替换掉。
git checkout 文件名 
// 类似ctrl + Z
```

#### 10 将纳入git管理的文件移除

```js
// 将纳入git管理的文件变为未跟踪的状态

git rm --cached 文件名  // 一个文件
git rm --cached -r .   // 所有文件 
git rm -r --cached .  // -r的位置可以交换
```

#### 11. 忽略某些文件，不需要被git管理

```js
// 创建一个新的文件 sercet.js
1. 创建一个.gitignore 文件
2. 将不需要纳入git管理的这个文件，写到里面  # 表示注释
3. git add .
4. git commit -m "添加gitignore文件"
5. 再修改这个文件， git status查看一下状态

----
.gitignore 只忽略没有跟踪的文件 如果文件已经纳入git管理了，则修改.gitignore无效 

// 解决方案
1. 在gitignore文件中写需要忽略的文件信息
2. 让所有纳入git管理的文件，都变为未跟踪
git rm -r --cached .
3. git add .  重新添加到暂存区 ，再提交
4. 提交当前的更新，备注说明 （添加了gitignore）
```

#### 12 中文乱码解决

```js
// 解决git status中文显示问题
git config --global core.quotepath false

```

#### 13 小结‘

```js
1. 用户名和邮箱的配置
git config --global user.name ""
git config --global user.email ""

2. 初始化仓库
git init 

3. 查看状态
git status

4. 将修改的文件放到暂存区 
git add 文件名 
git add .   ==> 全部一起提交

5. 提交更新（存档）
git commit -m "本次提交的描述信息"

6. 查看历史记录
git log --oneline 
git reflog  查看所有的 

7. 回退版本
git reset --hard id
```

#### 14 VSCode 配置git bash

```js
// Ctrl + j  
// cmd + j

Ctrl + shift + p  ==> 输入 JSON 

// where git 
// path 修改为Git bash的路径

"terminal.integrated.profiles.windows": {
    "PowerShell -NoProfile": {
      "source": "PowerShell",
      "args": [
        "-NoProfile"
      ]
    },
    "Git-Bash": {
      "path": "D:\\Program Files\\Git\\bin\\bash.exe",  
    }
  },
"terminal.integrated.defaultProfile.windows": "Git-Bash",
```

#### 15  一些常见的命令

```bash
cd 文件夹名字  进入某个文件夹
cd ..  返回上一层       ./ 一个点表示当前目录 .. 上级目录

clear 清屏 （git-bash）
cls  清屏  window黑色终端 cmd中 

# 查看文件内容
cat 文件名
# 创建文件夹
mkdir 文件夹名  
# 创建文件
touch 文件名 

# 查看文件列表
ls 
# 显示当前目录
pwd


使用 Vim编辑器 修改内容


vi 文件名  
# 进入vim编辑模式 
进入这个模式之后， 按键盘 i   ==》 插入模式 可以输入内容

# 退出？
1. 按ESC 
2. shift+:  => 冒号（英文）

:q   不保存退出
:q!  不保存强制退出
:w   保存
:wq   保存并退出
:wq!  强制保存退出
```

