fffffhttps://learngitbranching.js.org/?locale=zh_CN

##                                 提交 Git Commit

------

Git 仓库中的提交记录保存的是你的目录下所有文件的快照，就像是把整个目录复制，然后再粘贴一样，但比复制粘贴优雅许多！

Git 希望提交记录尽可能地轻量，因此在你每次进行提交时，它并不会盲目地复制整个目录。条件允许的情况下，它会将当前版本与仓库中的上一个版本进行对比，并把所有的差异打包到一起作为一个提交记录。

Git 还保存了提交的历史记录。这也是为什么大多数提交记录的上面都有 parent 节点的原因 —— 我们会在图示中用箭头来表示这种关系。对于项目组的成员来说，维护提交历史对大家都有好处。

关于提交记录太深入的东西咱们就不再继续探讨了，现在你可以把提交记录看作是项目的快照。提交记录非常轻量，可以快速地在这些提交记录之间切换！

------

咱们来实际操作一下，看看提交记录是怎样的。右边展示了一个（小型）Git 代码库。当前有两个提交记录 —— 初始提交 `C0` 和其后可能包含某些有用修改的提交 `C1`。

点击下面的按钮 git commit 创建一个新的提交记录。

<img src="/Users/wjb/Library/Application Support/typora-user-images/image-20250925133230594.png" alt="image-20250925133230594"  />

点击后，如下图 ，我们刚才修改了代码库，并把这些修改保存成了一个**提交记录 `C2`**。**`C2` 的 parent 节点是 `C1`**， **parent 节点**是当前提交中变更的基础。

![image-20250925133623573](/Users/wjb/Library/Application Support/typora-user-images/image-20250925133623573.png)



------



##                                      分支  Git Branch

Git 的分支也非常轻量。它们只是简单地指向某个提交记录 —— 仅此而已。所以许多 Git 爱好者传颂：

```
早建分支！多用分支！
```

这是因为即使创建再多的分支也不会造成储存或内存上的开销，并且按逻辑分解工作到不同的分支要比维护那些特别臃肿的分支简单多了。

在将分支和提交记录结合起来后，我们会看到两者如何协作。现在只要记住使用分支其实就相当于在说：“我想基于这个提交以及它所有的 parent 提交进行新的工作。”

------

咱们通过实际操作来看看分支是什么样子的。

接下来，我们将要**创建**一个到名**为 `newImage` 的分支**。

![image-20250925134800031](/Users/wjb/Library/Application Support/typora-user-images/image-20250925134800031.png)

看到了吗，创建分支就是这么容易！**新创建的分支 `newImage`**指向的是**提交记录 `C1`**。

![image-20250925135018088](/Users/wjb/Library/Application Support/typora-user-images/image-20250925135018088.png)

现在咱们试着往**新分支**里**提交**一些东西。点击下面的按钮

![image-20250925135209168](/Users/wjb/Library/Application Support/typora-user-images/image-20250925135209168.png)

哎呀！为什么 **`main` 分支前进**了，但 **`newImage` 分支还待在原地**呢？！这是**因为**我们**没有“在”这个新分支上**，看到 **`main` 分支**上的那**个星号（*）**了吗？这**表示当前所在的分支是 `main`**。

![image-20250925135435332](/Users/wjb/Library/Application Support/typora-user-images/image-20250925135435332.png)

现在咱们告诉 **Git** 我们想要**切换到新的分支**上

```
git checkout <name>
```

上面的**命令**会让我们在提交修改之前先**切换到新的分支**上

![image-20250925135649397](/Users/wjb/Library/Application Support/typora-user-images/image-20250925135649397.png)

点击**执行  git checkout newImage**，使（ * ）**当前分支变到 newImage** 上，然后 **git commit 提交**后结果如下

![image-20250925140326002](/Users/wjb/Library/Application Support/typora-user-images/image-20250925140326002.png)

