# 如何在vscode 里面愉快的使用vim编程

1. 下载vscode 的vim插件
2. 然后进行配置
3. 我的配置 基于neo-vim[neovim配置文件](https://github.com/Aoshisen/neo-vim)
4. 然后打开 easymotion 这个插件进行单页的快速移动
5. 然后折叠函数块需要把vim:Foldfix 这个选项打开 这样上下移动的时候 折叠的代码块就不会展开了
6. 然后整理一下折叠代码块的操作和打开代码块的操作

## 如何快速的折叠代码块以及打开代码块 以及代码块相关的操作(实在不行就用鼠标，小声bb)

- zc 折叠代码块(但是不递归折叠)
- zC 递归折叠代码块
- zo 打开折叠的代码块
- zO 递归打开折叠的代码块

## VSCode + VIM 快捷键组合

VSCode 是一款完美的编辑器，现在它已经成长为 Github 上最大的开源项目。其官方团队的吕鹏，在他的极客时间专栏《玩转 VS Code》（已绝版）中，花费了大量篇幅来讲解其快捷键设计理念。

为了能将 VSCode + VIM 的快捷键组合效率最大化，VSCode 官方团队选择自己亲自维护 VIM 插件。

### VSCode VIM 示例

![alt 示例文本](https://user-images.githubusercontent.com/344283/67942034-de8df680-fc11-11e9-9392-f3f129c5f598.gif)
如以上示例图所示，组合使用 VSCode 快捷键和 VIM 快捷键，能在不使用鼠标的前提下，快速地实现以下操作：

- vib 选中小括号内的代码块
- S Visual 模式下，使用 VSCode VIM 内置的 Surround 插件，在代码块外插入 HTML Tag
- af Visual 模式下，快速选中更大范围代码块
- % 跳转至对应的括号对({[]})
- ⌘⇧\ 跳转至相应的符号对（VSCode 快捷键）
- gd 跳转至代码定义处
- ctrl+o （从代码定义处）跳转回上次代码位置
- ⌘s 保存文件（VSCode 快捷键）
- "*" Visual 模式下,快速查找光标下的单词

## vimSurround 的使用

"Hello World"

使用cs" ' 改变 " " 为 '

使用cs" < 就会出现一个提示框让你选择标签名字 然后再输入q 就可以变成

<q>Hello World</q>

如果想要变回之前的双引号的话可以用cst" 替换掉tag 为"

如果要删除双引号(ds")

如果想要给单词添加双引号

Hellow => ysiw" => "Hello"

我们还可以通过yss 来给整行添加括号什么的(yssb)

(Hello Word)
yssb
(Hello Word)

删除的话也很简单(dsb)
(Hello Word)

然后我们可以进入可视模式下面再按S< 然后就可以输入标签名字 然后可以添加标签什么的

<Template>
<div>assdfds</div>
<div>assdfds</div>
</Template>

<div>hello</div>

用t 来实现之前我们敲<插入html 节点的操作
Hello
比如ysiwt +div
<div>Hello</div>
然后ysst +div
<div><div>Hello</div></div>

## 删除一个函数

通过daI 来在函数体内部删除一个函数
如果用dai 的话会删不掉最后一个花括号
所以通过这个来补充一下

```json
  "vim.operatorPendingModeKeyBindings": [
    {
      "before": ["a", "i"],
      "after": ["a", "I"]
    }
  ],
  "vim.visualModeKeyBindings": [
    {
        "before": ["a", "i"],
        "after": ["a", "I"]
    },        
  ]
```

通过>ii 来增加缩进 我们可以看到在motion 位置的 i其实是一个ident 就是一个缩进
而通过dii 来修改函数体内所有的逻辑，当然也可以用diB 

而通过 V$%d 在函数定义行删除一个函数 是先找到函数 的第一个花括号然后再通过%定位到末端的花括号然后再删除

    const test1 = (a = 1) => {
        console.log(a)
        a = 11

        setTimeout(() => {
        console.log(a)
        }, 500);
    }

我们通过leader键来改一下

```json
  "vim.normalModeKeyBindings": [
    {
      "before": ["<Leader>", "d", "f"],
      "after": ["V", "$", "%", "d"]
    },
  ],
```