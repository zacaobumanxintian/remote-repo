```
PS C:\Users\wzx> git -v
git version 2.49.0.windows.1
PS C:\Users\wzx> git config --global user.name "wzx"
PS C:\Users\wzx> git config --global user.email zexinwu86@gmail.com
PS C:\Users\wzx> git config --global credential.helper store
PS C:\Users\wzx> git config --global --list
user.name=wzx
user.email=zexinwu86@gmail.com
credential.helper=store


git init + 仓库名  创建仓库
ls 查看工作区文件
git ls-files 查看暂存区文件
git status 查看仓库状态 版本库
```



```

wzx@zexinwuethereal MINGW64 /test (main)
$ git init repo
Initialized empty Git repository in D:/Download/Git/test/repo/.git/

wzx@zexinwuethereal MINGW64 /test (main)
$ cd repo

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo 111 > file1.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo 222 > file1.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo 222 > file2.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo 333 > file3.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git add file1.txt
warning: in the working copy of 'file1.txt', LF will be replaced by CRLF the nex
t time Git touches it

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -m "commit1"
[main (root-commit) 049a927] commit1
 1 file changed, 1 insertion(+)
 create mode 100644 file1.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git add file2.txt
warning: in the working copy of 'file2.txt', LF will be replaced by CRLF the nex
t time Git touches it

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -m "commit2"
[main 4562685] commit2
 1 file changed, 1 insertion(+)
 create mode 100644 file2.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git add file3.txt
warning: in the working copy of 'file3.txt', LF will be replaced by CRLF the nex
t time Git touches it

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -m "commit3"
[main fdcc627] commit3
 1 file changed, 1 insertion(+)
 create mode 100644 file3.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git log
commit fdcc6278289a8ff8f1ef135bc6dd7eb61f3d406c (HEAD -> main)
Author: wzx <424086634@qq.com>
Date:   Mon Feb 24 22:14:48 2025 +0800

    commit3

commit 45626856c6c16e487442588fbc31c39795b04fae
Author: wzx <424086634@qq.com>
Date:   Mon Feb 24 22:14:40 2025 +0800

    commit2

commit 049a9276ee43fd07a802ebc6760ed6da229fa555
Author: wzx <424086634@qq.com>
Date:   Mon Feb 24 22:14:26 2025 +0800

    commit1

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git log --oneline
fdcc627 (HEAD -> main) commit3
4562685 commit2
049a927 commit1

wzx@zexinwuethereal MINGW64 /test/repo (main)
```

回退 reset



```
$ cp -rf repo repo-soft
$ cp -rf repo repo-hard
$ cp -rf repo repo-mixed
$ cd repo-soft
$ git reset --soft 4562685
$ git ls-files  查看暂存区的内容
$ git reset --hard HEAD^ 表示回退上一个版本
$ git reset HEAD^ 默认mixed
$ git reflog 查看历史命令记录
```

```
git diff 比较工作区和暂存区的内容

git diff HEAD 比较工作区和版本库的差异

git diff --cached 暂存区和版本库的差异

git diff fdcc627 4562685 比较两个版本的内容
后一个版本对比前一个版本进行了什么变化
git diff 4562685 fdcc627 比较两个版本的内容
后一个版本对比前一个版本进行了什么变化

git diff HEAD^ HEAD 当前与上一个版本的对比
git diff HEAD~ HEAD 当前与上一个版本的对比
git diff HEAD~2 HEAD 当前与上上一个版本的对比
git diff HEAD~ HEAD file3.txt查看具体文件的版本对比
```

```
rm file1.txt 删除工作区文件
git add . 进行同步
git ls-files 查看暂存区文件 已经被删除
另一种删除
git rm file2.txt 工作区和暂存区同时删除
git status 查看仓库状态
git commit -m "detete1" 再提交从版本库中删除
```

.gitignore 生效前提文件不能是已经被添加到版本库的文件

`*`统配任意个字符 `?`匹配单个字符

`[]`表示匹配列表中的单个字符 比如[abc]表示a/b/c

`**`表示匹配任意的中间目录

中括号可以用短中线连接 如[0-9] ([a-z]) 表示任意一位数字(字母)

```
wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo "some log" > access.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        access.log

nothing added to commit but untracked files present (use "git add" to track)

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo "other log" > other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        access.log
        other.log

nothing added to commit but untracked files present (use "git add" to track)

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo access.log > .gitignore

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ cat .gitignore
access.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        other.log

nothing added to commit but untracked files present (use "git add" to track)

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git add .
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches
it
warning: in the working copy of 'other.log', LF will be replaced by CRLF the next time Git touches i
t

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore
        new file:   other.log


wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -m "ignore flie"
[main a63a764] ignore flie
 2 files changed, 2 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
nothing to commit, working tree clean

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git ls-files
.gitignore
file1.txt
file2.txt
file3.txt
other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ vi .gitignore

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo hello > hello.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -m "test ignore flie"
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -am "test ignore flie"
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches
it
[main 46b69e0] test ignore flie
 1 file changed, 3 insertions(+)

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git ls-files
.gitignore
file1.txt
file2.txt
file3.txt
other.log
从版本库中删除而不删除本地文件
$ git rm --cached other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo "some change" >> other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    other.log


wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -am "delete other.log"
[main 165dbfd] delete other.log
 1 file changed, 1 deletion(-)
 delete mode 100644 other.log

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status
On branch main
nothing to commit, working tree clean

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ mkdir temp

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ echo "hello" > temp/hello.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ ls
access.log  file1.txt  file2.txt  file3.txt  hello.log  other.log  temp/

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ vi .gitignore

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git status -s
 M .gitignore

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git commit -am "test ignore folder"
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches
it
[main b246ed2] test ignore folder
 1 file changed, 1 insertion(+), 1 deletion(-)

wzx@zexinwuethereal MINGW64 /test/repo (main)
$ git ls-files
.gitignore
file1.txt
file2.txt
file3.txt

wzx@zexinwuethereal MINGW64 /test/repo (main)

```

ssh配置和克隆仓库

```
git 没密码
.pub结尾的是公钥文件
```

