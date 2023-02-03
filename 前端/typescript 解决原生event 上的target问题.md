# typescript 解决原生 event target 的问题

原因: 我想要在这样*e.target.value* 使用我的代码 但是这样我们的 ts 代码会飘红报错

下面介绍三种方法来使得类型校验通过

1. 前置的类型断言

   ```typescript
   this.countUpdate.emit((<HTMLTextAreaElement>e.target).value./*...*/)
   ```

2. 使用后置的 as 断言

   ```typescript
        const target = e.target as HTMLTextAreaElement;

       this.countUpdate.emit(target.value./*...*/)
   ```

3. 构造一个含有类型参数的函数来帮助我们断言

   ```typescript

        // create a new type HTMLElementEvent that has a target of type you pass
        // type T must be a HTMLElement (e.g. HTMLTextAreaElement extends HTMLElement)
        type HTMLElementEvent<T extends HTMLElement> = Event & {
        target: T;
        // probably you might want to add the currentTarget as well
        // currentTarget: T;
        }

        // use it instead of Event
        let e: HTMLElementEvent<HTMLTextAreaElement>;

        console.log(e.target.value);

        // or in the context of the given example
        emitWordCount(e: HTMLElementEvent<HTMLTextAreaElement>) {
        this.countUpdate.emit(e.target.value);
        }

    ```

> NOTE：前两个方法都有弊端，我们无法很好的拓展我们的申明，前两种的做法也太生硬了，无法做到通用，所以个人很推荐第三种写法，这也和react里面的实现方法如出一辙

