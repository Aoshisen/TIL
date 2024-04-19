## fullscreen 遇到的问题

项目要想点击某个视频然后全屏 并且在全屏的视频里面镶嵌 一些自定义的元素

我的实现方法是基于Element.requestFullscreen() [mdn链接](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/requestFullscreen)

但是实现了所有的交互逻辑之后,到了移动端的ios 设备,他全局是没有这个方法的 在此期间发现了这个全屏的 npm库来兼容各个浏览器 [fscreen](https://www.npmjs.com/package/fscreen)

但是到最后放弃了全屏方案改用全屏弹窗来适配各个浏览器 主要的问题还是 移动端的ios 设备不能使用全屏api



