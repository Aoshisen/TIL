# git clone 一个项目到本地之后通过编辑器打开当前项目目录无项目代码的问题 探究及修复

> 场景 git clone  xxxx.git 到windows 主机 然后cd xxxx ls 查看当前目录结构发现没有项目代码

```bash
git clone xxxx.git
cd xxxx
ls
```

### 解决
之前在macos 上面推过我的项目仓库，现在是在windows 系统上面拉取代码，根据提示发现git clone 是成功的,但是checkout 到主分支的时候失败了，那么可能是不同文件系统下面的文件属性或者是策略导致的checkout 不成功
[git ntfs 保护机制](https://git-scm.com/docs/git-config)
<em> If set to true, do not allow checkout of paths that would cause problems with the NTFS filesystem, e.g. conflict with 8.3 "short" names. Defaults to true on Windows, and false elsewhere.</em>

```bash
git config core.protectNTFS false
git checkout main
```

然后就可以检出成功了 bingo