# this全面解析

1. 已知this绑定完全取决于函数的调用位置（调用方法），因为有些函数会隐藏真正的调用位置，那么这个调用位置从哪里找或者说从哪里分析（答案三个字）？

   调用栈。

   

2. 调用位置决定this绑定的四条绑定规则分别是？

   - 默认绑定

     - 注意严格模式和非严格模式是不同的

   - 隐式绑定

     - 考虑上下文对象，会把函数调用的this绑定到这个上下文对象
     - 被隐式绑定的函数会丢失绑定对象，this可能会默认绑定到全局或者undefined上，取决于是否是严格模式
     - 回调函数的函数可能会修改this，甚至一些会强制绑定到触发事件的DOM上

   - 显示绑定

     call，apply等api

     硬绑定

     - call绑定第一次，第二次再用call不一定可以修改
     - 一般而言用于创建包裹函数或者是可重复使用的辅助函数

     API调用的“上下文”

     - forEach这种方法（本质上硬绑定也是call和apply）

   - new绑定

     1. 创建一个新对象
     2. 执行[[Prototype]]连接
     3. 新对象绑定到函数调用的this
     4. 函数没有返回其他对象，则new表达式中的函数自动返回这个新对象

   

3. this的默认绑定是什么？在严格模式下有什么不同？

   默认绑定到window或者是函数内部。

   严格模式下， 如果函数被直接调用而不是作为对象的方法调用，`this` 不会默认绑定到全局对象，而是绑定到 `undefined`。

   

4. 下面两种代码的区别和输出结果以及原因？

   ```javascript
   function foo(){
   	"use strict";
   	
   	console.log(this.a);
   }
   
   var a = 2;
   
   foo();
   ```

   ```javascript
   function foo(){
   	console.log(this.a);
   }
   
   var a = 2;
   
   (function(){
   	"use strict";
   	
   	foo();
   })();
   ```

   undefined

   2

   

5. 参考以下代码，隐式绑定规则的函数调用绑定的this取决于什么？

   ```javascript
   function foo(){
   	console.log(this.a);
   }
   
   var obj2 = {
   	a: 42,
   	foo: foo
   };
   
   var obj1 = {
   	a: 2,
   	obj2: obj2
   };
   
   obj1.obj2.foo();
   ```

   42

   对象属性引用链只有上一层或者说最后一层调用位置中起作用，你可以视为obj2.foo()

   

6. 参考第七第八题，回答隐式丢失是什么？

   `foo` 函数的执行上下文被更改，导致隐式绑定丢失，`this` 不再指向预期的对象，实际上就是指你传递的只有函数而已。

   

7. 下列代码的结果是什么？

   ```javascript
   function foo(){
   	console.log(this.a);
   }
   
   var obj = {
   	a: 2,
   	foo: foo
   }
   
   var bar = obj.foo;
   
   var a = "oops, global!";
   
   bar();
   ```

   oops, global!

   

8. 下列代码的结果是什么？

   ```javascript
   function foo(){
       console.log(this.a);
   }
   
   var obj ={
       a: 2,
       foo: foo
   }
   
   var a = "oops, global!";
   
   setTimeout(obj.foo, 100);
   ```

   oops, global!

   

9. 显示绑定是什么？

   call，apply这种JavaScript内置的绑定this的方法。

   

10. 下列代码的结果是什么？

    ```javascript
    function greet(name) {
    	console.log(`Hello, ${name}! My name is ${this.name}.`);
    }
    
    var person = { name: "John" };
    
    greet.apply(person, ["Alice"]);
    ```

    Hello, Alice! My name is John.

    

11. 下列代码的obj是什么？

    ```javascript
    [1, 2, 3].forEach(foo, obj);
    ```

    绑定的对象，实际就是foo绑定一个名为obj的对象，然后1，2，3分别三次传参。

    

12. 使用new调用函数会发生什么操作？

    1. 创建一个新对象。
    2. 执行[[Prototype]]连接。
    3. 新对象绑定到函数调用的this。
    4. 函数没有返回其他对象，则new表达式中的函数自动返回这个新对象。

    

13. 四条绑定规则的优先级是怎样的？

    默认 < 隐式 < new < 显示（强）

    

