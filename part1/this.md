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

   this.count：undefined经过增值操作之后，console.log(this.count)就会报错NaN

   foo.count：就没增加，所以还是0

   使用词法作用域也能解决这一问题。

   

2. 使用call强制绑定this指向应该怎么改？

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
           foo.call(foo, i);
       }
   }
   
   console.log(foo.count);
   ```

   

3. 普通函数调用时，this会绑定在哪里？

   this在任何情况下都不会指向词法作用域，普通函数调用会绑定在window上。

   

4. 下列代码的输出结果是什么，为什么？

   ```javascript
   function foo(){
   	var a = 2;
   	this.bar();
   }
   
   function bar(){
       console.log(this.a)
   }
   
   foo();
   ```

   undefined或者是ReferenceError，ReferenceError是可能出现的情况。

   因为this是window。

   

5. this的绑定和函数声明位置的关系是？

   this的绑定和声明位置无关，只取决于函数的调用方式。
