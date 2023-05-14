# ES6中的Class

1. 下列代码的结果是什么？

   ```javascript
   class C{
   	constructor(){
   		C.prototype.count++;
   		console.log("Hello " + this.count);
   	}
   }
   
   C.prototype.count = 0;
   
   var c1 = new C();
   var c2 = new C();
   
   c1.count === 2;
   c1.count === c2.count;
   ```

2. 下列代码的结果是什么，为什么？

   ```javascript
   class C{
       constructor(id){
           this.id = id;
       }
       id(){
           console.log("id " + id);
       }
   }
   
   var c1 = new C("c1");
   c1.id;
   c1.id();
   ```

3. 下列代码的结果是什么，为什么？

   ```javascript
   class P{
   	foo(){
           console.log("P.foo");
       }
   }
   
   class C extends P{
       foo(){
           super();
       }
   }
   
   var c1 = new C();
   c1.foo();
   
   var D = {
       foo: function(){
           console.log("D.foo");
       }
   };
   
   var E = {
       foo: C.prototype.foo
   };
   
   Object.sePrototypeOf(E, D);
   
   E.foo();
   ```

4. 下列代码的结果是什么，为什么？

   ```javascript
   var D = {
   	foo: function(){
   		console.log("D.foo");
   	}
   };
   
   var E = Object.create(D);
   
   E.foo();
   ```