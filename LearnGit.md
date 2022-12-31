# 关于版本协作的一些简单教程

by：Harry Zhou

Git是一种分布式版本管理软件，由Linus开发，它的基本界面是命令行界面。

通过Git，你可以管理某个目录下的所有代码文件，追踪其变化，并且增量地进行保存、同步和合并。

Git有许多基本指令，但是日常使用仅仅使用少数。

这里推荐入门教程：[廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)，
建议通读并且自己简单尝试。

里面可以了解Git的基本操作。

同时，Git的[官方文档](https://git-scm.com/docs)是查阅详细命令的好地方。

同时有一个很好的[Visual CheatSheet](https://ndpsoftware.com/git-cheatsheet.html)，点击里面的不同区域就可以看到相关的命令。

当然，如果你只是忘记了参数的命令行意义，可以使用

```bash
git --help
git <command> -h
git <command> --help
```

获得命令的帮助或者详细帮助文档。

以下的文档，默认读者已经**基本了解并且实践**过git的简单命令（add commit fetch merge push 等），并且清楚至少workspace，index，local repo，upstream repo的概念。

## 1. 推荐的Git操作环境

我们使用的Linux系统，包括WSL中，只需用包管理器安装Git即可。Windows系统建议安装[Git for Windows](https://gitforwindows.org/)软件，这样就同时安装了Git Bash，一个Windows上面运行的比较接近bash语法的shell。安装包安装时尽量采用Windows环境推荐配置（默认的），尤其是**CRLF相关**。

Windows 11集成了Terminal，Windows 10上面建议从应用商店安装Windows Terminal应用。Windows Terminal应该可以检测到Powershell、CMD、git bash，可以自由选择。同时，资源管理器中右键菜单可以出现“在此处打开Terminal”的选项，方便我们随地进入命令行而不用手动cd/dir到想要的目录。

VsCode是一个强大的文本编辑器，通过扩展可以功能上接近完整的IDE。安装Vscode时，**建议选择将VsCode加入右键菜单**。

资源管理器在文件夹空白处右键菜单如下：

![图片](pics/rightGlick.png)

### 1.1. VsCode的Git操作

VsCode可以实现Git的部分图形化操作，对理解分支结构帮助比较大。VsCode内置了一部分Git辅助功能。

首先，在左侧工具栏可以找到Source Control栏目，如果VsCode的工作根目录属于一个Git Repo，即有完整的.git文件夹内容（如clone下来，或者自己init的），这时Source Control栏目会显示Staged Changes，以及Changes的情况，点击每个文件名可以打开一个对比的双列文件，用来显示有哪些修改。

其次，在代码中会显示workspace文件与index的差别，在左侧以**彩色竖条呈现**。绿色代表新加内容，蓝色是修改内容，红色是删除内容。单击左侧的彩色条可以观察此处发生了什么修改。这些修改和Source Control中在Changes栏目点击看到是一致的。

虽然VsCode的Git功能提供了add、commit、push、sync的按钮，但是本文**不建议**直接使用，实际的Git操作尽量在命令行执行，除非你**对Git很熟悉**而且**对这个图形界面执行的是哪些Git操作很熟悉**。其他Git图形界面同理。时刻牢记，虽然Git操作不会损坏repo里面的commit，绝大多数git指令后，无论如何都能恢复之前的commit，但是git对你workspace的代码有**全部权限**，误操作可能导致**新写的代码丢失或者损坏**，可能一上午就白干了。

VsCode可以安装很多Git相关扩展，功能都很强大，但是简单入门+小团队应用时，可以完全不使用。唯一推荐安装的是Git Graph，可以直接应用商店搜索得到，用来观察分支情况、commit情况，这在需要回滚到很久之前的某个commit，之后跳回来时非常有用。

## 2. 从Gitlab clone 项目

你看到这里时已经向Gitlab group的管理员申请了加入群组，才能看到群组私有项目。单击代码首页的clone，就可以发现有不同选项。这里推荐SSH方式。

首先设置账户的SSH授权，Windows下生成SSH的密钥后，将公钥文本拷贝到Gitlab个人账户设置界面的对应位置，你的Windows上的git即可通过SSH与Gitlab的repo通信。

随后拷贝clone按钮给出的SSH版本的URL，类似于

```url
https://gitlab.com/cfdlab_thu/learn_git.git
```

这样，打开Windows的一个shell（此处以git bash为例）：

```bash
/e/projects/$ git clone https://gitlab.com/cfdlab_thu/learn_git.git
```

那么项目的完整目录就出现在/e/projects/learn_git。

tips：通过Gitlab网站对Remote Repo进行的修改，其commit在git中作者名字都是用户名，但是在本地commit的，就是本地git设置的用户名（第一次commit会强制设置）。但是你将其推送到Gitlab后，Gitlab可以自动分析出对应的是哪个Gitlab账号。因此，假如你本地和Gitlab的账户名不一样，在分析git log时名字就是不一样的。而且你在不同设备或者系统下也可以用不同的用户名，甚至可以手动更改。虽然不影响Gitlab端分析的代码提交者归属，但是在本地看git log或者可视化时无法确定是同一个作者。为了项目的清晰程度，*建议使用者的所有git环境采用一套用户名和邮箱（不要乱写），同时GitLab上面注册邮箱时尽量采用同一个邮箱。*

## 3. 一个简单的Follow Through

### 3.1. 进行 add commit push

当你看到这个markdown时，已经是clone了learn_git项目了，同时作为团队的成员，有push的权限。首先新建一个文件code_\<yourname>.txt（对于我来说就是code_HarryZhou.txt，以下用这个指代），
并写道：

```txt
GayHub is good and popular but blocked in prc
GayLab is good and connected
```

（用来描述为啥我们不使用更为流行的Github）。此时git status，会显示code_HarryZhou.txt是untracked状态。

命令行add后看status

```bash
$ git add code_HarryZhou.txt
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   code_HarryZhou.txt
```

很明显，这个文件被stage进入了index区，但是没有被commit。根据提示，我们可以使用git restore --staged命令来逆转这个操作。这在我们不小心add了某个不需要add的文件的时候，比如忘记修改.gitignore时很有用。注意，**commit前看status比较保险，尤其注意新文件，以免将不需要的文件（如编译结果，二进制文件，大型数据，编译辅助文件如VS的构建中间件）commit，这样需要一定工作才能逆转**。

接下来commit一下，并且查看git log （最后键入q退出）

```bash
$ git commit -m 'added code_HarryZhou.txt'
[main 00d22c5] added code_HarryZhou.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 code_HarryZhou.txt

$ git log
commit 00d22c5c982a2c6be101fbb996a13015640ebe9f (HEAD -> main)
Author: HarryZhou <2373256746@qq.com>
Date:   Fri Dec 30 17:42:45 2022 +0800

    added code_HarryZhou.txt
```

具体内容会有不同，但我们都可以看到有一个commit被提交，这样本次修改就被安全封存在本地了。

之后查看一下remote的状态：

```bash
$ git branch -vv
* main 00d22c5 [origin/main: ahead 1] added code_HarryZhou.txt
$ git remote get-url origin
git@gitlab.com:cfdlab_thu/learn_git.git
```

可以看到，我们目前在branch main上面，其track的upstream是git

## 3.2 进行push


