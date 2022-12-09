# VSCode + VIM 快捷键组合

VSCode 是一款完美的编辑器，现在它已经成长为 Github 上最大的开源项目。其官方团队的吕鹏，在他的极客时间专栏《玩转 VS Code》（已绝版）中，花费了大量篇幅来讲解其快捷键设计理念。

为了能将 VSCode + VIM 的快捷键组合效率最大化，VSCode 官方团队选择自己亲自维护 VIM 插件。

## VSCode VIM 示例

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
- * Visual 模式下,快速查找光标下的单词
