# Git

初始化仓库 git init

#### 一、添加文件到暂存区

+ git add xxx.txt： 提交指定文件到暂存区
+ **git add .** ：提交所有被修改的文件。
+ git add -u：提交所有被修改和被删除的文件，不包括被删除的文件。

---

#### 二、将暂存区的文件添加到版本库

+ **git commit -m "xxx"**：将暂存区的文件提交到当前分支，-m后面是此次修改的修改信息。
+ git commit -a -m "xxx"：将工作区的文件跳过暂存区，全部提交到版本库。

---

#### 三、显式各种信息

+ **git status**：显式哪些文件已暂存，未暂存，未被跟踪，被删除，被修改，被添加。
+ git status -s ：git status更简短的显式。
+ git log：显式全部commit历史记录。
+ git reflog：显式commit操作历史记录以及reset操作回退记录。
+ **git log --pretty=oneline**：以一行的形式显式commit历史记录。

---

#### 四、版本回退

+ git reset --hard head^：head代表最新版本，^代表从最新版本往前回退一个版本，几个^就代表回退几个版本。
+ git reset --hard head~n：n代表从head开始往前回退n个版本。
+ **git reset --hard 6ab09**：跟版本号，代表回退到指定的版本(每个版本都有一个版本号，可以通过git log看到)。

---

#### 五、比较区别

+ git diff：比较工作区和暂存区的修改。
+ git diff head：比较工作区和上一次commit后的修改。
+ git diff --cached：比较暂存区和上一次commit后的修改。

---

#### 六、撤回操作

+ git restore xxx.txt：撤回某个文件在工作区的全部修改，也等同于git checkout -- xxx.txt。
+ git restore --staged xxx.txt：把暂存区的修改撤销掉，让这个文件重新放回工作区，此命令也等价于git reset head xxx.txt。
+ git restore . || git resotre --statged .  ：撤回全部，对应上面两个。
+ git rm --cached xxx：将git管理的xxx文件变为未跟踪的状态。
+ git rm -r --cached . ：将git管理的所有文件变为未跟踪的状态。

---

#### 七、远程仓库

+ **git remote add origin https://gitee.com/QH2021/gitstudy.git**：关联一个远程仓库，以后就可以将本地的操作远程提交到这个仓库，远程仓库的别名是origin。
+ git push -u origin master：用git push将本地的操作推送到远程，实际是把master分支推送到远程，第一次推送加上-u，将本地master与远程的master分支关联，以后推送或拉取就可以简化命令。

git remote add origin xxxxx一般是先有本地库，再有远程库，将远程库与本地库关联，再将本地库推送到远程库。如果从零开发，最好先创建远程库。

+ **git clone https://gitee.com/QH2021/gitstudy.git**：使用git clone 地址，就可以将远程仓库克隆到本地了，git支持多种协议，如https、但ssh最快。
+ git remote rm xxx: 删除远程xxx分支。

```js
/*
warning: ----------------- SECURITY WARNING ----------------
warning: | TLS certificate verification has been disabled! |
warning: ---------------------------------------------------
warning: HTTPS connections may not be secure. See https://aka.ms/gcmcore-tlsverify for more information.
warning: ----------------- SECURITY WARNING ----------------
warning: | TLS certificate verification has been disabled! |
warning: ---------------------------------------------------
warning: HTTPS connections may not be secure. See https://aka.ms/gcmcore-tlsverify for more information.
*/

//如果在git push 时出现以上信息，用git config --global http.sslVerify true
```

---

#### 八、分支

+ **git switch -c xxx**：创建并切换到xxx分支。与git checkout -b xxx效果相同。
+ git branch xxx：创建一个xxx分支。
+ git switch xxx：切换到xxx分支。与git checkout xxx效果相同。
+ git branch：查看当前分支。
+ **git merge xxx**：将xxx分支合并到当前分支。
+ **git branch -d xxx**：删除xxx分支。
+ git branch -D xxx：强制删除xxx分支。xxx分支没有被合并的话，用 -d会被提示，还没有合并，不会被删除
+ git log --graph --pretty=oneline --abbrev-commit：查看分支合并情况。
+ git merge --no-ff -m "merge with no-ff" xxx：禁用Fast-forward的形式合并xxx分支到当前分支，并且做一次提交。

---

#### 九、bug分支

在dev分支上出现了bug，可以创建一个bug分支用来解决bug，解决了以后再合并到dev分支，然后删除掉bug分支，但是有一个问题就是，如果此时我dev分支上的代码还没写完，不能提交上去，这时可以用git stash将状态暂存起来，等到以后恢复。

+ **git stash**：将工作区与暂存区的文件暂存起来，git status提示没有修改，这时就可以切换分支了。
+ git stash list：可以查看暂存起来的stash列表。
+ git stash apply：恢复最近一次的状态。
+ **git stash pop**：恢复并删除最近一次的状态。
+ git cherry-pick xxx版本号：将指定提交的版本号合并到这个分支。

---

#### 十、多人协作

+ git remote：查看远程库的信息，git remote -v可以查看详细信息。
+ **git push origin xxx**：推送xxx分支到远程仓库。
+ git checkout -b xxx origin/xxx：创建远程xxx分支到本地。
+ **git pull**：拉取远程分支，如果失败了，是因为没有绑定本地分支与远程分支之间的联系，需要git branch --set-upstream-to=origin/xxx xxx，这个命令将远程的origin/xxx 与本地的 xxx联系，然后再git pull，就可以拉取代码了。

多人协作工作模式通常如下：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。