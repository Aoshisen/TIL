# 通过bind函数传递函数到已经存在的函数里面

我们先定义一个方法,有两个参数

```javascript
 function Foo(a,b){
    return a+b
}
```

但是我想使用的时候只传递第二个参数进去

```javascript
 function Foo(a,b){
    return a+b
}
 function FooPlus(b){
    return Foo(1,b)
}
```

如果是填充第一个参数的话，上面这个方法不免有点粗暴，但是如果需要填充第二个参数的话暂时只能想到上面的方法

通过bind改造 Foo

```javascript
 function Foo(a,b){
    return a+b
}
//bind的第二个值会填充到Foo函数的第一个参数上面
Foo=Foo.bind(null,1)
```
