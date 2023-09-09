## 需要将正在开发中的一部分代码提交一个PR，如何操作？

首先，你正在开发的代码一定在某一个开发分支上，不妨假定为dev分支。其次，你在dev分支上做了涉及到多个模块/功能的修改，假设修改所在相对路径分别为 ./module1 ./module2。现在你需要将./module1 中写完的代码提交一个PR，并merge到master分支上。该怎么做？

- 基于master分支新建一个分支，专门用来做PR（在PR approved 之后可以删除）。
```git
git branch mypr master
```

- 将dev分支中的指定文件/目录checkout到mypr分支中。
```git
git checkout dev ./module1
```
关于该命令可参考git的官方文档：
```
git checkout [<tree-ish>] [--] <pathspec>…​

Overwrite paths in the working tree by replacing with the contents in the index or in the <tree-ish> (most often a commit). When a <tree-ish> is given, the paths that match the <pathspec> are updated both in the index and in the working tree.

The index may contain unmerged entries because of a previous failed merge. By default, if you try to check out such an entry from the index, the checkout operation will fail and nothing will be checked out. Using -f will ignore these unmerged entries. The contents from a specific side of the merge can be checked out of the index by using --ours or --theirs. With -m, changes made to the working tree file can be discarded to re-create the original conflicted merge result.
```

这个操作之后，dev分支中的 ./module1 将会覆盖你 mypr分支中的相应目录（如果没有则会新建）。这样，你的更改就被放到了mypr分支。

- 在mupr分支提交你的更改并push到远端

```
git add .
git commit -m"modify module1"
git push
```