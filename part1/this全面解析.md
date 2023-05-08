# this全面解析

1. 已知this绑定完全取决于函数的调用位置（调用方法），因为有些函数会隐藏真正的调用位置，那么这个调用位置从哪里找或者说从哪里分析（答案三个字）？

2. 调用位置决定this绑定的四条绑定规则分别是？

3. this的默认绑定是什么？在严格模式下有什么不同？

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
   	foo: foo
   };
   
   obj1.obj2.foo();
   ```

6. 参考第七第八题，回答隐式丢失是什么？

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
   
   setTimeout( obj.foo, 100);
   ```

9. 显示绑定是什么？

10. 下列代码的结果是什么？

    ```javascript
    function greet(name) {
    	console.log(`Hello, ${name}! My name is ${this.name}.`);
    }
    
    var person = { name: "John" };
    
    greet.apply(person, ["Alice"]);
    ```

11. 下列代码的obj是什么？

    ```javascript
    [1, 2, 3].forEach(foo, obj);
    ```

12. 使用new调用函数会发生什么操作？

13. 四条绑定规则的优先级是怎样的？

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

17. 下列代码的结果是什么，其中为什么要使用null？

    ```java
    function foo(p1, p2){
    	this.val = p1 + p2;
    }
    
    var bar = foo.bind(null, "p1");
    
    var baz = new bar("p2");
    
    console.log(baz.val);
    ```

18. 下列代码的结果是什么，会造成什么问题？

    ```javascript
    function foo(){
        console.log(this.a);
    }
    
    var a = 2;
    
    foo.call(null);
    
    foo.call(undefined);
    ```

19. 下列代码的结果是什么？

    ```javascript
    function foo(a, b){
    	console.log("a: " + a, "b" + b);
    }
    
    foo.apply(null, [2, 3]);
    
    var bar = foo.bind(null, 2);
    bar(3);
    ```

20. 怎么创建一个对象，使this绑定到他，但不会对程序产生任何副作用？

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

23. 对于第22题如果使用new呢？

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