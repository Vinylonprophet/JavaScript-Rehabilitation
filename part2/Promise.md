# Promise

1. JavaScript中什么是线程？

    JavaScript 是一种**单线程语言**，不需要担心多个线程之间的竞争条件和死锁等并发问题。但是，有时候 JavaScript 需要处理一些需要长时间运行的操作，例如网络请求、文件 I/O 或者复杂的计算。为了避免这些操作阻塞主线程，JavaScript 提供了一些异步编程机制，如回调函数、Promise 和 async/await。这些机制允许代码在等待异步操作完成时继续执行其他任务，从而使得整个应用程序保持响应。

   

2. JavaScript中什么是进程？

   在浏览器环境下，通常情况下一个页面就是一个进程，每个标签页或者窗口都在其自己的进程中运行。这些进程之间相互隔离，一个页面的 JavaScript 代码不能直接访问另一个页面的 JavaScript 代码或者数据。这种隔离性有助于提高安全性和稳定性。

   

3. 下列代码中如果**I/O**异步会造成什么问题？

   ```javascript
   var a = {
       index: 1
   }
   
   console.log(a);
   
   a.index++;
   ```

   会导致输出是2

   

4. 下列代码的结果是什么？

   ```javascript
   var a = 20;
   
   function foo(){
       a = a + 1;
   }
   
   function bar(){
       a = a * 2;
   }
   
   ajax("http://demo.url.1", foo);
   ajax("http://demo.url.2", bar);
   ```

   41或者42（有两种结果）

   

5. JavaScript中任务队列和事件队列是什么？

   **任务队列**：

   - 任务队列是一个存储异步任务的队列，异步任务包括异步函数的回调函数、定时器的回调函数、事件处理程序等。
   - 当异步任务完成时，它会被添加到任务队列中等待执行。
   - JavaScript 引擎在执行完当前的同步任务后，会不断地检查任务队列，如果任务队列不为空，就会从队列中取出任务并执行。

   **事件循环队列**（Event Loop Queue）：

   - 事件循环是 JavaScript 引擎执行异步任务的机制之一，其核心是一个永无休止的循环，负责从任务队列中获取任务并执行。
   - 事件循环包括了宏任务队列（Macrotask Queue）和微任务队列（Microtask Queue）两个队列。
   - 宏任务队列用于存储宏任务，比如 setTimeout、setInterval、I/O 操作等，它们在主线程上执行。
   - 微任务队列用于存储微任务，比如 Promise 的回调函数、DOM 变动观察器等，它们优先于宏任务执行，且在每个宏任务执行完毕后立即执行。

   事件循环的执行过程可以简述为：

   1. 从宏任务队列中取出一个任务执行。
   2. 执行过程中产生的微任务会被添加到微任务队列中。
   3. 执行当前宏任务完毕后，立即执行微任务队列中的所有微任务。
   4. 检查是否需要更新渲染，执行渲染。
   5. 返回步骤 1，继续从宏任务队列中取出下一个任务执行。

   `setTimeout` 函数允许将任务添加到宏任务队列中，而 `setTimeout(fn, 0)` 是一个常见的技巧，用于将任务推迟到下一个事件循环迭代中执行，即放到宏任务队列的末尾，但尽可能地快速执行。

   **注意：**事件循环每一轮称为一个tick。

   

6. JavaScript的回调是什么？

   回调（Callback）是一种常见的编程模式，用于处理异步操作。在JavaScript中，回调通常是一个函数，作为参数传递给另一个函数，并在异步操作完成后被调用执行。

   

7. 下列代码的执行顺序是什么？

   ```javascript
   // A
   ajax("..", function(..){
       // C
   });
   // B
   ```

   A

   B

   C

   

8. 如果下列代码functionName()是回调函数，那么执行顺序是什么？

   ```javascript
   doA(function(){
       doB();
       
       doC(function(){
           doD();
       });
   
   	doE();
   });
   
   doF();
   ```

   doA

   doF

   doB

   doC

   doE

   doD

   

9. 下列代码返回的是什么？

   ```javascript
   function A(){
   	return Promise.all()
           .then()
   }
   ```

   返回的是一个 Promise 对象，promise.then()返回的也是promise

   

