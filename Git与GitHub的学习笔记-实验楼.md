# Git与GitHub的学习笔记-实验楼

## 一、来历等无关紧要的东西

* Linus想要版本控制软件然后就改进了BitKeeper
* 2005年BitKeeper要收回版权，Linus就花10天写了Git
* 2007年三个年轻人觉得Git是个好东西，就搞了个GitHub

## 二、在GitHub上创建仓库

* 创建仓库

  > ![1570022298995](Git与GitHub的学习笔记-实验楼.assets/1570022298995.png)

* 注意 （忽略文件、选择所属协议）

  > ![1570022457809](Git与GitHub的学习笔记-实验楼.assets/1570022457809.png)
  >
  > 这两项作用之后再讲

## 三、安装、升级Git

* git版本查看

  ```shell
  git --version
  ```

* Linux下升级

  ```shell
  sudo apt update  # 更新源
  sudo apt install software-properties-common # 安装 PPA 需要的依赖
  sudo add-apt-repository ppa:git-core/ppa    # 向 PPA 中添加 git 的软件源
  ```

  > linux下升级可能会出错，这时候可能是Python版本问题，可以选择Python3.4：
  >
  > ```shell
  > sudo apt update  # 更新源
  > sudo apt install software-properties-common # 安装 PPA 需要的依赖
  > sudo add-apt-repository ppa:git-core/ppa    # 向 PPA 中添加 git 的软件源
  > ```

  > Windows下安装就直接去官网下载安装好了

## 四、克隆GitHub上的仓库到本地

### 4.1 git clone

* 得到仓库地址：地址栏中复制或者选择Clone or download

  >![1570023411107](Git与GitHub的学习笔记-实验楼.assets/1570023411107.png)

* 克隆到本地 git clone

  > 先在到你希望下载到的文件夹中，gitbash here
  >
  > git clone [url]

#### //还有一些其他指令如 -b 之后补充

### 4.2 .git隐藏目录

进入仓库主目录，如下图所示，仓库主目录中有个 `.git` 隐藏目录，它里面包含了仓库的全部信息，**删掉这个目录，仓库就变成普通的目录了**。进入到仓库目录中，命令行前缀发生了一些变化，出现了红色（win是蓝绿色）的 master ，它就是当前所在的分支名：

> ![1570024161857](Git与GitHub的学习笔记-实验楼.assets/1570024161857.png)

### 4.3 远程仓信息 git remote -v

克隆一个 GitHub 仓库（也叫远程仓库）到本地，本地仓库则会自动关联到这个远程仓库，执行 `git remote -v` 命令可以**查看本地仓库所关联的远程仓库信息：**

> ![1570073111975](Git与GitHub的学习笔记-实验楼.assets/1570073111975.png)

Git 要求对本地仓库关联的每个远程主机都必须指定一个主机名（默认为 origin），用于本地仓库识别自己关联的主机，`git remote` 命令就用于管理本地仓库所关联的主机，一个本地仓库可以关联任意多个主机（即远程仓库）。

### 4.4 初始化个人仓库 git init

它会把当前所在目录变成一个本地仓库，因为有 GitHub 的存在，这个命令在我们的生产生活中用到的次数应该是零，除非你想费时费力自己搭建服务器。其实本地进行版本控制是不是也可以git init下？

---

---

## 五、Git的基本操作

### 5.1 git仓库三大区域

Git 本地仓库有三大区域：**工作区、暂存区、版本区**。这是一个概念，有这个了解即可，随着使用 Git 的时间增多，慢慢就会理解这三个区域的作用以及为何要这么设计，学习阶段只需按照文档逐步操作即可。接下来我们以命令为主线介绍 Git 的操作。

> ![1570078990474](Git与GitHub的学习笔记-实验楼.assets/1570078990474.png)

### 5.2 git status 查看状态

> ![1570088052434](Git与GitHub的学习笔记-实验楼.assets/1570088052434.png)
>
> 以上是在工作区进行了修改，也就是有未跟踪的文件/Untracked files

### 5.3 git add 添加到暂存区

* 先 git add test.md

> ![1570088539343](Git与GitHub的学习笔记-实验楼.assets/1570088539343.png)

* 撤销暂存操作 git reset -- test.md或者 git rm --cached test,md

  > git reset -- //把暂存区的全部修改撤销

### 5.4 git diff 查看修改详情

现在介绍另一个命令 `git diff`，它可以用来查看工作区被跟踪的文件的修改详情，此时新建文件 one.txt 并未被跟踪，而已被跟踪的文件 README.md 无修改，所以看不到。注意，只有在版本区中存在的文件才是被跟踪文件。

* git diff 

  > 查看尚未暂存的文件更新了哪些部分，不加参数直接输入
  >
  > **此命令比较的是工作目录(Working tree)和暂存区域快照(index)之间的差异**
  >
  > 也就是修改之后还没有暂存起来的变化内容。
  >
  > ![1570089938792](Git与GitHub的学习笔记-实验楼.assets/1570089938792.png)

* git diff --cached/staged

  > 查看已经暂存起来的文件(staged)和上次提交时的快照之间(HEAD)的差异

