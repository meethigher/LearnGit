---
title: Git本地仓库入门教程
---

> 详细教程：参考[https://www.liaoxuefeng.com/wiki/896043488029600](https://www.liaoxuefeng.com/wiki/896043488029600)

### 

#### 第一步 初始化本地仓库

`git init`初始化一个本地仓库

```
$ git init
Initialized empty Git repository in C:/Users/kitchen/Desktop/Theme/.git/
```

---



#### 第二步 将文件添加到版本库

1. `git add <filename>`将文件添加到版本库
2. `git commit -m <message>`完成，<message>最好是写，而且是`英文`！

```
$ git add test.txt

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   test.txt

$ git commit -m "first commit"
[master (root-commit) 42ce0e6] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

---



#### 第三步 随时掌握工作区状态

如果修改了项目内容，可以通过`git status`来查看工作区的状态

如果`git status` 告诉你文件被修改过，用过`git diff <filename>`可以查看修改内容

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")


$ git diff test.txt
diff --git a/test.txt b/test.txt
index a1b78e2..aab983c 100644
--- a/test.txt
+++ b/test.txt
@@ -1 +1,2 @@
-first commit
\ No newline at end of file
+first commit
+second commit
\ No newline at end of file

```

---



#### 第四步 版本回退

可以通过`git log`查看***最近到远***的版本日志

```
$ git log
commit f6af78dc6dc5944e0e04df3ac46b83ecc667a3c4 (HEAD -> master)
Author: meethigher <meethigher@qq.com>
Date:   Thu Oct 3 18:18:28 2019 +0800

    third commit

commit 535bf16545a58f9e8c6f9d29218e5c46befa9a67
Author: meethigher <meethigher@qq.com>
Date:   Thu Oct 3 18:17:25 2019 +0800

    second commit

commit 5d8a7ff0c255d26df63e675393a85c756e4230ce
Author: meethigher <meethigher@qq.com>
Date:   Thu Oct 3 18:07:23 2019 +0800

    first commit
```

如果想要只输出文件版本号<head>跟注释，可以通过`git log --pretty=oneline`查看

```
$ git log --pretty=oneline
f6af78dc6dc5944e0e04df3ac46b83ecc667a3c4 (HEAD -> master) third commit
535bf16545a58f9e8c6f9d29218e5c46befa9a67 second commit
5d8a7ff0c255d26df63e675393a85c756e4230ce first commit
```

现在的位置是在third commit，如果想要回退到first commit，可以通过`git reset --hard <HEAD>`

```
$ git reset --hard 5d8a7ff0c255d26df63e675393a85c756e4230ce
HEAD is now at 5d8a7ff first commit
```

可以看到现在已经回退到了first commit

但是，此时如果再用`git log`会发现之后的最新的那几个版本已经看不到了！

这就好比你从21世纪穿梭到19世纪，回不去了。

解决办法：

1. 命令行没有清空的情况下，可以找之前的版本号
2. 命令行清空的情况下，可以通过`git reflog`来找版本号，`git reflog`用来记录你的每一次命令

```
$ git reflog
5d8a7ff (HEAD -> master) HEAD@{0}: reset: moving to 5d8a7ff0c255d26df63e675393a85c756e4230ce
f6af78d HEAD@{1}: commit: third commit
535bf16 HEAD@{2}: commit: second commit
5d8a7ff (HEAD -> master) HEAD@{3}: commit (initial): first commit
```

牛批，我又找到版本号了！

### 