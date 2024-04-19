# 前端 pointer-events:none 的妙用

- 需求场景: 我有一个视频区域,视频区域本身就是可点击的,我想要视频区域不可点击,并且包裹视频区域的他的父级节点可点击
  [mdn 文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/pointer-events)

这个时候由于点击事件的触发逻辑,他肯定是先捕获到点击到了 video 标签,然后再冒泡到视频容器组件. 这个时候如果去禁止冒泡行为,那么外层的父级节点的点击事件是触发不了的

我又想如果我阻止冒泡行为,不行那么我就去阻止 video 元素的捕获阶段,但是我 video 是封装的组件,不太好操作

然后就是最后的解决方案

使用 pointer-events:none 来禁用用户的所有行为,比如 hover click 等等, 这个属性添加在视频 video 标签的 video 容器上,而 video 的容器的父节点的点击事件还是可以正常触发

bingo
完美解决
