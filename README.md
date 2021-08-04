一、简答题
1、请说出下列最终的执行结果，并解释为什么？

    var a = [];
    for(var i = 0; i < 10; i++){
    a[i] = function (){
        console.log(i);
    };
    }
    a[6]();

>执行结果：10

>说明：这里打印的i都是全局作用域里面的i，在循环执行完成过后，这里的i已经累加到了10，无论打印的是哪个元素，它的结果都是10.


2、请说出下列最终的执行结果，并解释为什么？

    var tmp = 123;

    if(true){
    console.log(tmp);
    let tmp;
    }

>执行结果：报错，Cannot access 'tmp' before initialization。

>说明：es2015语法层面必须要先声明变量，再使用变量，否则会报出未定义的错误。


3、结合ES6新语法，用最简单的方式找出数组中的最小值？

    var arr = [12, 34, 32, 89, 4];

>答：console.log(Math.min(...arr));
执行结果：4

4、请详细说明var,let,const三种声明变量的方式之间的具体差别？

>let：
1、没有预解析，不存在变量提升
在代码块内，只要let定义变量，在之前使用，都是报错
先定义完，再使用
2、同一个作用域里，不能重复定义变量

>const:(特性和let一样,多了个“只读”)
1、const定义变量不能修改
2、const定义完变量，必须有值，不能后赋值，不能修改
3、Object.freeze(对象)

>var：
1、声明了一个变量，并且可以同时初始化该变量。
2、var语句声明的变量的作用域是当前执行位置的上下文：一个函数的内部（声明在函数内）或者全局（声明在函数外）。
3、可以在声明之前使用。


>最佳实践：不用var,主用const,配合let。

5、请说出下列代码最终输出的结果，并解释为什么？

    var a = 10;
    var obj = {
    a:20,
    fn(){
        setTimeout(()=>{
        console.log(this.a)
        })
    }
    }
    obj.fn()

>执行结果：20
>说明：变量a在obj中它的值被改为20，调用obj.fn(),当前这个this值得是指obj这个对象{ a: 20, fn: [Function: fn] },所以打印的this.a就为20。

6、简述symbol类型的用途？

>答：最主要的作用是为对象添加独一无二答属性名。
>注意：
1、Symbol不能new
2、Symbol()返回是一个唯一值
坊间传说：做一个key,定义一些唯一或者私有东西
3、symbol是一个单独的数据类型，就叫symbol，基本类型
4、如果symbol作为key,用for in循环，出不来

7、说说什么是浅拷贝、什么是深拷贝？

>答：浅拷贝：也就是拷贝A对象里面的数据，但是不拷贝A对象里面的子对象
>深拷贝：会克隆出一个对象，数据相同，但是引用地址不同（就是拷贝A对象里面的数据，而且拷贝它里面的子对象）

8、谈谈你是如何理解js异步编程的，Event Loop是做什么的，什么是宏任务，什么是微任务？

>答：
1、javascript语言的一大特点就是单线程，怎么做到异步编程？回调函数。异步解决方案一直在发展中，从 callback => promise => generator => async/await。
2、Event Loop 是一个很重要的概念，指的是计算机系统的一种运行机制，来解决单线程运行带来的一些问题。"Event Loop是一个程序结构，用于等待和发送消息和事件。
3、宏任务是回调队列中的任务，宏任务执行过程中可以临时加上一些额外需求，可以选择作为一个新的宏任务进入到队列中排队。
4、微任务，直接在当前任务结束过后立即执行。提高整体的响应能力。promise的回调作为微任务执行的。还有MutationObserver,process.nextTick.

9、将下面异步代码使用Promise改进？

    setTimeout(function(){
    var a = "hellow";
    setTimeout(function(){
        var b = "lagou";
        setTimeout(function(){
        var c = "I 💗 U";
        console.log(a+b+c);
        },10)
    },10)
    },10)


>答：
```
const p = new Promise(function(resolve,reject){
    resolve("hellow");
}).then(function(value){ // 第一个then // 1
  return Promise.resolve(value+"lagou"); 
}).then(function(value){ // 第二个then // 2
  return Promise.resolve(value+"I 💗U");
}).then(function(value){ // 第三个then // 3
  console.log(value);
}, function(err) {
  console.log('reject:' + err);
});
```
执行结果：hellowlagouI 💗U

10、请简述TypeScript与JavaScript之间的关系？

>答：TypeScript是JavaScript的超集。TypeScript包含JavaScript，类型系统，es6+然后编译为JavaScript。


11、请谈谈你所认为的TypeScript优缺点？

>答：TypeScript的优点：TypeScript功能更为强大，生态也更健全，更完善。TypeScript是前端领域的第二语言。大长周期项目建议使用TypeScript。
TypeScript的缺点：语言本身多了很多概念；TypeScript属于渐进式；项目初期，会增加一些成本；








