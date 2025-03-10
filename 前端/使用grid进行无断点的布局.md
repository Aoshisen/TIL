# 使用grid 进行无媒体查询的布局


```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>

<body>
	<div class="grid-container">
		<div class="cell">1</div>
		<div class="cell">2</div>
		<!-- <div class="cell">3</div>
		<div class="cell">4</div>
		<div class="cell">5</div> -->
		<!-- <div class="cell">6</div> -->
	</div>
</body>
<style>
	/* autofill auto-fit	 */
	.grid-container {
		--grid-min-col-size: 275px;
		display: grid;
		/* grid-template-columns: repeat(3, 1fr); */
		/* grid-template-columns: repeat(auto-fill, 1fr); */
		/* 这样始终得到一行 但是我们可以固定设置其值		 */
		grid-template-columns: repeat(auto-fit, 1fr);

		/* 会 从左到右排列 并且没有剩余的地方会空出来*/
		grid-template-columns: repeat(auto-fit, 300px);
		/*使用minmx()来优化 单个列的宽度*/
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		/*如果 屏幕宽度小于minmax 里面小的值,那么会有超出区域的危险 使用min 函数来优化*/
		/*在小于 550px 的时候 独占一份 如果不满一行也会撑满一行 两个元素的时候 平分,单个的时候占满*/
		grid-template-columns: repeat(auto-fit, minmax(min(100%, 275px), 1fr));
		/* 看看auto-fill 的区别 所有的元素不会撑满,如果只有两个那么也从左到右排列,然后 空的地方空着*/
		grid-template-columns: repeat(auto-fill, minmax(min(100%, var(--grid-min-col-size, 200px)), 1fr));
		gap: 10px;
	}

	.cell {
		color: red;
		font-size: 30px;
		border: 1px solid;
	}
</style>

</html>
```