*注意：在 Git 2.23 版本中，引入了一个名为 `git switch` 的新命令，最终会取代 `git checkout`，因为 `checkout` 作为单个命令有点超载（它承载了很多独立的功能）。 由于现在很多人还无法使用 `switch`，本次课程仍然使用 `checkout`而不是 `switch`， 但是如果你想尝试一下新命令，我们的应用也是支持的！并且你可以从[这里](https://git-scm.com/docs/git-switch)学到更多关于新命令的内容。*



**如果你想创建一个新的分支同时切换到新创建的分支的话，可以通过 git checkout -b <your-branch-name>`来实现**。

**`git checkout -b <新分支名> [<起始点>]`。**

- **若未指定起始点（如提交哈希或分支名），默认基于当前分支的最新提交创建分支**
- 

------

##                                 切换分支Git Switch 

`git switch` 是 Git 2.23 版本引入的命令，用于**切换分支**，旨在替代 **git checkout <branch>**的分支切换功能（[文件恢复](https://so.csdn.net/so/search?q=文件恢复&spm=1001.2101.3001.7020)功能由 **git restore** 替代）。它的设计更清晰、语义化，能减少误操作风险。

1. **切换到已有分支**

```
git switch <existing-branch-name>
```

示例：

```
git switch main      # 切换到本地 main 分支
git switch feature   # 切换到本地 feature 分支
```

2. **创建并切换到新分支**

```
git switch -c <new-branch-name>    # 基于当前分支创建
git switch -c <new-branch> <base>  # 基于指定提交/分支创建
```

示例：

```
git switch -c dev              # 从当前分支创建 dev 分支并切换
git switch -c hotfix origin/main  # 基于远程的 origin/main 创建 hotfix 分支
```

3. **切换到远程分支（自动跟踪）**

```
git switch <remote-branch-name>
```

Git 会自动创建**同名本地分支**并跟踪远程分支。
示例：

```
git switch origin/develop  # 创建本地 develop 分支，跟踪 origin/develop

```

| 选项              | 作用                                                        |
| ----------------- | ----------------------------------------------------------- |
| -c <name>         | 创建新分支并切换（同 `--create`）                           |
| -C <name>         | 强制创建新分支（覆盖已存在的同名分支，同 `--force-create`） |
| -d` / `--detach   | 切换到提交的游离状态（HEAD 分离）                           |
| -t` / `--track    | 显式设置跟踪远程分支（通常自动启用）                        |
| --orphan <branch> | 创建孤立分支（无提交历史）                                  |
| -m` / `--merge    | 切换时尝试合并工作区修改（解决未提交更改导致的切换失败）    |



**典型场景示例**

场景 1：基于远程分支创建新分支

```
git fetch origin                     # 获取远程最新数据
git switch -c feat-login origin/main # 从 origin/main 创建 feat-login 分支
```

场景 2：强制覆盖旧分支

```
git switch -C main  # 若 main 已存在，强制重置为新状态
```

场景 3：解决切换冲突（工作区有未提交修改）

```
git switch -m target-branch  # 尝试合并工作区修改到目标分支
# 或
git stash                    # 暂存修改
git switch target-branch     # 切换分支
git stash pop                # 恢复修改
```

**注意事项**

1. **未提交的更改**：
   若工作区/暂存区有未提交修改，切换分支可能失败（除非使用 `-m` 或 `stash`）。
2. **与 `git checkout` 对比**：

```
git switch main         # 替代 git checkout main
git switch -c new-feat  # 替代 git checkout -b new-feat
```

**兼容性**：
需 Git ≥ 2.23。旧版本请继续使用 `git checkout`。

**总结**

| 操作                   | 命令                         |
| ---------------------- | ---------------------------- |
| 切换分支               | `git switch <branch>`        |
| 创建并切换分支         | `git switch -c <new-branch>` |
| 从远程分支创建并跟踪   | `git switch <remote-branch>` |
| 强制创建（覆盖旧分支） | `git switch -C <branch>`     |



------

##                              合并分支 Git Merge

  太好了! 我们已经知道如何提交以及如何使用分支了。接下来咱们看看如何将两个分支合并到一起。就是说我们新建一个分支，在其上开发某个新功能，开发完成后再合并回主线。

咱们先来看一下第一种方法 —— **`git merge`**。在 Git 中**合并两个分支**时会**产生**一个**特殊的提交记录**，它**有两个 parent** **节点**。翻译成自然语言相当于：“我要把这两个 parent 节点本身及它们所有的祖先都包含进来。”

通过图示更容易理解一些，咱们看一下。

我们准备了**两个分支**，**每个分支**上各有一个**独有的提交**。这意味着**没有一个分支包含**了我们**修改的所有内容**。咱们通过合并这两个分支来解决这个问题。

我们要把 **`bugFix`** **合并**到 **`main`** 里   

```
get merge bugFix
```

![image-20250925144428288](/Users/wjb/Library/Application Support/typora-user-images/image-20250925144428288.png)

下图所示，首先，**main** 现在**指向**了一个**拥有两个 parent 节点**的**提交记录**。假如从 `main` 开始沿着箭头向上看，在到达起点的路上会经过所有的提交记录。这意味着 `main` 包含了对代码库的所有修改。

![image-20250925144700279](/Users/wjb/Library/Application Support/typora-user-images/image-20250925144700279.png)

咱们再把 **`main` 分支合并到 `bugFix`**：

```
git checkout bugFix;
git merge main;
```

因为 **`main` 继承自 `bugFix`**，Git 什么都不用做，**只是简单地**把 **`bugFix`** 移动到 **`main` 所指向的那个提交记录**。

![image-20250925145146021](/Users/wjb/Library/Application Support/typora-user-images/image-20250925145146021.png)



------

##                                 合并分支 Git Rebase

第二种**合并分支**的方法是 **`git rebase`**。**Rebase** 实际上就是**取出一系列**的**提交记录**，**“复制”**它们，然后在另外一个地方逐个的放下去。

Rebase 的优势就是可以创造更线性的提交历史，这听上去有些难以理解。如果只允许使用 Rebase 的话，代码库的提交历史将会变得异常清晰。

咱们还是实际操作一下吧……

还是准备了**两个分支**；注意当前所在的**分支是 bugFix**（**星号**标识的是**当前分支**）

我们想要**把 bugFix 分支**里的工作直接**移到 main 分支**上。**移动**以**后**会使得两个分支的功能**看起来**像**是按顺序开发**，但**实际上**它们**是并行开发**的。

```
 git rebase [选项] [基底分支]    将基底分支移动到选项上 
 如 git rebase  main bugFix       将分支bugFix移到main上
```

咱们这次用 **`git rebase`** 实现此目标

```
git rebase main
```

![image-20250925150415212](/Users/wjb/Library/Application Support/typora-user-images/image-20250925150415212.png)

如下图，现在 **bugFix 分支**上的工作**在 main 的最顶端**，同时我们也得到了一个更线性的提交序列。

**注意**，**提交记录 C3 依然存在（**树上那个半透明的节点），而 **C3'** **是**我们 **Rebase 到 main 分支上的 C3 的副本**。

![image-20250925150624863](/Users/wjb/Library/Application Support/typora-user-images/image-20250925150624863.png)

**现在唯一的问题就是 main 还没有更新，**下面咱们就来更新它吧……

```
get checkout main
```

现在我们切**换到了 `main`** 上

![image-20250925151035333](/Users/wjb/Library/Application Support/typora-user-images/image-20250925151035333.png)

把它**合并（rebase）**到 **`bugFix`** 分支上……

```
git rebase bugFix
```

于 `bugFix` 继承自 `main`，所以 Git 只是简单的把 `main` 分支的引用向前移动了一下而已。如下图

![image-20250925151618202](/Users/wjb/Library/Application Support/typora-user-images/image-20250925151618202.png)



------

##                                     在提交树上移动

###                                                       HEAD

我们首先看一下 “HEAD”。 **HEAD** 是一个**对当前所在分支的符号引用** —— 也就是**指向**你**正在**其基础上**进行**工作的**提交记录。**

**HEAD 总是指向当前分支上最近一次提交记录**。大多数修改提交树的 Git 命令都是从改变 HEAD 的指向开始的。

HEAD 通常情况下是指向分支名的（如 bugFix）。在你提交时，改变了 bugFix 的状态，这一变化通过 HEAD 变得可见。

下面咱们通过实际操作看一下。我们将会观察提交前后 HEAD 的位置。

![image-20250925161738528](/Users/wjb/Library/Application Support/typora-user-images/image-20250925161738528.png)

```
git checkout c1;
git checkout main;
git commit;
git checkout c2;
```

看到了吗？ HEAD 指向了 `main`，随着提交向前移动。

（译者注：实际这些命令并不是真的在查看 HEAD 指向，看下一屏就了解了。如果想看 HEAD 指向，可以通过 **`cat .git/HEAD`** 查看， 如果 HEAD 指向的是一个引用，还可以用 **`git symbolic-ref HEAD`** 查看它的指向。但是该程序不支持这两个命令）

![image-20250925162112595](/Users/wjb/Library/Application Support/typora-user-images/image-20250925162112595.png)

###                                                  分离的 HEAD

**分离的 HEAD** 就是**让其指向**了某个**具体的提交记录**而不是分支名。在命令执行之前的状态如下所示： 

HEAD -> main -> C1

HEAD 指向 main， main 指向 C1

![image-20250925162503058](/Users/wjb/Library/Application Support/typora-user-images/image-20250925162503058.png)

```
git checkout c1
```

现在变成了

HEAD -> C1

![image-20250925162559775](/Users/wjb/Library/Application Support/typora-user-images/image-20250925162559775.png)



------

##                                               相对引用

通过指定提交记录哈希值的方式在 Git 中移动不太方便。在实际应用时，并没有像本程序中这么漂亮的可视化提交树供你参考，所以你就**不得不用 `git log` 来查查看提交记录的哈希值**。

并且哈希值在真实的 Git 世界中也会更长（译者注：基于 SHA-1，共 40 位）。例如前一关的介绍中的提交记录的哈希值可能是 `fed2da64c0efc5293610bdd892f82a58e8cbc5d8`。舌头都快打结了吧...

比较令人欣慰的是，Git 对哈希的处理很智能。你只需要提供能够唯一标识提交记录的前几个字符即可。因此我可以**仅输入`fed2`** 而不是上面的一长串字符。

正如我前面所说，通过**哈希值指定提交记录很不方便**，所以 **Git 引入了相对引用**。这个就很厉害了!

使用相对引用的话，你就可以从一个易于记忆的地方（比如 `bugFix` 分支或 `HEAD`）开始计算。

相对引用非常给力，这里我介绍两个简单的用法：

- **使用 `^` 向上移动 1 个提交记录**

- **使用 `~<num>` 向上移动多个提交记录，如 `~3`**

  

### 														**操作符 (^)**

首先看看**操作符 (^)**。**把这个符号加在引用名称的后面**，**表示让 Git 寻找指定提交记录的 parent 提交**。

所以 **`main^` 相当于“`main` 的 parent 节点”**。

**`main^^` 是 `main` 的第二个 parent 节点**

![image-20250925163446698](/Users/wjb/Library/Application Support/typora-user-images/image-20250925163446698.png)

现在咱们切换到 main 的 parent 节点

```
git checkout main^
```

![image-20250925163533837](/Users/wjb/Library/Application Support/typora-user-images/image-20250925163533837.png)

你也可以将 `HEAD` 作为相对引用的参照。下面咱们就用 `HEAD` 在提交树中向上移动几次。

![image-20250925163640177](/Users/wjb/Library/Application Support/typora-user-images/image-20250925163640177.png)

```
git checkout c3;
git checkout HEAD^;//HEAD指向c2
git checkout HEAD^;//HEAD指向c1
git checkout HEAD^;//HEAD指向c0
```

很简单吧？！我们可以一直使用 `HEAD^` 向上移动

![image-20250925163745291](/Users/wjb/Library/Application Support/typora-user-images/image-20250925163745291.png)



###                                           操作符(~)

如果你想在提交树中向上移动很多步的话，敲那么多 `^` 貌似也挺烦人的，Git 当然也考虑到了这一点，于是又引入了操作符 `~`。

该操作符后面可以跟一个数字（可选，不跟数字时与 `^` 相同，向上移动一次），指定向上移动多少次。咱们还是通过实际操作看一下吧

![image-20250925164246887](/Users/wjb/Library/Application Support/typora-user-images/image-20250925164246887.png)

咱们用 `~<num>` 一次后退四步

```
git checkout HEAD~4
```

![image-20250925164303794](/Users/wjb/Library/Application Support/typora-user-images/image-20250925164303794.png)

### 													强制修改分支位置git branch -f 

你现在是相对引用的专家了，现在用它来做点实际事情。

我使用**相对引用最多的就是移动分支**。可以**直接使用 `-f` 选项让分支指向另一个提交**。例如:

```
git branch -f main HEAD~3
或 git branch -f main c1  //main指向c1
```

上面的命令会将 **main 分支强制指向 HEAD 的第 3 级 parent 提交**

![image-20250925164514998](/Users/wjb/Library/Application Support/typora-user-images/image-20250925164514998.png)

如下图， **相对引用为**我们提供了一种简洁的引用**提交记录 `C1` 的方式**， 而 **`-f` 则容许我们将分支强制移动到那个位置**。

![image-20250925164610499](/Users/wjb/Library/Application Support/typora-user-images/image-20250925164610499.png)





------

##                                              撤销变更

在 Git 里撤销变更的方法很多。和提交一样，撤销变更由底层部分（暂存区的独立文件或者片段）和上层部分（变更到底是通过哪种方式被撤销的）组成。我们这个应用主要关注的是后者。

主要有**两种**方法用来**撤销变更** —— 一是 **`git reset`，**还有就是 **`git revert`。**接下来咱们逐个进行讲解。

###                                                         

### 																	Git Reset

**`git reset`** 通过把**分支记录回退几个提交记录来实现撤销改动**。你可以将这想象成“改写历史”。**`git reset` 向上移动分支，原来指向的提交记录就跟从来没有提交过一样。**

让我们来看看演示：

![image-20250925170906134](/Users/wjb/Library/Application Support/typora-user-images/image-20250925170906134.png)

```
git reset HEAD~1  	或	git reset main~1
```

漂亮! Git 把 **main 分支移回到 `C1`**；现在我们的本地代码库根本就不知道有 `C2` 这个提交了

![image-20250925171019662](/Users/wjb/Library/Application Support/typora-user-images/image-20250925171019662.png)





### 															Git Revert

虽然在你的**本地分支**中**使用 `git reset`** 很方便，但是**这种**“改写历史”的**方法对**大家**一起使用的远程分支**是**无效**的哦！

为了**撤销更改并分享**给别人，我们需要**使用 `git revert`**。来看演示：

![image-20250925171325788](/Users/wjb/Library/Application Support/typora-user-images/image-20250925171325788.png)

奇怪！在我们**要撤销的提交记录后面居然多了一个新提交**！这是因为**新提交记录 `C2'`** 引入了**更改** —— **这些更改刚好是用来撤销 `C2` 这个提交的。也就是说 `C2'` 的状态与 `C1` 是相同的。**

**revert 之后**就可以把你的更改推送到远程仓库与别人分享啦。

![image-20250925171459193](/Users/wjb/Library/Application Support/typora-user-images/image-20250925171459193.png)



------

##     									整理提交记录

到现在我们已经学习了 Git 的基础知识 —— 提交、分支以及在提交树上移动。 这些概念涵盖了 Git 90% 的功能，同样也足够满足开发者的日常需求 

然而, 剩余的 10% 在处理复杂的工作流时(或者当你陷入困惑时）可能就显得尤为重要了。接下来要讨论的这个话题是“整理提交记录” —— 开发人员有时会说“我想要**把这个提交放到这里**, **那个提交放到刚才那个提交的后面**”, 而接下来就讲的就是它的实现方式，非常清晰、灵活，还很生动。

看起来挺复杂, 其实是个很简单的概念。

### 						                                Git Cherry-pick

本系列的第一个命令是 **`git cherry-pick`**, 命令形式为: 

- **`git cherry-pick <提交号>...`**

如果你想**将一些提交复制到当前所在的位置**（**`HEAD`**）下面的话， Cherry-pick 是最直接的方式了。我个人非常喜欢 `cherry-pick`，因为它特别简单。

咱们还是通过例子来看一下！

这里有一个仓库, 我们想**将 `side` 分支上的工作复制到 `main` 分支**，你立刻想到了之前**学过的 `rebase`** 了吧？但是咱们还是看看 `cherry-pick` 有什么本领吧。

![image-20250926111709114](/Users/wjb/Library/Application Support/typora-user-images/image-20250926111709114.png)

```
git cherry-pick c2 c4
```

![image-20250926112043789](/Users/wjb/Library/Application Support/typora-user-images/image-20250926112043789.png)

这就是了！我们**只需要提交记录 `C2` 和 `C4`**，所以 **Git 就将被它们抓过来放到当前分支下**了。 就是这么简单!

### 		

### 													交互式的 rebase git rebase -i

当你**知道**你所需要的**提交记录**（**并且**还知道这些提交记录的哈希值）时, **用 cherry-pick** 再好不过了 —— 没有比这更简单的方式了。

但是如果你**不清楚**你想要的**提交记录的哈希值**呢? 幸好 Git 帮你想到了这一点, 我们**可以利用交互式的 rebase** —— 如果你想从一系列的提交记录中找到想要的记录, 这就是最好的方法了

咱们具体来看一下……

**交互式 rebase 指的是使用带参数 `--interactive` 的 rebase 命令, 简写为 `-i`**

如果**你在命令后增加了这个选项, Git 会打开一个 UI 界面并列出将要被复制到目标分支的备选提交记录**，它**还会显示每个提交记录的哈希值**和**提交说明**，**提交说明有助于**你**理解**这个**提交进行了哪些更改**。

在实际使用时，所谓的 UI 窗口一般会在文本编辑器 —— 如 Vim —— 中打开一个文件。 考虑到课程的初衷，我弄了一个对话框来模拟这些操作。

**当 rebase UI界面打开时, 你能做3件事:**

- **调整提交记录的顺序（通过鼠标拖放来完成）**
- **删除你不想要的提交（通过切换 `pick` 的状态来完成，关闭就意味着你不想要这个提交记录）**
- **合并提交。** 遗憾的是由于某种逻辑的原因，我们的课程不支持此功能，因此我不会详细介绍这个操作。简而言之，它允许你把多个提交记录合并成一个。

接下来咱们看个实例

![image-20250926113712678](/Users/wjb/Library/Application Support/typora-user-images/image-20250926113712678.png)

当你**点击下面的按钮**时，会出现一个**交互对话框**。对**提交记录**做个**排序**（当然你也可以删除某些提交），点击确定看结果

```
git rebase -i HEAD~4
```

![image-20250926113850794](/Users/wjb/Library/Application Support/typora-user-images/image-20250926113850794.png)

Git 严格按照你在对话框中指定的方式进行了复制。如下图点击c4   c5进行了复制，删除了c2 c3

![image-20250926114205719](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114205719.png)



![image-20250926114531404](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114531404.png)

**下面是对c2 c3 c4 c5进行了复制**

![image-20250926114606389](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114606389.png)

![image-20250926114724994](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114724994.png)

**下面是对c3 c2 c5 c4依次进行了复制**

![image-20250926114833676](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114833676.png)

![image-20250926114928031](/Users/wjb/Library/Application Support/typora-user-images/image-20250926114928031.png)



------

## 									本地栈式提交

来看一个在开发中经常会遇到的情况：我正在解决某个特别棘手的 Bug，为了便于调试而在代码中添加了一些调试命令并向控制台打印了一些信息。

这些调试和打印语句都在它们各自的提交记录里。最后我终于找到了造成这个 Bug 的根本原因，解决掉以后觉得沾沾自喜！

最后就差把 `bugFix` 分支里的工作合并回 `main` 分支了。你可以选择通过 fast-forward 快速合并到 `main` 分支上，但这样的话 `main` 分支就会包含我这些调试语句了。你肯定不想这样，应该还有更好的方式……

实际我们只要**让 Git 复制解决问题的那一个提交记录就可以了。跟之前我们在“整理提交记录”中学到的一样，我们可以使用**

- **`git rebase -i`**
- **`git cherry-pick`**

**来达到目的。**

### 																提交的技巧 #1

接下来这种情况也是很常见的：**你之前在 `newImage` 分支上进行了一次提交，然后又基于它创建了 `caption` 分支，然后又提交了一次。**

**此时你想对某个以前的提交记录**进行一些小小的**调整**。比如设计师想修改一下 `newImage` 中图片的分辨率，尽管那个提交记录并不是最新的了

**我们可以通过下面的方法来克服困难：**

- **先用 `git rebase -i` 将提交重新排序，然后把我们想要修改的提交记录挪到最前**
- **然后用 `git commit --amend` 来进行一些小修改**
- **接着再用 `git rebase -i` 来将他们调回原来的顺序**
- **最后我们把 main 移到修改的最前端（用你自己喜欢的方法），就大功告成啦！**

当然完成这个任务的方法不止上面提到的一种（我知道你在看 cherry-pick 啦），之后我们会多点关注这些技巧啦，但现在暂时只专注上面这种方法。 最后有必要说明一下目标状态中的那几个`'` —— 我们把这个提交移动了两次，每移动一次会产生一个 `'`；而 C2 上多出来的那个是我们在使用**了 amend 参数**提交时产生的，所以最终结果就是这样了。

### 																	提交的技巧 #2

*如果你还没有完成“提交的技巧 #1”（前一关）的话，请先通过以后再来！*

正如你在上一关所见到的，我们可以使用 `rebase -i` 对提交记录进行重新排序。只要把我们想要的提交记录挪到最前端，我们就可以很轻松的用 `--amend` 修改它，然后把它们重新排成我们想要的顺序。

但这样做就唯一的问题就是要进行两次排序，而这有可能造成由 rebase 而导致的冲突。下面还是**看看 `git cherry-pick`是怎么做的吧。**

要在心里牢记 **cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上**（只要不是 HEAD 上游的提交就没问题）。

来看看这个例子：

![image-20250926122848451](/Users/wjb/Library/Application Support/typora-user-images/image-20250926122848451.png)

```
git cherry-pick c2
```

![image-20250926122938638](/Users/wjb/Library/Application Support/typora-user-images/image-20250926122938638.png)



### 																	Git Tag标签命名

信通过前面课程的学习你已经发现了：分支很容易被人为移动，并且当有新的提交时，它也会移动。分支很容易被改变，大部分分支还只是临时的，并且还一直在变。

你可能会问了：有没有什么可以***永远*指向某个提交记录的标识**呢，比如软件发布新的大版本，或者是修正一些重要的 Bug 或是增加了某些新特性，**有没有比分支更好的可以永远指向这些提交的方法**呢？

当然有了！**Git 的 tag 就是干这个用**的啊，它们可以（在某种程度上 —— 因为**标签可以被删除后重新在另外一个位置创建同名的标签**）**永久地将某个特定的提交命名为里程**碑，然后就可以像分支一样引用了。

更难得的是，它们并不会随着新的提交而移动。你也不能切换到某个标签上面进行修改提交，它**就像是提交树上的一个锚点，标识了某个特定的位置**。

咱们来看看标签到底是什么样。

**咱们先建立一个标签，指向提交记录 `C1`，表示这是我们 1.0 版本。**

![image-20250926123946373](/Users/wjb/Library/Application Support/typora-user-images/image-20250926123946373.png)

```
git tag v1 c1
```

很容易吧！我们将这个**标签命名为 `v1`**，并且**明确地让它指向提交记录 `C1`**，如果**你不指定提交记录**，**Git 会用 `HEAD` 所指向的位置**。

![image-20250926124110832](/Users/wjb/Library/Application Support/typora-user-images/image-20250926124110832.png)



### 																	Git Describe

由于**标签在代码库中起着“锚点”的作用**，**Git 还为此专门设计了一个命令用来描述离你最近的锚点（也就是标签）**，它就是 `git describe`！

**Git Describe 能帮你在提交历史中移动了多次以后找到方向**；当你用 `git bisect`（一个查找产生 Bug 的提交记录的指令）找到某个提交记录时，或者是当你坐在你那刚刚度假回来的同事的电脑前时， 可能会用到这个命令。

**`git describe` 的语法是：**

```
git describe <ref>
```

**`<ref>` 可以是任何能被 Git 识别成提交记录的引用**，如果**你没有指定的话，Git 会使用你目前所在的位置（`HEAD`）**。

它输出的结果是这样的：

```
<tag>_<numCommits>_g<hash>
```

**`tag` 表示的是离 `ref` 最近的标签**， **`numCommits` 是表示这个 `ref` 与 `tag` 相差有多少个提交记录**， **`hash` 表示的是你所给定的 `ref` 所表示的提交记录哈希值的前几位。**

**当 `ref` 提交记录上有某个标签时，则只输出标签名称**

让我们来看一个例子，对于下面的提交树：

![image-20250926125243342](/Users/wjb/Library/Application Support/typora-user-images/image-20250926125243342.png)

```
git tag v2 c3
```

![image-20250926125406083](/Users/wjb/Library/Application Support/typora-user-images/image-20250926125406083.png)

**git describe main 输出：**

```
v1_2_gC2
```

**`git describe side` 会输出：**

```
v2_1_gC4
```





------

## 										多分支 rebase

哇，现在我们这里出现了很多分支呢！让我们把所有这些分支上所做的工作都通过 rebase 合并到 main 分支上吧。

但是你的领导给你提了点要求 —— 他们希望得到有序的提交历史，也就是我们最终的结果应该是 `C6'` 在 `C7'` 上面， `C5'` 在 `C6'` 上面，依此类推。

即使你搞砸了也没关系，用 `reset` 命令就可以重新开始了。记得看看我们提供的答案，看你能否使用更少的命令来完成任务！

```
 git rebase [选项] [基底分支]    将基底分支移动到选项上  head指向基底分支
 如 git rebase  main one       将分支one移到main上    head指向one
```



###                                                          选择 parent 提交记录

**操作符 `^` 与 `~` 符一样，后面也可以跟一个数字**。

但是该操**作符^后面的数字与 `~` 后面的不同**，并不是用来指定向上返回几代，而是**指**定**合并提交记录的某个 parent 提交**。还记得前面提到过的一个合并提交有两个 parent 提交吧，所以遇到这样的节点时该选择哪条路径就不是很清晰了。

<u>**Git 默认选择合并提交的“第一个” parent 提交，在操作符 `^` 后跟一个数字可以改变这一默认行为。**</u>

废话不多说，举个例子。

这里有一个**合并提交记录**。如果**不加数字修改符直接切换到 `main^`**，**会回到第一个 parent 提交记录**。

(*在我们的图示中，**第一个 parent 提交记录是指合并提交记录正上方的那个提交记录**。*)

![image-20250926135450983](/Users/wjb/Library/Application Support/typora-user-images/image-20250926135450983.png)

```
git checkout main^
```

![image-20250926135922074](/Users/wjb/Library/Application Support/typora-user-images/image-20250926135922074.png)

现在来试试选择另一个 parent 提交……

![image-20250926140037419](/Users/wjb/Library/Application Support/typora-user-images/image-20250926140037419.png)

```
git checkout main^2
```

![image-20250926140115296](/Users/wjb/Library/Application Support/typora-user-images/image-20250926140115296.png)

**使用 `^` 和 `~` 可以自由地在提交树中移动，非常给力：**

![image-20250926140729832](/Users/wjb/Library/Application Support/typora-user-images/image-20250926140729832.png)

```
git checkout HEAD~;   //head 指向c6
git checkout HEAD^2;  //head指向c5
git checkout HEAD~2;  //head指向c3
```

![image-20250926141010092](/Users/wjb/Library/Application Support/typora-user-images/image-20250926141010092.png)

更厉害的是，这些操作符还支持链式操作！试一下这个

```
git checkout HEAD~^2~2
```

**和前面的结果一样，但只用了一条命令**







------



## 									远程仓库

远程仓库并不复杂, 在如今的云计算盛行的世界很容易把远程仓库想象成一个富有魔力的东西, 但实际上它们只**是你的仓库在另个一台计算机上的拷贝**。你可以通过因特网与这台计算机通信 —— 也就是增加或是获取提交记录

话虽如此, 远程仓库却有一系列强大的特性

- 首先也是最重要的的点, **远程仓库是一个强大的备份**。**本地仓库**也**有恢复文件到指定版本的能力,** **但所有的信息都是保存在本地的**。有了**远程仓库**以后，即使**丢失了本地所有数据**, 你仍可以**通过远程仓库拿回你丢失的数据**。
- 还有就是, 远程让代码社交化了! 既然你的项目被托管到别的地方了, 你的朋友可以更容易地为你的项目做贡献(或者拉取最新的变更)

现在用网站来对远程仓库进行可视化操作变得越发流行了(像 [GitHub](https://github.com/)), 但远程仓库**永远**是这些工具的顶梁柱, 因此理解其概念非常的重要!



### 																Git Clone

直到现在, 教程都聚焦于**本地**仓库的操作（branch、merge、rebase 等等）。但我们现在需要学习远程仓库的操作 —— 我们需要一个配置这种环境的命令, 它就是 **`git clone`**。 从技术上来讲，`git clone` 命令在真实的环境下的作用是在**本地创建**一个**远程仓库的拷贝**（比如从 github.com）。 但在我们的教程中使用这个命令会有一些不同 —— 它会在远程创建一个你本地仓库的副本。显然这和真实命令的意思刚好相反，但是它帮咱们把本地仓库和远程仓库关联到了一起，在教程中就凑合着用吧。



咱们慢慢来，先看看远程仓库（在图示中）的样子。

![image-20250928170259342](/Users/wjb/Library/Application Support/typora-user-images/image-20250928170259342.png)

```
git clone
```

![image-20250928170349232](/Users/wjb/Library/Application Support/typora-user-images/image-20250928170349232.png)

现在我们**有了**一个**自己项目的远程仓库**。除了**远程仓库使用虚线**之外, 它们几乎没有什么差别 —— 在后面的关卡中, 你将会学习怎样在本地仓库和远程仓库间分享工作成果。



### 															远程分支

既然你已经看过 `git clone` 命令了，咱们深入地看一下发生了什么。

你可能注意到的第一个事就是在我们的**本地仓库多了一个名为 `o/main` 的分支**, 这种类型的分支就叫**远程分支**。由于远程分支的特性导致其拥有一些特殊属性。

**远程分支反映了远程仓库(在你上次和它通信时)的状态**。这会有助于你理解本地的工作与公共工作的差别 —— 这是你与别人分享工作成果前至关重要的一步.

远程分支有一个特别的属性，在你**切换到远程分支时**，**自动进入分离 HEAD 状态**。Git 这么做是出于不能直接在这些分支上进行操作的原因, 你必须在别的地方完成你的工作, （更新了远程分支之后）再用远程分享你的工作成果。

**为什么有 `o/`？**

你可能想问这些远程分支的前面的 `o/` 是什么意思呢？好吧, **远程分支有一个命名规范** —— 它们的格式是: 

- **`<remote name>/<branch name>`**

因此，如果你看到一个名为 `o/main` 的分支，那么这个分支就叫 `main`，远程仓库的名称就是 `o`。

**大多数的开发人员会将它们主要的远程仓库命名为 `origin`，并不是 `o`。**这是因为当你**用 `git clone` 某个仓库**时，**Git** 已经**帮你把远程仓库的名称设置为 `origin`** 了

不过 `origin` 对于我们的 UI 来说太长了，因此不得不使用简写 `o` :) 但是要记住, 当你使用真正的 Git 时, 你的远程仓库默认为 `origin`! 

说了这么多，让我们看看实例。

![image-20250928171648980](/Users/wjb/Library/Application Support/typora-user-images/image-20250928171648980.png)

如果切换到远程分支会怎么样呢？

```
git checkout o/main ;
git commit;
```

正如你所见，**Git 变成了分离 HEAD 状态**，**当添加新的提交时 `o/main` 也不会更新**。这是**因为 `o/main` 只有在远程仓库中相应的分支更新了以后才会更新。**

![image-20250928171931766](/Users/wjb/Library/Application Support/typora-user-images/image-20250928171931766.png)



### 															Git Fetch

**Git 远程仓库**相当的**操作**实际可以**归纳为两点**：**向远程仓库传输数据**以及从**远程仓库获取数据**。既然我们能与远程仓库同步，那么就可以分享任何能被 Git 管理的更新（因此可以分享代码、文件、想法、情书等等）。

本节课我们将学习**如何从远程仓库获取数据** —— 命令如其名，它就是 **`git fetch`。**

你会看到当我们从远程仓库获取数据时, 远程分支也会更新以反映最新的远程仓库。在上一节课程中我们已经提及过这一点了。

![image-20250928173239862](/Users/wjb/Library/Application Support/typora-user-images/image-20250928173239862.png)

在解释 `git fetch` 前，我们先看看实例。这里我们有一个远程仓库, 它有两个我们本地仓库中没有的提交。

```
git fetch
```

就是这样了! **`C2`,`C3` 被下载到了本地仓库，同时远程分支 `o/main` 也被更新**，反映到了这一变化

![image-20250928173513047](/Users/wjb/Library/Application Support/typora-user-images/image-20250928173513047.png)

**git fetch 做了些什么**

`git fetch` 完成了仅有的但是很重要的两步:

- **从远程仓库下载本地仓库中缺失的提交记录**
- **更新远程分支指针(如 `o/main`)**

`git fetch` 实际上将本地仓库中的远程分支更新成了远程仓库相应分支最新的状态。

如果你还记得上一节课程中我们说过的，远程分支反映了远程仓库在你**最后一次与它通信时**的状态，`git fetch` 就是你与远程仓库通信的方式了！希望我说的够明白了，你已经了解 `git fetch` 与远程分支之间的关系了吧。

`git fetch` 通常通过互联网（使用 `http://` 或 `git://` 协议) 与远程仓库通信。



**git fetch 不会做的事**

**`git fetch` 并不会改变你本地仓库的状态。它不会更新你的 `main` 分支，也不会修改你磁盘上的文件**。

理解这一点很重要，因为许多开发人员误以为执行了 `git fetch` 以后，他们本地仓库就与远程仓库同步了。它可能已经将进行这一操作所需的所有数据都下载了下来，但是**并没有**修改你本地的文件。我们在后面的课程中将会讲解能完成该操作的命令 :D

所以, 你可以将 `git fetch` 的理解为单纯的下载操作。



###  													Git Pull

既然我们已经知道了如何用 `git fetch` 获取远程的数据, 现在我们学习如何将这些变化更新到我们的工作当中。

其实有很多方法的 —— 当**远程分支中有新的提交**时，你可以**像合并本地分支那样来合并远程分支**。也就是说就是你可以执行以下命令: 

- **`git cherry-pick o/main`**
- **`git rebase o/main`**
- **`git merge o/main`**
- **等等**

实际上，由于**先抓取更新再合并到本地分支**这个流程很常用，因此 Git 提供**了一个专门的命令来完成这两个操作**。它就是我们要讲的 **`git pull`**。

![image-20250928174947547](/Users/wjb/Library/Application Support/typora-user-images/image-20250928174947547.png)

我们先来看看 `fetch`、`merge` 依次执行的效果

```
git fetch;
git merge o/main;
```

我们**用 `fetch` 下载了 `C3`**, 然后通过 **`git merge o/main`合并了这一提交记录**。现在我们的 `main` 分支包含了远程仓库中的更新（在本例中远程仓库名为 `origin`）

![image-20250928175159287](/Users/wjb/Library/Application Support/typora-user-images/image-20250928175159287.png)

如果使用 `git pull` 呢?

```
git pull
```

同样的结果！这清楚地说明了 **`git pull` 就是 git fetch 和 git merge** 的**缩写**！

![image-20250928175441285](/Users/wjb/Library/Application Support/typora-user-images/image-20250928175441285.png)





### 																	Git Push

OK，我们已经学过了如何从远程仓库获取更新并合并到本地的分支当中。这非常棒……但是我如何与大家分享我的成果呢？

嗯，上传自己分享内容与下载他人的分享刚好相反，那与 `git pull` 相反的命令是什么呢？`git push`！

**`git push`** 负责将你的变更**上传到指定的远程仓库**，**并在远程仓库上合并你的新提交记录**。一旦 `git push` 完成, 你的朋友们就可以从这个远程仓库下载你分享的成果了！

你可以将 `git push` 想象成发布你成果的命令。它有许多应用技巧，稍后我们会了解到，但是咱们还是先从基础的开始吧……

*注意 —— **`git push` 不带任何参数时的行为与 Git 的一个名为 `push.default` 的配置有关。它的默认值取决于你正使用的 Git 的版本，**但是在教程中我们使用的是 `upstream`。 这没什么太大的影响，但是在你的项目中进行推送之前，最好检查一下这个配置。*



这里我们准备了一些远程仓库中没有的提交记录, 咱们开始先上传吧!

![image-20250928182617787](/Users/wjb/Library/Application Support/typora-user-images/image-20250928182617787.png)

```
git push
```

过去了, **远程仓库接收了 `C2`**，**远程仓库中的 `main` 分支也被更新到指向 `C2`** 了，我们**的远程分支 (o/main) 也同样被更新**了。所有的分支都同步了！

![image-20250928182717427](/Users/wjb/Library/Application Support/typora-user-images/image-20250928182717427.png)



### 															偏离的工作

现在我们已经知道了如何从其它地方 `pull` 提交记录，以及如何 `push` 我们自己的变更。看起来似乎没什么难度，但是为何还会让人们如此困惑呢？

困难来自于**远程库提交历史的偏离。**在讨论这个问题的细节前，我们先来看一个例子……

**假设你周一克隆了一个仓库，然后开始研发某个新功能**。到周五时，你新功能开发测试完毕，可以发布了。但是 —— 天啊！**你的同事这周写了一堆代码，还改了许多你的功能中使用的 API**，这些变动会导致你新开发的功能变得不可用。但是他们已经将那些提交推送到远程仓库了，因此你**的工作就变成了基于项目旧版的代码，与远程仓库最新的代码不匹配**了。

这种情况下, `git push` 就不知道该如何操作了。如果你执行 `git push`，Git 应该让远程仓库回到星期一那天的状态吗？还是直接在新代码的基础上添加你的代码，亦或由于你的提交已经过时而直接忽略你的提交？

**因为这情况（历史偏离）有许多的不确定性，Git 是不会允许你 `push` 变更的。实际上它会强制你先合并远程最新的代码，然后才能分享你的工作**。



说了这么多，咱们还是看看实际案例吧！

![image-20250928183347747](/Users/wjb/Library/Application Support/typora-user-images/image-20250928183347747.png)

```
git push
```

**看见了吧？什么都没有变，因为命令失败了**！**`git push` 失败是因为你最新提交的 `C3` 基于远程分支中的 `C1`**。而远程仓库中该分支已经更新到 `C2` 了，所以 Git 拒绝了你的推送请求。

![image-20250928183506744](/Users/wjb/Library/Application Support/typora-user-images/image-20250928183506744.png)

**那该如何解决这个问题呢？很简单，你需要做的就是使你的工作基于最新的远程分支。**

**有许多方法做到这一点呢，不过最直接的方法就是通过 rebase 调整你的工作。咱们继续，看看怎么 rebase！**

**如果我们在 push 之前做 rebase 呢？**

![image-20250928183639140](/Users/wjb/Library/Application Support/typora-user-images/image-20250928183639140.png)

```
git fetch;
git rebase o/main;
git push;
```

我们用 **`git fetch` 更新了本地仓库中的远程分支**，然后**用 rebase 将我们的工作移动到最新的提交记录下**，最后再**用 `git push` 推送到远程仓库。**

![image-20250928184023852](/Users/wjb/Library/Application Support/typora-user-images/image-20250928184023852.png)

还有其它的方法可以在远程仓库变更了以后更新我的工作吗? 当然有，我们还可以使用 `merge`

**尽管 `git merge` 不会移动你的工作（它会创建新的合并提交）**，**但是它会告诉 Git 你已经合并了远程仓库的所有变更**。这是因为**远程分支现在是你本地分支的祖先**，也就是说你**的提交已经包含了远程分支的所有变化。**

看下演示...

**咱们用 merge 替换 rebase 来试一下……**

```
git fetch;
git merge o/main;
git push;
```

我们用 **`git fetch` 更新了本地仓库中的远程分支**，然**后合并了新变更到我们的本地分支（**为了包含远程仓库的变更），最后我们用 `git push` 把工作推送到远程仓库

![image-20250928184725906](/Users/wjb/Library/Application Support/typora-user-images/image-20250928184725906.png)

很好！但是要敲那么多命令，有没有更简单一点的？

当然 —— 前面已经介绍过 **`git pull` 就是 fetch 和 merge 的简写**，类似的 **`git pull --rebase` 就是 fetch 和 rebase** 的简写！

让我们看看简写命令是如何工作的。

**这次用 `--rebase`……**

![image-20250928185113202](/Users/wjb/Library/Application Support/typora-user-images/image-20250928185113202.png)

```
git pull --rebase;
git push ;
```

**跟之前结果一样，但是命令更短了。**

![image-20250928185305089](/Users/wjb/Library/Application Support/typora-user-images/image-20250928185305089.png)

**换用常规的 `pull`**

![image-20250928185710351](/Users/wjb/Library/Application Support/typora-user-images/image-20250928185710351.png)

```
git pull;
git push;
```

还是和以前一样

![image-20250928185813501](/Users/wjb/Library/Application Support/typora-user-images/image-20250928185813501.png)





### 													远程服务器拒绝!(Remote Rejected)

如果你是在一个大的合作团队中工作, 很可能是**main被锁定**了, **需要**一些**Pull Request流程**来**合并修改**。**如果你直接提交(commit)到本地main, 然后试图推送(push)修改, 你将会收到这样类似的信息:**

```
! [远程服务器拒绝] main -> main (TF402455: 不允许推送(push)这个分支; 你必须使用pull request来更新这个分支.)
```

**为什么会被拒绝?**

远程服务器拒绝直接推送(push)提交到main, **因为策略配置要求 pull requests 来提交更新.**

你应该按照流程,新建一个分支, 推送(push)这个分支并申请pull request,但是你忘记并直接提交给了main.现在你卡住并且无法推送你的更新.

**解决办法**

**新建一个分支feature,** **推送到远程服务器**. 然后**reset你的main分支和远程服务器保持一致**, 否则下次你pull并且他人的提交和你冲突的时候就会有问题.







------

## 									合并特性分支

既然你应该很熟悉 fetch、pull、push 了，现在我们要通过一个新的工作流来测试你的这些技能。

在大型项目中**开发人员通常会在（从 `main` 上分出来的）特性分支上工作**，工作完成后只做一次集成。这跟前面课程的描述很相像（把 side 分支推送到远程仓库），不过本节我们会深入一些.

但是有些开发人员只在 main 上做 push、pull —— 这样的话 main 总是最新的，始终与远程分支 (o/main) 保持一致。

对于接下来这个工作流，我们集成了两个步骤：

- **将特性分支集成到 `main` 上**
- **推送并更新远程分支**

让我们看看如何快速的更新 `main` 分支并推送到远程。

![image-20250930134127869](/Users/wjb/Library/Application Support/typora-user-images/image-20250930134127869.png)

```
git pull --rebase;
git push;
```

我们执行了两个命令: 

- 将我们的工作 rebase 到远程分支的最新提交记录
- 向远程仓库推送我们的工作

![image-20250930134312586](/Users/wjb/Library/Application Support/typora-user-images/image-20250930134312586.png)

**为什么不用 merge 呢?**

为了 push 新变更到远程仓库，你要做的就是**包含**远程仓库中最新变更。意思就是只要你的本地分支包含了远程分支（如 `o/main`）中的最新变更就可以了，至于具体是用 rebase 还是 merge，并没有限制。

那么既然没有规定限制，为何前面几节都在着重于 rebase 呢？为什么在操作远程分支时不喜欢用 `merge` 呢？

在开发社区里，有许多**关于 merge 与 rebase** 的讨论。以下是关于 **rebase 的优缺点**：

**优点:**

- **Rebase 使你的提交树变得很干净, 所有的提交都在一条线上**

**缺点:**

- **Rebase 修改了提交树的历史**

比如, 提交 **C1 可以被 rebase 到 C3** 之后。这看起**来 C1 中的工作是在 C3 之后进行**的，但实**际上是在 C3 之前。**

一些开发人员**喜欢保留提交历史**，因此**更偏爱 merge**。而其他人（比如我自己）可能更**喜欢干净的提交树**，于是**偏爱 rebase**。仁者见仁，智者见智。 :D



### 													远程跟踪分支

在前几节课程中有件事儿挺神奇的，Git 好像知**道 `main` 与 `o/main` 是相关**的。当然这些分支的名字是相似的，可能会让你觉得是依此将远程分支 main 和本地的 main 分支进行了关联。这种关联在以下两种情况下可以清楚地得到展示：

- **pull 操作**时, **提交记录**会被**先下载到 o/main** 上，之**后再合并到本地的 main 分支**。隐含的合并目标由这个关联确定的。
- **push 操作**时, 我们**把工作从 `main` 推到远程仓库中的 `main` 分支**(**同时会更新远程分支 `o/main`**) 。这个推送的目的地也是由这种关联确定的！



### 																	远程跟踪

直接了当地讲，**`main` 和 `o/main` 的关联关系**就是**由分支的“remote tracking”属性决定的**。**`main` 被设定为跟踪 `o/main`** —— 这意味着为 **`main` 分支指定了推送的目的地**以及**拉取后合并的目标**。

你可能想知道 `main` 分支上这个属性是怎么被设定的，你并没有用任何命令指定过这个属性呀！好吧, **当你克隆仓库**的时候, **Git 就自动帮你把这个属性设置好**了。

当你**克隆时**, Git 会为远程仓库中的**每个分支在本地仓库**中**创建一个远程分支**（比如 `o/main`）。然**后再创建一个跟踪远程仓库中活动分支的本地分支**，**默认**情况下这个本地分支会被命名**为 `main`**。

**克隆完成后**，你会**得到一个本地分支**（如果没有这个本地分支的话，你的目录就是“空白”的），但是可**以查看远程仓库中所有的分支**（如果你好奇心很强的话）。这样做对于本地仓库和远程仓库来说，都是最佳选择。

这也解释了为什么会在克隆的时候会看到下面的输出：

```
local branch "main" set to track remote branch "o/main"
```



**我能自己指定这个属性吗？**

当然可以啦！你**可以让任意分支跟踪 `o/main`,** 然后该**分支会像 `main` 分支一样得到隐含**的 **push 目的地**以及 **merge 的目标**。 这意味着你**可以在分支 `totallyNotMain` 上执行 `git push`，**将工作**推送到远程仓库的 `main` 分支上**。

**有两种方法设置这个属性**，第一种就是**通过远程分支切换到一个新的分支**，执行: 

```
git checkout -b totallyNotMain o/main
```

就可以**创建一个名**为 **`totallyNotMain` 的分支**，它**跟踪远程分支 `o/main`。**

闲话少说，咱们先看看演示！我们切换到一个名叫 `foo` 的新分支，让其跟踪远程仓库中的 `main`

![image-20250930142927153](/Users/wjb/Library/Application Support/typora-user-images/image-20250930142927153.png)

```
git checkout -b foo o/main;
git pull;
```

正如你所看到的, 我们**使用了隐含的目标 `o/main` 来更新 `foo` 分支**。需要注意的是 **main 并未被更新**！

![image-20250930143326021](/Users/wjb/Library/Application Support/typora-user-images/image-20250930143326021.png)

**git push 同样适用**

![image-20250930143405954](/Users/wjb/Library/Application Support/typora-user-images/image-20250930143405954.png)

```
git checkout -b foo o/main;
git commit ;
git push;
```

**我们将一个并不叫 `main` 的分支上的工作推送到了远程仓库中的 `main` 分支上**

![image-20250930143639590](/Users/wjb/Library/Application Support/typora-user-images/image-20250930143639590.png)



**第二种方法**

另一种**设置远程追踪分支的方法**就是使用：**`git branch -u`** 命令，执行：

```
git branch -u o/main foo
```

这样 **`foo` 就会跟踪 `o/main`** 了。如果**当前就在 foo 分支上, 还可以省略 foo**：

```
git branch -u o/main
```

看看这种方式的实际的效果...

![image-20250930143954956](/Users/wjb/Library/Application Support/typora-user-images/image-20250930143954956.png)

```
git branch -u o/main foo;
git commit ;
git push;
```

跟之前一样, 但这个命令更明确

![image-20250930144146183](/Users/wjb/Library/Application Support/typora-user-images/image-20250930144146183.png)





------

## 									Git Push 的参数

很好! 既然你知道了远程跟踪分支，我们可以开始揭开 git push、fetch 和 pull 的神秘面纱了。我们会逐个介绍这几个命令，它们在理念上是非常相似的。

首先来看 `git push`。在远程跟踪课程中，你已经学到了 Git 是通过当前所在分支的属性来确定远程仓库以及要 push 的目的地的。这是未指定参数时的行为，我们可以为 push 指定参数，语法是：

```
git push <remote> <place>
```

**`<place>` 参数是什么意思呢**？我们稍后会深入其中的细节, 先看看例子, 这个命令是:

```
git push origin main
```

把这个命令翻译过来就是：

***切到本地仓库中的“main”分支**，**获取所有的提交**，**再到远程仓库“origin”中找到“main”分支**，将**远程仓库中没有的提交记录都添加上去**，搞定之后告诉我。*

我们通过“**place”参数**来**告诉 Git 提交记录来自于 main,** 要推送到远程仓库中的 main。它实际就是要同步的两个仓库的位置。

需要注意的是，因为我们通过**指定参数告诉了 Git 所有它需要的信息, 所以它就忽略了我们所切换分支的属性**！

我们看看指定参数的例子。**注意下我们当前分支的位置**。

![image-20250930150054169](/Users/wjb/Library/Application Support/typora-user-images/image-20250930150054169.png)

```
git checkout c0;
git push origin main;
```

好了! **通过指定参数, 远程仓库中的 `main` 分支得到了更新**。

![image-20250930150229566](/Users/wjb/Library/Application Support/typora-user-images/image-20250930150229566.png)

**如果不指定参数会发生什么呢?**

![image-20250930150312551](/Users/wjb/Library/Application Support/typora-user-images/image-20250930150312551.png)

```
git checkout c0;
git push;
```

**命令失败了（正如你看到的，什么也没有发生）! 因为我们所切换的 HEAD 没有跟踪任何分支。**

### 							

### 											`<place>`参数详解

还记得之前课程说的吧，当为 **git push 指定 place 参数为 `main` 时，我们同时指定了提交记录的来源和去向**。

你可能想问 —— 如果来源和去向分支的名称不同呢？比如你想**把本地的 `foo` 分支推送到远程仓库中的 `bar` 分支**。

哎，很遗憾 Git 做不到…… 开个玩笑，别当真！当然是可以的啦 :) Git 拥有超强的灵活性（有点过于灵活了）

