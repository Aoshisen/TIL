# css变量的一些骚操作，也是为了代码更加的整洁以及好维护

> 痛点，在进行移动端适配的时候 一些文字大小或者是间距发生变化，我这时候会重新的在媒体查询下面写 一些样式覆盖之前已经存在的pc 端的样式,更重要的是如果我又有其他的类来更改我当前class 类的 一些特有属性，那么代码就看起来很乱，到处都在更改属性，
 例如下面这样

```css
.text {
	font-size:20px;
}
.red {
	color:red;
	font-size: 10px;
}
@media screen and (width<=768px) {
	.text,.red {
	/* 移动端样式 */
	font-size:16px;
	}
}
```


一种更好的代码组织方案，利用var 变量以及 var 变量未读取到全局变量的情况来设置 初始默认值

```css
.text {
	font-size: var(--text-font-size,10px);
	color: var(--text-font-color,black);
}
.red {
	--text-font-size:10px;
	--text-font-color:red;
}


@media screen and (width<=768px) {
	.text,.red {
	/* 移动端样式 */
	--text-font-size:16px;
	}
}

```

这样做的好处是，在最初设定的时候给color,font-size 赋值的时候，赋值操作只进行了一次，其他的条件都是后加上去的，这样就不会到处都是样式的赋值，重新覆盖了,而是使用了类似于变量的一种形式，有当前变量就使用当前变量，变量的申明 成了控制样式切换的关键
