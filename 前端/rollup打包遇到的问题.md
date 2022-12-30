# rollup 打包遇到的问题

> 问题描述 我需要把使用konva这个包，但是konva这个包会动态的引入canvas这个包，我 npm run dev 动态打包的时候就会报 Unresolved dependencies  ...canvas (imported by "canvas?commonjs-external")
> 看了一下konva这个库会依赖canvas这个库
> 解决方法 [@rollup/plugin-node-resolve](https://www.npmjs.com/package/@rollup/plugin-node-resolve) browser 属性 官方解释(If true, instructs the plugin to use the browser module resolutions in package.json and adds 'browser' to exportConditions if it is not present so browser conditionals in exports are applied.)

```javascript
import typescript from "@rollup/plugin-typescript";
import { nodeResolve } from "@rollup/plugin-node-resolve";
import serve from "rollup-plugin-serve";
import html from "@rollup/plugin-html";
import livereload from "rollup-plugin-livereload";
import commonjs from "@rollup/plugin-commonjs";
import css from "rollup-plugin-import-css";
export default {
  input: "src/index.ts",
  output: {
    file: "dist/bundle.js",
    format: "es",
  },

  plugins: [
    nodeResolve({
    //通过node把包解析成browser版本
      browser: true,
    }),
    commonjs(),
    css(),
    html(),
    typescript(),
    serve("dist"),
    livereload(),
  ],
};
```

> 问题二: 我引入了这个包，但是typescript提示不可用
> 原因:项目解析模块不正确

```json
{
"compilerOptions":{
    ...,
    //解决typescript 类型提示不正确的问题
    "moduleResolution": "Node" /* Specify how TypeScript looks up a file from a given module specifier. */,
}
}
```
