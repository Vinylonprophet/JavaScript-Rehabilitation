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

6. 参考第七第八题，回答隐式丢失是什么？。

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

13. 