接下来咱们看看是怎么做的……

**要同时为源和目的地指定 `<place>` 的话，只需要用冒号 `:` 将二者连起来就可以了**：

```
git push origin <source>:<destination>
```

这个参数实际的值是个 refspec，“refspec” 是一个自造的词，意思是 Git 能识别的位置（比如分支 `foo` 或者 `HEAD~1`）

一旦你指定了独立的来源和目的地，就可以组织出言简意赅的远程操作命令了，让我们看看演示！



**记住，`source` 可以是任何 Git 能识别的位置：**

![image-20250930151559756](/Users/wjb/Library/Application Support/typora-user-images/image-20250930151559756.png)

```
git push origin foo^:main
```

这是个令人困惑的命令，但是它确实是可以运行的 —— **Git 将 `foo^` 解析为一个位置**，**上传所有未被包含到远程仓库里 `main` 分支中的提交记录**

![image-20250930151911846](/Users/wjb/Library/Application Support/typora-user-images/image-20250930151911846.png)



**如果你要推送到的目的分支不存在会怎么样呢？没问题！Git 会在远程仓库中根据你提供的名称帮你创建这个分支！**

![image-20250930152023412](/Users/wjb/Library/Application Support/typora-user-images/image-20250930152023412.png)

```
git push origin main:newBranch
```

