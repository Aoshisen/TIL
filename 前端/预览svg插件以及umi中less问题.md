## 预览svg的windows 插件

**问题由来**: 前端项目使用svg 图片，但是在文件夹里面预览的时候只能看到相同的图标无法具体的区分哪个是哪个，如果要区分的话就要点开图标，在网页中打开，这样太鸡肋了

**解决问题**： 下载windows 预览svg 的插件
下载地址 [SVG-Explorer-Extension](https://download.cnet.com/SVG-Explorer-Extension/3000-2248_4-78237543.html)

## umi中的global.less 问题探究
*之前探有一个问题就是说umi中的global.less中定义的全局变量没有办法在其他less 文件里面引用，然后需要在每个单独的less 文件里面再引入一下global.less 文件，这样的话又会有新的问题，就是说全局变量的自动补全不好用，如果定义的全局变量过多的话，那么我想用变量的时候找不到岂不是很蛋疼 ，然后基于这个问题又去找到了一个less var的vscode插件来帮助我们自动补全代码*

> 但是转念一想这么牛逼的一个大厂做的东西竟然有这么不人性话的东西，我去请问了我们公司的大佬

> 然后得到了这样的一个结论，global.less 作为不被编译的，就是说在global.less 中的类不会加上hash 的就相当于用less 写了普通的css 一样

那我要声明全局变量怎么办呢
**umirc.ts 配置中有一个themes的属性，可以在里面书写，然后看看效果**
>umirc.ts
```typescript
import { defineConfig } from 'umi';

export default defineConfig({
  nodeModulesTransform: {
    type: 'none',
  },
  routes: [
    { path: '/', component: '@/pages/index' },
  ],
  fastRefresh: {},
  theme:{
    "max":"100px",
  }
});
```

> index.less

```less
.test{
  height: @max;
  border: 1px solid #000;
  width: @max;
}
```

但是这个时候还是没有提醒就很难受，只是可以用这个全局变量

**思考解决方法**
1. 如果这样的话，我可以单独创建一个variable.less 单独存储变量
2. 然后在less var 里面指定这个目录，就拥有了自动补全提醒的功能
3. 然后再把这个variable.less 文件解析到umirc.ts 里面，解析成theme 规定的结构，那么就实现了功能也正常。(芜湖起飞)

> 稍稍改造了一下，嘿嘿，成了

tips: 使用了[less-vars-to-js](https://www.npmjs.com/package/less-vars-to-js)插件转化less 成对象格式 <code>import lessToJs from "less-vars-to-js";</code>
```typescript
import { defineConfig } from 'umi';
import fs from "fs";
import path from "path";

// @ts-ignore
import lessToJs from "less-vars-to-js";

const paletteLess = fs.readFileSync(path.resolve(__dirname,"./src/variable.less"), 'utf8');
const palette =lessToJs(paletteLess, {resolveVariables: true, stripPrefix: true});

export default defineConfig({
  nodeModulesTransform: {
    type: 'none',
  },
  routes: [
    { path: '/', component: '@/pages/index' },
  ],
  fastRefresh: {},
  theme:{
   ...palette
  }
});
```

>配合 less var 插件美滋滋

