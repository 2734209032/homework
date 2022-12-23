#### 推送到远端

```js
1. HTTPS   ==> 直接用链接推送  推送完之后要输入账号密码   
2. SSH    ==> 推荐的方式，密钥对 。

私钥  本地电脑上
公钥  需要配置到github / gitee / gitlab 平台上
```

#### 打开gitee网站上，查看SSH，右下角怎么生成秘钥

```js
1. 生成密钥对 
https://gitee.com/help/articles/4181#article-header0

ssh-keygen -t ed25519 -C "xxxxx@xxxxx.com"   改一下邮箱

2. 将公钥配置到gitee/github平台上
cat ~/.ssh/id_ed25519.pub

3. 验证是否配置秘钥成功 
ssh -T git@gitee.com‘

4. 先移除原来的origin名称 
git remote rm origin 
git remote -v 查看 

5. 重新关联仓库
git remote add origin git地址 （ssh）

6. 第一次推送
git push -u origin master
```

#### 之后的每次推送

```js
推送 把本地（电脑上的修改的版本更新  同步到远端）
// 修改代码，修改之后
1. git add . 
2. git commit -m "msg"
3. git push 
```

## 分支 

#### branch

```bash
# 1. 查看分支
git branch  
# 2. 新建一个分支 
git branch 新分支名字  （基于当前的分支，创建一个新分支）
# 3. 切换分支
git checkout 分支名字
# 4. 简写 创建一个分支，并切换分支
git checkout -b 新分支的名字 

# 5. 合并 
# 1. 在其他分支上修改的内容，一定要记得提交更新（记录）
# 2. 合并之前 切换到master分支上合并
git merge 分支名字

# 6. 删除分支
git branch -d 分支的名字  不能自己删除自己

# 下载项目（拉项目）
git clone  项目地址 （SSH / HTTPS）
```

#### 合并冲突

```js
1. 产生的场景 不同的分支，对同一份文件，（同一个位置）做了不同的修改，再合并这两个分支的时候，就会产生冲突。conflict

2. 在新分支中 找一个文件 记下位置，修改代码，
git add .
git commit -m "提交"
（目前处于刚创建好的分支）

3. 选择一个要保留的分支代码  
保存之后，
git add .
git commit -m "解决了冲突"

// 1. 采用当前的更改  2. 采用传入的修改  3. 保留两个分支的修改  4. 比较变更
// 还可以手动操作  ===> 不要忘记了删除哪些  ==== >>>> <<<<<<
```

#### sourceTree的操作

1. #### 如果要根据master创建新分支,并切换到新分支上

![image-20221215145136521](imgs/image-20221215145136521.png)

![image-20221215145155681](imgs/image-20221215145155681.png)



#### 2. 切换分支

双击左边的分支 直接切换

#### 3. 合并分支

```js
1. 先双击master分支，回到master分支上 
2. 鼠标放在要合并到master的分支上，点击右键 ， 选择 ==> 合并到当前分支
```

#### 4. 删除分支

```js
选择要删除的分支，右键，删除分支。
```

## 远端分支

```js
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例   :重命名    原来名字:新名字
git push -u origin payment:pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化
git push -u origin payment
```

#### 推送本地的分支到远端

```js
1. 创建一个本地的分支并切换  local
2. 修改部分代码
3. git add . /  git commit -m "msg"
4. 本地这个local推送到远端 

git push -u origin 本地分支的名字:远端分支名字
git push -u origin local 
```

#### 将远端分支下载到本地

```js
1. 先删除本地的分支  
git branch -d 本地分支名字
2. git checkout 远端分支名字 
==> 下载远端分支，并切换到那个分支上去
```

#### 删除远端分支

```js
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称

# 示例
git push origin --delete pay
```

#### 实际开发的情况

```js
dev  开发环境
test 测试环境
master 主分支 （线上环境）

master-login --> 把这个分支的代码 合并到test分支上 ， 测试人员测试我们的代码功能等是否有问题

master-login  最后等待上线 。。  某个周五的晚上 
git push   ==》 把这个分支推送到远端仓库

gitlab 你的组长 帮你合并分支 
```



#### 去公司的第一天

```js
1. leader 给你分配邮箱，账号
2. leader 给你一个 gitlab的地址， 同时，配套给你邮箱和密码    zxd@公司名字.com  密码 
3. 用公司给的邮箱密码，登录gitlab
4. 配置SSH， 方式和我们今天讲的一样   
5. 需要你的leader给你一个访问项目的权限 ，如果没有，是拉不了代码的   git pull(下载)
6. git clone 项目地址  下载项目。
7. 熟悉代码 
```



```js
1. git status
2. git add .
3. git commit -m "update"
4. git push 
5. 新建分支，基于master新建分支并切换到那个分支
git checkout -b 分支名 
6. 合并分支  git merge 

推送到远端仓库的时候，远端仓库的地址 
git remote add origin 地址名 
移除它
git remote rm origin
git remote -v 查看关联上了哪个分支 

代码回退 
git reset --hard id  
git reflog 
git log --oneline
```