10. 下列代码创建的是什么？

    ```javascript
    const promise = new Promise(function(resolve, reject) {
      // 异步操作，例如发送 Ajax 请求
      setTimeout(function() {
        const data = '这是异步操作返回的数据';
        if (data) {
          resolve(data); // 异步操作成功，将状态改变为 resolved，并传递数据
        } else {
          reject(new Error('异步操作失败')); // 异步操作失败，将状态改变为 rejected，并传递错误
        }
      }, 2000);
    });
    ```

    `new Promise(function(resolve, reject))` 是创建一个新的 Promise 对象的语法。Promise 是用于异步编程的一种方式，用于处理异步操作的结果或错误。

    在 `new Promise()` 中，传递一个带有两个参数的函数，这个函数通常称为执行器函数（executor function）。这个执行器函数会在创建 Promise 对象时立即执行，并且接收两个参数 `resolve` 和 `reject`，这两个参数都是函数。

    - `resolve` 函数用于将 Promise 对象的状态从 pending（进行中）转变为 resolved（已完成），并将结果传递给后续的 `.then()` 方法。
    - `reject` 函数用于将 Promise 对象的状态从 pending（进行中）转变为 rejected（已拒绝），并将错误原因传递给后续的 `.catch()` 方法。

    

11. 如何检查一个值是不是真正的Promise？

    如果用instanceof的话如果是iframe等等，无法识别Promise实例。

    所以只要一个对象或者方法有then，我们就认为是Promise。（duck  typing）

    

12. 下列代码的v是一个鸭子类型吗？

    ```javascript
    var o = { then: function(){} };
    
    var v = Object.create(o);
    
    v.someStuff = "cool";
    
    v.hasOwnProperty("then");
    ```

    是

    

13. 下列代码的结果是什么？为什么？

    ```javascript
    p.then(function(){
        p.then(function(){
            console.log("c");
        })
        console.log("a")
    })
    p.then(function(){
        console.log("b")
    })
    ```

    a b c

    一个Promise议决后，这个Promise上所有通过.then()注册的回调都会在下一个异步时机点上依次被立即调用。

    **顺序：**

    1. 外部的 `p.then` 返回的 Promise 进入 resolved 状态，并且外部的回调函数执行。这导致打印 "a"，然后内部的 `p.then` 被添加到微任务队列中。
    2. 外部的 `p.then` 返回的 Promise 已经 resolved，所以接着执行第二个 `p.then` 链中的回调函数，打印 "b"。
    3. 微任务队列中的任务开始执行，内部的 `p.then` 链中的回调函数执行，并打印 "c"。

    

14. 下列代码的结果是什么？

    ```javascript
    var p3 = new Promise(function(resolve, reject){
        resolve("B");
    })
    
    var p1 = new Promise(function(resolve, reject){
        resolve(p3);
    })
    
    var p2 = new Promise(function(resolve, reject){
        resolve("A");
    })
    
    p1.then(function(v){
        console.log(v);
    })
    
    p2.then(function(v){
        console.log(v);
    })
    ```

    A

    B

    

15. Promise能被议决几次？

    一次，再多也是第一次。

    

16. 下列代码的结果是什么？

    ```javascript
    var p = new Promise(function(resolve, reject){
        foo.bar();
        resolve(42);
    })
    
    p.then(
    	function fulfilled(){
            console.log("==vl==");
        },
        function rejected(err){
            console.log("Error: ", err)
        }
    )
    ```

    ReferenceError

    

17. 下列代码结果是什么？

    ```javascript
    var p1 = Promise.resolve(42);
    
    var p2 = Promise.resolve(p1);
    
    p1 === p2;
    ```

    true

    

18. 构造一个发完A请求发B请求的函数（用Promise）

    ```javascript
    function request(url){
        return new Promise(function(resolve, reject){
            ajax(url, resolve);
        })
    }
    
    request("APIA")
    .then(function(reponse){
        return request("APIB" + response);
    })
    .then(function(response2){
        console.log(response2);
    })
    ```

    