##### 学习简单的git命令

------

什么是版本库？版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。

跟着我，开启时光之旅。

1. 首先建个文件夹来存放版本信息，在D盘下建个gittest文件夹，此时文件夹为空文件夹。

2. 进入gittest文件夹，右键选择 “Git Bash Here”，打开了命令行窗口。

3. 初始化版本库，初始完成后，gittest文件夹下多了个.git文件夹,这个目录是Git来跟踪管理版本的，没事千万不要手动乱改这个目录里面的文件，否则，会把git仓库给破坏了

   ```bash
   git init
   ```

4.把文件添加到版本库中

- 在gittest文件夹中新建一个文件，例如 “first.c”，文件内容为。

```c
#include "stdio.h"

int main()
{
    printf("hello world");
    return 0;
}

```

- 把“first.c”添加到到暂存区

  ```bash
  git add first.c
  ```

- 把文件添加到仓库

```bash
git commit -m "提交first.c文件到仓库"
```

- 修改“first.c”内容，改为如下：

```c
#include "stdio.h"

int main()
{
    int i = 0;
    printf("the i is %d ",i);
    return 0;
}
```

