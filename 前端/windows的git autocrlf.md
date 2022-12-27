# 关于windows 系统下的autocrlf 问题

**问题描述**:我拉取了代码后没有做任何更改，但是却有很多新的提交，git diff 查看一下文件的不同，提示说crlf will replace lf

```bash
git config --get core.autocrlf #查看默认的autocrlf 状态
```

上面的输出如果是true的话，那么执行一下,再把所有的更改全部撤销一下就好啦

```bash
git config --global core.autocrlf false
```
