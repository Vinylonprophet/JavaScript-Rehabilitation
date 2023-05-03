# LHS&RHS

在 JavaScript 中，LHS 和 RHS 分别是左值引用和右值引用的简称。它们在赋值操作和变量声明中具有不同的含义和行为。

LHS（Left-hand Side）引用指的是在赋值操作中，左侧的变量或对象属性，它是赋值操作的目标，即等号左边的部分。例如：

```javascript
let a = 42; // 对变量 a 进行 LHS 引用
obj.prop = "hello"; // 对对象属性 prop 进行 LHS 引用
```

如果 LHS 引用的目标不存在，JavaScript 引擎会在当前作用域下创建一个同名的变量或对象属性。如果当前代码运行在严格模式下，当 LHS 引用的目标不存在时会抛出一个 `ReferenceError` 错误。

RHS（Right-hand Side）引用指的是在赋值操作中，右侧的值，即等号右边的部分。例如：

```javascript
let a = b; // 对变量 b 进行 RHS 引用，并将其值赋给变量 a
console.log(obj.prop); // 对对象属性 prop 进行 RHS 引用，并将其值作为参数传递给 console.log 函数
```

如果 RHS 引用的目标不存在，JavaScript 引擎会抛出一个 `ReferenceError` 错误。

需要注意的是，LHS 和 RHS 引用是在编译时确定的，而不是在运行时。在代码执行过程中，LHS 和 RHS 引用的值可能会发生变化，但是它们所指向的变量或对象属性在编译时就已经确定了。