![image-20250930152148272](/Users/wjb/Library/Application Support/typora-user-images/image-20250930152148272.png)



## 									Git fetch 的参数

我们刚学习了 git push 的参数，很酷的 `<place>` 参数，还有用冒号分隔的 refspecs（`<source>:<destination>`）。 这些参数可以用于 `git fetch` 吗？

你猜中了！**`git fetch` 的参数和 `git push` 极其相似**。他们的概念是相同的，只是方向相反罢了（因为现在你是下载，而非上传）

让我们逐个讨论下这些概念……

### `<place>` 参数

如果你像如下命令这样为 git fetch 设置 的话：

```
git fetch origin foo
```

**Git 会到远程仓库的 `foo` 分支上，然后获取所有本地不存在的提交，放到本地的 `o/foo`** 上。

来看个例子（还是前面的例子，只是命令不同了）

![image-20250930153040348](/Users/wjb/Library/Application Support/typora-user-images/image-20250930153040348.png)

```
git fetch origin foo
```

我们只下载了远程仓库中 **`foo` 分支中的最新提交记录，并更新了 o/foo**

![image-20250930153212101](/Users/wjb/Library/Application Support/typora-user-images/image-20250930153212101.png)

你可能会好奇 —— 为何 Git **会将新提交放到 `o/foo` 而不是放到我本地的 foo 分支呢？**之前不是说这样的 参数就是同时应用于本地和远程的位置吗？

