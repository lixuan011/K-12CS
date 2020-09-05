### 学习简单的git命令

------

什么是版本库？版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。

跟着我，开启时光之旅。



#### 初始化版本

------
1. **首先建个文件夹来存放版本信息，在D盘下建个gittest文件夹，此时文件夹为空文件夹。**

2. **进入gittest文件夹，右键选择 “Git Bash Here”，打开了命令行窗口。**

3. **初始化版本库，初始完成后，gittest文件夹下多了个.git文件夹,这个目录是Git来跟踪管理版本的，没事千万不要手动乱改这个目录里面的文件，否则，会把git仓库给破坏了**

   ```bash
   git init
   ```



#### 把文件添加到版本库中

------

- **在gittest文件夹中新建一个文件，例如 “first.c”，文件内容为。**

```c
#include "stdio.h"

int main()
{
    printf("hello world");
    return 0;
}

```

- **把“first.c”添加到到暂存区**

```bash
git add first.c
```

- **把文件添加到仓库，需要添加描述信息，良好的描述信息有助于与别人沟通，后悔的时候，也容易知道从什么地方从头再来。**

```bash
git commit -m "提交first.c文件到仓库"
```

- **修改“first.c”内容，改为如下：**

```c
#include "stdio.h"

int main()
{
    int i = 0;
    printf("the i is %d ",i);
    return 0;
}
```

- **修改了文件后，我们可以用查看下状态，可以查看我们对文件进行的操作。**

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   first.c

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        first.exe
        first.o

no changes added to commit (use "git add" and/or "git commit -a")

```

- **通过以下命令，我们查看到具体改变了什么。**

```bash
$ git diff first.c
diff --git a/first.c b/first.c
index 5931bdb..6ab7cb7 100644
--- a/first.c
+++ b/first.c
@@ -2,6 +2,7 @@

 int main()
 {
-    printf("hello world");
+    int i = 0;^M
+    printf("the i is %d ",i);^M
     return 0;
 }

```

#### 版本回退（时光倒流）
------
##### 回滚操作

- **文件经过不断的修改，要回到过去，需要知道过去到底经历了什么，此时我们可以查看log信息，查看文件变动记录。**

```bash
$ git log
commit 8b6d11af5fda821479cc9e22f43e1849256eb9f0 (HEAD -> master)
Author: lixuan011 <37377858+lixuan011@users.noreply.github.com>
Date:   Sat Sep 5 22:02:10 2020 +0800

    修改代码

```

```bash
$ git log --pretty=oneline
24e5c052732a88f76791702ec1063bba909b964c (HEAD -> master) d第三次修改
8b6d11af5fda821479cc9e22f43e1849256eb9f0 修改代码
51c276a9a2a8526d666006d31338266b093317e4 提交first.c到库

```

- **知道了文件变动历史，我们就可以回到文件历史长河中的某个节点。"git log --pretty=oneline"查看的记录中，可以通过HEAD^回到上一个版本。通过HEAD^~10回到之前的10个版本。**

```bash
$ git reset --hard HEAD^
HEAD is now at 8b6d11a 修改代码

```

##### 回滚到指定的版本

- **首先我们查看版本号，“git reflog”结果的第一行就是版本号。**

```bash
$ git reflog
8b6d11a (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
24e5c05 HEAD@{1}: reset: moving to 24e5c05
8b6d11a (HEAD -> master) HEAD@{2}: reset: moving to 8b6d11a
24e5c05 HEAD@{3}: commit: d第三次修改
8b6d11a (HEAD -> master) HEAD@{4}: reset: moving to 8b6d11a
51c276a HEAD@{5}: reset: moving to HEAD^
8b6d11a (HEAD -> master) HEAD@{6}: commit: 修改代码
51c276a HEAD@{7}: commit (initial): 提交first.c到库

```

- **知道版本号后，我们就可以回到指定的版本。**

```bash
$ git reset --hard 8b6d11a
HEAD is now at 8b6d11a 修改代码
```

