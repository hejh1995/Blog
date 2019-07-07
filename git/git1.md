# git

<a name="nMLJm"></a>
### 简介：
1. 版本控制系统：
  1. 集中式：版本库集中 放在‘中央服务器’上，比如 SVN。最大的缺点是必须联网工作，网速慢的时候，要等很久。![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559291260557-f92a0712-e3fd-4b2a-acff-65adbfd4f41a.png#align=left&display=inline&height=149&name=image.png&originHeight=297&originWidth=411&size=59140&status=done&width=205.5)
  1. 分布式：每台电脑都是一个 完整的版本库，工作时就不需要联网了。没有‘中央服务器’， 但是有一个 用来 方便大家‘交换’各自的修改 的‘中央服务器’。                                        ![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559291247784-35141c35-c1cc-4c95-95a6-dd51d95ca786.png#align=left&display=inline&height=217&name=image.png&originHeight=433&originWidth=504&size=104972&status=done&width=252)
2. 下载：git 官网 [https://git-scm.com/downloads](https://git-scm.com/downloads)
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

3. 版本库：又名 仓库（repository），这个文件会被git 管理起来，以便追踪历史版本。
- 创建一个空的仓库：

```
$ mkdir empty
$ cd empty
$ pwd   // 显示当前目录
/Users/juanhong/gitLearn/empty
$ git init  // 把这个目录变成 git 可以管理的仓库。
Initialized empty Git repository in /Users/juanhong/gitLearn/empty/.git/
// 此时会多出一个 .git 的目录，这是git 用来跟踪管理版本的，千万不要修改这个目录里的内容。
```

- 把文件添加到 版本库：
  - 将文件放在 仓库下（子目录也可以）， 然后：

```
$ git add . / git add <file>
$ git commit -m "我是本次提交的说明，一定要输入有意义的内容哦，可以方便的从历史记录找到改动记录"
```
<a name="dvluI"></a>
### 时光机穿梭：

1. git status ： 可以查看工作区的状态，如果有修改可以使用 git diff <file> 来查看修改了什么。
1. 版本回退：
- git log ， 可以显示 从最近到最远的提交日志，会显示比较全的信息，所以可以使用 git log --pretty=oneline, 结果：
```
3c86380056aa95268ea679d82ea7154c4428c65f (HEAD -> master) second

c7ffbf2591f20d6357e2fc798033fb1c3be2db00 first

(commit的id commit的注释) 
```

- 在 git 中 HEAD 表示 当前版本，也就是最新提交的版本，上一个版本是 HEAD^ ,后面的用 HEAD~100。
- 回退：git reset --hard HEAD^ / git reset --hard 3c86380056  (commit 的 id 可以不写全，git 会自动去找) 
- 如果之前的版本，不知道 commit id了， 可以使用 git reflog, 它会记录你的每一次操作，可以查到之前操作的 commit id。
- 为什么版本切换这么容易呢：git 的内部 有个指向当前版本的 HEAD 指针，回退版本的时候，只是将 指针的指向改变，并顺便把工作区的文件更新了。
3. 工作区和暂存区：
- 工作区（working directory）：在电脑里能看到的目录。
- 暂存区：
  - 版本库（repository）：在工作区内，有一个隐藏的.git 目录，这个不算 工作区，是git 的 版本库。
  - 版本库内存放了很多东西，最总要的 就是 暂存区（stage）、主分支 master 、 以及HEAD。

        ![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559295870612-f3cb36b8-fae8-43d1-aee4-3cc4fa3fdf76.png#align=left&display=inline&height=171&name=image.png&originHeight=234&originWidth=458&size=48549&status=done&width=334)

4. 管理修改：
- 每次修改，如果不用 git add 添加到暂存区，commit 的时候就不会加入到 分支 中。
5. 撤销修改：
- git checkout -- <file>  把文件 在工作区的修改全部撤销。
  - 如果这个文件没有被添加到  暂存区，撤销修改就回到和版本库一样的状态。
  - 如果这个文件以及被添加到  暂存区，又做了修改，撤销修改就会回到添加暂存区后的状态。
  - 如果想把已添加到 暂存区 的 文件撤回，要用 git reset HEAD^，然后如果要继续撤销 工作区的修改，使用 git checkout -- <file>
6. 删除文件：
- 确定 从版本库 删除文件，可以使用 git rm <file> ，并且 git commit 。(不用 git add .)
- 如果删错了，可以使用git  checkout -- <file>。（git checkout ， 其实使用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以‘一键还原’）
<a name="GrCan"></a>
### 远程仓库：

1. git 是分布式 版本控制系统，同一个git 仓库，可以分布在不同的机器上，而且它们之间没有主次之分。
1. github 注册后，可以得到一个git 远程仓库。
1. 使用 git push 命令，可以把当前分支 推送到远程。
1. git clone 地址， 可以从远程仓库克隆 一个仓库。
<a name="CfJnm"></a>
### 分支管理：

1. 创建与合并分支
- git 会把每一次的提交 都串成一条时间线，也就是一个分支。
- 主分支是 master 分支，HEAD 指向 master，master 指向提交。每次提交一次，master 分支就会向前移动一步。
- 创建分支，并切换到分支时， HEAD 指向 分支， 分支窒息那个提交，提交一次，分支指针就会移动一步，而master 指针不变。
- 合并分支的时候，把 master 指向 分支的当前提交，就完成了合并。
- 删除分支，就是删除分支指针。
- 创建分支，只是增加一个分支指针，改变HEAD 的指向，工作区的文件都没有任何变化。合并分支也只是改改指针。

```
git checkout -b dev  // 创建并切换到dev 分支
git branch   // 查看分支
git add .  
git commit -m ''  
git checkout master  // 切换到 主分支
git merge dev // 合并 dev 分支 到祝分支
git branch -d dev  // 删除 dev 分支
```


2. 解决冲突
- 在将 分支 合并 到 主干的时候，因为版本的问题可能会发生冲突，发生冲突后，冲突文件会用 `<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容。

例： 

```
$ git merge dev2
  Auto-merging a.txt
  CONFLICT (content): Merge conflict in a.txt
  Automatic merge failed; fix conflicts and then commit the result.
$ cat a.txt
  dsss
  <<<<<<< HEAD
  wo shi master!s`
  =======
  wo shi zai dev shang mian xiu gai de
  wo shi dev2!
  >>>>>>> dev2
////////////  修改冲突后！
$ git add .
$ git commit -m '1'
[master 56fa90e] 1
$ git merge dev2
Already up to date.

```


- （        合并前                     -----                     冲突解决后）
- ![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559307208361-5fa19334-ccf9-4782-88cb-507255f117ec.png#align=left&display=inline&height=136&name=image.png&originHeight=272&originWidth=425&size=13888&status=done&width=212.5)![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559307216441-b3007035-8451-41a7-af5c-370531210f9f.png#align=left&display=inline&height=136&name=image.png&originHeight=272&originWidth=551&size=15969&status=done&width=275.5)
- 可以用git log --graph 命令看出分支合并图。
3. 分支管理策略
- git merge ，默认开启 fast forward ，删除分支后 ，分支信息会丢失， 看不出来曾经做过合并。
- 可以使用 git merge --no-ff -m ’merge‘ dev（dev 为 分支名），git 会在merge 的时候生成一个新的 commit，这样，可以在分支历史上看出分支信息(git log --graph --pretty=oneline --abbrev-commit)。
- 分支管理原则：
  - master 分支 应该是 非常稳定的， 仅用来 发布新版本，平时不能在上面干活。
  - 干活在dev 分支上，它是不稳定的，到某个版本发布的时候，再把 dev 分支 合并到 master 上。
  - 每个人都在dev 上面干活，每个人都有自己的分支，时不时往分支上合并就可以了。![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/216540/1559372736565-602d3894-013b-4303-9cfd-f1084b2893e3.png#align=left&display=inline&height=106&name=image.png&originHeight=125&originWidth=498&size=13198&status=done&width=422)
4. bug分支
- 场景：正在 dev 分支 开发，突然有bug需要修改，但是不想commit 当前的代码，可以保护现场，然后新建分支修改bug，修复完再切换到当前现场继续开发。
- git stash   // 将当前工作现场 ’储藏‘起来。注意，新增加的文件，需要 git add , 最好在 stash 之前，用git status 查看状态。
- 修改 bug 并 merge 后，切换到当前分支， git stash list // 可以查看 工作现场。
- git stash pop  // 恢复 工作现场的 内容，并删除 stash 中的内容。或者 可以 git stash apply 先恢复，然后使用 git stash drop 删除。
- 使用 git stash apply 可以恢复特定的工作区：
```
$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
$ git stash apply stash@{0}
```

<br />5. feature分支
- 开发一个新的 功能，最好新建一个 feature 分支，在上面开发、完成后，合并，最后删除。
- 强制删除一个 分支 git branch -D dev2 (普通删除是 -d)
6. 多人协作
- git remote // 可以查看 远程库的信息
- git remote -v  // 显示更详细的 远程库 信息
- git push  远程库 分支名 // 把 该分支上的 所有本地 提交到远程库。
- 哪些分支需要推送：
  - `master`分支是主分支，因此要时刻与远程同步；<br />
  - `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；<br />
  - bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；<br />
  - feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
- 多人写作的工作模式（通常）：
  - 首先，可以试图用`git push origin <branch-name>`推送自己的修改；<br />
  - 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；<br />
  - 如果合并有冲突，则解决冲突，并在本地提交；<br />
  - 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！<br />
  - 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

7. rebase :[https://www.liaoxuefeng.com/wiki/896043488029600/1216289527823648](https://www.liaoxuefeng.com/wiki/896043488029600/1216289527823648)
<a name="YfW46"></a>
### 标签管理：

1. 创建 标签：
- git tag 'tag' // 打标签，默认是打在 最新提交的 commit 上的， 可以使用 $ git log --pretty=oneline --abbrev-commit 查看详情：

```
f62d4f5 (HEAD -> master, tag: tag1) tag
7520103 (tag: v1.0) merge dev
f2ebe27 (tag: tag-dev, dev) dev
c27cae9 (dev3) dev3
```

- 将标签打在 特定的某个commit 下（commit 后忘记打标签） git tag 'tag1' commitid
- 可以使用 git tag 查看标签，是按照字母顺序排列的，不是按时间排序的哦~
- git show <tagname> ，查看标签信息， 显示 commit 的信息。
- 还可以创建 具有说明的 标签， git tag -a <tagname> -m "" <commit id>
- 标签总是和某个 commit 挂钩，如果这个 commit 既出现在master 分支，又出现在 dev 分支，name在这两个分支 都可以看到这个标签。
2. 操作标签
- 删除标签： git tag -d <tagname>   // 没有推动到远程的，直接可以在本地安全删除。
- 推送某个标签到远程：git push origin <tagname>
- 推送 所有 尚未 推送到远程的本地标签：git push origin --tags
- 标签已经推送到 远程， 需要删除： git tag -d <tagname>  （先从本地删除， 然后从远程删除）git push origin :refs/tag/<tagname>
<a name="3mujF"></a>
### 自定义Git：

1. 忽略特殊文件
- 某些 必须 放在 git 工作目录的文件，但又不能提交他们，就需要在提交时被忽略。
- 忽略文件为 .gitignore， 这个文件 本身要放在版本库里，并且可以对 它 做 版本管理。
- GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore
- 强制添加 被忽略的文件， git add -f <filename>
- 查看不能提交文件 是什么原因导致的：

```
$ git check-ignore -v ignore.txt     // git check-ignore -v <filename>
.gitignore:2:ignore.txt	ignore.txt   // 在 .gitignore 的第 2 行
```


2. 配置别名
-  --global ， 是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
```
git config --global alias.st status //  以后， st 就表示 status 
```

- git 的简写，在  .oh-my-zsh/plugins/git/git.plugin.zsh 文件下，可以用 cat .oh-my-zsh/plugins/git/git.plugin.zsh 查看。
- 搭建git 服务器：[https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)

