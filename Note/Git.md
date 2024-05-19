# Git

---

> 分布式版本控制系统

- git学习网站 [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)

- git初始化

  - git Clone 克隆已存在项目
    - git Clone github链接
    - clone网络错误问题
    - 设置代理:7890 clash的代理端口号
      - git config --**global** http.proxy http:*//127.0.0.1:7890* 
      - git config --**global** https.proxy http:*//127.0.0.1:7890*
  - git init 将本地某个项目加入git管理
    - 如果新建的仓库,这个仓库的文件都是未被跟踪状态, 未被跟踪的文件不会加入版本控制
    - git add将状态改为已跟踪加入版本控制并且加入缓冲区

- 代码提交

  - git add 加入缓存区

    - git add. 操作当前目录所有文件

  - git commit -m "备注" 提交到本地仓库

    - 注意 如果直接输入git commit会打开vim让你填写备注,如果直接-m 备注不用打开vim
      - 输入i启动编辑模式开始输入
      - 输入esc退出编辑模式
      - 输入:wq保存内容  

  - git log 查看提交记录

    ![image-20230511214248026](https://raw.githubusercontent.com/1v10/Photo/main/photo/202405192217213.png)

    > commit 后面为此次提交id
    >
    > git reset --head 提交id 用来恢复到某次提交版本 
    >
    > --head:重置模式,会将工作空间,暂存区,仓库,全部重置
    >
    > head:当前活跃的分支

  - git push 提交到远程仓库

  - git branch 分支名根据当前分支状态创建分支,分支上提交代码不会影响主分支

    - git checkout 分支名 切换到该分支
    - git checkout -b 分支名 创建并切换到该分支

  - git pull拉取到工作目录

    - git fetch 拉取到本地仓库 执行git merge才会跟工作空间合并

  - git remote add upstream 改变merge分支']

  - originl:默认远端仓库名

- ### 基础命令
  
  - pwd:显示当前位置
  - ls:显示目录下所有文件
  - cd:切换目录,后面跟目录名是下一级,..是上一级
  - git config :设置配置文件
    - git config --global代表全局
    - git config --global user.name 用户名 设置用户名
    - git config --global user.email 邮箱 设置邮箱 
  
- 添加文件进缓冲区
  
  - git init 初始化当前文件夹 加入git控制
  - git add 文件名.后缀 提交到缓冲区,临时保存
    - git add 添加当前目录所有文件
  - git commit 提交到本地仓库  拥有历史记录
    - 会进入vim编辑器进行编辑提交备注
    - vim操作
      - i:进入编辑模式
      - esc退出编辑模式
      - :wq 保存并退出vim
    - git commit -m 消息 可以跳过vim编辑
  
- git log 查看提交日志
  
- ### 指令
  
  - git clone 拉取远程项目到工作空间
  - git push 从本地仓库提交到远程仓库
  - git init git初始化 当前文件夹设置为git文件夹
  - git status 查看当前文件状态
  - git add 加入暂存区
    - git add 文件名 指定文件加入
    - git add . 所有文件加入
  - git commit 提交本地仓库
    - git commit - m  "备注内容"
    - 提交时添加备注信息
  
- git push  提交到远程仓库
  
- ### 忽略文件

  - 将一部分本地配置文件或者不想提交的文件进行忽略配置

  - 主目录新键.gitignore文件,按照语法进行配置即可

    ![image-20230319181403577](https://raw.githubusercontent.com/1v10/Photo/main/photo/202303191814723.png)



- git提交到远程仓库时需要生成公钥, 注册到对应远程仓库,比如github,gitee

- 关于设置后仍然无法 clone和push 需要设置git代理
  
  - [Git - SSL_ERROR_SYSCALL 问题解决 | hyperzsb's ideas](https://hyperzsb.io/posts/git-ssl-error/)
  
- 命令: ssh-keygen -t rsa

- 会自动生成在用户名/.shh目录下
  
  - ![image-20230319185546591](https://raw.githubusercontent.com/1v10/Photo/main/photo/202303191855630.png)
  
- git branch 分支名称 创建分支

- git checkout 分支名称 切换到该分支

- git checkout -b 分支名称 创建并切换到该分支

- git checkout commitID 让HEAD指向某次提交记录

  - commitID:提交记录的ID hash值 sha算法
  - HEAD:变量 默认指向当前分支的最新提交记录

- 多条提交记录合并:

  - https://juejin.cn/post/7050705771218075684

    git rebase -i commitId(该提价记录之后的提交记录进行合并)

    ![img]()

    命令名称+commit hash +comment

    \#则是提示说明

    Pick:保留该提交记录 缩写p

    Squash:与前一个commit合并 缩写s

    这里使用的是Vim编辑器!

    VIM:https://www.freecodecamp.org/chinese/news/vim-editor-modes-explained/

    git rebase合并提交记录 :https://juejin.cn/post/7050705771218075684

     Enter:进入编辑模式

    :q! 强制退出不保存

    :wq 保存后退出

    :wq! 强制保存后退出
    
     之后会进行编辑注释 提交即可

- Cherry pick 将指定的提交记录提交到其他分支

  - git cherry-pick commitid
  -  Git cherry-pick commitID 可以写多个ID 以空格分开

- 交互式rebase

  rebase加参数--interactive (-i)

  增加了该参数 git会打开一个UI界面列出可以被复制的备选提交记录 会显示Hash值

   这个UI可以做几件事:

  1.调整提交记录的顺序 通过鼠标拖放

  2.删除不想要的提交 通过切换PICK来完成

  3 合并提交

   如果有多次提交记录 需要只把某一次提交记录提交的主分支 那么就需要用到

  Git rebase - i

  Git cherry-pick

   git commit --amend 修正提交记录

   Git merge git rebase 要合并的分支或者提交记录

- 恢复

  - git reset commitID:直接退回到某次提交记录 抹除本次提交历史

  - git revert commitID: 增加一次提交 提交内容为想恢复的提交记录 会留下恢复历史

  - 假设有A,B,C三次提交 A为最新想要撤销

    撤销提交

    git reset HEAD~1 当前引用指向了B 恢复到了B的版本

    此时A就消失了 相当于改写了历史 

    于是最好使用另一个命令

    先把HEAD移动某次想恢复的提交记录上

    git revert 该命令就是在提交一次新提交D 而这个D与上一个B内容相同 只是留下了履历

    本地就用git reset 

    远程就用gir revert

    后面可以跟提交记录 也可以用HEAD

- HEAD 指向分支和提交的指针有什么区别?

  - HEAD 是一个特殊的指针，它指向当前所在的分支或提交。 当 HEAD 指向分支时，它指向该分支的最新提交，表示当前所在的分支。在这种情况下，如果进行提交，该分支将会移动到新的提交上，并且新的提交将成为分支的最新提交。 当 HEAD 指向具体的提交时，它指向一个特定的提交，而不是分支。这种情况被称为"分离 HEAD"。在分离 HEAD 的状态下，如果进行提交，将创建一个匿名分支，该分支不与任何命名分支关联，因此新的提交不会影响其他分支。这种情况下直接在分离 HEAD 上提交可能会导致提交被遗忘，因为没有其他分支引用该提交。 总结起来，HEAD 指向分支时表示当前所在的分支，而HEAD 指向提交时处于分离 HEAD 状态，表示当前位于一个特定的提交上，没有与该提交相关联的分支引用。

- git 远程操作

  - git clone
  - main 本地仓库
  - origin/main  远程仓库名/远程分支名  origin默认为远程仓库的名称 缩写o
    - 远程分支本质上用来反应远程仓库对应分支的状态   远程分支反映了远程仓库在你**最后一次与它通信时**的状态
  - 如果在本地直接切换到远程仓库 那么HEAD不会指向远程仓库 会成为分离HEAD 此时所有的提交都会提交到一个匿名分支 不会与其他任何分支有关联

- git fetch

  - 远程分支本质上用来反应远程仓库的状态   但是不会自动更新 可能会与远程有所差别 那么单独更新远程仓库分支 就需要用到git fetch
  - 当远程仓库获取数据时 远程分支也会更新以反应远程仓库的状态 
  - 本质上git fetch就是将本地仓库的远程分支更新成远程仓库对应分支的最新状态
  - git fetch不会更改你本地仓库的状态 也不会更新你本地的main分支 也不会修改磁盘上的文件
  - git fetch 只是单纯将更新下载下来了 并没有合并
  - 适用git fetch 将更新下载到了远程分支上 我们只需要将该远程分支上的更新合并到本地仓库的分支即可 比如适用 git merge

- git cherry-pick 针对于单个提交

- git rebase 和git merge针对整个分支的提交

- git pull

  - = git fetch + git merge

- git push

  - 与git pull相反
  - push有一些行为设定 与push.default文件有关

- 一般会在 feather的特性分支上工作!

- rebase和merge的优缺点

  - rebase整洁 但是由于会修改提交树 会将提交记录早的记录放在晚的记录之后
  - rebase会有多个提交合并 但是会保留提交历史

- 远程仓库分支与本地远程仓库分支关联

  - 本地分支是如何与远程分支关通过remote tracking进行关联

  - git clone时会将这种关系进行绑定 

  - git clone时首先会把远程仓库中分支都会在本地仓库创建对应远程分支

    然后会默认创建一个本地分支main用来跟踪本地的远程分支

  - 所以 git clone时 会输出 local branch "main" set to track remote branch "o/main"

  - 这种隐式关联会设置push目的地和pull的目标

- 指定remote tracking

  - git checkout -b feature origin/main
    - 此时创建一个分支feature 它跟踪 远程分支 origin/main
  - git brnach -u origin/main 在当前分支执行该命令 就会让当前分支追踪origin/main

- git push remote-name  local-branch-name

  - 想将本地更改推送都某个远程分支 但又不想切换分支 或者是游离HEAD状态 push时指定远程和分支名称进行推送
  -  git push origin(远程仓库名称) main(本地分支名称) 将main改动推送到到 origin仓库main分支中
  - 可以在分离HEAD下使用

- git push remote-name  local-branch-name: remote-branch-name

  - git push origin  feature:main
  - push也可以指定远程仓库的具体分支  比如上面就是将本地分支feature推送到远程的main分支  
  - 本地分支可以使用相对引用只提交一部分记录 feature^  
  - 如果指定的远程分支不存在 那么就会创建

- 本地的远程分支其实叫远程追踪分支

  - git clone 会把远程分支的快照保存到本地
  - 在 Git 中，本地仓库和远程仓库是分开管理的。当你克隆一个远程仓库时，Git 会在本地保存远程仓库的快照。这包括所有分支和标签。本地对远程的追踪是通过 "远程追踪分支" 实现的。

- git fetch 指定参数拉取 跟push类似 但方向相反

  - git fetch origin main :会到远程仓库的main分支进行拉取然后放到本地的o/main上
    - 该拉取只会下载对应本地远程分支更新 并不会下载其他远程分支  而且也不会合并的对应分支上
    - git fetch默认下载所有远程分支的更新
  
- git fecht origin main:feature  会到远程仓库的main分支拉取并且放到本地的o/feature分支上 如果feature不存在 则会进行创建
    - 拉取指定分支 合并到指定分支
  - git push 指定参数的危险用法!
    - git push origin  :foo   把空推送到foo分支 这会删除远程分支foo!
    - git fetch origin   foo:  这会在本地创建foo分支
  - git pull本质上就是在git fetch后面加git merge 所有参数通用
    - git pull origin foo = git fetch origin foo + git merge origin/foo
    - git pull origin bar-1:bugfix = git fetch origin bar~1:bugFix + git merge bugFix
  - git pull 最终会合并到当前分支里
  - git pull origin main:feature
    - 如果feature不存在则会创建 然后拉取main分支最新 然后把合并到feature里面 然后再合并到当前分支
  - 文件的几种状态
    - Untracked:未跟踪 指在工作目录存在 但不在上一次的快照记录 也不再之前的提交中 也没有在忽略列表中
    - Tracked:已跟踪 已经纳入了版本控制的文件 存在于上一次的提交快照中 这些文件的状态可以是 未修改  已修改 或者已经放入暂存区
      - Unmodified 未修改   自上次提交以来没有修改
      - Modified 已修改 针对一个已经跟踪的文件进行了修改 但还没有提交到暂存区 文件状态未已修改 但还没有准备好提交
      - Staged 已暂存
        - 执行git add命令后 标记为已暂存 已经将新的变动包含在下一次提交中 整个阶段的信息存储在暂存区
  - 工作目录:用户实际操作和编辑文件的地方
  - git 暂存区 是存在于工作目录和git仓库之间的中间层 用来存储你准备好到下一个提交中的更改  就是组织你即将提交的更改的地方
    - git add就是把文件加入暂存区 代表 我认为这些已经准备好称为下一个提交的一部分了
  - 当执行git commit会将暂存区内容转到仓库 生成一个新的快照 提交的内容是暂存区的内容 而不是工作目录 如果你修改了文件而没有git add 则不会提交
  - 暂存区容许用户检查他们即将提交的更改
  
- git 仓库

  - 存储项目和所有历史版本的地方

- GIT客户端为什么可以直接提交不用git add?

  - 因为git用图形界面让你选择你想要提交的文件 无论是新增还是修改 删除 这一步本质上就在执行git add 但在用户界面上是一个选择 并非添加动作

- git config --list可以查看当前git配置

  - git config  --global user.name ''
  - git config --global user.email ''
    - global  用户配置 针对不同用户设置
    - systeam 系统配置 所有用户
    - project   项目配置

- git 配置第三方比较软件

  - 需要体现配置该软件的Path路径

  - #### 1、配置merge工具

     git config --[global](https://so.csdn.net/so/search?q=global&spm=1001.2101.3001.7020) merge.tool winmerge

     git config --global mergetool.winmerge.path "C:\Program Files (x86)\WinMerge\WinMergeU.exe"

    #### 2、配置diff工具

     git config --global diff.tool winmerge

     git config --global difftool.winmerge.path "C:\Program Files (x86)\WinMerge\WinMergeU.exe"

  - 使用方式

    - git mergetool 文件名
    - git difftool 文件名 
    
  - [ChatGPT Next Web](https://chatgpt.nextweb.fun/#/chat)
  
  - https://beta.cdn.api.sa.ai.bkgc.tech/v1
  
  - sk-tJXZtqBofV0GYjYf2c371e3f5zhanglongqiang3A94e39Ad5aC40e940aC4C0
  
- 关于不同状态恢复代码

    - 没有add添加进版本控制
        - checkout 文件名 检出最新的该文件丢弃本地修改
        - checkout . 检出所有
    - 已经add添加进暂存区 已暂存状态 staged 但还没有commit
        - reset HEAD 文件名
        - reset HEAD . 重置当前所有目录
        - reset --hard 重置所有
    - 已经commit到本地仓库
        - reset --hard commitID 
        - revert  commitID 会产生一个新提交 撤回之前的变更

 