好吧, 本例中 Git 做了一些特殊处理，因为你可能在 foo 分支上的工作还未完成，你也不想弄乱它。还记得在 `git fetch` 课程里我们讲到的吗 —— 它不会更新你的本地的非远程分支, 只是下载提交记录（这样, 你就可以对远程分支进行检查或者合并了）。



“如**果我们指定 `<source>:<destination>` 会发生什么**呢？”

如果你觉得直接更新本地分支很爽，那你就用冒号分隔的 refspec 吧。不过，你不能在当前切换的分支上干这个事，但是其它分支是可以的。

这里有一点是需要注意的 —— **`source` 现在指的是远程仓库中的位置**，而 `<destination>` 才是要放置提交的本地仓库的位置。它与 git push 刚好相反，这是可以讲的通的，因为我们在往相反的方向传送数据。

理论上虽然行的通，但开发人员很少这么做。我在这里介绍它主要是为了从概念上说明 `fetch` 和 `push` 的相似性，只是方向相反罢了。

来看个疯狂的例子：

![image-20250930153750238](/Users/wjb/Library/Application Support/typora-user-images/image-20250930153750238.png)

```
git fetch origin c2:bar
```

哇! 看见了吧, **Git 将 `C2` 解析成一个 origin 仓库的位置，然后将那些提交记录下载到了本地的 `bar` 分支（**一个本地分支）上。

