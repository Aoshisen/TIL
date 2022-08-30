## less var 插件
问题由来:
     我在umi中开发后台配置的时候用的less 用umi脚手架添加了src/global.less 文件后
     在其他其他组件less 文件里面用global.lesss 里面申明的变量的时候未生效

解决问题办法:
    创建一个最小复现的本地仓库，然后再创建一个src/global.less 文件

```javascript
@max:100px;
.box{
    width: @max;
    height: 100px;
    border: 1px solid #000;
}
```
    然后在index.tsx 里面去用
```
import styles from './index.less';

export default function IndexPage() {
  return (
    <div>
      <h1 className={styles.title}>Page index</h1>
      <h2 className={styles.test}>this is h2</h2>
      <h2 className='box'>111</h2>
    </div>
  );
}
```
    
>观察现象为box的样式添加上了

>得出结论:
    umi 只是把 global.less 引入到了每一个tsx文件的最前面，没有把global.less 引入到每一个less 文件的前面，所以如果需要使用全局的less 文件那么就还得在单个的less 文件里面引入一遍global.less

## 另一个痛点（引入样式过后，vscode无法自动补全我定义在global.less 里面的变量）

> 痛点的解决(vscode 安装 less var 这个插件)

### less var 插件的使用
    - 随便打开一个less 文件，然后右键，就会出现设置的东西
    - 然后设置就行了

## 新的痛点

每次新切换一个项目的时候都要去替换less var 里面定义的文件路径，就很麻烦，或许可以考虑把这个插件集成在umi脚手架中
