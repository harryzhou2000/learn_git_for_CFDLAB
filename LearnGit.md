# 关于版本协作的一些简单教程

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
git [command] -h
git [command] --help
```

获得命令的帮助或者详细帮助文档。

## 推荐的Git操作环境

我们使用的Linux系统，包括WSL中，只需用包管理器安装Git即可。Windows系统建议安装[Git for Windows](https://gitforwindows.org/)软件，这样就同时安装了Git Bash，一个Windows上面运行的比较接近bash语法的shell。

Windows 11集成了Terminal，Windows 10上面建议从应用商店安装Windows Terminal应用。Windows Terminal应该可以检测到Powershell、CMD、git bash，可以自由选择。同时，资源管理器中右键菜单可以出现“在此处打开Terminal”的选项，方便我们随地进入命令行而不用手动cd/dir到想要的目录。

VsCode是一个强大的文本编辑器，通过扩展可以功能上接近完整的IDE。安装Vscode时，**建议选择将VsCode加入右键菜单**。

资源管理器在文件夹空白处右键菜单如下：

![图片](pics/rightGlick.png)

## VsCode的Git操作

VsCode可以实现Git的部分图形化操作，对理解分支结构帮助比较大。