14. 下列代码的结果是什么？

    ```javascript
    function foo(){
    	console.log(this.a);
    }
    
    var obj1 = {
        a: 2,
        foo: foo
    };
    
    var obj2 = {
        a: 3,
        foo: foo
    };
    
    obj1.foo();
    obj2.foo();
    
    obj1.foo.call(obj2);
    obj1.foo.call(obj1);
    ```

    2

    3

    3

    2

    

15. 下列代码的结果是什么？

    ```javascript
    function foo(something){
    	this.a = something;
    }
    
    var obj1 = {
    	foo: foo
    };
    
    var obj2 = {};
    
    obj1.foo(2);
    obj1.foo.call(obj2, 3);
    
    console.log(obj1.a);
    console.log(obj2.a);
    
    var bar = new obj1.foo(4);
    console.log(obj1.a);
    console.log(bar.a);
    ```

    2

    3

    2

    4

    

16. 下列代码的结果是什么？

    ```javascript
    function foo(something){
        this.a = something;
    }
    
    var obj1 = {};
    
    var bar = foo.bind(obj1);
    bar(2);
    console.log(obj1.a);
    
    var baz = new bar(3);
    console.log(obj1.a);
    console.log(baz.a);
    ```

    2

    2

    3

    

17. 下列代码的结果是什么，其中为什么要使用null？

    ```javascript
    function foo(p1, p2){
    	this.val = p1 + p2;
    }
    
    var bar = foo.bind(null, "p1");
    
    var baz = new bar("p2");
    
    console.log(baz.val);
    ```

    p1p2

    bind用来`柯里化`，就是把除了第一个参数之外的其他参数都传给下层。

    使用 `null` 作为 `bind()` 方法的第一个参数的原因是，我们并不需要在这个场景中关心 `this` 的绑定对象，我们只是想预先填充函数参数。因此，传递 `null` 是为了忽略 `this` 的绑定，让 `bind()` 方法仅仅预先填充函数参数。

    

18. 下列代码的结果是什么，会造成什么问题？

    ```javascript
    function foo(){
        console.log(this.a);
    }
    
    var a = 2;
    
    foo.call(null);
    
    foo.call(undefined);
    ```

    2

    2

    

19. 下列代码的结果是什么？

    ```javascript
    function foo(a, b){
    	console.log("a: " + a, "b" + b);
    }
    
    foo.apply(null, [2, 3]);
    
    var bar = foo.bind(null, 2);
    bar(3);
    ```

    2 3

    2 3

    

20. 怎么创建一个对象，使this绑定到他，但不会对程序产生任何副作用？

    要创建一个对象，并确保 `this` 绑定到该对象上，同时又不会对程序产生任何副作用，可以使用空对象 `{}`。空对象是一个简单的对象，不会对程序产生影响，并且可以被用作 `this` 的绑定目标。

    ```javascript
    foo.bind(Object.create(null), 2);
    ```

    

21. 下列代码的结果是什么？

    ```javascript
    function foo(){
    	console.log(this.a);
    }
    
    var a = 2;
    var o = {
        a: 3,
        foo: foo
    };
    var p = {
        a: 4
    };
    
    o.foo();
    (p.foo = o.foo)();
    ```

    3

    2

    

22. 下列代码的结果是什么？

    ```javascript
    function foo(){
        return (a) => {
            console.log(this.a);
        }
    }
    
    var obj1 = {
        a: 2
    };
    
    var obj2 = {
        a: 3
    };
    
    var bar = foo.call(obj1);
    bar.call(obj2);
    ```

    2

    箭头函数的this绑定规则是根据函数的作用域绑定的。

    

23. 对于第22题如果使用new呢？

    无论是否使用 `new` 关键字，都是 `2`，因为 `foo` 函数被 `call` 时的上下文是 `obj1`，而箭头函数中的 `this.a` 会绑定到 `obj1.a`。

    

24. 下列代码的结果是什么？

    ```javascript
    function foo(){
    	var self = this;
    	setTimeout( function(){
    		console.log(self.a);
    	}, 100)
    }
    
    var obj = {
    	a: 2
    }
    
    foo.call(obj);
    ```

    2