![image-20250930153904260](/Users/wjb/Library/Application Support/typora-user-images/image-20250930153904260.png)

**如果执行命令前目标分支不存在会怎样呢？我们看一下上个对话框中没有 bar 分支的情况。**

![image-20250930154001314](/Users/wjb/Library/Application Support/typora-user-images/image-20250930154001314.png)

```
git fetch origin c2:bar
```

**看见了吧，跟 git push 一样，Git 会在 fetch 前自己创建立本地分支, 就像是 Git 在 push 时，如果远程仓库中不存在目标分支，会自己在建立**一样。

![image-20250930154411827](/Users/wjb/Library/Application Support/typora-user-images/image-20250930154411827.png)

没有参数呢?

**如果 `git fetch` 没有参数，它会下载所有的提交记录到各个远程分支……**

![image-20250930154536812](/Users/wjb/Library/Application Support/typora-user-images/image-20250930154536812.png)

```
git fetch
```

![image-20250930154623826](/Users/wjb/Library/Application Support/typora-user-images/image-20250930154623826.png)

###                      	  					 古怪的 `<source>`

Git 有两种关于 `<source>` 的用法是比较诡异的，即你可以在 **git push 或 git fetch 时不指定任何 `source`，方法就是仅保留冒号和 destination 部分，source 部分留空。**

