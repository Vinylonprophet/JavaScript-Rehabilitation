# this

1. 以下代码的输出结果是什么，为什么？

   ```javascript
   function foo(num){
   	console.log("foo: " + num);
       
       this.count++;
       console.log(this.count);
   }
   
   foo.count = 0;
   
   var i;
   
   for(i=0; i< 10; i++){
       if(i>5){
           foo(i);
       }
   }
   
   console.log(foo.count);
   ```

2. 使用call强制绑定this指向应该怎么改？

3. 普通函数调用时，this会绑定在哪里？

4. 下列代码的输出结果是什么，为什么？

   ```javascript
   function foo(){
   	var a = 2;
   	this.bar();
   }
   
   function bar(){
       console.log(this.a)
   }
   
   bar();
   ```

5. this的绑定和函数声明位置的关系是？

