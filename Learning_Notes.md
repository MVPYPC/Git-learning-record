# Git学习笔记

>通过[廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)简单学习Git，本文件夹正好可以用作创建仓库
>
>开始日期：2022.1.14

## Git简介

Git是目前世界上最先进的分布式版本控制系统~~之一~~。

如果有一个软件，不但能自动帮我记录每次文件的改动，还可以让同事协作编辑，这样就不用自己管理一堆类似的文件了，也不需要把文件传来传去。如果想查看某次改动，只需要在软件里瞄一眼就可以，岂不是很方便？

这个软件用起来就应该像这个样子，能记录每次文件的改动：

| 版本 | 文件名      | 用户 | 说明                   | 日期       |
| :--- | :---------- | :--- | :--------------------- | :--------- |
| 1    | service.doc | 张三 | 删除了软件服务条款5    | 7/12 10:38 |
| 2    | service.doc | 张三 | 增加了License人数限制  | 7/12 18:09 |
| 3    | service.doc | 李四 | 财务部门调整了合同金额 | 7/13 9:51  |
| 4    | service.doc | 张三 | 延长了免费升级周期     | 7/14 15:17 |

这样，你就结束了手动管理多个“版本”的史前时代，进入到版本控制的20世纪。



## Git历史

==Linus 永远的神！==

---

很多人都知道，Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。

Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。



## 分布式 || 集中式？

### 集中式版本控制系统

版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。

---

### 分布式版本控制系统

没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

---



## Git安装

由于大一时已经安装好了，所以不再赘述安装过程，安装成功截图如下：


![image-20220115224323306](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/1.png?raw=true)




## Git使用

### 创建版本库

#### 第一步

即创建仓库，这里在~/Documents/ 里面建立一个Git文件夹（用于学习Git）

使用了三条命令：

```java
mkdir Git              //mkdir即 make direct的缩写
cd Git                 //cd是进入文件夹的命令，这里即是进入cd文件
pwd                    //pwd命令用于显示当前目录
```

执行后的Git界面如下：

![image-20220114171616680](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/2.png?raw=true)

即显示这里进入了/c/Users/86072/Documents/Git 目录下。

#### 第二步

通过git init命令把这个目录变成git管理的仓库，如下

![image-20220114171940806](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/3.png?raw=true)

```java
git init              //git init 命令将当前目录变成Git可以管理的仓库
```

创建后仓库内会有一个.git的目录，在本地无法查看，可使用ls -ah查看如下：

![image-20220114172332080](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/4.png?raw=true)

>### 二进制 || 文本？
>
>***二进制文件***是在电脑里用 0, 1 进行编码的文件, 他们把信息(如图片, 音频等)用高效的存储方式**编码为二进制**, 存在
>电脑里, 打开的时候**需要用对应的方式解码**, 比如 `png` 要用图片查看器打开, `mp3` 要用音乐播放器打开等等, 正
>是这些软件能解码对应的特定类型的文件.
>**不同的二进制文件编码方式不同**. 如果你尝试用音乐播放器打开一张图片, 肯定是不会识别出来的
>
>***文本文件***就是直接记录人能阅读的字符的文件, 如`txt`, 但是 `ppt` 或者 `pdf` 文件不是文本文件, 虽然你打开
>他也能看到人能阅读的字符, 但是正如上文所说, 这是需要被解码出来才能看到的信息
>常见的文本文件有`txt`, 但是对于我们程序员来说, 最常见的文本文件就是各种代码的源文件了

==**千万不要使用Windows自带的记事本编辑任何文本文件**==

