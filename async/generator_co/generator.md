# es6的generator是什么？

generator指的是

```
function* xxx(){
} 
```
是es6里的写法。

```
function* test() {
    console.log('1');
    yield 1;
    console.log('2');
    yield 2;
    console.log('3');
}
```


代码中间插了两行yield，代表什么呢？

- 当test执行到 yield 1这一行的时候，程序将被挂起，要等待执行下一步的指令；
- 当接收到指令后，test将继续往下运行，直到yield 2这一行，然后程序又被挂起并等待指令；
- 收到指令后，test又将继续运行，而下面已经没有yield了，那么函数运行结束。

这是不是就像，我们调试代码的时候，给插的断点 ？

当然，断点这个比喻，只是表象上比较相像，实质原理还是有非常大差异。


yield就是让后面的generator执行完成后，才继续往下走。


要注意，function后面多了一个星号，这样是表明这个函数将变成一个生成器函数，而不是一个普通函数了。意思就是，test这个函数，将不能被这样执行

test();
但可以获得一个生成器

var gen = test();  // gen就是一个生成器了
然后，生成器可以通过next()来执行运行

gen.next();

也就是上面说的，让函数继续运行的指令。

简单地总结一下：

- 生成器通过yield设置了一些类似”断点“的东西，使得函数执行到yield的时候会被阻断；
- 生成器要通过next()指令一步一步地往下执行（两个yield之间为一步）；
- yield 语句后面带着的表达式或函数，将在阻断之前执行完毕；
- yield 语句下面的代码，将不可能在阻断之前被执行；

由此可以看出，yield是如何将异步非阻塞代码，变成 异步阻塞代码。