- `git push origin :side`
- `git fetch origin :bugFix`

我们分别来看一下这两条命令的作用……

**如果 push 空 到远程仓库会如何呢？它会删除远程仓库中的分支！**

![image-20250930160102691](/Users/wjb/Library/Application Support/typora-user-images/image-20250930160102691.png)

```
git push origin :foo
```

**就是这样子, 我们通过给 push 传空值 source，成功删除了远程仓库中的 `foo` 分支, 这真有意思...**

![image-20250930160206304](/Users/wjb/Library/Application Support/typora-user-images/image-20250930160206304.png)

**如果 fetch 空 到本地，会在本地创建一个新分支。**

![image-20250930160238734](/Users/wjb/Library/Application Support/typora-user-images/image-20250930160238734.png)

```
git fetch origin :bar
```

![image-20250930160320079](/Users/wjb/Library/Application Support/typora-user-images/image-20250930160320079.png)



## 									Git pull 参数

既然你已经掌握关于 `git fetch` 和 `git push` 参数的方方面面了，关于 git pull 几乎没有什么可以讲的了 :)

因为 **git pull 到头来就是 fetch 后跟 merge 的缩写**。你可以理解为用同样的参数执行 git fetch，然后再 merge 你所抓取到的提交记录。

还可以和其它更复杂的参数一起使用, 来看一些例子:

