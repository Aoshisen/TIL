# less 的一些便捷的写法

```less
@fallback: Georgia, serif;

h1, .h1 {
  // 备份字体
  font-family: @fallback;

  .font-loaded & {
    font-family: "My Family";
  }
}
```

就相当于下面的写法

```css
h1, .h1 {
  font-family: Georgia, serif;
}
.font-loaded h1, .font-loaded .h1 {
  font-family: "My Family";
}
```