> 原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载[Visual Studio Code](https://code.visualstudio.com/)代替记事本，不但功能强大，而且免费！

#### 第三步

在仓库中建立一个文件（即本文件），使用两条命令。

```c
git add Learning_Notes.md                  //git add命令即将该文件添加到仓库
git commit -m "create a markdown file"     //用命令git commit告诉Git，把文件提交到仓库
```

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

> 这个参数"-m"有讲究，详情可以参见[git commit 参数详解](https://www.atlassian.com/git/tutorials/saving-changes/git-commit)

列举一些常用选项

```java
git commit  //慎用！！！尽量别用！
//提交暂存的快照。这将启动一个文本编辑器，提示您输入提交消息。输入消息后，保存文件并关闭编辑器以创建实际提交。
    
git commit -a
//提交工作目录中所有更改的快照
    
git commit -m "commit message"
//最常用
    
git commit -am "commit message"
//结合了-a和-m选项的高级用户快捷命令。这种组合会立即创建所有分阶段更改的提交，并采用内联提交消息。
    
git commit --amend
//传递此选项将修改最后一次提交。不是创建新的提交，而是将分阶段的更改添加到之前的提交中。此命令将打开系统配置的文本编辑器并提示更改先前指定的提交消息。
```

***

### 时光机穿梭

使用了2条指令：

```java
git status  //git status命令可以让我们时刻掌握仓库当前的状态
git diff    //git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式
```

更新本文件，保存后运行`git status`如图所示：

![image-20220114220233046](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/5.png?raw=true)

这里git告诉我们`Learning_Notes.md`文件被更改了，但是

```java
no changes added to commit (use "git add" and/or "git commit -a")
```

告诉我们该更改还没被commit（确认提交）。

前文提到，这里我们知道了该文件被更改过，但是如果能知道具体的更改在哪就更好了，使用`git diff`命令可以显示具体的更改。具体如下图：

![image-20220114221538235](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/6.png?raw=true)

如图，可以看到所有的更改，知道了做了什么修改后便可以放心的提交到仓库了。

---

#### 版本回退

到现在为止，提交了4个版本的文件，还可以记住，但是当这个文件日益发展壮大，有了几十、几百、甚至成千上万个版本，如何查看捏？答案是`git log`命令。

```java
git log   //命令显示从最近到最远的提交日志
          //如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：
git log --pretty=oneline
```

用`git log`命令如下图：可以看到按照提交顺序由近到远排列，且能看到提交参数中的“说明”

> 这里注意，有可能版本过多以后会出现进入版本管理器的情况，这时候按回车查看下一行直到（END）结束。可以按<kbd>q键</kbd>退出。

![image-20220114223244179](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/7.png?raw=true)

简易版的如下图：![image-20220114223644821](Chttps://github.com/MVPYPC/Git-learning-record/blob/main/picture/8.png?raw=true)

其中黄色的那些十六进制数是Git的`commit id`，用于识别各个版本，一般前几位即可。

这里新建了两个版本，即`version back initial`和`version back after`，现在HEAD指向...after，准备回退到...initial的版本。

![image-20220114225101835](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/9.png?raw=true)

***回退***

Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`8b35513...`，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本`version back after`回退到上一个版本`version back before`，就可以使用`git reset`命令：

```java
git reset --hard HEAD^    //回退到上一个版本，其中--hard参数现在完全可以放心使用
```

可以看到被还原到了***回退***之前的版本。

但是！现在有个更严峻的问题，这时候回退到了最近的版本，如果要想返回刚刚最新的版本，没办法通过HEAD指针访问，比如，通过`git log`已经无法得知最新版本的`commit id`了。

所以，牛逼的Linus已经考虑到这种情况了，他赐予了我们后悔的机会——`git reflog`

```java
git reflog    //用来记录你的每一次命令
```

![image-20220114231555449](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/10.png?raw=true)

如图，可以查看历史所有版本以及HEAD指针的指向，感觉有时候比`git log`好用。

---

#### 工作区 || 暂存区？

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的`Git`文件夹就是一个工作区

#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中**最重要的就是称为stage（或者叫index）的暂存区**，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

1. 用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
2. `git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区(`git add`)，然后，一次性提交暂存区的所有修改(`git commit -m "..."`)

---

#### 管理修改

划重点：==Git管理的是修改，而不是文件==

每当我们使用`git add`命令将文件提交至暂存区，即将现在的文件提交(可以理解为拷贝一份，在拷贝以后，文件所做的改变并不影响已经拷贝的内容吧）

所以，如果我们做了 <u> 第一次修改 -> `git add` -> 第二次修改 -> `git commit`</u> 这样的操作，那么commit的就只有第一次修改，因为第二次的修改未提交。

可以使用`git diff`命令查看工作区和版本库里面最新版本的区别，具体代码如下：

```java
git diff HEAD -- Learning_Notes.md  //最后是文件名，其中 -- 很重要，标志着当前分支，
```

---

#### 撤销修改

~~自然，你是不会犯错的。  ——廖雪峰~~

在使用`git status`后Git会告诉你，`git checkout -- file`可以丢弃工作区的修改(discard changes in working directory)

意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

1. 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

2. 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

在Git仓库中使用该命令如下图所示：

![image-20220115224323306](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/11.png?raw=true)

回到了`工作区||暂存区`的位置。

还可以使用`git reset HEAD <file>`命令把暂存区的修改撤销掉（unstage），重新放回工作区

> 噢~我懂了，在这里写没有保存，Git也会视为没有更新，保存以后用`git status`命令才会显示更改过。

#### 删除文件

添加`delete.txt`文件，如下图

![image-20220118225204837](C:\Users\86072\Documents\Git\pic\12.png)

删除命令是`rm`，代码：

```java
rm delete.txt        //删除delete.txt文件
```

那么这时候，工作区和版本库产生了差别，使用`git status`命令可以告诉我们哪些文件被删除了，如下图

![image-20220118225545350](C:\Users\86072\Documents\Git\pic\13.png)

这时候，我们有两个选择

1. 的确要删除这个文件，那么直接提交`git commit -m ""`即可

2. 删错了，那么我们想要将版本库中的该文件返回工作区，使用`checkout`命令：

   ```java
   git checkout -- delete.txt
   ```

   即可还原。

到这里我们可以猜到，`git checkout`命令的作用就是用版本库里的版本替换工作区里的版本。

> `git restore` 是git 2.23版本新增的命令，用来代替身兼数职的git checkout。功能是一样的。

### ==远程仓库==

如何使用伟大的Github进行自动代码托管捏？

首先，需要`ssh`密钥，~~不再赘述。~~

一定要赘述:exclamation::exclamation::exclamation::exclamation::exclamation::exclamation::exclamation::exclamation:这里耗费了好多时间，结果就是ssh密钥的问题，本来我大一时候绑定了一个ssh密钥，然后我就直接跳过了生成密钥的步骤，结果一直说无法取得我的github的权限，结果:exclamation::exclamation::exclamation::exclamation::exclamation:这个ssh密钥要是一年没用，就会被github删除，或者说失效，我就一直卡在这里，廖老师的教程上没有这方面的经验，特此记录一下。

谨记:exclamation::exclamation::exclamation::exclamation::exclamation::exclamation:在教程行不通的情况下一定要去看==官方文档==

#### 添加远程库
当建立好ssh密钥公钥后，需要建立一个远程仓库和本地仓库的关联，使用`git remote add`命令

```java
git remote add origin git@github.com:MVPYPC/Git-learning-record.git
    //origin是远程库的名字，这是这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。
    //MVPYPC/Git-learning-record是我的github名+仓库名
```

下一步，就可以把本地库的所有内容推送到远程库上，使用`git push`命令，在此之前，建议使用`git remote -v`指令查看现在的远程库信息，若有需要删除的，使用`git remote rm <name>`删除远程库。

```java
git push -u origin main
    //由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
git push origin main
    //在以后的push或者fetch时就不用 -u 了
```

廖老师的教程上是使用的master分支，这里如果是已经建立好的仓库就会有一个main分支，所以我是push到main分支上，感觉比较方便。

> 至于为什么有这个变化，在公元 2020年 6 月份，受美国大规模的 “Black Lives Matter”运动影响，为了安抚愈演愈烈的民众情绪，GitHub 就宣布将替换掉 master 等术语，以避免联想奴隶制。同年10月份，在外界一些声音的催促下，这一举措则终于正式落地了。
>
> 不得不说，吃饱了闲的。:sweat_smile::sweat_smile::sweat_smile:

而且这玩意牛逼的地方在于，他只更新变动的，不会把github上有但是本地没有的给删了。

btw，我下载了[github桌面版](https://desktop.github.com/)，感觉很香，每次就这么在change里面点commit然后点push就行了

> push就在fetch那个位置，在commit以后就会变成push

![image-20220121162640096](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/14.png?raw=true?)

#### 克隆远程库

使用`git clone`命令克隆一个远程库到本地上来

```java
git clone git@github:MVPYPC/....  //这里暂时没啥有用的就不演示了，等有用武之地了再来更新
```

GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。

使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。

> 踩坑记录
>
> 我因为是先搞了github，后来才学习的git技术，所以有很多历史遗留仓库并没有跟本地仓库链接，尤其是我现在正在更新的一些库，所以要将他们进行链接可以将其同步以后使用`git push origin main -f`这个 -f 是force的意思，即强迫将本地的push到远程仓库中去。  
如何在vscode中提交?艹艹艹艹艹
nmdwsm

创建新库时可能git bash默认master分支，可以使用`git branch -m oldName newName`来重命名

```java
git branch -m master main
```

>这段时间过年吃饭较多，还要准备考研资料，实在没有心情学git，现在我已经基本能够通过`git bash`,`github desktop`,`idea`,`vscode`合作进行本地和远程（github.com/mvpypc）仓库的同步，感觉太方便了！

### 分支管理

#### 创建与合并分支

在在`版本回退`里，我们已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`main`分支。`HEAD`严格来说不是指向提交，而是指向`main`，`main`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![git-br-initial](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/15.png?raw=true?)

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![git-br-create](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/16.png?raw=true?)

你看，Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![git-br-dev-fd](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/17.png?raw=true?)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![git-br-ff-merge](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/18.png?raw=true?)

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![git-br-rm](https://github.com/MVPYPC/Git-learning-record/blob/main/picture/19.png?raw=true?)