以下命令在 Git 中是等效的:

`**git pull origin foo` 相当于：**

```
git fetch origin foo; git merge o/foo
```

还有...

**`git pull origin bar:bugFix` 相当于：**

```
git fetch origin bar:bugFix; git merge bugFix
```

看到了? git pull 实际上就是 fetch + merge 的缩写, git pull 唯一关注的是提交最终合并到哪里（也就是为 git fetch 所提供的 destination 参数）

一起来看个例子吧：

**如果我们指定要抓取的 place，所有的事情都会跟之前一样发生，只是增加了 merge 操作**

![image-20250930160717739](/Users/wjb/Library/Application Support/typora-user-images/image-20250930160717739.png)

```
git pull origin main
```

**通过指定 `main` 我们更新了 `o/main`。然后将 `o/main` merge 到我们的所在的分支，无论我们当前所在的位置是哪。**

![image-20250930161031562](/Users/wjb/Library/Application Support/typora-user-images/image-20250930161031562.png)

**pull 也可以用 source:destination 吗? 当然喽, 看看吧:**

![image-20250930161130822](/Users/wjb/Library/Application Support/typora-user-images/image-20250930161130822.png)

```
git pull origin main:foo
```

**哇, 这个命令做的事情真多。它先在本地创建了一个叫 `foo`的分支，从远程仓库中的 main 分支中下载提交记录，并合并到 `foo`，然后再 merge 到我们的当前所在的分支 `bar`上。操作够多的吧？！**

![image-20250930161525603](/Users/wjb/Library/Application Support/typora-user-images/image-20250930161525603.png)

