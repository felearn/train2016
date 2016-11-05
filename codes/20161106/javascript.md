## 表达式

表达式是由数字、运算符、数字分组符号（如括号）、自由变量和约束变量等以能求得数值的有意义排列方法所得的组合。JavaScript 表达式主要有以下几种形式：

- 原始表达式：常量、变量、保留字。
- 对象、数组初始化表达式：`var obj={a:1,b:2};`，`var arr=[1,2,3];`。
- 函数定义表达式：`var fn=function(){}`。
- 属性访问表达式：`Math.abs`。
- 调用表达式：`alert('hello');`。
- 对象创建表达式：`new object();`。

## 运算符

JavaScript 中的运算符用于算术表达式、比较表达式、逻辑表达式、赋值表达式等。需要注意的是，大多数运算符都是由标点符号表示的，比如 `+` 和 `=`。而另外一些运算符则是由关键字表示的，比如 `typeof` 和 `instanceof`，关键字运算符和标点符号都是正规的运算符。

下表列出了 JavaScript 中所有的运算符，并按照运算符的优先级排序的，前面的运算符优先级要高于后面的运算符优先级，被空行分隔开来的运算符具有不同的优先级。标题为 A 的列表示运算符的结合性（Associativity），L 表示从左至右、R 表示从右至左，标题为 N 的列表示操作数的个数（Number）。

| 运算符 | 操作 | A | N |
| --- | --- | --- | --- |
| `++` | 前/后增量 |  R | 1 |
| `--` | 前/后增量 | R | 1 |
| `-` | 求反 | R | 1 |
| `+` | 转换为数字 | R | 1 |
| `~`| 按位求反 | R | 1 |
| `!` | 逻辑非 | R | 1 |
| `delete` | 删除属性 | R | 1 |
| `typeof` | 检测类型 | R | 1 |
| `void` | 返回`undefined` | R | 1 |
|||||
| `*` `/` `%` | 乘，除，求模 | L | 2 | 
| `+` `-` | 加，减| L | 2 |
| `+` | 字符串连接 | L | 2 |
| `<<`  | 左移位 | L | 2 |
| `>>`  | 有符号右移 | L | 2 |
| `>>>` | 无符号右移 | L | 2 |
| `<` `<=` `>` `>=` | 比较数字顺序 | L | 2 |
| `<` `<=` `>` `>=` | 比较字母顺序 | L | 2 |
| `instanceof` | 测试对象类 | L | 2 |
| `in` | 测试属性是否存在 | L | 2 |
|||||
| `==` | 判断相等 | L | 2 |
| `!=` | 判断不等 | L | 2 |
| `===` | 判断恒等 | L | 2 |
| `!==` | 判断恒不等 | L | 2 |
| `&` | 按位与 | L | 2 |
|||||
| `^` | 按位异或 | L | 2 |
| `┃` | 按位或 | L | 2 |
|||||
| `&&` | 逻辑与 | L | 2 |
|||||
| `┃┃` | 逻辑或 | L | 2 |
| `?:` | 条件运算符 | R | 3 |
|||||
| `=` | 赋值 | R | 2 |
| `*=` `/=` `%=` <br> `+=` `-=` `&=` <br>  `<<=` `>>=` <br> `^=` `┃=` `>>>=` | 运算且赋值 | R | 2 |
|||||
| `,` | 忽略第一个操作数，<br> 返回第二个操作数  | L | 2 |

> 因为 `|` 是制表符，会导致格式混乱，所以表格中的 `|` 均以 `┃` 代替。

### 一元运算符

#### `delete` 运算符

`delete` 运算符用来删除对象属性或者数组元素，如果删除成功或所删除的目标不存在，`delete` 将返回 `true`。然而，并不是所有的属性都可删除，一些内置核心和客户端属性是不能删除的，通过 `var` 语句声明的变量不能删除，通过 `function` 语句定义的函数也是不能删除的。例如：

``` javascript
var o = { x: 1, y: 2};          // 定义一个对象
console.log(delete o.x);        // true，删除一个属性
console.log(delete o.x);        // true，什么都没做，x 在已上一步被删除
console.log("x" in o);          // false，这个属性在对象中不再存在
console.log(delete o.toString); // true，什么也没做，toString是继承来的
console.log(delete 1);          // true，无意义

var a = [1,2,3];                // 定义一个数组
console.log(delete a[2]);       // true，删除最后一个数组元素
console.log(2 in a);            // false，元素2在数组中不再存在
console.log(a.length);          // 3，数组长度并不会因 delete 而改变
console.log(a[2]);              // undefined，元素2所在的位置被空了出来
console.log(delete a);          // false，通过 var 语句声明的变量不能删除

function f(args){}              // 定义一个函数
console.log(delete f);          // false，通过 function 语句声明的函数不能删除
```

#### `void` 运算符

`void` 运算符可以应用于任何表类型的表达式，表达式会被执行，但计算结果会被忽略并返回 `undefined`。例如：

``` javascript
void 0;
void "you are useless?";
void false;
void [];
void /(useless)/ig;
void function(){ console.log("you are so useless?"); }
// always return undefined
```

> 扩展阅读「谈谈 JavaScript 中的 void 运算符」  
> https://segmentfault.com/a/1190000000474941

#### `typeof` 运算符

> 请参见[「变量和数据类型」-「数据类型」-「`typeof` 运算符」](https://github.com/stone0090/javascript-lessons/tree/master/1.4-Variable%26Types#typeof-运算符)。

#### `++` `--` 运算符

`++` `--` 递增递减运算符借鉴自 C 语言，它们分前置型和后置型，作用是改变一个变量的值。例如：

``` javascript
var a = 5;
console.log(a++);   // 5
console.log(++a);   // 7
console.log(a--);   // 7
console.log(--a);   // 5
```

#### `+` `-` 运算符

当 `+` `-` 作为一元运算符时，应用于数值，表示数值的正负。应用于非数值，先按 `Number()` 转型函数对这个值执行转换，再表示该值的正负。

#### `~` `!` 运算符

> `~` 按位非运算符，请参见下面[「位运算符」](https://github.com/stone0090/javascript-lessons/tree/master/1.5-Expression&Operators#位运算符)。  
> `!` 逻辑非运算符，请参见下面[「逻辑运算符」](https://github.com/stone0090/javascript-lessons/tree/master/1.5-Expression&Operators#逻辑运算符)。

### 乘性运算符

JavaScript 定义了3个乘性运算符：乘法、除法和求模。这些运算符与 C 语言的相应运算符用途类似，只不过在操作数为非数值的情况下会执行自动的类型转换。如果参与乘法计算的某个操作数不是数值，后台会先使用 `Number()` 转型函数将其转换为数值。也就是说，空字符串将被当作 `0`，布尔值 `true` 将被当作 `1`。

#### `*` 乘法运算符

用于计算两个数值的乘积，在处理特殊值的情况下，乘法运算符遵循下列特殊的规则：

- 如果操作数都是数值，执行常规的乘法计算，即两个正数或两个负数相乘的结果还是正数，而如果只有一个操作数有符号，那么结果就是负数。如果乘积超过了 JavaScript 数值的表示范围，则返回 `Infinity` 或 `-Infinity`；
- 如果有一个操作数是 `NaN`，则结果是 `NaN`；
- 如果是 `Infinity` 与 `0` 相乘，则结果是 `NaN`；
- 如果是 `Infinity` 与非 `0` 数值相乘，则结果是 `Infinity` 或 `-Infinity`，取决于有符号操作数的符号；
- 如果是 `Infinity` 与 `Infinity` 相乘，则结果是 `Infinity`；
如果有一个操作数不是数值，则在后台调用 `Number()`将其转换为数值，然后再应用上面的规则。

#### `/` 除法运算符

用于计算两个数值的商，与乘法运算符类似，除法运算符对特殊的值也有特殊的处理规则。这些规则如下：

- 如果操作数都是数值，执行常规的除法计算，即两个正数或两个负数相除的结果还是正数，而如果只有一个操作数有符号，那么结果就是负数。如果商超过了 JavaScript 数值的表示范围，则返回 `Infinity` 或 `-Infinity`；
- 如果有一个操作数是 `NaN`，则结果是 `NaN`；
- 如果是 `Infinity` 被 `Infinity` 除，则结果是 `NaN`；
- 如果是零被零除，则结果是 `NaN`；
- 如果是非零的有限数被零除，则结果是 `Infinity` 或 `-Infinity`，取决于有符号操作数的符号；
- 如果是 `Infinity` 被任何非零数值除，则结果是 `Infinity` 或 `-Infinity`，取决于有符号操作数的符号；
- 如果有一个操作数不是数值，则在后台调用 `Number()` 将其转换为数值，然后再应用上面的规则。

#### `%` 求模运算符

用于计算两个数值的余数，与另外两个乘性运算符类似，求模运算符会遵循下列特殊规则来处理特殊的值：

- 如果操作数都是数值，执行常规的除法计算，返回除得的余数；
- 如果被除数是无穷大值而除数是有限大的数值，则结果是 `NaN`；
- 如果被除数是有限大的数值而除数是零，则结果是 `NaN`；
- 如果是 `Infinity` 被 `Infinity` 除，则结果是 `NaN`；
- 如果被除数是有限大的数值而除数是无穷大的数值，则结果是被除数；
- 如果被除数是零，则结果是零；
- 如果有一个操作数不是数值，则在后台调用 `Number()` 将其转换为数值，然后再应用上面的规则。

### 加性运算符

加法和减法这两个加性运算符应该说是编程语言中最简单的算术运算符了。但是在 JavaScript 中，这两个运算符却都有一系列的特殊行为。与乘性运算符类似，加性运算符也会在后台转换不同的数据类型。然而，对于加性运算符而言，相应的转换规则还稍微有点复杂。

#### `+` 加法运算符

如果两个运算符都是数值，执行常规的加法计算，然后根据下列规则返回结果：

- 如果有一个操作数是 `NaN`，则结果是 `NaN`；
- 如果是 `Infinity` 加 `Infinity`，则结果是 `Infinity`；
- 如果是 `-Infinity` 加 `-Infinity`，则结果是 `-Infinity`；
- 如果是 `Infinity` 加- `Infinity`，则结果是 `NaN`；
- 如果是 `+0` 加 `+0`，则结果是 `+0`；
- 如果是 `-0` 加 `-0`，则结果是 `-0`；
- 如果是 `+0` 加 `-0`，则结果是 `+0`;

如果有一个操作数不是数值，那么就要应用如下规则：

- 如果两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来；
- 如果只有一个操作数是字符串，则将另一个操作数转换为字符串，然后再将两个字符串拼接起来。
- 如果有一个操作数是对象、数值或布尔值，则调用它们的 `toString()` 方法取得相应的字符串值，然后再应用前面关于字符串的规则。对于 `undefined` 和 `null`，则分别调用 `String()` 函数并取得字符串 `"undefined"` 和 `"null"`。
- 如果是 `null` 加 `null`，则结果是 `0`;
- 如果是 `undefined` 加 `undefined`，则结果是 `NaN`;

下面来举几个例子：

``` javascript
var result1 = 5 + 5;            // 两个数值相加
console.log(result1);           // 10

var result2 = 5 + "5";          // 一个数值和一个字符串相加
console.log(result2);           // "55"

var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + num1 + num2;
console.log(message);   // "The sum of 5 and 10 is 510"，如何修改？
```

#### `-` 减法运算符

如果两个运算符都是数值，执行常规的减法计算，然后根据下列规则返回结果：

- 如果有一个操作数是 `NaN`，则结果是 `NaN`；
- 如果是 `Infinity` 减 `Infinity`，则结果是 `NaN`；
- 如果是 `-Infinity` 减 `-Infinity`，则结果是 `NaN`；
- 如果是 `Infinity` 减 `-Infinity`，则结果是 `Infinity`；
- 如果是 `-Infinity` 减 `Infinity`，则结果是 `-Infinity`；
- 如果是 `+0` 减 `+0`，则结果是 `+0`；
- 如果是 `+0` 减 `-0`，则结果是 `-0`；
- 如果是 `-0` 减 `-0`，则结果是 `+0`；

如果有一个操作数不是数值，那么就要应用如下规则：

- 如果有一个操作数是字符串、布尔值、`null` 或 `undefined`，则先在后台调用 `Number()` 函数将其转换为数值，然后再根据前面的规则执行减法计算。如果转换的结果是 `NaN`，则减法的结果就是 `NaN`；
- 如果有一个操作数是对象，则调用对象的 `valueOf()` 方法以取得表示该对象的数值。如果得到的值是 `NaN`，则减法的结果就是 `NaN`。如果对象没有 `valueOf()` 方法，则调用其 `toString()`方法并将得到的字符串转换为数值。
- 如果是 `null` 减 `null`，则结果是 `0`;
- 如果是 `undefined` 减 `undefined`，则结果是 `NaN`;

下面来举几个例子：

``` javascript
var result1 = 5 - true;         // 4，因为true被转换成了1
var result2 = NaN - 1;          // NaN
var result3 = 5 - 3;            // 2
var result4 = 5 - "";           // 5，因为"" 被转换成了0
var result5 = 5 - "2";          // 3，因为"2"被转换成了2
var result6 = 5 - null;         // 5，因为null被转换成了0
```

### 等值运算符

确定两个变量是否相等是编程中的一个非常重要的操作。在比较简单数据类型之间的相等性时，问题还比较简单。但在涉及到对象之间的比较时，问题就变得复杂了。最早的 JavaScript 中的相等和不等运算符会在执行比较之前，先将对象转换成相似的类型。后来，有人提出了这种转换到底是否合理的质疑。最后，JavaScript 的解决方案就是提供两组运算符：相等和不相等（先转换再比较），恒等和不恒等（仅比较而不转换）。

#### `==` `!=` 运算符

`==` `!=` 这两个运算符都会先转换操作数（通常称为强制转型），然后再比较它们的相等性。在转换不同的数据类型时，相等和不相等运算符遵循下列基本规则：

- 如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值（`false` 转换为 `0`，而 `true` 转换为 `1`）；
- 如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值；
- 如果一个操作数是对象，另一个操作数不是，则调用对象的 `valueOf()` 方法，用得到的基本类型值按照前面的规则进行比较；
- `null` 和 `undefined` 是相等的。
要比较相等性之前，不能将 `null` 和 `undefined` 转换成其他任何值。
- 如果有一个操作数是 `NaN`，则相等运算符返回 `false`，而不相等运算符返回 `true`。重要提示：即使两个操作数都是 `NaN`，相等运算符也返回 `false`；因为按照规则，`NaN` 不等于 `NaN`。
- 如果两个操作数都是对象，则比较它们是不是同一个对象。如果两个操作数都指向同一个对象，则相等运算符返回 `true`；否则，返回 `false`。

列出了一些特殊情况及比较结果：

``` javascript
null == undefined   // true
"NaN" == NaN        // false
5 == NaN            // false
NaN == NaN          // false
NaN != NaN          // true
false == 0          // true
true == 1           // true
true == 2           // false
undefined == 0      // false
null == 0           // false
"5" == 5            // true
```

#### `===` `!==` 运算符

除了在比较之前不转换操作数之外，恒等和不恒等运算符与相等和不相等运算符没有什么区别。它只在两个操作数未经转换就相等的情况下返回 `true`，如下面的例子所示：

``` javascript
var result1 = ("55" == 55);     // true，因为转换后相等
var result2 = ("55" === 55);    // false，因为不同的数据类型不相等
var result3 = (null == undefined)   // true，因为它们是类似的值
var result4 = (null === undefined)  // false，因为它们是不同类型的值
```

### 关系运算符

#### `<` `>` `<=` `>=` 运算符

`<` 小于、`>` 大于、`<=` 小于等于、 `>=` 大于等于 这几个关系运算符用于对两个值进行比较返回一个布尔值。与 JavaScript 中的其他运算符一样，当关系运算符的操作数使用了非数值时，也要进行数据转换或完成某些奇怪的操作。以下就是相应的规则。

- 如果两个操作数都是数值，则执行数值比较。
- 如果两个操作数都是字符串，则比较两个字符串对应的字符编码值（可以通过字符串的 `charCodeAt()` 函数获取字符编码值）。
- 如果一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较。
- 如果一个操作数是对象，则调用这个对象的 `valueOf()` 方法，用得到的结果按照前面的规则执行比较。如果对象没有 `valueOf()`方法，则调用 `toString()`方法，并用得到的结果根据前面的规则执行比较。
- 如果一个操作数是布尔值，则先将其转换为数值，然后再执行比较。

请思考下面几个例子的结果是如何得出的：

``` javascript
var result1 = "Brick" < "alphabet";     // true
var result2 = "brick" < "alphabet";     // false
var result3 = "23" < "3";   // true
var result4 = "23" < 3;     // false
var result5 = "a" < 3;      // false
var result6 = NaN < 3;      // false
var result7 = NaN >= 3;     // false
```

#### `in` 运算符

`in` 运算符希望它的左操作数是一个字符串或可以转换为字符串，希望它的右操作数是一个对象。如果右侧的对象拥有一个名为左操作数值的属性名，那么表达式返回 `true`，例如：

``` javascript
var point = { x:1, y:1 };       // 定义一个对象
"x" in point                    // true，对象有一个名为"x"的属性
"z" in point                    // false，对象中不存在名为"z"的属性
"toString" in point             // true，对象继承了toString()方法

var data = [7,8,9];             // 拥有三个元素的数组
"0" in data                     // true，数组包含元素"0"
1 in data                       // true，数字转换为字符串
3 in data                       // false，没有索引为3的元素
```

#### `instanceof` 运算符

`instanceof` 运算符希望左操作数是一个对象，右操作数标识对象的类。如果左侧的对象是右侧类的实例，则表达式返回 `true`；否则返回 `false`。后面会讲 JavaScript 中对象的类是通过初始化它们的构造函数来定义的。这样的话，`instanceof` 的右操作数应当是一个函数。比如：

``` javascript
var d = new Date();     // 通过 Date() 构造函数来创建一个新对象
d instanceof Date;      // true，d 是由 Date() 创建的
d instanceof Object;    // true，所有的对象都是 Object 的实例
d instanceof Number;    // false，d 不是一个 Number 对象

var a = [1, 2, 3];      // 通过数组字面量的写法创建一个数组
a instanceof Array;     // true，a 是一个数组
a instanceof Object;    // true，所有的数组都是对象
a instanceof RegExp;    // false，数组不是正则表达式
```

需要注意的是，所有的对象都是 `Object` 的实例。当通过 `instanceof` 判断一个对象是否是一个类的实例的时候，这个判断也会包含对「父类」的检测。如果 `instanceof` 的左操作数不是对象的话，`instanceof` 返回 `false`。如果右操作数不是函数，则抛出一个类型错误异常。

### 逻辑运算符

逻辑运算符是对操作数进行布尔算术运算，经常和关系运算符一起配合使用，逻辑运算符将多个关系表达式组合起来组成一个更复杂的表达式。

#### `&&` 逻辑与

逻辑与操作可以应用于任何类型的操作数，而不仅仅是布尔值。在有一个操作数不是布尔值的情况下，逻辑与操作不一定返回布尔值；此时，它遵循下列规则：

- 如果第一个操作数是对象，则返回第二个操作数；
- 如果第二个操作数是对象，则只有在第一个操作数的求值结果为 `true` 的情况下才会返回该对象；
- 如果两个操作数都是对象，则返回第二个操作数；
- 如果有一个操作数是 `null`，则返回 `null`；
- 如果有一个操作数是 `NaN`，则返回 `NaN`；
- 如果有一个操作数是 `undefined`，则返回 `undefined`。

逻辑与操作属于短路操作，即如果第一个操作数能够决定结果，那么就不会再对第二个操作数求值。对于逻辑与操作而言，如果第一个操作数是 `false`，无论第二个操作数是什么值，结果都不再可能是 `true` 了。

#### `||` 逻辑或

与逻辑与操作相似，如果有一个操作数不是布尔值，逻辑或也不一定返回布尔值；此时，它遵循下列规则：

- 如果第一个操作数是对象，则返回第一个操作数；
- 如果第一个操作数的求值结果为 `false`，则返回第二个操作数；
- 如果两个操作数都是对象，则返回第一个操作数；
- 如果两个操作数都是 `null`，则返回 `null`；
- 如果两个操作数都是 `NaN`，则返回 `NaN`；
- 如果两个操作数都是 `undefined`，则返回 `undefined`。

与逻辑与运算符相似，逻辑或运算符也是短路运算符。也就是说，如果第一个操作数的求值结果为 `true`，就不会对第二个操作数求值了。

#### `!`  逻辑非

逻辑非操作可以应用于任何类型的操作数，无论这个值是什么数据类型，这个运算符都会返回一个布尔值。逻辑非运算符首先会将它的操作数转换为一个布尔值，然后再对其求反。逻辑非运算符遵循下列规则：

- 如果操作数是一个对象，返回 `false`；
- 如果操作数是一个空字符串，返回 `true`；
- 如果操作数是一个非空字符串，返回 `false`；
- 如果操作数是数值 `0`，返回 `true`；
- 如果操作数是任意非 `0` 数值（包括 `Infinity`），返回 `false`；
- 如果操作数是 `null`，返回 `true`；
- 如果操作数是 `NaN`，返回 `true`；
- 如果操作数是 `undefined`，返回 `true`。

下面几个例子展示了应用上述规则的结果：

``` javascript
console.log(!false);          // true
console.log(!"blue");         // false
console.log(!0);              // true
console.log(!NaN);            // true
console.log(!"");             // true
console.log(!12345);          // false
```

逻辑非运算符也可以用于将一个值转换为与其对应的布尔值。而同时使用两个逻辑非运算符，实际上就会模拟 `Boolean()` 转型函数的行为。其中，第一个逻辑非操作会基于无论什么操作数返回一个布尔值，而第二个逻辑非操作则对该布尔值求反，于是就得到了这个值真正对应的布尔值。当然，最终结果与对这个值使用 `Boolean()` 函数相同，例如：

``` javascript
console.log(!!"blue");        //true
console.log(!!0);             //false
console.log(!!NaN);           //false
console.log(!!"");            //false
console.log(!!12345);         //true
```

### 位运算符

在 JavaScript 中，当对数值应用位运算符时，后台会发生如下转换过程：64位的数值被转换成32位数值，然后执行位操作，最后再将32位的结果转换回64位数值。这个转换过程导致了一个严重的副效应，即在对特殊的 `NaN` 和 `Infinity` 值应用位操作时，这两个值都会被当成 `0` 来处理。如果对非数值应用位运算符，会先使用 `Number()` 函数将该值转换为一个数值，然后再应用位操作，得到的结果将是一个数值。

#### `~` 按位非

简单的理解，对任一数值 `x` 进行按位非操作的结果为 `-(x+1)`。例如：

``` javascript
console.log(~null);         // -1
console.log(~undefined);    // -1
console.log(~0);            // -1
console.log(~{});           // -1
console.log(~[]);           // -1
console.log(~(1/0));        // -1
console.log(~false);        // -1
console.log(~true);         // -2
console.log(~1.2543);       // -2
console.log(~4.9);          // -5
console.log(~(-2.999));     // 1
```

#### `&` 按位与

按位与操作就是将两个数值的每一位对齐，两个数值的对应位都是 `1` 时才返回 `1`，任何一位是 `0`，结果都是 `0`。如下表所示：

| 第一个数值的位 | 第二个数值的位 | 结果 |
| --- | --- | --- |
| 1 | 1 | 1 |
| 1 | 0 | 0 | 
| 0 | 1 | 0 |
| 0 | 0 | 0 |

#### `|` 按位或

按位或操作就是将两个数值的每一位对齐，两个数值只要有一个位是 `1` 就返回 `1`，只在两个位都是 `0` 的情况下才返回 `0`。如下表所示：

| 第一个数值的位 | 第二个数值的位 | 结果 |
| --- | --- | --- |
| 1 | 1 | 1 |
| 1 | 0 | 1 | 
| 0 | 1 | 1 |
| 0 | 0 | 0 |

#### `^` 按位异或

按位异或与按位或的不同之处在于，两个数值只有一个 `1` 时才返回 `1`，如果对应的两位都是 `1` 或都是 `0`，则返回 `0`。

| 第一个数值的位 | 第二个数值的位 | 结果 |
| --- | --- | --- |
| 1 | 1 | 0 |
| 1 | 0 | 1 | 
| 0 | 1 | 1 |
| 0 | 0 | 0 |

#### `<<` 左移

这个运算符会将数值的所有位向左移动指定的位数。例如：

``` javascript
var oldValue = 2;                       // 等于二进制的 10
var newValue = oldValue << 5;           // 等于二进制的 1000000，十进制的 64
```

注意，左移不会影响操作数的符号位。换句话说，如果将 `-2` 向左移动 `5` 位，结果将是 `-64`，而非 `64`。

#### `>>` 有符号的右移

这个运算符会将数值向右移动，但保留符号位（即正负号标记）。

``` javascript
var oldValue = 64;                      // 等于二进制的 1000000
var newValue = oldValue >> 5;           // 等于二进制的 10 ，即十进制的 2
```

#### `>>>` 无符号的右移

这个运算符会将数值的所有32位都向右移动。对正数来说，无符号右移的结果与有符号右移相同。

``` javascript
var oldValue = 64;                      // 等于二进制的 1000000
var newValue = oldValue >>> 5;          // 等于二进制的 10 ，即十进制的 2
```

无符号右移运算符会把负数的二进制码当成正数的二进制码。而且，由于负数以其绝对值的二进制补码形式表示，因此就会导致无符号右移后的结果非常之大。

``` javascript
var oldValue = -64;                     // 等于二进制的 11111111111111111111111111000000
var newValue = oldValue >>> 5;          // 等于十进制的 134217726
```

### 赋值运算符

简单的赋值运算符由等于号 `=` 表示，其作用就是把右侧的值赋给左侧的变量，如下面的例子所示：

``` javascript
var num = 10;
```

如果在等于号 `=` 前面再添加乘性运算符、加性运算符或位运算符，就可以完成复合赋值操作。这种复合赋值操作相当于是对下面常规表达式的简写形式：

``` javascript
var num = 10;
num += 10;      // 等同于 num = num + 10;
```

每个主要算术运算符（以及个别的其他运算符）都有对应的复合赋值运算符。这些运算符如下所示：

- 乘/赋值 `*=`；
- 除/赋值 `/=`；
- 模/赋值 `%=`；
- 加/赋值 `+=`；
- 减/赋值 `-=`；
- 左移/赋值 `<<=`；
- 有符号右移/赋值 `>>=`；
- 无符号右移/赋值 `>>>=`。

设计这些运算符的主要目的就是简化赋值操作，使用它们不会带来任何性能的提升。

### 条件运算符

` ? : ` 条件运算符应该算是 JavaScript 中最灵活的一种运算符了，而且它遵循与 Java 中的条件运算符相同的语法形式，如下面的例子所示：

``` javascript
variable = boolean_expression ? true_value : false_value;
```

### 逗号运算符

逗号运算符多用于声明多个变量；但除此之外，逗号运算符还可以用于赋值。在用于赋值时，逗号运算符总会返回表达式中的最后一项，如下面的例子所示：

``` javascript
var num = (5, 1, 4, 8, 0); // num 的值为 0
```

由于 `0` 是表达式中的最后一项，因此 `num` 的值就是 `0`。虽然逗号的这种使用方式并不常见，但这个例子可以帮我们理解逗号的这种行为。

# 语句

表达式在 JavaScript 中是短语，那么语句就是整句命令。表达式用来计算出一个值，语句用来执行以使某件事发生。从本质上看，语句定义了 JavaScript 中的主要语法，语句通常使用一或多个关键字来完成给定任务。语句可以很简单，例如通知函数退出；也可以比较复杂，例如指定重复执行某个命令的次数。下表列出了 JavaScript 大部分语句的语法和用途：

| 语句 | 语法 | 用途 |
| --- | --- | --- |
| `break` | `break [label];` | 退出最内层循环或者退出 `switch` 语句，又或者退出 `label` 指定的语句 |
| `case` | `case expression:` | 在 `switch` 语句中标记一条语句 |
| `continue` | `continue [label];` | 重新开始最内层的循环或重新开始 `label` 指定的循环 |
| `debugger` | `debugger;` | 断点器调试 |
| `default` | `default;` | 在 `switch` 中标记默认的语句 |
| `do-while` | `do statement while(expression);` | `while` 循环的一种替代形式 |
| `empty` | `;` | 什么都不做 |
| `for` | `for(init;expr;incr) statement` | 简写的循环结构 |
| `for-in` | `for(var in object) statement` | 遍历一个对象的属性 |
| `function` | `function name([param[],...])`<br>`{statement}` | 声明一个函数 |
| `if-else` | `if (expression) statement1`<br>`[else statement2]` | 执行 `statement1` 或者 `statement2` |
| `label` | `label:statement` | 给 `statement` 指定一个名字 `label` |
| `return` | `return [expression];` | 从函数返回一个值 |
| `switch` | `switch(expression){statement}` | 用 `case` 或者 `default` 语句标记的多分支语句 |
| `throw` | `throw expression;` | 抛出异常 |
| `try` | `try {statement}`<br>`[catch {handler statement}]`<br>`[finally {cleaup statement}]` | 捕获异常 |
| `use strict` | `"use strict"` | 对脚本和函数应用严格模式 |
| `var` | `var name=[=expr][,...];` | 声明并初始化一个或多个变量 |
| `while` | `while(expression) statement` | 基本的循环结构 |
| `with` | `with(object) statement` | 扩展作用域链 |

## 条件语句

### `if-else` 语句

大多数编程语言中最为常用的一个语句就是 `if-else` 语句。以下是 `if-else` 语句的语法：

``` javascript
if (condition) statement1 [else statement2]
```

其中的 `condition` 可以是任意表达式；而且对这个表达式求值的结果不一定是布尔值。JavaScript 会自动调用 `Boolean()` 转换函数将这个表达式的结果转换为一个布尔值。如果对 `condition` 求值的结果是 `true`，则执行 `statement1`，如果对 `condition` 求值的结果是 `false`，则执行 `statement2`。而且这两个语句既可以是一行代码，也可以是一个代码块（以一对花括号括起来的多行代码）。请看下面的例子：


``` javascript
if (i > 25)
    console.log("Greater than 25.");              // 单行语句
else {
    console.log("Less than or equal to 25.");     // 代码块中的语句
}
```

业界普遍推崇的最佳实践是始终使用代码块，即使要执行的只有一行代码。因为这样可以消除人们的误解，否则可能让人分不清在不同条件下要执行哪些语句。

### `switch` 语句

`switch` 语句与 `if` 语句的关系最为密切，而且也是在其他语言中普遍使用的一种流控制语句。JavaScript 中 `switch` 语句的语法与其他基于 C 的语言非常接近，如下所示：

``` javascript
switch (expression) {
  case value: statement
    break;
  case value: statement
    break;
  case value: statement
    break;
  case value: statement
    break;
  default: statement
}
```

`switch` 语句中的每一种情形的含义是：“如果表达式等于这个值（value），则执行后面的语句（statement）”。而 `break` 关键字会导致代码执行流跳出 `switch` 语句。如果省略 `break` 关键字，就会导致执行完当前 `case` 后，继续执行下一个 `case`。最后的 `default` 关键字则用于在表达式不匹配前面任何一种情形的时候，也相当于一个 `else` 语句。从根本上讲，`switch` 语句就是为了让开发人员免于编写像下面这样的代码：

``` javascript
if (i === 25){
  console.log("25");
} else if (i === 35) {
  console.log("35");
} else if (i === 45) {
  console.log("45");
} else {
  console.log("Other");
}
```

而与此等价的switch语句如下所示：

``` javascript
switch (i) {
    case 25: 
        console.log("25");
        break;
    case 35: 
        console.log("35");
        break;
    case 45: 
        console.log("45");
        break;
    default: 
        console.log("Other");
}
```

通过为每个case后面都添加一个break语句，就可以避免同时执行多个case代码的情况。假如确实需要混合几种情形，不要忘了在代码中添加注释，说明你是有意省略了break关键字。

虽然 JavaScript 中的 `switch` 语句借鉴自其他语言，但这个语句也有自己的特色。首先，可以在 `switch` 语句中使用任何数据类型（在很多其他语言中只能使用数值），无论是字符串，还是对象都没有问题。其次，每个 `case` 的值不一定是常量，可以是变量，甚至是表达式。请看下面这两个例子：

``` javascript
switch ("hello world") {
    case "hello" + " world": 
        console.log("Greeting was found.");
        break;
    case "goodbye": 
        console.log("Closing was found.");
        break;
    default: 
        console.log("Unexpected message was found.");
}

var num = 25;
switch (true) {
    case num < 0: 
        console.log("Less than 0.");
        break;
    case num >= 0 && num <= 10: 
        console.log("Between 0 and 10.");
        break;
    case num > 10 && num <= 20: 
        console.log("Between 10 and 20.");
        break;
    default: 
        console.log("More than 20.");
}
```

`switch` 语句首先计算 `switch` 关键字后的表达式，然后按照从上到下的顺序计算每个 `case` 后的表达式，直到执行到 `case` 的表达式的值与 `switch` 的表达式的值相等时为止。由于对每个 `case` 的匹配操作实际上是 `===` 恒等运算符比较，而不是 `==` 相等运算符比较，因此，表达式和 `case` 的匹配并不会做任何类型转换。

## 循环

### `while` 语句

`while` 语句属于前测试循环语句，也就是说，在循环体内的代码被执行之前，就会对出口条件求值。因引，循环体内的代码有可能永远不会被执行。以下是 `while` 语句的语法：

``` javascript
while(expression) statement
```

下面是一个示例：

``` javascript
var i = 0;
while (i < 10) {
    i += 2;
}
```

### `do-while` 语句

`do-while` 语句是一种后测试循环语句，即只有在循环体中的代码执行之后，才会测试出口条件。换句话说，在对条件表达式求值之前，循环体内的代码至少会被执行一次。以下是 `do-while` 语句的语法：

``` javascript
do {
    statement
} while (expression);
```

下面是一个示例：

``` javascript
var i = 0;
do {
   i += 2;
} while (i < 10);
```

### `for` 语句

`for` 语句也是一种前测试循环语句，但它具有在执行循环之前初始化变量和定义循环后要执行的代码的能力。以下是 `for` 语句的语法：

``` javascript
for (initialization; expression; post-loop-expression) statement
```

下面是一个示例：
``` javascript
var count = 10;
for (var i = 0; i < count; i++){
    console.log(i);
}
```
这个 `for` 循环语句与下面的 `while` 语句的功能相同：


``` javascript
var count = 10;
var i = 0;
while (i < count){
    console.log(i);
    i++;
}
```

由于 JavaScript 中不存在块级作用域，因此在循环内部定义的变量也可以在外部访问到。例如：

``` javascript
var count = 10;
for (var i = 0; i < count; i++){
    console.log(i);
}
console.log(i); // 10
```

此外，`for` 语句中的初始化表达式、控制表达式和循环后表达式都是可选的。将这两个表达式全部省略，就会创建一个无限循环，例如：

``` javascript
// 无限循环
for (;;) {
    doSomething();
}

```

### `for-in` 语句

`for-in` 语句是一种精准的迭代语句，可以用来枚举对象的属性。以下是 `for-in` 语句的语法：

``` javascript
for (property in object) statement
```

下面是一个示例：

``` javascript
for (var propName in window) {
    console.log(propName);
}
```

在这个例子中，我们使用 `for-in` 循环来显示了 BOM 中 `window` 对象的所有属性。每次执行循环时，都会将 `window` 对象中存在的一个属性名赋值给变量 `propName`。这个过程会一直持续到对象中的所有属性都被枚举一遍为止。与 `for` 语句类似，这里控制语句中的 `var` 操作符也不是必需的。但是，为了保证使用局部变量，我们推荐上面例子中的这种做法。

JavaScript 对象的属性没有顺序。因此，通过 `for-in` 循环输出的属性名的顺序是不可预测的。具体来讲，所有属性都会被返回一次，但返回的先后次序可能会因浏览器而异。

如果表示要迭代的对象的变量值为 `null` 或 `undefined`，`for-in` 语句会抛出错误。虽然 ECMAScript 5 更正了这一行为；对这种情况不再抛出错误，而只是不执行循环体。为了保证最大限度的兼容性，建议在使用 `for-in` 循环之前，先检测确认该对象的值不是 `null` 或 `undefined`。

## 跳转

### `label` 语句

使用 `label` 语句可以在代码中添加标签，以便将来使用。以下是 `label` 语句的语法：

``` javascript
label: statement
```

下面是一个示例：

``` javascript
start: for (var i=0; i < count; i++) {
    console.log(i); 
}
```

这个例子中定义的 `start` 标签可以在将来由 `break` 或 `continue` 语句引用。加标签的语句一般都要与 `for` 语句等循环语句配合使用。

### `break` 和 `continue` 语句

`break` 和 `continue` 语句用于在循环中精确地控制代码的执行。其中，`break` 语句会立即退出循环，强制继续执行循环后面的语句。而 `continue` 语句虽然也是立即退出循环，但退出循环后会从循环的顶部继续执行。请看下面的例子：

``` javascript
var num = 0;

for (var i=1; i < 10; i++) {
    if (i % 5 == 0) {
       break;
    }
    num++;
}

console.log(num);   // 4
```

这个例子中的 `for` 循环会将变量 `i` 由1递增至 `10`。在循环体内，有一个 `if` 语句检查 `i` 的值是否可以被 `5` 整除（使用求模运算符）。如果是，则执行 `break` 语句退出循环。另一方面，变量 `num` 从 `0` 开始，用于记录循环执行的次数。在执行 `break` 语句之后，结果显示 `4`。也就是说，在变量 `i` 等于 `5` 时，循环总共执行了 `4` 次；而 `break` 语句的执行，导致了循环在 `num` 再次递增之前就退出了。如果在这里把 `break` 替换为 `continue` 的话，则可以看到另一种结果：

``` javascript
var num = 0;

for (var i=1; i < 10; i++) {
if (i % 5 == 0) {
        continue;
    }
    num++;
}

console.log(num);   // 8
```

例子的结果显示 `8`，也就是循环总共执行了 `8` 次。当变量 `i` 等于 `5` 时，循环会在 `num` 再次递增之前退出，但接下来执行的是下一次循环，即i的值等于 `6` 的循环。于是，循环又继续执行，直到 `i` 等于 `10` 时自然结束。而 `num` 的最终值之所以是 `8`，是因为 `continue` 语句导致它少递增了一次。

`break` 和 `continue` 语句都可以与 `label` 语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套的情况下，如下面的例子所示：

``` javascript
var num = 0;

outermost:
for (var i = 0; i < 10; i++) {
     for (var j = 0; j < 10; j++) {
        if (i == 5 && j == 5) {
            break outermost;
        }
        num++;
    }
}

console.log(num);   // 55
```


在这个例子中，`outermost` 标签表示外部的 `for` 语句。如果每个循环正常执行 `10` 次，则 `num++` 语句就会正常执行 `100` 次。换句话说，如果两个循环都自然结束，`num` 的值应该是 `100`。但内部循环中的 `break` 语句带了一个参数：要返回到的标签。添加这个标签的结果将导致 `break` 语句不仅会退出内部的 `for` 语句（即使用变量 `j` 的循环），而且也会退出外部的 `for` 语句（即使用变量 `i` 的循环）。为此，当变量 `i` 和 `j` 都等于 `5` 时， `num`的值正好是 `55`。同样，`continue` 语句也可以像这样与 `label` 语句联用，如下面的例子所示：

``` javascript
var num = 0;

outermost:
for (var i = 0; i < 10; i++) {
    for (var j = 0; j < 10; j++) {
        if (i == 5 && j == 5) {
            continue outermost;
        }
        num++;
    }
}

console.log(num);   // 95
```

在这种情况下，`continue` 语句会强制继续执行循环，退出内部循环，执行外部循环。当 `j` 是 `5` 时，`continue` 语句执行，而这也就意味着内部循环少执行了 `5` 次，因此 `num` 的结果是 `95`。

虽然联用 `break`、`continue` 和 `label` 语句能够执行复杂的操作，但如果使用过度，也会给调试带来麻烦。在此，我们建议如果使用 `label` 语句，一定要使用描述性的标签，同时不要嵌套过多的循环。

### `return` 语句

`return` 语句的作用是指定函数调用后的返回值。`return` 语句的语法如下：

``` javascript
return [expression];
```

下面是一个示例：

``` javascript
function square(x) { return x*x; }  // 一个包含 return 语句的函数
square(2);                          // 调用结果为 4
```

`return` 语句只能在函数体内出现，如果不是的话会报语法错误。当执行到 `return` 语句的时候，函数终止执行，并返回 `expression` 的值给调用程序。如果没有 `return` 语句，则函数调用仅依次执行函数体内的每一条语句直到函数结束，最后返回调用程序。这种情况下，调用表达式的结果是 `undefined`。`return` 语句经常作为函数内的最后一条语句出现，但并不是说要一定放在函数最后。`return` 语句可以单独使用而不必带有 `expression`，这样的话函数也会向调用程序返回 `undefined`。

由于 JavaScript 可以自动插入分号，因此在 `return` 关键字和它后面的表达式之间不能有换行。

### `throw` 语句

`throw` 语句的作用是把程序运行时产生的错误显式地抛出异常。`throw` 语句的语法如下：

``` javascript
throw expression;
```

`expression` 的值可以是任意类型的。可以抛出一个代表错误码的数字，或者包含可读的错误消息的字符串。当 JavaScript 解释器抛出异常的时候通常采用 `Error` 类型和其子类型。`Error` 对象有一个 `name` 属性表示错误类型，一个 `message` 属性用来存放传递给构造函数的字符串，在下面的例子中，当使用非法参数调用函数时就抛出一个 `Error` 对象：

``` javascript
function factorial(x) {
// 如果输入参数是非法的，则抛出一个异常
    if (x < 0) throw new Error("x不能是负数");
    // 否则，计算出一个值，并正常地返回它
    for(var f = 1; x > 1; f *= x, x--) /* empty */ ;
    return f;
}
```

当抛出异常时，JavaScript 解释器会立即停止当前正在执行的逻辑，并跳转至就近的异常处理程序。如果没有找到任何异常处理程序，异常就会沿着 JavaScript 方法的词法结构和调用栈向上传播。最终 JavaScript 将把异常当成程序错误来处理，并报告给用户。

### `try` 语句

`try-catch-finally` 语句是 JavaScript 中异常处理机制，`try-catch-finally` 语句的语法如下：

``` javascript
try {statement} [catch {handler statement}] [finally {cleaup statement}]
```

`try` 从句定义了需要处理的异常所在的代码块。`catch` 从句跟随在 `try` 从句之后，当 `try` 块内某处发生了异常时，调用 `catch` 内的代码逻辑。`catch` 从句后跟随 `finally` 块，后者中放置清理代码，不管 `try` 块中是否产生异常，`finally` 块内的逻辑总是会执行。尽管 `catch` 和 `finally` 都是可选的，但 `try` 从句需要至少二者之一与之组成完整的语句。`try`、`catch` 和 `finally` 语句块都需要使用花括号括起来，这里的花括号是必需的，即使从句中只有一条语句也不能省略花括号。

下面的代码详细的说明了 `try-catch-finally` 的使用目的：

``` javascript
try {
    // 通常来讲，这里的代码会从头执行到尾而不会产生任何问题，
    // 但有时会抛出一个异常，要么是由 throw 语句直接抛出异常，
    // 要么是通过调用一个方法间接抛出异常
}
catch(e) {
    // 当且仅当 try 语句块抛出了异常，才会执行这里的代码
    // 这里可以通过局部变量 e 来获得对 Error 对象或者抛出的其他值的引用
    // 这里的代码块可以基于某种原因处理这个异常，也可以忽略这个异常，
    // 还可以通过 throw 语句重新抛出异常
}
finally {
    // 不管 try 语句块是否抛出了异常，这里的逻辑总是会执行，终止 try 语句块的方式有：
    // 1）正常终止，执行完语句块的最后一条语句
    // 2）通过 break、continue 或 return 语句终止
    // 3）抛出一个异常，异常被 catch 从句捕获
    // 4）抛出一个异常，异常未被捕获，继续向上传播
}
```

## 其他

### `with` 语句

`with` 语句的作用是将代码的作用域设置到一个特定的对象中。`with` 语句的语法如下：

``` javascript
with (expression) statement;
```

定义 `with` 语句的目的主要是为了简化多次编写同一个对象的工作，如下面的例子所示：

``` javascript
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;
```

上面几行代码都包含 `location` 对象。如果使用 `with` 语句，可以把上面的代码改写成如下所示：

``` javascript
with(location){
    var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
}
```

在这个重写后的例子中，使用 `with` 语句关联了 `location` 对象。这意味着在 `with` 语句的代码块内部，每个变量首先被认为是一个局部变量，而如果在局部环境中找不到该变量的定义，就会查询 `location` 对象中是否有同名的属性。如果发现了同名属性，则以 `location` 对象属性的值作为变量的值。

由于大量使用 `with` 语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用 `with` 语句。严格模式下不允许使用 `with` 语句，否则将视为语法错误。

### `debugger` 语句

`debugger` 语句通常什么也不做。然而，当浏览器的调试工具可用并运行的时候，JavaScript 解释器将会以调式模式运行。实际上，这条语句用来产生一个断点（breakpoint），JavaScript 代码的执行会停止在断点的位置，这时可以使用调试器输出变量的值、检查调用栈等。例如：

``` javascript
function f(o) {
    if (o === undefined) {
        debugger;  // 程序会停止在该位置
    }
    // 函数的其他部分
}
```
# 对象

对象是 JavaScript 的数据类型。它将很多值（原始值或者其他对象）聚合在一起，可通过名字访问这些值，因此我们可以把它看成是从字符串到值的映射。对象是动态的，可以随时新增和删除自有属性。对象除了可以保持自有的属性，还可以从一个称为原型的对象继承属性，这种「原型式继承（prototypal inheritance）」是 JavaScript 的核心特征。

对象最常见的用法是创建（create）、设置（set）、查找（query）、删除（delete）、检测（test）和枚举（enumerate）它的属性。

属性包括名字和值。属性名可以是包含空字符串在内的任意字符串，但对象中不能存在两个同名的属性。值可以是任意 JavaScript 值，或者在 ECMAScript 5 中可以是 `getter` 或 `setter` 函数。

除了名字和值之外，每个属性还有一些与之相关的值，称为「属性特性（property attribute）」：

- 可写（writable attribute），表明是否可以设置该属性的值。
- 可枚举（enumerable attribute），表明是否可以通过 `for-in` 循环返回该属性。
- 可配置（configurable attribute），表明是否可以删除或修改该属性。

在 ECMAScript 5 之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。在 ECMAScript 5 中则可以对这些特性加以配置。

除了包含属性特性之外，每个对象还拥有三个相关的「对象特性（object attribute）」：

- 对象的类（class），是一个标识对象类型的字符串。
- 对象的原型（prototype），指向另外一个对象，本对象的属性继承自它的原型对象。
- 对象的扩展标记（extensible flag），指明了在 ECMAScript 5 中是否可以向该对象添加新属性。

最后，用下面术语来对 JavaScript 的「三类对象」和「两类属性」进行区分：

- 内置对象（native object），是由 JavaScript 规范定义的对象或类。例如，数组、函数、日期和正则表达式都是内置对象。
- 宿主对象（host object），是由 JavaScript 解释器所嵌入的宿主环境（比如 Web 浏览器）定义的。客户端 JavaScript 中表示网页结构的 HTMLElement 对象均是宿主对象。
- 自定义对象（user-defined object），是由运行中的 JavaScript 代码创建的对象。
- 自有属性（own property），是直接在对象中定义的属性。
- 继承属性（inherited property），是在对象的原型对象中定义的属性。

## 创建对象

可以使用对象字面量、`new` 关键字和 ECMAScript 5 中的 `Object.create()` 函数来创建对象。

### 使用对象字面量创建对象（推荐）

创建对象最简单的方式就是在 JavaScript 代码中使用对象字面量。对象字面量是由若干名值对组成的映射表，名值对中间用冒号分隔，名值对之间用逗号分隔，整个映射表用花括号括起来。属性名可以是 JavaScript 标识符也可以是字符串直接量（包括空字符串）。属性的值可以是任意类型的 JavaScript 表达式，表达式的值（可以是原始值也可以是对象值）就是这个属性的值。例如：

``` javascript
// 推荐写法
var person = {
    name : "stone",
    age : 28
};

// 也可以写成
var person = {};
person.name = "stone";
person.age = 28;
```

### 使用 `new` 关键字创建对象

new 关键字创建并初始化一个新对象。关键字 new 后跟随一个函数调用。这里的函数称做构造函数（constructor），构造函数用以初始化一个新创建的对象。JavaScript 语言核心中的原始类型都包含内置构造函数。例如：

``` javascript
var person = new Object();
person.name = "stone";
person.age = 28;
```

其中 `var person = new Object();` 等价于 `var person = {};` 。


### 使用 `Object.create()` 函数创建对象

ECMAScript 5 定义了一个名为 `Object.create()` 的方法，它创建一个新对象，其中第一个参数是这个对象的原型。`Object.create()` 提供第二个可选参数，用以对对象的属性进行进一步描述。`Object.create()` 是一个静态函数，而不是提供给某个对象调用的方法。使用它的方法很简单，只须传入所需的原型对象即可。例如：

``` javascript
var person = Object.create(Object.prototype);
person.name = "stone";
person.age = 28;
```

其中 `var person = Object.create(Object.prototype);` 也等价于 `var person = {};` 。

### 原型（prototype）

所有通过对象字面量创建的对象都具有同一个原型对象，并可以通过 JavaScript 代码 `Object.prototype` 获得对原型对象的引用。通过关键字 `new` 和构造函数调用创建的对象的原型就是构造函数的 `prototype` 属性的值。因此，同使用 `{}` 创建对象一样，通过 `new Object()` 创建的对象也继承自 `Object.prototype`。同样，通过 `new Array()` 创建的对象的原型就是 `Array.prototype`，通过 `new Date()` 创建的对象的原型就是 `Date.prototype`。

没有原型的对象为数不多，`Object.prototype` 就是其中之一。它不继承任何属性。其他原型对象都是普通对象，普通对象都具有原型。所有的内置构造函数（以及大部分自定义的构造函数）都具有一个继承自 `Object.prototype` 的原型。例如，`Date.prototype` 的属性继承自 `Object.prototype`，因此由 `new Date()` 创建的 `Date` 对象的属性同时继承自 `Date.prototype` 和 `Object.prototype`。

这一系列链接的原型对象就是所谓的「原型链（prototype chain）」。

## 属性的查询和设置

前面有提到过，可以通过点 `.` 或方括号 `[]` 运算符来获取属性的值。对于点 `.` 来说，左侧应当是一个对象，右侧必须是一个以属性名称命名的简单标识符。对于方括号来说 `[]` ，方括号内必须是一个计算结果为字符串的表达式，这个字符串就是属性的名称。例如：

``` javascript
// 推荐写法
console.log(person.name);   // "stone"
console.log(person.age);    // "28"

// 也可以写成
console.log(person["name"]);    // stone
console.log(person["age"]);     // 28
```

和获取属性的值写法一样，通过点和方括号也可以创建属性或给属性赋值，但需要将它们放在赋值表达式的左侧。例如：

``` javascript
// 推荐写法
person.name = "sophie"; // 赋值
person.age = 30;        // 赋值
person.weight = 38;     // 创建

// 也可以写成
person["name"] = "sophie";  // 赋值
person["age"] = 30;         // 赋值
person["weight"] = 38;      // 创建
```

当使用方括号时，方括号内的表达式必须返回字符串。更严格地讲，表达式必须返回字符串或返回一个可以转换为字符串的值。

## 属性的访问错误

查询一个不存在的属性并不会报错，如果在对象 `o` 自身的属性或继承的属性中均未找到属性 `x`，属性访问表达式 `o.x` 返回 `undefined`。例如：

``` javascript
var person = {};
person.wife;    // undefined
```

但是，如果对象不存在，那么试图查询这个不存在的对象的属性就会报错。`null` 和 `undefined` 值都没有属性，因此查询这些值的属性会报错。例如：

``` javascript
var person = {};
person.wife.name;   // Uncaught TypeError: Cannot read property 'name' of undefined.
```

除非确定 `person` 和 `person.wife` 都是对象，否则不能这样写表达式 `person.wife.name`，因为会报「未捕获的错误类型」，下面提供了两种避免出错的方法：

``` javascript
// 冗余但易懂的写法
var name;
if (person) {
    if (person.wife) 
        name = person.wife.name;
}

// 简练又常用的写法（推荐写法）
var name = person && person.wife && person.wife.name;
```

## 删除属性

`delete` 运算符用来删除对象属性，事实上 `delete` 只是断开属性和宿主对象的联系，并没有真正的删除它。`delete` 运算符只能删除自有属性，不能删除继承属性（要删除继承属性必须从定义这个属性的原型对象上删除它，而且这会影响到所有继承自这个原型的对象）。

> 代码范例，请参见[「变量和数据类型」-「数据类型」-「delete 运算符」](https://github.com/stone0090/javascript-lessons/tree/master/1.5-Expression%26Operators#delete-运算符)。

## 检测属性

JavaScript 对象可以看做属性的集合，我们经常会检测集合中成员的所属关系（判断某个属性是否存在于某个对象中）。可以通过 `in` 运算符、`hasOwnPreperty()` 和 `propertyIsEnumerable()` 来完成这个工作，甚至仅通过属性查询也可以做到这一点。

`in` 运算符的左侧是属性名（字符串），右侧是对象。如果对象的自有属性或继承属性中包含这个属性则返回 `true`。例如：

``` javascript
var o = { x: 1 }
console.log("x" in o);          // true，x是o的属性
console.log("y" in o);          // false，y不是o的属性
console.log("toString" in o);   // true，toString是继承属性
```

对象的 `hasOwnProperty()` 方法用来检测给定的名字是否是对象的自有属性。对于继承属性它将返回 `false`。例如：

``` javascript
var o = { x: 1 }
console.log(o.hasOwnProperty("x"));          // true，x是o的自有属性
console.log(o.hasOwnProperty("y"));          // false，y不是o的属性
console.log(o.hasOwnProperty("toString"));   // false，toString是继承属性
```

`propertyIsEnumerable()` 是 `hasOwnProperty()` 的增强版，只有检测到是自有属性且这个属性的可枚举性（enumerable attribute）为 `true` 时它才返回 `true`。某些内置属性是不可枚举的。通常由 JavaScript 代码创建的属性都是可枚举的，除非在 ECMAScript 5 中使用一个特殊的方法来改变属性的可枚举性。例如：

``` javascript
var o = inherit({ y: 2 });
o.x = 1;
o.propertyIsEnumerable("x");    // true:，x是o的自有属性，可枚举
o.propertyIsEnumerable("y");    // false，y是继承属性
Object.prototype.propertyIsEnumerable("toString");  // false，不可枚举
```

除了使用 `in` 运算符之外，另一种更简便的方法是使用 `!==` 判断一个属性是否是 `undefined`。例如：

``` javascript
var o = { x: 1 }
console.log(o.x !== undefined);              // true，x是o的属性
console.log(o.y !== undefined);              // false，y不是o的属性
console.log(o.toString !== undefined);       // true，toString是继承属性
```

然而有一种场景只能使用 `in` 运算符而不能使用上述属性访问的方式。`in` 可以区分不存在的属性和存在但值为 `undefined` 的属性。例如：

``` javascript
var o = { x: undefined }        // 属性被显式赋值为undefined
console.log(o.x !== undefined); // false，属性存在，但值为undefined
console.log(o.y !== undefined); // false，属性不存在
console.log("x" in o);          // true，属性存在
console.log("y" in o);          // false，属性不存在
console.log(delete o.x);        // true，删除了属性x
console.log("x" in o);          // false，属性不再存在
```

> 扩展阅读「JavaScript 检测原始值、引用值、属性」  
> http://shijiajie.com/2016/06/20/javascript-maintainable-javascript-validate1/

> 扩展阅读「JavaScript 检测之 basevalidate.js」  
> http://shijiajie.com/2016/06/25/javascript-maintainable-javascript-basevalidatejs/

## 枚举属性

除了检测对象的属性是否存在，我们还会经常遍历对象的属性。通常使用 `for-in` 循环遍历，ECMAScript 5 提供了两个更好用的替代方案。

`for-in` 循环可以在循环体中遍历对象中所有可枚举的属性（包括自有属性和继承的属性），把属性名称赋值给循环变量。对象继承的内置方法不可枚举的，但在代码中给对象添加的属性都是可枚举的。例如：

``` javascript
var o = {x:1, y:2, z:3};            // 三个可枚举的自有属性
o.propertyIsEnumerable("toString"); // false，不可枚举
for (p in o) {          // 遍历属性
    console.log(p);     // 输出x、y和z，不会输出toString
}
```

有许多实用工具库给 `Object.prototype` 添加了新的方法或属性，这些方法和属性可以被所有对象继承并使用。然而在 ECMAScript 5 标准之前，这些新添加的方法是不能定义为不可枚举的，因此它们都可以在 `for-in` 循环中枚举出来。为了避免这种情况，需要过滤 `for-in` 循环返回的属性，下面两种方式是最常见的：

``` javascript
for(p in o) {
   if (!o.hasOwnProperty(p)) continue;          // 跳过继承的属性
   if (typeof o[p] === "function") continue;    // 跳过方法
}
```

除了 `for-in` 循环之外，ECMAScript 5 定义了两个用以枚举属性名称的函数。第一个是 `Object.keys()`，它返回一个数组，这个数组由对象中可枚举的自有属性的名称组成。第二个是 `Object.getOwnPropertyNames()`，它和 `Ojbect.keys()` 类似，只是它返回对象的所有自有属性的名称，而不仅仅是可枚举的属性。在 ECMAScript 3 中是无法实现的类似的函数的，因为 ECMAScript 3 中没有提供任何方法来获取对象不可枚举的属性。

## 属性的 `getter` 和 `setter`

我们知道，对象属性是由名字、值和一组特性（attribute）构成的。在 ECMAScript 5 中，属性值可以用一个或两个方法替代，这两个方法就是 `getter` 和 `setter`。由 `getter` 和 `setter` 定义的属性称做「存取器属性（accessor property）」，它不同于「数据属性（data property）」，数据属性只有一个简单的值。

当程序查询存取器属性的值时，JavaScript 调用 `getter` 方法。这个方法的返回值就是属性存取表达式的值。当程序设置一个存取器属性的值时，JavaScript 调用 `setter` 方法，将赋值表达式右侧的值当做参数传入 `setter`。从某种意义上讲，这个方法负责「设置」属性值。可以忽略 `setter` 方法的返回值。

和数据属性不同，存取器属性不具有可写性（writable attribute）。如果属性同时具有 `getter` 和 `setter` 方法，那么它是一个读/写属性。如果它只有 `getter` 方法，那么它是一个只读属性。如果它只有 `setter` 方法，那么它是一个只写属性，读取只写属性总是返回 `undefined`。定义存取器属性最简单的方法是使用对象直接量语法的一种扩展写法。例如：

``` javascript
var o = {
    // 普通的数据属性
    data_prop: value,

    // 存取器属性都是成对定义的函数
    get accessor_prop() { /*这里是函数体 */ },
    set accessor_prop(value) { /* 这里是函数体*/ }
};
```

存取器属性定义为一个或两个和属性同名的函数，这个函数定义没有使用 `function` 关键字，而是使用 `get` 或 `set`。注意，这里没有使用冒号将属性名和函数体分隔开，但在函数体的结束和下一个方法或数据属性之间有逗号分隔。

## 序列化对象（JSON）

对象序列化（serialization）是指将对象的状态转换为字符串，也可将字符串还原为对象。ECMAScript 5 提供了内置函数 `JSON.stringify()` 和 `JSON.parse()` 用来序列化和还原 JavaScript 对象。这些方法都使用 JSON 作为数据交换格式，JSON 的全称是「JavaScript 对象表示法（JavaScript Object Notation）」，它的语法和 JavaScript 对象与数组直接量的语法非常相近。例如：

``` javascript
o = {x:1, y:{z:[false,null,""]}};       // 定义一个对象
s = JSON.stringify(o);                  // s是 '{"x":1,"y":{"z":[false,null,""]}}'
p = JSON.parse(s);                      // p是o的深拷贝
```

ECMAScript 5 中的这些函数的本地实现和 https://github.com/douglascrockford/JSON-js 中的公共域 ECMAScript 3 版本的实现非常类似，或者说完全一样，因此可以通过引入 `json2.js` 模块在 ECMAScript 3 的环境中使用 ECMAScript 5 中的这些函数。

JSON 的语法是 JavaScript 语法的子集，它并不能表示 JavaScript 里的所有值。它支持对象、数组、字符串、无穷大数字、`true`、`false` 和 `null`，可以序列化和还原它们。`NaN`、`Infinity` 和 `-Infinity` 序列化的结果是 `null`，日期对象序列化的结果是 ISO 格式的日期字符串（参照 `Date.toJSON()` 函数），但 `JSON.parse()` 依然保留它们的字符串形态，而不会将它们还原为原始日期对象。函数、`RegExp`、`Error` 对象和 `undefined` 值不能序列化和还原。`JSON.stringify()` 只能序列化对象可枚举的自有属性。对于一个不能序列化的属性来说，在序列化后的输出字符串中会将这个属性省略掉。`JSON.stringify()` 和 `JSON.parse()` 都可以接收第二个可选参数，通过传入需要序列化或还原的属性列表来定制自定义的序列化或还原操作。

# 数组

数组是值的有序集合。每个值叫做一个元素，而每个元素在数组中有一个位置，以数字表示，称为索引。

JavaScript 数组是无类型的，数组元素可以是任意类型，并且同一个数组中的不同元素也可能有不同的类型。数组的元素甚至也可能是对象或其他数组。

JavaScript 数组是动态的，根据需要它们会增长或缩减，并且在创建数组时无须声明一个固定的大小或者在数组大小变化时无须重新分配空间。

JavaScript 数组可能是稀疏的，数组元素的索引不一定要连续的，它们之间可以有空缺。每个 JavaScript 数组都有一个 `length` 属性。针对非稀疏数组，该属性就是数组元素的个数。针对稀疏数组，`length` 比所有元素的索引要大。

JavaScript 数组是 JavaScript 对象的特殊形式，数组索引实际上和碰巧是整数的属性名差不多。通常，数组的实现是经过优化的，用数字索引来访问数组元素一般来说比访问常规的对象属性要快很多。

数组继承自 `Array.prototype` 中的属性，它定义了一套丰富的数组操作方法。

## 创建数组

可以使用数组字面量和 `new` 关键字来创建数组。

### 使用数组字面量创建数组（推荐）

``` javascript
var empty = [];                 // 没有元素的数组
var primes = [2, 3, 5, 7, 11];  // 有5个数值的数组
var misc = [1.1, true, "a"];    // 3个不同类型的元素

// 数组直接量中的值不一定要是常量，可以是任意的表达式
var base = 1024;
var table = [base, base+1, base+2, base+3];

// 也可以包含对象直接量或其他数组直接量
var b = [[1, {x:1, y:2}], [2, {x:3, y:4}]];
```

注意，不要忽略数组字面量的最后一个元素，仅以逗号结尾。下面几个案例，在不同的浏览器下，可能会被识别成2个元素，也有可能识别成3个元素，而造成程序bug。例如：

``` javascript
var nums = [,,,];               // 不好的写法
var names = ["stone",,];        // 不好的写法
var colors = ["red","green",];  // 不好的写法
```

### 使用 `new` 关键字创建数组

使用 `new` 关键字调用构造函数 `Array()` 是创建数组的另一种方法，可以用三种方式调用构造函数。例如：

``` javascript
// 调用时没有参数
var a = new Array();

// 调用时有一个数值参数，它指定长度
var a = new Array(10); 

// 显式指定多个数组元素或者数组的一个非数值元素
var a = new Array(5, 4, 3, 2, 1, "testing");
```

## 数组元素的读和写

使用 `[]` 操作符来访问数组中的一个元素。数组的引用位于方括号的左边。方括号中是一个返回非负整数值的任意表达式。使用该语法既可以读又可以写数组的一个元素。例如：

``` javascript
var a = ["world"];     // 从一个元素的数组开始
var value = a[0];      // 读第0个元素
a[1] = 3.14;           // 写第1个元素
var i = 2; 
a[i] = 3;              // 写第2个元素
a[i + 1] = "hello";    // 写第3个元素
a[a[i]] = a[0];        // 读第0个和第2个元素，写第3个元素
```

请记住，数组是对象的特殊形式，可以为其创建任意名字的属性。但如果使用的属性是数组的索引，数组的特殊行为就是将根据需要更新它们的length属性值。

注意，可以使用负数或非整数来索引数组。这种情况下，数值转换为字符串，字符串作为属性名来用。既然名字不是非负整数，它就只能当做常规的对象属性，而非数组的索引。同样，如果凑巧使用了是非负整数的字符串，它就当做数组索引，而非对象属性。当使用的一个浮点数和一个整数相等时情况也是一样的。例如：

``` javascript
a[-1.23] = true;  // 这将创建一个名为"-1.23"的属性
a["1000"] = 0;    // 这是数组的第1001个元素
a[1.000]          // 和 a[1] 相等
```

事实上数组索引仅仅是对象属性名的一种特殊类型，这意味着 JavaScript 数组没有「越界」错误的概念。当试图查询任何对象中不存在的属性时，不会报错，只会得到 `undefined` 值。

## 稀疏数组

稀疏数组就是包含从0开始的不连续索引的数组。通常，数组的 `length` 属性值代表数组中元素的个数。如果数组是稀疏的，`length` 属性值大于元素的个数。可以用 `Array()` 构造函数或简单地指定数组的索引值大于当前的数组长度来创建稀疏数组。

``` javascript
a = new Array(5);   // 数组没有元素，但是 a.length = 5
a = [];             // 创建一个空数组，a.length = 0
a[1000] = 0;        // 添加一个元素，a.length 被自动更新为1001
```
足够稀疏的数组通常在实现上比稠密的数组更慢、内存利用率更高，在这样的数组中查找元素的时间与常规对象属性的查找时间一样长。

需要注意的是，当省略数组直接量中的值时（使用连续的逗号，比如 `[1,,3]` ），这时所得到的数组也是稀疏数组，省略掉的值是不存在的：

``` javascript
var a1 = [,'1','2'];    // 此数组长度是3 
var a2 = [undefined];   // 此数组包含一个值为 undefined 的元素 
console.log(0 in a1);   // false，a1 在索引0处没有元素
console.log(0 in a2);   // true，a2 在索引0处有一个值为 undefined 的元素 
```

了解稀疏数组是了解 JavaScript 数组的真实本质的一部分。尽管如此，实际上你所碰到的绝大多数 JavaScript 数组不是稀疏数组。并且，如果你确实碰到了稀疏数组，你的代码很可能像对待非稀疏数组一样来对待它们，只不过它们包含一些 `undefined` 值。

## 数组长度

每个数组有一个 `length` 属性，就是这个属性使其区别于常规的 JavaScript 对象。针对稠密（也就是非稀疏）数组，`length` 属性值代表数组中元素的个数。其值比数组中最大的索引大1。例如：

``` javascript
[].length             // 0，数组没有元素
['a','b','c'].length  // 3，最大的索引为2，length 为3
```

当数组是稀疏的时，`length` 属性值大于元素的个数。而且关于此我们可以说的一切也就是数组长度保证大于它每个元素的索引值。或者，换一种说法，在数组中（无论稀疏与否）肯定找不到一个元素的索引值大于或等于它的长度。为了维持此规则不变化，数组有两个特殊的行为。

- 第一个如同上面的描述：如果为一个数组元素赋值，它的索引 `i` 大于或等于现有数组的长度时，`length` 属性的值将设置为 `i+1`。
- 第二个特殊的行为就是设置 `length` 属性为一个小于当前长度的非负整数 `n` 时，当前数组中那些索引值大于或等于 `n` 的元素将从中删除。例如：

``` javascript
a = [1,2,3,4,5];     // 从5个元素的数组开始
a.length = 3;        // 现在 a 为[1,2,3]
a.length = 0;        // 删除所有的元素。a 为[ ]
a.length = 5;        // 长度为5，但是没有元素，就像 new Array(5)
```

还可以将数组的 `length` 属性值设置为大于其当前的长度。实际上这不会向数组中添加新的元素，它只是在数组尾部创建一个空的区域。

在 ECMAScript 5 中，可以用 `Object.defineProperty()` 让数组的 `length` 属性变成只读的。例如：

``` javascript
a = [1,2,3];                                            // 从3个元素的数组开始
Object.defineProperty(a, "length", {writable: false});  // 让 length 属性只读
a.length = 0;                                           // a 不会改变
```

## 数组元素的添加和删除

我们已经见过添加数组元素最简单的方法，为新索引赋值。例如：

``` javascript
a = []           // 开始是一个空数组
a[0] = "zero";   // 然后向其中添加元素
a[1] = "one";
```

也可以使用 `push()` 方法在数组末尾增加一个或多个元素。例如：

``` javascript
a = [];                 // 开始是一个空数组
a.push("zero");         // 在末尾添加一个元素。a = ["zero"]
a.push("one", "two");   // 再添加两个元素。a = ["zero", "one", "two"]
```

可以像删除对象属性一样使用 `delete` 运算符来删除数组元素。例如：

``` javascript
a = [1,2,3]; 
delete a[1];   // a在索引1的位置不再有元素
1 in a         // => false: 数组索引1并未在数组中定义
a.length       // => 3: delete操作并不影响数组长度
```

注意，对一个数组元素使用 `delete` 不会修改数组的 `length` 属性，也不会将元素从高索引处移下来填充已删除属性留下的空白。如果从数组中删除一个元素，它就变成稀疏数组。

## 数组遍历

使用 `for` 循环是遍历数组元素最常见的方法。例如：

``` javascript
var keys = Object.keys(o);   // 获得 o 对象属性名组成的数组
var values = []              // 在数组中存储匹配属性的值
for(var i = 0; i < keys.length; i++) {  // 对于数组中每个索引
    var key = keys[i];                  // 获得索引处的键值
    values[i] = o[key];                 // 在 values 数组中保存属性值
}
```

在嵌套循环或其他性能非常重要的上下文中，可以看到这种基本的数组遍历需要优化，数组的长度应该只查询一次而非每次循环都要查询。例如：

``` javascript
for(var i = 0, len = keys.length; i < len; i++) {
   // 循环体仍然不变
}
```

这些例子假设数组是稠密的，并且所有的元素都是合法数据。否则，使用数组元素之前应该先检测它们。例如：

``` javascript
for(var i = 0; i < a.length; i++) {
    if (!a[i]) continue;    // 跳过 null、undefined 和不存在的元素
    if (!(i in a)) continue ;   // 跳过不存在的元素
    if (a[i] === undefined) continue;   // 跳过 undefined 和不存在的元素
    // 循环体
}
```

还可以使用 `for-in` 循环处理稀疏数组。循环每次将一个可枚举的属性名（包括数组索引）赋值给循环变量，不存在的索引将不会遍历到。例如：

``` javascript
for(var index in sparseArray) {
   var value = sparseArray[index];
   // 此处可以使用索引和值做一些事情
}
```

但由于 `for-in` 循环能够枚举继承的属性名，如添加到 `Array.prototype` 中的方法。基于这个原因，在数组上不应该使用 `for-in` 循环，除非使用额外的检测方法来过滤不想要的属性。例如：

``` javascript
for(var i in a) {
    // 跳过继承的属性
    if (!a.hasOwnProperty(i)) continue;

    // 跳过不是非负整数的 i
    if (String(Math.floor(Math.abs(Number(i)))) !== i) continue;
}
```

`JavaScript` 规范允许 `for-in` 循环以不同的顺序遍历对象的属性。通常数组元素的遍历实现是升序的，但不能保证一定是这样的。如果数组同时拥有对象属性和数组元素，返回的属性名很可能是按照创建的顺序而非数值的大小顺序。如何处理这个问题的实现，各个浏览器都不相同，如果算法依赖于遍历的顺序，那么最好不要使用 `for-in` 而用常规的 `for` 循环。

ECMAScript 5 定义了一些遍历数组元素的新方法，按照索引的顺序按个传递给定义的一个函数。这些方法中最常用的就是 `forEach()` 方法。例如：

``` javascript
var data = [1,2,3,4,5];     // 这是需要遍历的数组
var sumOfSquares = 0;       // 要得到数据的平方和
data.forEach(function(x) {  // 把每个元素传递给此函数
    sumOfSquares += x*x;    // 平方相加
});
console.log(sumOfSquares);  // 55，1 + 4 + 9 + 16 + 25
```

## 数组检测

给定一个未知的对象，判定它是否为数组通常非常有用。在 ECMAScript 5 中，可以使用 `Array.isArray()` 函数来做这件事情。例如：

``` javascript
Array.isArray([])   // true
Array.isArray({})   // false
```

但是，在 ECMAScript 5 以前，要区分数组和非数组对象很困难。`typeof` 运算符对数组返回 `"object"`（并且对于除了函数以外的所有对象都是如此）。`instanceof` 操作符也只能用于简单的情形。例如：

``` javascript
[] instanceof Array     // true
({}) instanceof Array   // false
```

使用 `instanceof` 的问题是在 Web 浏览器中有可能有多个窗体存在。每个窗体都有自己的 JavaScript 环境，有自己的全局对象。并且，每个全局对象有自己的一组构造函数。因此一个窗体中的对象将不可能是另外窗体中的构造函数的实例。窗体之间的混淆不常发生，但这个问题足已证明 `instanceof` 操作符不能视为一个可靠的数组检测方法。

解决方案是检查对象的类属性，对数组而言该属性的值总是 `"Array"`，因此在 ECMAScript 3 中 `isArray()` 函数的代码可以这样书写。例如：

``` javascript
var isArray = Array.isArray || function(o) {
    return typeof o === "object" && Object.prototype.toString.call(o) === "[object Array]";
};
```

## 数组方法

ECMAScript 3 和 ECMAScript 5 在 `Array.prototype` 中定义了一些很有用的操作数组的方法。

### 转换方法

所有对象都具有 `toLocaleString()`、`toString()` 和 `valueOf()` 方法。其中，调用数组的 `toString()` 和 `valueOf()` 方法会返回相同的值，即由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串。实际上，为了创建这个字符串会调用数组每一项的 `toString()` 方法。例如：

``` javascript
var colors = ["red", "blue", "green"];  // 创建一个包含3个字符串的数组
alert(colors.toString()); // red,blue,green
alert(colors.valueOf());  // red,blue,green
alert(colors);            // red,blue,green
```

在这里，我们首先显式地调用了 `toString()` 和 `valueOf()` 方法，以便返回数组的字符串表示，每个值的字符串表示拼接成了一个字符串，中间以逗号分隔。最后一行代码直接将数组传递给了 `alert()`。由于 `alert()`要接收字符串参数，所以它会在后台调用 `toString()` 方法，由此会得到与直接调用 `toString()` 方法相同的结果。

另外，`toLocaleString()` 方法经常也会返回与 `toString()` 和 `valueOf()` 方法相同的值，但也不总是如此。当调用数组的 `toLocaleString()` 方法时，它也会创建一个数组值的以逗号分隔的字符串。而与前两个方法唯一的不同之处在于，这一次为了取得每一项的值，调用的是每一项的 `toLocaleString()` 方法，而不是 `toString()` 方法。例如：

``` javascript
var person1 = {
    toLocaleString : function () {
        return "Nikolaos";
    },
    toString : function() {
        return "Nicholas";
    }
};

var person2 = {
    toLocaleString : function () {
        return "Grigorios";
    },
    toString : function() {
        return "Greg";
    }
};

var people = [person1, person2];
alert(people);                           // Nicholas,Greg
alert(people.toString());                // Nicholas,Greg
alert(people.toLocaleString());          // Nikolaos,Grigorios
```

数组继承的 `toLocaleString()`、`toString()` 和 `valueOf()`方法，在默认情况下都会以逗号分隔的字符串的形式返回数组项。而如果使用 `join()` 方法，则可以使用不同的分隔符来构建这个字符串。`join()` 方法只接收一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串。例如：

``` javascript
var colors = ["red", "green", "blue"];
console.log(colors.join(","));    // red,green,blue
console.log(colors.join("||"));   // red||green||blue
```

 如果数组中的某一项的值是 `null` 或者 `undefined`，那么该值在 `join()`、`toLocaleString()`、`toString()` 和 `valueOf()` 方法返回的结果中以空字符串表示。

### 栈方法

栈是一种 LIFO（Last-In-First-Out，后进先出）的数据结构，也就是最新添加的项最早被移除。`push()` 方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。而 `pop()` 方法则从数组末尾移除最后一项，减少数组的 `length` 值，然后返回移除的项。结合 `push()` 和 `pop()` 方法，就可以像栈一样使用数组。例如：

``` javascript
var colors = [];                            // 创建一个数组
var count = colors.push("red", "green");    // 推入两项
console.log(count);                         // 2，数组的长度

count = colors.push("black");               // 推入另一项
console.log(count);                         // 3，数组的长度

var item = colors.pop();                    // 取得最后一项
console.log(item);                          // "black"
console.log(colors.length);                 // 2，数组的长度
```

### 队列方法

队列是一种 FIFO（First-In-First-Out，先进先出）的数据结构，队列在列表的末端添加项，从列表的前端移除项。`shift()` 方法则从数组前端移除第一项，减少数组的 `length` 值，然后返回移除的项。结合 `push()` 和 `shift()` 方法，就可以像队列一样使用数组。例如：

``` javascript
var colors = [];                            // 创建一个数组
var count = colors.push("red", "green");    // 推入两项
console.log(count);                         // 2，数组的长度

count = colors.push("black");               // 推入另一项
console.log(count);                         // 3，数组的长度

var item = colors.shift();                  // 取得第一项
console.log(item);                          // "red"
console.log(colors.length);                 // 2，数组的长度
```

JavaScipt 还为数组提供了一个 `unshift()` 方法。顾名思义，`unshift()` 与 `shift()` 的用途相反，它能在数组前端添加任意个项并返回新数组的长度。因此，同时使用 `unshift()` 和 `pop()` 方法，可以从相反的方向来模拟队列，即在数组的前端添加项，从数组末端移除项。

### 重排序方法

数组中有两个重排序的方法：`reverse()` 和 `sort()`。`reverse()` 方法可以反转数组元素的顺序。例如：

``` javascript
var values = [1, 2, 3, 4, 5];
values.reverse();
console.log(values);  // 5,4,3,2,1
```

`sort()` 方法可以按升序排列数组元素（即最小的值位于最前面，最大的值排在最后面）。`sort()` 方法在排序的过程中会调用每个数组元素的 `toString()`，然后比较得到的字符串，以确定如何排序。即使数组中的每一项都是数值，`sort()` 方法比较的也是字符串，例如：

``` javascript
var values = [0, 1, 5, 10, 15];
values.sort();
console.log(values);     // 0,1,10,15,5
```

这种排序方式在很多情况下都不是最佳方案，因此 `sort()` 方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面，以下就是一个简单的比较函数。例如：



``` javascript
function compare(value1, value2) {
    if (value1 < value2) {
        return -1;
    } else if (value1 > value2) {
        return 1;
    } else {
        return 0;
    }
}
```

这个比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回0，如果第一个参数应该位于第二个之后则返回一个正数。它可以适用于大多数情况，只要将其作为参数传递给 `sort()` 方法即可。例如：

``` javascript
var values = [10, 5, 1, 0, 15];
values.sort(compare);
console.log(values);   // 0,1,5,10,15
```

对于数值类型或者其 `valueOf()` 方法会返回数值类型的对象类型，可以使用一个更简单的比较函数。这个函数只要用第二个值减第一个值即可。例如：

``` javascript
function compare(value1, value2){
    return value2 - value1;
}
```

由于比较函数通过返回一个小于零、等于零或大于零的值来影响排序结果，因此减法操作就可以适当地处理所有这些情况。

### 操作方法

JavaScript 为操作已经包含在数组中的元素提供了很多方法。其中，`concat()` 方法可以基于当前数组中的所有项创建一个新数组。具体来说，这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。在没有给 `concat()` 方法传递参数的情况下，它只是复制当前数组并返回副本。如果传递给 `concat()` 方法的是一或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中。如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾。例如：

``` javascript
var colors = ["red", "green", "blue"];
var colors2 = colors.concat("yellow", ["black", "brown"]);

console.log(colors);     // red,green,blue
console.log(colors2);    // red,green,blue,yellow,black,brown
```

下一个方法是 `slice()`，它能够基于当前数组中的一或多个项创建一个新数组。`slice()` 方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下，`slice()` 方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项，但不包括结束位置的项。注意，`slice()` 方法不会影响原始数组。例如：

``` javascript
var colors = ["red", "green", "blue", "yellow", "purple"];
var colors2 = colors.slice(1);
var colors3 = colors.slice(1,4);

console.log(colors2);   // green,blue,yellow,purple
console.log(colors3);   // green,blue,yellow
```

> 如果 `slice()` 方法的参数中有一个负数，则用数组长度加上该数来确定相应的位置。例如，在一个包含5项的数组上调用 `slice(-2,-1)` 与调用 `slice(3,4)` 得到的结果相同。如果结束位置小于起始位置，则返回空数组。

下一个方法是 `splice()`，它的主要用途是向数组的中部插入元素，主要有以下3种使用方式。

- 删除：可以删除任意数量的项，只需指定2个参数：起始位置和要删除元素的数量。例如，`splice(0,2)` 会删除数组中的前两项。
- 插入：可以向指定位置插入任意数量的项，只需提供3个参数：起始位置、0（要删除元素的数量）和要插入的元素。如果要插入多个元素，可以再传入第四、第五，以至任意多个元素。例如，`splice(2,0,"red","green")` 会从当前数组的位置2开始插入字符串 `"red"` 和 `"green"`。
- 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定3个参数：起始位置、要删除元素的数量和要插入的元素。插入的项数不必与删除的项数相等。例如，`splice (2,1,"red","green")`会删除当前数组位置2的项，然后再从位置2开始插入字符串 `"red"` 和 `"green"`。

`splice()` 方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）。下面的代码展示了上述3种使用 `splice()` 方法的方式。例如：

``` javascript
var colors = ["red", "green", "blue"];
var removed = colors.splice(0,1);       // 删除第一项
console.log(colors);                    // green,blue
console.log(removed);                   // red，返回的数组中只包含一项

removed = colors.splice(1, 0, "yellow", "orange");  // 从位置1开始插入两项
console.log(colors);                    // green,yellow,orange,blue
console.log(removed);                   // 返回的是一个空数组

removed = colors.splice(1, 1, "red", "purple");     // 插入两项，删除一项
console.log(colors);                    // green,red,purple,orange,blue
console.log(removed);                   // yellow，返回的数组中只包含一项
```

### 位置方法

ECMAScript 5 为数组实例添加了两个位置方法：`indexOf()` 和 `lastIndexOf()`。这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中，`indexOf()` 方法从数组的开头（位置0）开始向后查找，`lastIndexOf()` 方法则从数组的末尾开始向前查找。

这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回 `-1`。在比较第一个参数与数组中的每一项时，会使用全等操作符；也就是说，要求查找的项必须严格相等（就像使用 `===` 一样）。例如：

``` javascript
var numbers = [1,2,3,4,5,4,3,2,1];
console.log(numbers.indexOf(4));          // 3
console.log(numbers.lastIndexOf(4));      // 5
console.log(numbers.indexOf(4, 4));       // 5
console.log(numbers.lastIndexOf(4, 4));   // 3

var person = { name: "Nicholas" };
var people = [{ name: "Nicholas" }];
var morePeople = [person];
console.log(people.indexOf(person));      // -1
console.log(morePeople.indexOf(person));  // 0
```

### 迭代方法

ECMAScript 5 为数组定义了5个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响访问的返回值。以下是这5个迭代方法的作用。

- `every()`，对数组中的每一项运行给定函数，如果该函数对每一项都返回 `true` ，则返回 `true`。
- `filter()`，对数组中的每一项运行给定函数，返回该函数会返回 `true` 的项组成的数组。
- `forEach()`，对数组中的每一项运行给定函数。这个方法没有返回值。
- `map()`，对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
- `some()`，对数组中的每一项运行给定函数，如果该函数对任一项返回 `true` ，则返回 `true`。

以上方法都不会修改数组中的包含的值。在这些方法中，最相似的是 `every()` 和 `some()`，它们都用于查询数组中的项是否满足某个条件。对 `every()` 来说，传入的函数必须对每一项都返回 `true`，这个方法才返回 `true`；否则，它就返回 `false`。而 `some()`方法则是只要传入的函数对数组中的某一项返回 `true`，就会返回 `true`。例如：

``` javascript
var numbers = [1,2,3,4,5,4,3,2,1];
var everyResult = numbers.every(function(item, index, array){
    return (item > 2); 
});
console.log(everyResult);   // false

var someResult = numbers.some(function(item, index, array){
    return (item > 2);
});
console.log(someResult);    // true
```

下面再看一看 `filter()` 函数，它利用指定的函数确定是否在返回的数组中包含的某一项。例如：

``` javascript
var numbers = [1,2,3,4,5,4,3,2,1];
var filterResult = numbers.filter(function(item, index, array){
    return (item > 2);
});
console.log(filterResult);  // [3,4,5,4,3]
```

`map()` 也返回一个数组，而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。例如，可以给数组中的每一项乘以2，然后返回这些乘积组成的数组。例如：

``` javascript
var numbers = [1,2,3,4,5,4,3,2,1];
var mapResult = numbers.map(function(item, index, array){
    return item * 2;
});
console.log(mapResult);     // [2,4,6,8,10,8,6,4,2]
```

最后一个方法是 `forEach()`，它只是对数组中的每一项运行传入的函数。这个方法没有返回值，本质上与使用 `for` 循环迭代数组一样。例如：

``` javascript
var numbers = [1,2,3,4,5,4,3,2,1];
numbers.forEach(function(item, index, array){
    //执行某些操作 
});
```

###　缩小方法

ECMAScript 5 还新增了两个缩小数组的方法：`reduce()` 和 `reduceRight()`。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中，`reduce()` 方法从数组的第一项开始，逐个遍历到最后。而 `reduceRight()` 则从数组的最后一项开始，向前遍历到第一项。

这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为缩小基础的初始值。传给 `reduce()` 和` reduceRight()` 的函数接收4个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

使用 `reduce()` 方法可以执行求数组中所有值之和的操作。例如：

``` javascript
var values = [1,2,3,4,5];
var sum = values.reduce(function(prev, cur, index, array){
    return prev + cur; 
});
console.log(sum); // 15
```

第一次执行回调函数，prev是1，cur是2。第二次，prev是3（1加2的结果），cur是3（数组的第三项）。这个过程会持续到把数组中的每一项都访问一遍，最后返回结果。

`reduceRight()` 的作用类似，只不过方向相反而已。例如：

``` javascript
var values = [1,2,3,4,5];
var sum = values.reduceRight(function(prev, cur, index, array){
    return prev + cur;
});
console.log(sum); // 15
```

使用 `reduce()` 还是 `reduceRight()`，主要取决于要从哪头开始遍历数组。除此之外，它们完全相同。

# 函数

函数是一段代码，它只定义一次，但可以被执行或调用任意次。在 JavaScript 里，函数即对象，程序可以随意操控它们。比如，可以把函数赋值给变量，或者作为参数传递给其他函数，也可以给它们设置属性，甚至调用它们的方法。如果函数挂载在一个对象上，作为对象的一个属性，就称它为对象的方法。如果函数嵌套在其他函数中定义，这样它们就可以访问它们被定义时所处的作用域中的任何变量。

## 函数定义

在 JavaScript 中，函数实际上是对象，每个函数都是 `Function` 构造函数的实例，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。函数通常有以下3中定义方式。例如：

``` javascript
// 写法一：函数声明（推荐写法）
function sum (num1, num2) {
    return num1 + num2;
}

// 写法二：函数表达式（推荐写法）
var sum = function(num1, num2){
    return num1 + num2;
};

// 写法三：Function 构造函数（不推荐写法）
var sum = new Function("num1", "num2", "return num1 + num2"); 
```

由于函数名仅仅是指向函数的指针，因此函数名与包含对象指针的其他变量没有什么不同。换句话说，一个函数可能会有多个名字。例如：

``` javascript
function sum(num1, num2){
    return num1 + num2;
}
console.log(sum(10,10));        // 20

var anotherSum = sum;
console.log(anotherSum(10,10)); // 20

sum = null;
console.log(anotherSum(10,10)); // 20
```

## 没有重载

将函数名想象为指针，也有助于理解为什么 JavaScript 中没有函数重载的概念。

``` javascript
function addSomeNumber(num){
    return num + 100;
}

function addSomeNumber(num) {
    return num + 200;
}

var result = addSomeNumber(100);    // 300
```

显然，这个例子中声明了两个同名函数，而结果则是后面的函数覆盖了前面的函数。以上代码实际上与下面的代码没有什么区别。

``` javascript
var addSomeNumber = function (num){
    return num + 100;
};

addSomeNumber = function (num) {
    return num + 200;
};

var result = addSomeNumber(100);    // 300
```

通过重写代码之后可以很容易明白，在创建第二个函数时，实际上覆盖了引用第一个函数的变量 `addSomeNumber`。

## 函数声明与函数表达式

解析器在向执行环境中加载数据时，对「函数声明」和「函数表达式」并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。例如：

``` javascript
console.log(sum(10,10)); // 20
function sum(num1, num2){
    return num1 + num2;
}
```

以上代码完全可以正常运行。因为在代码开始执行之前，解析器就已经通过一个名为函数声明提升（function declaration hoisting）的过程，读取并将函数声明添加到执行环境中。对代码求值时，JavaScript 引擎在第一遍会声明函数并将它们放到源代码树的顶部。所以，即使声明函数的代码在调用它的代码后面，JavaScript 引擎也能把函数声明提升到顶部。把上面的「函数声明」改为等价的「函数表达式」，就会在执行期间导致错误。例如：

``` javascript
console.log(sum(10,10)); // Uncaught TypeError: sum is not a function
var sum = function(num1, num2){
    return num1 + num2;
};
```

除了上述区别之外，「函数声明」与「函数表达式」的语法是等价的。

## 作为值的函数

因为 JavaScript 中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。来看一看下面的函数。

``` javascript
function callSomeFunction(someFunction, someArgument){
    return someFunction(someArgument);
}
```

这个函数接受两个参数。第一个参数应该是一个函数，第二个参数应该是要传递给该函数的一个值。然后，就可以像下面的例子一样传递函数了。

``` javascript
function add10(num){
    return num + 10;
}

var result1 = callSomeFunction(add10, 10);
console.log(result1);   // 20

function getGreeting(name){
    return "Hello, " + name;
}

var result2 = callSomeFunction(getGreeting, "Nicholas");
console.log(result2);   // "Hello, Nicholas"
```

这里的 `callSomeFunction()` 函数是通用的，即无论第一个参数中传递进来的是什么函数，它都会返回执行第一个参数后的结果。要访问函数的指针而不执行函数的话，必须去掉函数名后面的那对圆括号。因此上面例子中传递给 `callSomeFunction()` 的是 `add10` 和 `getGreeting`，而不是执行它们之后的结果。

当然，还可以从一个函数中返回另一个函数，而且这也是极为有用的一种技术。例如，假设有一个对象数组，我们想要根据某个对象属性对数组进行排序。而传递给数组 `sort()` 方法的比较函数要接收两个参数，即要比较的值。可是，我们需要一种方式来指明按照哪个属性来排序。要解决这个问题，可以定义一个函数，它接收一个属性名，然后根据这个属性名来创建一个比较函数，下面就是这个函数的定义。

``` javascript
function createComparisonFunction(propertyName) {
    return function(object1, object2){
        var value1 = object1[propertyName];
        var value2 = object2[propertyName];
        if (value1 < value2){
            return -1;
        } else if (value1 > value2){
            return 1;
        } else {
            return 0;
        }
    };
}
```

这个函数定义看起来有点复杂，但实际上无非就是在一个函数中嵌套了另一个函数，而且内部函数前面加了一个 `return` 操作符。在内部函数接收到 `propertyName` 参数后，它会使用方括号表示法来取得给定属性的值。取得了想要的属性值之后，定义比较函数就非常简单了。上面这个函数可以像在下面例子中这样使用。

``` javascript
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];

data.sort(createComparisonFunction("name"));
console.log(data[0].name);  // Nicholas

data.sort(createComparisonFunction("age"));
console.log(data[0].name);  // Zachary
```

这里，我们创建了一个包含两个对象的数组 `data`。其中，每个对象都包含一个 `name` 属性和一个 `age` 属性。在默认情况下，`sort()` 方法会调用每个对象的 `toString()` 方法以确定它们的次序；但得到的结果往往并不符合人类的思维习惯。因此，我们调用 `createComparisonFunction("name")` 方法创建了一个比较函数，以便按照每个对象的 `name` 属性值进行排序。而结果排在前面的第一项是 `name` 为 `"Nicholas"`，`age` 是 `29` 的对象。然后，我们又使用了 `createComparisonFunction("age")` 返回的比较函数，这次是按照对象的age属性排序。得到的结果是 `name` 值为 `"Zachary"`，`age` 值是 `28` 的对象排在了第一位。

## 函数的形参和实参

在函数内部，有两个特殊的对象：`arguments` 和 `this`。其中，`arguments` 是一个类数组对象，包含着传入函数中的所有参数。虽然 `arguments` 的主要用途是保存函数参数，但这个对象还有一个名叫 `callee` 的属性，该属性是一个指针，指向拥有这个 `arguments` 对象的函数。请看下面这个非常经典的阶乘函数。

``` javascript
function factorial(num){
	if (num <= 1) {
        return 1;
    } else {
        return num * factorial(num-1)
    }
}
```

定义阶乘函数一般都要用到递归算法，如上面的代码所示，在函数有名字，而且名字以后也不会变的情况下，这样定义没有问题。但问题是这个函数的执行与函数名 `factorial` 紧紧耦合在了一起。为了消除这种紧密耦合的现象，可以像下面这样使用 `arguments.callee`。

``` javascript
function factorial(num){
    if (num <=1) {
        return 1;
    } else {
        return num * arguments.callee(num-1)
    }
}
```

在这个重写后的 `factorial()` 函数的函数体内，没有再引用函数名 `factorial`。这样，无论引用函数时使用的是什么名字，都可以保证正常完成递归调用。例如：

``` javascript
var trueFactorial = factorial;

factorial = function(){
    return 0;
};

console.log(trueFactorial(5));  // 120
console.log(factorial(5));      // 0
```

在此，变量 `trueFactorial` 获得了 `factorial` 的值，实际上是在另一个位置上保存了一个函数的指针。然后，我们又将一个简单地返回 `0` 的函数赋值给 `factorial` 变量。如果像原来的 `factorial()` 那样不使用 `arguments.callee`，调用 `trueFactorial()` 就会返回 `0`。可是，在解除了函数体内的代码与函数名的耦合状态之后，`trueFactorial()` 仍然能够正常地计算阶乘；至于 `factorial()`，它现在只是一个返回 `0` 的函数。

函数内部的另一个特殊对象是 `this`，其行为与 Java 和 C# 中的 `this` 大致类似。换句话说，`this` 引用的是函数据以执行的环境对象（当在网页的全局作用域中调用函数时，`this` 对象引用的就是 `window`）。来看下面的例子。

``` javascript
window.color = "red";
var o = { color: "blue" };

function sayColor(){
    console.log(this.color);
}
sayColor();     // "red"

o.sayColor = sayColor;
o.sayColor();   // "blue"
```

上面这个函数 `sayColor()` 是在全局作用域中定义的，它引用了 `this` 对象。由于在调用函数之前，`this` 的值并不确定，因此 `this` 可能会在代码执行过程中引用不同的对象。当在全局作用域中调用 `sayColor()` 时，`this` 引用的是全局对象 `window`；换句话说，对 `this.color` 求值会转换成对 `window.color` 求值，于是结果就返回了 `"red"`。而当把这个函数赋给对象 `o` 并调用 `o.sayColor()` 时，`this` 引用的是对象 `o`，因此对 `this.color` 求值会转换成对 `o.color` 求值，结果就返回了 `"blue"`。

请大家一定要牢记，函数的名字仅仅是一个包含指针的变量而已。因此，即使是在不同的环境中执行，全局的 `sayColor()` 函数与 `o.sayColor()` 指向的仍然是同一个函数。

ECMAScript 5 也规范化了另一个函数对象的属性 `caller`。这个属性中保存着「调用当前函数的函数的引用」，如果是在全局作用域中调用当前函数，它的值为 `null`。例如：

``` javascript
function outer(){
    inner();
}

function inner(){
    console.log(arguments.callee.caller);
} 

outer();
```

以上代码会导致警告框中显示 `outer()` 函数的源代码。因为 `outer()` 调用了 `inter()`，所以 `arguments.callee.caller` 就指向 `outer()`。

在严格模式下，访问 `arguments.callee`属性，或为函数的 `caller` 属性赋值，都会导致错误。

## 函数的属性和方法

JavaScript 中的函数是对象，因此函数也有属性和方法。每个函数都包含两个属性：`length` 和 `prototype`。其中，`length` 属性表示函数希望接收的命名参数的个数，如下面的例子所示。

``` javascript
function sayName(name){
    console.log(name);
}

function sum(num1, num2){
    return num1 + num2;
}

function sayHi(){
    console.log("hi");
}

console.log(sayName.length);      // 1
console.log(sum.length);          // 2
console.log(sayHi.length);        // 0
```

对于 JavaScript 中的引用类型而言，`prototype` 是保存它们所有实例方法的真正所在。换句话说，诸如 `toString()` 和 `valueOf()` 等方法实际上都保存在 `prototype` 名下，只不过是通过各自对象的实例访问罢了。在创建自定义引用类型以及实现继承时，`prototype` 属性的作用是极为重要的。在 ECMAScript 5 中，`prototype` 属性是不可枚举的，因此使用 `for-in` 无法发现。

每个函数都包含两个非继承而来的方法：`apply()` 和 `call()`。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 `this` 对象的值。首先，`apply()` 方法接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是 `Array` 的实例，也可以是 `arguments` 对象。例如：

``` javascript
function sum(num1, num2){
    return num1 + num2;
}

function callSum1(num1, num2){
    return sum.apply(this, arguments);  // 传入 arguments 对象
}

function callSum2(num1, num2){
    return sum.apply(this, [num1, num2]);  // 传入数组
}

console.log(callSum1(10,10));   // 20
console.log(callSum2(10,10));   // 20
```

在上面这个例子中，`callSum1()` 在执行 `sum()` 函数时传入了 `this`（因为是在全局作用域中调用的，所以传入的就是 `window` 对象）和 `arguments` 对象。而 `callSum2` 同样也调用了 `sum()` 函数，但它传入的则是 `this` 和一个参数数组。这两个函数都会正常执行并返回正确的结果。

`call()` 方法与 `apply()` 方法的作用相同，它们的区别仅在于接收参数的方式不同。对于 `call()` 方法而言，第一个参数是 `this` 值没有变化，变化的是其余参数都直接传递给函数。换句话说，在使用 `call()` 方法时，传递给函数的参数必须逐个列举出来，如下面的例子所示。

``` javascript
function sum(num1, num2){
    return num1 + num2;
}

function callSum(num1, num2){
    return sum.call(this, num1, num2);
}

console.log(callSum(10,10));   // 20
```

在使用 `call()` 方法的情况下，`callSum()` 必须明确地传入每一个参数。结果与使用 `apply()` 没有什么不同。至于是使用 `apply()` 还是 `call()`，完全取决于你采取哪种给函数传递参数的方式最方便。如果你打算直接传入 `arguments` 对象，或者包含函数中先接收到的也是一个数组，那么使用 `apply()` 肯定更方便；否则，选择 `call()` 可能更合适。（在不给函数传递参数的情况下，使用哪个方法都无所谓。）
事实上，传递参数并非 `apply()` 和 `call()` 真正的用武之地；它们真正强大的地方是能够扩充函数赖以运行的作用域。下面来看一个例子。

``` javascript
window.color = "red";
var o = { color: "blue" };

function sayColor(){
    console.log(this.color);
}
sayColor();                // red

sayColor.call(this);       // red
sayColor.call(window);     // red
sayColor.call(o);          // blue
```

这个例子是在前面说明 `this` 对象的示例基础上修改而成的。这一次，`sayColor()` 也是作为全局函数定义的，而且当在全局作用域中调用它时，它确实会显示 `"red"`，因为对 `this.color` 的求值会转换成对 `window.color` 的求值。而 `sayColor.call(this)` 和 `sayColor.call(window)`，则是两种显式地在全局作用域中调用函数的方式，结果当然都会显示 `"red"`。但是，当运行 `sayColor.call(o)` 时，函数的执行环境就不一样了，因为此时函数体内的 `this` 对象指向了 `o`，于是结果显示的是 `"blue"`。

使用 `call()` 或 `apply()` 来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。在前面例子的第一个版本中，我们是先将 `sayColor()` 函数放到了对象 `o` 中，然后再通过 `o` 来调用它的；而在这里重写的例子中，就不需要先前那个多余的步骤了。

# BOM（浏览器对象模型）

ECMAScript 是 JavaScript 的核心，但如果要在 Web 中使用 JavaScript，那么 BOM（浏览器对象模型）则无疑才是真正的核心。BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关。多年来，缺少事实上的规范导致 BOM 有很多问题，因为浏览器提供商会按照各自的想法随意去扩展它。W3C 为了把浏览器中 JavaScript 最基本的部分标准化，已经将 BOM 的主要方面纳入了 HTML5 的规范中。

## `window` 对象

BOM 的核心对象是 `window`，它表示浏览器的一个实例。在浏览器中，`window` 对象有双重角色，它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 `Global` 对象。这意味着在网页中定义的任何一个对象、变量和函数，都以 `window` 作为其 `Global` 对象，因此有权访问 `isNaN()`、`isFinite()`、`parseInt()`、`parseFloat()` 等方法。

### 全局作用域

由于 `window` 对象同时扮演着 ECMAScript 中 `Global` 对象的角色，因此所有在全局作用域中声明的变量、函数都会变成 `window` 对象的属性和方法。来看下面的例子。

``` javascript
var age = 29;
function sayAge(){
    console.log(this.age);
}

console.log(window.age);    // 29
sayAge();                   // 29
window.sayAge();            // 29
```

抛开全局变量会成为 `window` 对象的属性不谈，定义全局变量与在 `window` 对象上直接定义属性还是有一点差别：全局变量不能通过 `delete` 运算符删除，而直接在 `window` 对象上的定义的属性可以。例如：

``` javascript
var age = 29;
window.color = "red";

// 在 IE < 9 时抛出错误，在其他所有浏览器中都返回 false 
delete window.age;

// 在 IE < 9 时抛出错误，在其他所有浏览器中都返回 true
delete window.color;        // return true

console.log(window.age);    // 29
console.log(window.color);  // undefined
```

使用 `var` 语句添加的 `window` 属性有一个名为 `Configurable` 的特性，这个特性的值被默认设置为 `false`，因此这样定义的属性不可以通过 `delete` 运算符删除。IE8 及更早版本在遇到使用 `delete` 删除 `window` 属性的语句时，不管该属性最初是如何创建的，都会抛出错误，以示警告。IE9 及更高版本不会抛出错误。

另外，还要记住一件事：尝试访问未声明的变量会抛出错误，但是通过查询 `window` 对象，可以知道某个可能未声明的变量是否存在。例如：

``` javascript
// 这里会抛出错误，因为 oldValue 未定义
var newValue = oldValue;

// 这里不会抛出错误，因为这是一次属性查询
// newValue 的值是 undefined
var newValue = window.oldValue;
```

### 窗口关系及框架

如果页面中包含框架，则每个框架都拥有自己的 `window` 对象，并且保存在 `frames` 集合中。在 `frames` 集合中，可以通过数值索引（从0开始，从左至右，从上到下）或者框架名称来访问相应的 `window` 对象。每个 `window` 对象都有一个 `name` 属性，其中包含框架的名称。下面是一个包含框架的页面：

``` html
<html>
    <head>
        <title>Frameset Example</title>
    </head>
    <frameset rows="160,*">
        <frame src="frame.htm" name="topFrame">
        <frameset cols="50%,50%">
            <frame src="anotherframe.htm" name="leftFrame">
            <frame src="yetanotherframe.htm" name="rightFrame">
        </frameset>
    </frameset>
</html>
```

对这个例子而言，可以通过 `window.frames[0]` 或者 `window.frames["topFrame"]` 来引用上方的框架。不过最好使用 `top` 而非 `window` 来引用这些框架（例如 `top.frames[0]`），因为 `top` 对象始终指向最高（最外）层的框架，也就是浏览器窗口。使用它可以确保在一个框架中正确地访问另一个框架。因为对于在一个框架中编写的任何代码来说，其中的 `window` 对象指向的都是那个框架的特定实例，而非最高层的框架。

与 `top` 相对的另一个 `window` 对象是 `parent`。顾名思义，`parent`（父）对象始终指向当前框架的直接上层框架。在某些情况下，`parent` 有可能等于 `top`；但在没有框架的情况下，`parent` 一定等于 `top`（此时它们都等于 `window`）。

与框架有关的最后一个对象是 `self`，它始终指向 `window`；实际上，`self` 和 `window` 对象可以互换使用。引入 `self` 对象的目的只是为了与 `top` 和 `parent` 对象对应起来，因此它不格外包含其他值。

所有这些对象都是 `window` 对象的属性，可以通过 `window.parent`、`window.top` 等形式来访问。同时，这也意味着可以将不同层次的 `window` 对象连缀起来，例如 `window.parent.parent.frames[0]`。

在使用框架的情况下，浏览器中会存在多个 `Global` 对象。在每个框架中定义的全局变量会自动成为框架中 `window` 对象的属性。由于每个 `window` 对象都包含原生类型的构造函数，因此每个框架都有一套自己的构造函数，这些构造函数一一对应，但并不相等。例如，`top.Object` 并不等于 `top.frames[0].Object`。这个问题会影响到对跨框架传递的对象使用 `instanceof` 运算符。

### 导航和打开窗口

使用 `window.open()` 方法既可以导航到一个特定的 URL，也可以打开一个新的浏览器窗口。这个方法可以接收4个参数：要加载的URL、窗口目标、一个特性字符串以及一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值。通常只须传递第一个参数，最后一个参数只在不打开新窗口的情况下使用。

如果为 `window.open()` 传递了第二个参数，而且该参数是已有窗口或框架的名称，那么就会在具有该名称的窗口或框架中加载第一个参数指定的 URL。看下面的例子。

``` javascript
// 等同于 <a href="http://shijiajie.com" target="newWindow"></a>
window.open("http://shijiajie.com/", "newWindow");
```

#### 弹出窗口

如果给 `window.open()` 传递的第二个参数并不是一个已经存在的窗口或框架，那么该方法就会根据在第三个参数位置上传入的字符串创建一个新窗口或新标签页。如果没有传入第三个参数，那么就会打开一个带有全部默认设置（工具栏、地址栏和状态栏等）的新浏览器窗口（或者打开一个新标签页）。在不打开新窗口的情况下，会忽略第三个参数。

第三个参数是一个逗号分隔的设置字符串，表示在新窗口中都显示哪些特性。下表列出了可以出现在这个字符串中的设置选项。

| 设置 | 值 | 说明 |
| --- | --- | --- |
| fullscreen | yes或no | 表示浏览器窗口是否最大化。仅限IE |
| height | 数值 | 表示新窗口的高度。不能小于100 |
| left | 数值 | 表示新窗口的左坐标。不能是负值 |
| location | yes或no | 表示是否在浏览器窗口中显示地址栏。不同浏览器的默认值不同。如果设置为no，地址栏可能会隐藏，也可能会被禁用（取决于浏览器） |
| menubar | yes或no | 表示是否在浏览器窗口中显示菜单栏。默认值为no |
| resizable | yes或no | 表示是否可以通过拖动浏览器窗口的边框改变其大小。默认值为no |
| scrollbars | yes或no | 表示如果内容在视口中显示不下，是否允许滚动。默认值为no |
| status | yes或no | 表示是否在浏览器窗口中显示状态栏。默认值为no |
| toolbar | yes或no | 表示是否在浏览器窗口中显示工具栏。默认值为no |
| top | 数值 | 表示新窗口的上坐标。不能是负值 |
| width | 数值 | 表示新窗口的宽度。不能小于100 |


这行代码会打开一个新的可以调整大小的窗口，窗口初始大小为400×400像素，并且距屏幕上沿和左边各10像素。

``` javascript
window.open("http://shijiajie.com/","newWindow",
    "height=400,width=400,top=10,left=10,resizable=yes");
```

`window.open()` 方法会返回一个指向新窗口的引用。引用的对象与其他 `window` 对象大致相似，但我们可以对其进行更多控制。例如，有些浏览器在默认情况下可能不允许我们针对主浏览器窗口调整大小或移动位置，但却允许我们针对通过window.open()创建的窗口调整大小或移动位置。通过这个返回的对象，可以像操作其他窗口一样操作新打开的窗口，如下所示。

``` javascript
var win = window.open("http://shijiajie.com/","newWindow",
    "height=400,width=400,top=10,left=10,resizable=yes");

// 调整大小
win.resizeTo(500,500);

// 移动位置
win.moveTo(100,100);

// 关闭窗口
win.close();
```

但是，`close()` 方法仅适用于通过 `window.open()` 打开的弹出窗口。对于浏览器的主窗口，如果没有得到用户的允许是不能关闭它的。

新创建的 `window` 对象有一个 `opener` 属性，其中保存着打开它的原始窗口对象。这个属性只在弹出窗口中的最外层 `window` 对象（top）中有定义，而且指向调用 `window.open()` 的窗口或框架。例如：

``` javascript
var win = window.open("http://shijiajie.com/","newWindow",
    "height=400,width=400,top=10,left=10,resizable=yes");

console.log(win.opener === window);   // true
```
虽然弹出窗口中有一个指针指向打开它的原始窗口，但原始窗口中并没有这样的指针指向弹出窗口。窗口并不跟踪记录它们打开的弹出窗口，因此我们只能在必要的时候自己来手动实现跟踪。

#### 弹出窗口屏蔽程序

曾经有一段时间，广告商在网上使用弹出窗口达到了肆无忌惮的程度。他们经常把弹出窗口打扮成系统对话框的模样，引诱用户去点击其中的广告。由于看起来像是系统对话框，一般用户很难分辨是真是假。为了解决这个问题，大多数浏览器内置有弹出窗口屏蔽程序，将绝大多数用户不想看到弹出窗口屏蔽掉。

于是，在弹出窗口被屏蔽时，就应该考虑两种可能性。如果是浏览器内置的屏蔽程序阻止的弹出窗口，那么 `window.open()` 很可能会返回 `null`，如果是浏览器扩展或其他程序阻止的弹出窗口，那么 `window.open()` 通常会抛出一个错误。因此，要想准确地检测出弹出窗口是否被屏蔽，必须在检测返回值的同时，将对 `window.open()` 的调用封装在一个 `try-catch` 块中，如下所示。

``` javascript
var blocked = false;

try {
    var win = window.open("http://shijiajie.com", "_blank");
    if (win == null){
        blocked = true;
    }
} catch (ex){
    blocked = true;
}
if (blocked){
    console.log("The popup was blocked!");
}
```

### 间歇调用和超时调用

JavaScript 是单线程语言，但它允许通过设置超时值和间歇时间值来调度代码在特定的时刻执行。前者是在指定的时间过后执行代码，而后者则是每隔指定的时间就执行一次代码。

超时调用需要使用 `window` 对象的 `setTimeout()` 方法，它接受两个参数：要执行的代码和以毫秒表示的时间（即在执行代码前需要等待多少毫秒）。其中，第一个参数可以是一个包含 JavaScript 代码的字符串（就和在 `eval()` 函数中使用的字符串一样），也可以是一个函数。例如，下面对 `setTimeout()` 的两次调用都会在一秒钟后显示一个警告框。

``` javascript
// 不建议传递字符串
setTimeout("console.log('Hello world!') ", 1000);

// 推荐的调用方式
setTimeout(function() { 
    console.log("Hello world!"); 
}, 1000);
```

虽然这两种调用方式都没有问题，但由于传递字符串可能导致性能损失，因此不建议以字符串作为第一个参数。

第二个参数是一个表示等待多长时间的毫秒数，但经过该时间后指定的代码不一定会执行。JavaScript 是一个单线程序的解释器，因此一定时间内只能执行一段代码。为了控制要执行的代码，就有一个 JavaScript 任务队列。这些任务会按照将它们添加到队列的顺序执行。`setTimeout()` 的第二个参数告诉 `JavaScript` 再过多长时间把当前任务添加到队列中。如果队列是空的，那么添加的代码会立即执行；如果队列不是空的，那么它就要等前面的代码执行完了以后再执行。

调用 `setTimeout()` 之后，该方法会返回一个数值 `ID`，表示超时调用。这个超时调用 `ID` 是计划执行代码的唯一标识符，可以通过它来取消超时调用。要取消尚未执行的超时调用计划，可以调用 `clearTimeout()` 方法并将相应的超时调用 `ID` 作为参数传递给它，如下所示。

``` javascript
// 设置超时调用
var timeoutId = setTimeout(function() {
    console.log("Hello world!");
}, 1000);

// 注意：把它取消
clearTimeout(timeoutId);
```

只要是在指定的时间尚未过去之前调用 `clearTimeout()`，就可以完全取消超时调用。前面的代码在设置超时调用之后马上又调用了 `clearTimeout()`，结果就跟什么也没有发生一样。

间歇调用与超时调用类似，只不过它会按照指定的时间间隔重复执行代码，直至间歇调用被取消或者页面被卸载。设置间歇调用的方法是 `setInterval()`，它接受的参数与 `setTimeout()` 相同：要执行的代码（字符串或函数）和每次执行之前需要等待的毫秒数。下面来看一个例子。

``` javascript
// 不建议传递字符串
setInterval ("console.log('Hello world!') ", 10000);

// 推荐的调用方式
setInterval (function() { 
    console.log("Hello world!"); 
}, 10000);
```

调用 `setInterval()` 方法同样也会返回一个间歇调用 `ID`，该 `ID` 可用于在将来某个时刻取消间歇调用。要取消尚未执行的间歇调用，可以使用 `clearInterval()` 方法并传入相应的间歇调用 `ID`。取消间歇调用的重要性要远远高于取消超时调用，因为在不加干涉的情况下，间歇调用将会一直执行到页面卸载。以下是一个常见的使用间歇调用的例子。

``` javascript
var num = 0;
var max = 10;
var intervalId = null;

function incrementNumber() {
    num++;
    // 如果执行次数达到了max设定的值，则取消后续尚未执行的调用
    if (num == max) {
        clearInterval(intervalId);
        console.log("Done");
    }
}

intervalId = setInterval(incrementNumber, 500);
```

在这个例子中，变量num每半秒钟递增一次，当递增到最大值时就会取消先前设定的间歇调用。这个模式也可以使用超时调用来实现，如下所示。

``` javascript
var num = 0;
var max = 10;

function incrementNumber() {
    num++;

    // 如果执行次数未达到max设定的值，则设置另一次超时调用
    if (num < max) {
        setTimeout(incrementNumber, 500);
    } else {
        console.log("Done");
    }
}

setTimeout(incrementNumber, 500);
```

可见，在使用超时调用时，没有必要跟踪超时调用 `ID`，因为每次执行代码之后，如果不再设置另一次超时调用，调用就会自行停止。一般认为，使用超时调用来模拟间歇调用的是一种最佳模式。在开发环境下，很少使用真正的间歇调用，原因是后一个间歇调用可能会在前一个间歇调用结束之前启动。而像前面示例中那样使用超时调用，则完全可以避免这一点。所以，最好不要使用间歇调用。

### 系统对话框

浏览器通过 `alert()`、`confirm()` 和 `prompt()` 方法可以调用系统对话框向用户显示消息。系统对话框与在浏览器中显示的网页没有关系，也不包含 HTML。它们的外观由操作系统及（或）浏览器设置决定，而不是由 CSS 决定。此外，通过这几个方法打开的对话框都是同步和模态的。也就是说，显示这些对话框的时候代码会停止执行，而关掉这些对话框后代码又会恢复执行。

第一种对话框是调用 `alert()` 方法生成的。它向用户显示一个系统对话框，其中包含指定的文本和一个 OK（“确定”）按钮。通常使用 `alert()` 生成的“警告”对话框向用户显示一些他们无法控制的消息，例如错误消息。而用户只能在看完消息后关闭对话框。

第二种对话框是调用 `confirm()` 方法生成的。从向用户显示消息的方面来看，这种“确认”对话框很像是一个“警告”对话框。但二者的主要区别在于“确认”对话框除了显示OK按钮外，还会显示一个 Cancel（“取消”）按钮，两个按钮可以让用户决定是否执行给定的操作。

为了确定用户是单击了OK还是Cancel，可以检查 `confirm()` 方法返回的布尔值：`true` 表示单击了OK，`false` 表示单击了Cancel或单击了右上角的 X 按钮。确认对话框的典型用法如下。

``` javascript
if (confirm("Are you sure?")) {
    alert("I'm so glad you're sure! ");
} else {
    alert("I'm sorry to hear you're not sure.");
}
```

最后一种对话框是通过调用 `prompt()` 方法生成的，这是一个“提示”框，用于提示用户输入一些文本。提示框中除了显示 OK 和 Cancel 按钮之外，还会显示一个文本输入域，以供用户在其中输入内容。`prompt()` 方法接受两个参数：要显示给用户的文本提示和文本输入域的默认值（可以是一个空字符串）。

如果用户单击了 OK 按钮，则 `promp()` 返回文本输入域的值；如果用户单击了 Cancel 或没有单击 OK 而是通过其他方式关闭了对话框，则该方法返回 `null`。下面是一个例子。

``` javascript
var result = prompt("What is your name? ", "");
if (result !== null) {
    alert("Welcome, " + result);
}
```

综上所述，这些系统对话框很适合向用户显示消息并请用户作出决定。由于不涉及 HTML、CSS 或 JavaScript，因此它们是增强 Web 应用程序的一种便捷方式。

## `location` 对象

`location` 对象提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能。事实上，`location` 对象是很特别的一个对象，因为它既是 `window` 对象的属性，也是 `document` 对象的属性；换句话说，`window.location` 和 `document.location` 引用的是同一个对象。`location` 对象的用处不只表现在它保存着当前文档的信息，还表现在它将 URL 解析为独立的片段，让开发人员可以通过不同的属性访问这些片段。下表列出了 `location` 对象的所有属性。

| 属性名 | 例子 | 说明 |
| --- | --- | --- |
| hash | "#contents" | 返回 URL 中的 hash（#号后跟零或多个字符），如果 URL 中不包含散列，则返回空字符串 |
| host | "shijiajie.com:80" | 返回服务器名称和端口号（如果有）
| hostname | "shijiajie.com" | 返回不带端口号的服务器名称 |
| href | "http:/shijiajie.com" | 返回当前加载页面的完整URL。而 `location` 对象的 `toString()` 方法也返回这个值 |
| pathname | "/WileyCDA/" | 返回URL中的目录和（或）文件名 |
| port | "8080" | 返回 URL 中指定的端口号。如果 URL 中不包含端口号，则这个属性返回空字符串 |
| protocol | "http:" | 返回页面使用的协议。通常是 http: 或 https:
| search | "?q=javascript" | 返回URL的查询字符串。这个字符串以问号开头 |

### 查询字符串参数

虽然通过上面的属性可以访问到 `location` 对象的大多数信息，但其中访问URL包含的查询字符串的属性并不方便。尽管 `location.search` 返回从问号到 URL 末尾的所有内容，但却没有办法逐个访问其中的每个查询字符串参数。为此，可以像下面这样创建一个函数，用以解析查询字符串，然后返回包含所有参数的一个对象：

``` javascript
/*
 * 这个函数用来解析来自URL的查询串中的name=value参数对
 * 它将name=value对存储在一个对象的属性中，并返回该对象
 * 这样来使用它
 *
 * var args = urlArgs(); // 从URL中解析参数
 * var q = args.q || ""; // 如果参数定义了的话就使用参数；否则使用一个默认值
 * var n = args.n ? parseInt(args.n) : 10;
 */
function urlArgs() {
    var args = {};                                  // 定义一个空对象
    var query = location.search.substring(1);       // 查找到查询串，并去掉'? '
    var pairs = query.split("&");                   // 根据"&"符号将查询字符串分隔开
    for (var i = 0; i < pairs.length; i++) {        // 对于每个片段
        var pos = pairs[i].indexOf('=');            // 查找"name=value"
        if (pos == -1) continue;                    // 如果没有找到的话，就跳过
        var name = pairs[i].substring(0, pos);      // 提取name
        var value = pairs[i].substring(pos + 1);    // 提取value
        value = decodeURIComponent(value);          // 对value进行解码
        args[name] = value;                         // 存储为属性
    }
    return args;                                    // 返回解析后的参数
}
```

### 位置操作

使用 `location` 对象可以通过很多方式来改变浏览器的位置。首先，也是最常用的方式，就是使用 `assign()`方法并为其传递一个 URL，如下所示。

``` javascript
location.assign("http://shijiajie.com");
```

这样，就可以立即打开新URL并在浏览器的历史记录中生成一条记录。如果是将 `location.href` 或 `window.location` 设置为一个URL值，也会以该值调用 `assign()` 方法。例如，下列两行代码与显式调用 `assign()` 方法的效果完全一样。

``` javascript
window.location = "http://shijiajie.com";
location.href = "http://shijiajie.com";
```

在这些改变浏览器位置的方法中，最常用的是设置 `location.href` 属性。

另外，修改 `location` 对象的其他属性也可以改变当前加载的页面。下面的例子展示了通过将 `hash`、`search`、`hostname`、`pathname` 和 `port` 属性设置为新值来改变 URL。

``` javascript
// 假设初始 URL 为 http://shijiajie.com/about/
location.href = "http://shijiajie.com/about/"

// 将 URL 修改为 "http://shijiajie.com/about/#ds-thread"
location.hash = "#ds-thread";

// 将 URL 修改为 "http://shijiajie.com/about/?args=123"
location.search = "?args=123";

// 将 URL 修改为 "https://segmentfault.com/"
location.hostname = "segmentfault.com";

// 将 URL 修改为 "http://segmentfault.com/u/stone0090/"
location.pathname = "u/stone0090";

// 将 URL 修改为 "https://segmentfault.com:8080/"
location.port = 8080;
```
当通过上述任何一种方式修改URL之后，浏览器的历史记录中就会生成一条新记录，因此用户通过单击“后退”按钮都会导航到前一个页面。要禁用这种行为，可以使用 `replace()` 方法。这个方法只接受一个参数，即要导航到的 URL；结果虽然会导致浏览器位置改变，但不会在历史记录中生成新记录。在调用 `replace()` 方法之后，用户不能回到前一个页面，来看下面的例子：

``` html
<!DOCTYPE html>
<html>
<head>
    <title>You won't be able to get back here</title>
</head>
    <body>
    <p>Enjoy this page for a second, because you won't be coming back here.</p>
    <script type="text/javascript">
        setTimeout(function () {
            location.replace("http://shijiajie.com/");
        }, 1000);
    </script>
</body>
</html>
```

如果将这个页面加载到浏览器中，浏览器就会在1秒钟后重新定向到 `shijiajie.com`。然后，“后退”按钮将处于禁用状态，如果不重新输入完整的 URL，则无法返回示例页面。

与位置有关的最后一个方法是 `reload()`，作用是重新加载当前显示的页面。如果调用 `reload()` 时不传递任何参数，页面就会以最有效的方式重新加载。也就是说，如果页面自上次请求以来并没有改变过，页面就会从浏览器缓存中重新加载。如果要强制从服务器重新加载，则需要像下面这样为该方法传递参数 `true`。

``` javascript
location.reload();        // 重新加载（有可能从缓存中加载）
location.reload(true);    // 重新加载（从服务器重新加载）
```

位于 `reload()` 调用之后的代码可能会也可能不会执行，这要取决于网络延迟或系统资源等因素。为此，最好将 `reload()` 放在代码的最后一行。

## `history` 对象

`history` 对象保存着用户上网的历史记录，从窗口被打开的那一刻算起。因为 `history` 是 `window` 对象的属性，因此每个浏览器窗口、每个标签页乃至每个框架，都有自己的 `history` 对象与特定的 `window` 对象关联。出于安全方面的考虑，开发人员无法得知用户浏览过的 URL。不过，借由用户访问过的页面列表，同样可以在不知道实际 URL 的情况下实现后退和前进。

使用 `go()` 方法可以在用户的历史记录中任意跳转，可以向后也可以向前。这个方法接受一个参数，表示向后或向前跳转的页面数的一个整数值。负数表示向后跳转（类似于单击浏览器的“后退”按钮），正数表示向前跳转（类似于单击浏览器的“前进”按钮）。来看下面的例子。

``` javascript
// 后退一页
history.go(-1);

// 前进一页
history.go(1);

// 前进两页
history.go(2);
```

也可以给 `go()` 方法传递一个字符串参数，此时浏览器会跳转到历史记录中包含该字符串的第一个位置——可能后退，也可能前进，具体要看哪个位置最近。如果历史记录中不包含该字符串，那么这个方法什么也不做，例如：

``` javascript
// 跳转到最近的 shijiajie.com 页面
history.go("shijiajie.com");
```

另外，还可以使用两个简写方法 `back()` 和 `forward()` 来代替 `go()`。顾名思义，这两个方法可以模仿浏览器的“后退”和“前进”按钮。

``` javascript
// 后退一页
history.back();

// 前进一页
history.forward();
```

除了上述几个方法外，`history` 对象还有一个 `length` 属性，保存着历史记录的数量。这个数量包括所有历史记录，即所有向后和向前的记录。对于加载到窗口、标签页或框架中的第一个页面而言，`history.length` 等于0。通过像下面这样测试该属性的值，可以确定用户是否一开始就打开了你的页面。

``` javascript
if (history.length == 0){
    //这应该是用户打开窗口后的第一个页面
}
```

虽然 `history` 并不常用，但在创建自定义的“后退”和“前进”按钮，以及检测当前页面是不是用户历史记录中的第一个页面时，还是必须使用它。

## 小结

BOM（浏览器对象模型）以 `window` 对象为依托，表示浏览器窗口以及页面可见区域。同时，`window` 对象还是 ECMAScript 中的 `Global` 对象，因而所有全局变量和函数都是它的属性，且所有原生的构造函数及其他函数也都存在于它的命名空间下。本章讨论了下列 BOM 的组成部分。

- 在使用框架时，每个框架都有自己的 `window` 对象以及所有原生构造函数及其他函数的副本。每个框架都保存在 `frames` 集合中，可以通过位置或通过名称来访问。
- 有一些窗口指针，可以用来引用其他框架，包括父框架。
- `top` 对象始终指向最外围的框架，也就是整个浏览器窗口。
- `parent` 对象表示包含当前框架的框架，而 `self` 对象则回指 `window`。
- 使用 `location` 对象可以通过编程方式来访问浏览器的导航系统。设置相应的属性，可以逐段或整体性地修改浏览器的 URL。
- 调用 `replace()` 方法可以导航到一个新 URL，同时该 URL 会替换浏览器历史记录中当前显示的页面。
- `navigator` 对象提供了与浏览器有关的信息。到底提供哪些信息，很大程度上取决于用户的浏览器；不过，也有一些公共的属性（如 `userAgent`）存在于所有浏览器中。

BOM中还有两个对象：`screen` 和 `history`，但它们的功能有限。`screen` 对象中保存着与客户端显示器有关的信息，这些信息一般只用于站点分析。`history` 对象为访问浏览器的历史记录开了一个小缝隙，开发人员可以据此判断历史记录的数量，也可以在历史记录中向后或向前导航到任意页面。

# 事件

JavaScript 程序采用了异步事件驱动编程模型。在这种程序设计风格下，当文档、浏览器、元素或与之相关的对象发生某些有趣的事情时，Web 浏览器就会产生事件（event）。例如，当 Web 浏览器加载完文档、用户把鼠标指针移到超链接上或敲击键盘时，Web 浏览器都会产生事件。如果 JavaScript 应用程序关注特定类型的事件，那么它可以注册当这类事件发生时要调用的一个或多个函数。请注意，这种风格并不只应用于 Web 编程，所有使用图形用户界面的应用程序都采用了它，它们静待某些事情发生（即，它们等待事件发生），然后它们响应。

请注意，事件本身并不是一个需要定义的技术名词。简而言之，事件就是 Web 浏览器通知应用程序发生了什么事情，这种在传统软件工程中被称为观察员模式。

## 事件流

当浏览器发展到第四代时（IE4 及 Netscape Communicator 4），浏览器开发团队遇到了一个很有意思的问题：页面的哪一部分会拥有某个特定的事件？要明白这个问题问的是什么，可以想象画在一张纸上的一组同心圆。如果你把手指放在圆心上，那么你的手指指向的不是一个圆，而是纸上的所有圆。两家公司的浏览器开发团队在看待浏览器事件方面还是一致的。如果你单击了某个按钮，他们都认为单击事件不仅仅发生在按钮上。换句话说，在单击按钮的同时，你也单击了按钮的容器元素，甚至也单击了整个页面。

**事件流**描述的是从页面中接收事件的顺序。但有意思的是，IE 和 Netscape 开发团队居然提出了差不多是完全相反的事件流的概念。IE 的事件流是事件冒泡流，而 Netscape Communicator 的事件流是事件捕获流。

### 事件冒泡

IE 的事件流叫做**事件冒泡**（event bubbling），即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）。以下面的HTML页面为例：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Event Bubbling Example</title>
</head>
<body>
    <div id="myDiv">Click Me</div>
</body>
</html>
```

如果你单击了页面中的 `<div>` 元素，那么这个 `click` 事件会按照如下顺序传播：

1. `<div>`
2. `<body>`
3. `<html>`
4. `document`

也就是说，`click` 事件首先在 `<div>` 元素上发生，而这个元素就是我们单击的元素。然后，`click` 事件沿 DOM 树向上传播，在每一级节点上都会发生，直至传播到 `document` 对象。下图展示了事件冒泡的过程。

![](http://qiniu.shijiajie.com/blog/javascript-lesson/2.3/1.jpg)

### 事件捕获

Netscape Communicator 团队提出的另一种事件流叫做**事件捕获**（event capturing）。事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。事件捕获的用意在于在事件到达预定目标之前捕获它。如果仍以前面的 HTML 页面作为演示事件捕获的例子，那么单击 `<div>` 元素就会以下列顺序触发 `click` 事件。

1. `document`
2. `<html>`
3. `<body>`
4. `<div>`

在事件捕获过程中，`document` 对象首先接收到 `click` 事件，然后事件沿 DOM 树依次向下，一直传播到事件的实际目标，即 `<div>` 元素。下图展示了事件捕获的过程。

![](http://qiniu.shijiajie.com/blog/javascript-lesson/2.3/2.jpg)

由于老版本的浏览器不支持，因此很少有人使用事件捕获。我们也建议大家放心地使用事件冒泡，在有特殊需要时再使用事件捕获。

## 事件处理程序

事件就是用户或浏览器自身执行的某种动作。诸如 `click`、`load` 和 `mouseover`，都是事件的名字。而响应某个事件的函数就叫做**事件处理程序**（或**事件侦听器**）。事件处理程序的名字以 `"on"` 开头，因此 `click` 事件的事件处理程序就是 `onclick`，`load` 事件的事件处理程序就是 `onload`。为事件指定处理程序的方式有好几种。

### HTML 事件处理程序

某个元素支持的每种事件，都可以使用一个与相应事件处理程序同名的 HTML 特性来指定。这个特性的值应该是能够执行的 JavaScript 代码。例如，要在按钮被单击时执行一些 JavaScript，可以像下面这样编写代码：

```html
<input type="button" value="Click Me" onclick="console.log('Clicked')" />
```

当单击这个按钮时，就会在控制台打印 `"Clicked"`。这个操作是通过指定 `onclick` 特性并将一些 JavaScript 代码作为它的值来定义的。由于这个值是 JavaScript，因此不能在其中使用未经转义的 HTML 语法字符，例如和号（&）、双引号（""）、小于号（<）或大于号（>）。为了避免使用 HTML 实体，这里使用了单引号。如果想要使用双引号，那么就要将代码改写成如下所示：

```html
<input type="button" value="Click Me" onclick="console.log(&quot;Clicked&quot;)" />
```

在 HTML 中定义的事件处理程序可以包含要执行的具体动作，也可以调用在页面其他地方定义的脚本，如下面的例子所示：

```javascript
<script type="text/javascript">
    function showMessage(){
        console.log("Hello world!");
    }
</script>
<input type="button" value="Click Me" onclick="showMessage()" />
```

在这个例子中，单击按钮就会调用 `showMessage()` 函数。这个函数是在一个独立的 `<script>` 元素中定义的，当然也可以被包含在一个外部文件中。事件处理程序中的代码在执行时，有权访问全局作用域中的任何代码。

这样指定事件处理程序具有一些独到之处。首先，这样会创建一个封装着元素属性值的函数。这个函数中有一个局部变量 `event`，也就是事件对象：

```html
<!-- 输出 "click" -->
<input type="button" value="Click Me" onclick="console.log(event.type)">
```

通过 `event` 变量，可以直接访问事件对象，你不用自己定义它，也不用从函数的参数列表中读取。

在这个函数内部，`this` 值等于事件的目标元素，例如：

```html
<!-- 输出 "Click Me" -->
<input type="button" value="Click Me" onclick="console.log(this.value)">
```

如此一来，事件处理程序要访问自己的属性就简单多了。下面这行代码与前面的例子效果相同：

```html
<!-- 输出 "Click Me" -->
<input type="button" value="Click Me" onclick="console.log(value)">
```

不过，在 HTML 中指定事件处理程序有三个缺点。首先，存在一个时差问题。因为用户可能会在 HTML 元素一出现在页面上就触发相应的事件，但当时的事件处理程序有可能尚不具备执行条件。以前面的例子来说明，假设 `showMessage()` 函数是在按钮下方、页面的最底部定义的。如果用户在页面解析 `showMessage()` 函数之前就单击了按钮，就会引发错误。为此，很多HTML事件处理程序都会被封装在一个 `try-catch` 块中，以便错误不会浮出水面，如下面的例子所示：

```html
<input type="button" value="Click Me" onclick="try{showMessage();}catch(ex){}">
```

这样，如果在 `showMessage()` 函数有定义之前单击了按钮，用户将不会看到 JavaScript 错误，因为在浏览器有机会处理错误之前，错误就被捕获了。

第二个缺点是，这样扩展事件处理程序的作用域链在不同浏览器中会导致不同结果。不同 JavaScript 引擎遵循的标识符解析规则略有差异，很可能会在访问非限定对象成员时出错。

第三个缺点是，HTML 与 JavaScript 代码紧密耦合。如果要更换事件处理程序，就要改动两个地方：HTML 代码和 JavaScript 代码。而这正是许多开发人员摒弃 HTML 事件处理程序，转而使用 JavaScript 指定事件处理程序的原因所在。

### DOM1 级事件处理程序

通过 JavaScript 指定事件处理程序的传统方式，就是将一个函数赋值给一个事件处理程序属性。这种为事件处理程序赋值的方法是在第四代Web浏览器中出现的，而且至今仍然为所有现代浏览器所支持。原因一是简单，二是具有跨浏览器的优势。要使用 JavaScript 指定事件处理程序，首先必须取得一个要操作的对象的引用。

每个元素（包括 `window` 和 `document`）都有自己的事件处理程序属性，这些属性通常全部小写，例如 `onclick`。将这种属性的值设置为一个函数，就可以指定事件处理程序，如下所示：

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    console.log("Clicked");
};
```

在此，我们通过文档对象取得了一个按钮的引用，然后为它指定了 `onclick` 事件处理程序。但要注意，在这些代码运行以前不会指定事件处理程序，因此如果这些代码在页面中位于按钮后面，就有可能在一段时间内怎么单击都没有反应。

使用 DOM1 级方法指定的事件处理程序被认为是元素的方法。因此，这时候的事件处理程序是在元素的作用域中运行；换句话说，程序中的 `this` 引用当前元素。来看一个例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    console.log(this.id);    // "myBtn"
};
```

单击按钮显示的是元素的 ID，这个 ID 是通过 `this.id` 取得的。不仅仅是 ID，实际上可以在事件处理程序中通过 `this` 访问元素的任何属性和方法。以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理。

也可以删除通过 DOM1 级方法指定的事件处理程序，只要像下面这样将事件处理程序属性的值设置为 `null` 即可：

```javascript
btn.onclick = null;     // 删除事件处理程序
```

将事件处理程序设置为 `null` 之后，再单击按钮将不会有任何动作发生。

### DOM2 级事件处理程序

DOM2 级事件定义了两个方法，用于处理指定和删除事件处理程序的操作：`addEventListener()` 和 `removeEventListener()`。所有 DOM 节点中都包含这两个方法，并且它们都接受3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是 `true`，表示在捕获阶段调用事件处理程序；如果是 `false`，表示在冒泡阶段调用事件处理程序。

要在按钮上为 `click` 事件添加事件处理程序，可以使用下列代码：

```javascript
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
    console.log(this.id);
}, false);
```

上面的代码为一个按钮添加了 `onclick` 事件处理程序，而且该事件会在冒泡阶段被触发（因为最后一个参数是 `false`）。与 DOM1 级方法一样，这里添加的事件处理程序也是在其依附的元素的作用域中运行。使用 DOM2 级方法添加事件处理程序的主要好处是可以添加多个事件处理程序。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
    console.log(this.id);
}, false);
btn.addEventListener("click", function(){
    console.log("Hello world!");
}, false);
```

这里为按钮添加了两个事件处理程序。这两个事件处理程序会按照添加它们的顺序触发，因此首先会显示元素的 ID，其次会显示 `"Hello world!"` 消息。

通过 `addEventListener()` 添加的事件处理程序只能使用 `removeEventListener()` 来移除；移除时传入的参数与添加处理程序时使用的参数相同。这也意味着通过 `addEventListener()` 添加的匿名函数将无法移除，如下面的例子所示。

```javascript
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
    console.log(this.id);
}, false);
btn.removeEventListener("click", function(){ // 没有用！
    console.log(this.id);
}, false);
```

在这个例子中，我们使用 `addEventListener()` 添加了一个事件处理程序。虽然调用 `removeEventListener()` 时看似使用了相同的参数，但实际上，第二个参数与传入 `addEventListener()` 中的那一个是完全不同的函数。而传入 `removeEventListener()` 中的事件处理程序函数必须与传 入`addEventListener()` 中的相同，如下面的例子所示。

```javascript
var btn = document.getElementById("myBtn");
var handler = function(){
    console.log(this.id);
};
btn.addEventListener("click", handler, false);
btn.removeEventListener("click", handler, false); // 有效！
```

重写后的这个例子没有问题，是因为在 `addEventListener()` 和 `removeEventListener()` 中使用了相同的函数。

大多数情况下，都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度地兼容各种浏览器。最好只在需要在事件到达目标之前截获它的时候将事件处理程序添加到捕获阶段。如果不是特别需要，我们不建议在事件捕获阶段注册事件处理程序。

> IE9、Firefox、Safari、Chrome 和 Opera 支持 DOM2 级事件处理程序。

### IE 事件处理程序

IE 实现了与 DOM 中类似的两个方法：`attachEvent()` 和 `detachEvent()`。这两个方法接受相同的两个参数：事件处理程序名称与事件处理程序函数。由于 IE8 及更早版本只支持事件冒泡，所以通过 `attachEvent()` 添加的事件处理程序都会被添加到冒泡阶段。

要使用 `attachEvent()` 为按钮添加一个事件处理程序，可以使用以下代码。

```javascript
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
    console.log("Clicked");
});
```

注意，`attachEvent()` 的第一个参数是 `"onclick"`，而非 DOM 的 `addEventListener()` 方法中的 `"click"`。

在 IE 中使用 `attachEvent()` 与使用 DOM1 级方法的主要区别在于事件处理程序的作用域。在使用 DOM1 级方法的情况下，事件处理程序会在其所属元素的作用域内运行；在使用 `attachEvent()` 方法的情况下，事件处理程序会在全局作用域中运行，因此 `this` 等于 `window`。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
    console.log(this === window);    // true
});
```

在编写跨浏览器的代码时，牢记这一区别非常重要。

与 `addEventListener()` 类似，`attachEvent()` 方法也可以用来为一个元素添加多个事件处理程序。不过，与 DOM 方法不同的是，这些事件处理程序不是以添加它们的顺序执行，而是以相反的顺序被触发。

使用 `attachEvent()` 添加的事件可以通过 `detachEvent()` 来移除，条件是必须提供相同的参数。与 DOM 方法一样，这也意味着添加的匿名函数将不能被移除。不过，只要能够将对相同函数的引用传给 `detachEvent()`，就可以移除相应的事件处理程序。

> 支持 IE 事件处理程序的浏览器有 IE 和 Opera。

### 跨浏览器的事件处理程序

为了以跨浏览器的方式处理事件，不少开发人员会使用能够隔离浏览器差异的 JavaScript 库，还有一些开发人员会自己开发最合适的事件处理的方法。自己编写代码其实也不难，只要恰当地使用能力检测即可。要保证处理事件的代码能在大多数浏览器下一致地运行，只需关注冒泡阶段。

第一个要创建的方法是 `addHandler()`，它的职责是视情况分别使用 DOM1 级方法、DOM2 级方法或 IE 方法来添加事件。这个方法属于一个名叫 `EventUtil` 的对象，本书将使用这个对象来处理浏览器间的差异。`addHandler()` 方法接受3个参数：要操作的元素、事件名称和事件处理程序函数。

与 `addHandler()` 对应的方法是 `removeHandler()`，它也接受相同的参数。这个方法的职责是移除之前添加的事件处理程序——无论该事件处理程序是采取什么方式添加到元素中的，如果其他方法无效，默认采用 DOM1 级方法。

`EventUtil` 的用法如下所示。

```javascript
var EventUtil = {
    addHandler: function(element, type, handler){
        if (element.addEventListener){
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent){
            element.attachEvent("on" + type, handler);
        } else {
            element["on" + type] = handler;
        }
    },
    removeHandler: function(element, type, handler){
        if (element.removeEventListener){
            element.removeEventListener(type, handler, false);
        } else if (element.detachEvent){
            element.detachEvent("on" + type, handler);
        } else {
            element["on" + type] = null;
        }
    }
};
```

这两个方法首先都会检测传入的元素中是否存在 DOM2 级方法。如果存在 DOM2 级方法，则使用该方法：传入事件类型、事件处理程序函数和第三个参数 `false`（表示冒泡阶段）。如果存在的是 IE 的方法，则采取第二种方案。注意，为了在 IE8 及更早版本中运行，此时的事件类型必须加上 `"on"` 前缀。最后一种可能就是使用 DOM1 级方法（在现代浏览器中，应该不会执行这里的代码）。此时，我们使用的是方括号语法来将属性名指定为事件处理程序，或者将属性设置为 `null`。

可以像下面这样使用 `EventUtil` 对象：

```javascript
var btn = document.getElementById("myBtn");
var handler = function(){
    console.log("Clicked");
};
EventUtil.addHandler(btn, "click", handler);
EventUtil.removeHandler(btn, "click", handler);
```

`addHandler()` 和 `removeHandler()` 没有考虑到所有的浏览器问题，例如在 IE 中的作用域问题。不过，使用它们添加和移除事件处理程序还是足够了。

## 事件对象

在触发 DOM 上的某个事件时，会产生一个事件对象 `event`，这个对象中包含着所有与事件有关的信息。包括导致事件的元素、事件的类型以及其他与特定事件相关的信息。例如，鼠标操作导致的事件对象中，会包含鼠标位置的信息，而键盘操作导致的事件对象中，会包含与按下的键有关的信息。所有浏览器都支持 `event` 对象，但支持方式不同。

### DOM 中的事件对象

兼容 DOM 的浏览器会将一个 `event` 对象传入到事件处理程序中。无论指定事件处理程序时使用什么方法（DOM1 级或 DOM2 级），都会传入 `event` 对象。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
    console.log(event.type);     // "click"
};
btn.addEventListener("click", function(event){
    console.log(event.type);     // "click"
}, false);
```

这个例子中的两个事件处理程序都会弹出一个警告框，显示由 `event.type` 属性表示的事件类型。这个属性始终都会包含被触发的事件类型，例如 `"click"`（与传入 `addEventListener()` 和 `removeEventListener()` 中的事件类型一致）。

在通过 HTML 特性指定事件处理程序时，变量 `event` 中保存着 `event` 对象。请看下面的例子。

```html
<input type="button" value="Click Me" onclick="console.log(event.type)"/>
```

以这种方式提供 `event` 对象，可以让 HTML 特性事件处理程序与 JavaScript 函数执行相同的操作。

`event` 对象包含与创建它的特定事件有关的属性和方法。触发的事件类型不一样，可用的属性和方法也不一样。不过，所有事件都会有下表列出的成员。

- `bubbles`，表明事件是否冒泡。
- `cancelable`，表明是否可以取消事件的默认行为。
- `currentTarget`，其事件处理程序当前正在处理事件的那个元素。
- `defaultPrevented`，为 `true` 表示已经调用了 `preventDefault()`（DOM3 级事件中新增）。
- `detail`，与事件相关的细节信息。
- `eventPhase`，调用事件处理程序的阶段：1表示捕获阶段，2表示“处于目标”，3表示冒泡阶段。
- `preventDefault()`，取消事件的默认行为。如果 `cancelable` 是 `true`，则可以使用这个方法。
- `stopImmediatePropagation()`，取消事件的进一步捕获或冒泡，同时阻止任何事件处理程序被调用（DOM3 级事件中新增）。
- `stopPropagation()`，取消事件的进一步捕获或冒泡。如果 `bubbles` 为 `true`，则可以使用这个方法。
- `target`，事件的目标。
- `trusted`，为 `true` 表示事件是浏览器生成的。为 `false` 表示事件是由开发人员通过 JavaScript 创建的（DOM3 级事件中新增）。
- `type`，被触发的事件的类型。
- `view`，与事件关联的抽象视图，等同于发生事件的 `window` 对象。

在事件处理程序内部，对象 `this` 始终等于 `currentTarget` 的值，而 `target` 则只包含事件的实际目标。如果直接将事件处理程序指定给了目标元素，则 `this`、`currentTarget` 和 `target` 包含相同的值。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
    console.log(event.currentTarget === this);    // true
    console.log(event.target === this);           // true
};
```

这个例子检测了 `currentTarget` 和 `target` 与 `this` 的值。由于 `click` 事件的目标是按钮，因此这三个值是相等的。如果事件处理程序存在于按钮的父节点中（例如 `document.body`），那么这些值是不相同的。再看下面的例子。

```javascript
document.body.onclick = function(event){
    console.log(event.currentTarget === document.body);  // true
    console.log(this === document.body);                 // true
    console.log(event.target === document.getElementById("myBtn"));  // true
};
```

当单击这个例子中的按钮时，`this` 和 `currentTarget` 都等于`document.body`，因为事件处理程序是注册到这个元素上的。然而，`target` 元素却等于按钮元素，因为它是 `click` 事件真正的目标。由于按钮上并没有注册事件处理程序，结果 `click` 事件就冒泡到了 `document.body`，在那里事件才得到了处理。

在需要通过一个函数处理多个事件时，可以使用 `type` 属性。例如：

```javascript
var btn = document.getElementById("myBtn");
var handler = function(event){
    switch(event.type){
        case "click":
            console.log("Clicked");
            break;
        case "mouseover":
            event.target.style.backgroundColor = "red";
            break;
        case "mouseout":
            event.target.style.backgroundColor = "";
            break;
    }
};
btn.onclick = handler;
btn.onmouseover = handler;
btn.onmouseout = handler;
```

这个例子定义了一个名为 `handler` 的函数，用于处理3种事件：`click`、`mouseover` 和 `mouseout`。当单击按钮时，会出现一个与前面例子中一样的警告框。当按钮移动到按钮上面时，背景颜色应该会变成红色，而当鼠标移动出按钮的范围时，背景颜色应该会恢复为默认值。这里通过检测 `event.type` 属性，让函数能够确定发生了什么事件，并执行相应的操作。

要阻止特定事件的默认行为，可以使用 `preventDefault()` 方法。例如，链接的默认行为就是在被单击时会导航到其 `href` 特性指定的 URL。如果你想阻止链接导航这一默认行为，那么通过链接的 `onclick` 事件处理程序可以取消它，如下面的例子所示。

```javascript
var link = document.getElementById("myLink");
link.onclick = function(event){
    event.preventDefault();
};
```

只有 `cancelable` 属性设置为 `true` 的事件，才可以使用 `preventDefault()` 来取消其默认行为。

另外，`stopPropagation()` 方法用于立即停止事件在 DOM 层次中的传播，即取消进一步的事件捕获或冒泡。例如，直接添加到一个按钮的事件处理程序可以调用 `stopPropagation()`，从而避免触发注册在 `document.body` 上面的事件处理程序，如下面的例子所示。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
    console.log("Clicked");
    event.stopPropagation();
};
document.body.onclick = function(event){
    console.log("Body clicked");
};
```

对于这个例子而言，如果不调用 `stopPropagation()`，就会在单击按钮时出现两个警告框。可是，由于 `click` 事件根本不会传播到 `document.body`，因此就不会触发注册在这个元素上的 `onclick` 事件处理程序。

事件对象的 `eventPhase` 属性，可以用来确定事件当前正位于事件流的哪个阶段。如果是在捕获阶段调用的事件处理程序，那么 `eventPhase` 等于 `1`；如果事件处理程序处于目标对象上，则 `eventPhase` 等于 `2`；如果是在冒泡阶段调用的事件处理程序，`eventPhase` 等于 `3`。这里要注意的是，尽管“处于目标”发生在冒泡阶段，但 `eventPhase` 仍然一直等于 `2`。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
    console.log(event.eventPhase); // 2
};
document.body.addEventListener("click", function(event){
    console.log(event.eventPhase); // 1
}, true);
document.body.onclick = function(event){
    console.log(event.eventPhase); // 3
};
```

当单击这个例子中的按钮时，首先执行的事件处理程序是在捕获阶段触发的添加到 `document.body` 中的那一个，结果会弹出一个警告框显示表示 `eventPhase` 的 `1`。接着，会触发在按钮上注册的事件处理程序，此时的 `eventPhase` 值为 `2`。最后一个被触发的事件处理程序，是在冒泡阶段执行的添加到 `document.body` 上的那一个，显示 `eventPhase` 的值为 `3`。而当 `eventPhase` 等于 `2` 时，`this`、`target` 和 `currentTarget` 始终都是相等的。

> 只有在事件处理程序执行期间，**event**对象才会存在；一旦事件处理程序执行完成，**event**对象就会被销毁。

### IE 中的事件对象

与访问 DOM 中的 `event` 对象不同，要访问IE中的 `event` 对象有几种不同的方式，取决于指定事件处理程序的方法。在使用 DOM1 级方法添加事件处理程序时，`event` 对象作为 `window` 对象的一个属性存在。来看下面的例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    var event = window.event;
    console.log(event.type);     // "click"
};
```

在此，我们通过 `window.event` 取得了 `event` 对象，并检测了被触发事件的类型（IE 中的 `type` 属性与 DOM 中的 `type` 属性是相同的）。可是，如果事件处理程序是使用 `attachEvent()` 添加的，那么就会有一个 `event` 对象作为参数被传入事件处理程序函数中，如下所示。

```javascript
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(event){
    console.log(event.type);     // "click"
});
```

在像这样使用 `attachEvent()` 的情况下，也可以通过 `window` 对象来访问 `event` 对象，就像使用 DOM1 级方法时一样。不过为方便起见，同一个对象也会作为参数传递。

如果是通过 HTML 特性指定的事件处理程序，那么还可以通过一个名叫 `event` 的变量来访问 `event` 对象（与 DOM 中的事件模型相同）。再看一个例子。

```html
<input type="button" value="Click Me" onclick="console.log(event.type)">
```

IE 的 `event` 对象同样也包含与创建它的事件相关的属性和方法。其中很多属性和方法都有对应的或者相关的 DOM 属性和方法。与 DOM 的 `event` 对象一样，这些属性和方法也会因为事件类型的不同而不同，但所有事件对象都会包含下表所列的属性和方法。

- `cancelBubble`，默认值为 `false`，但将其设置为 `true` 就可以取消事件冒泡（与 DOM 中的 `stopPropagation()` 方法的作用相同）。
- `returnValue`，默认值为 `true`，但将其设置为 `false` 就可以取消事件的默认行为（与 DOM 中的 `preventDefault()` 方法的作用相同） 。
- `srcElement`，事件的目标（与 DOM 中的 `target` 属性相同） 。
- `type`，被触发的事件的类型 。

因为事件处理程序的作用域是根据指定它的方式来确定的，所以不能认为 `this` 会始终等于事件目标。故而，最好还是使用 `event.srcElement` 比较保险。例如：

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    console.log(window.event.srcElement === this);  // true
};
btn.attachEvent("onclick", function(event){
    console.log(event.srcElement === this);         // false
});
```

在第一个事件处理程序中（使用 DOM1 级方法指定的），`srcElement` 属性等于 `this`，但在第二个事件处理程序中，这两者的值不相同。

如前所述，`returnValue` 属性相当于 DOM 中的 `preventDefault()` 方法，它们的作用都是取消给定事件的默认行为。只要将 `returnValue` 设置为 `false`，就可以阻止默认行为。来看下面的例子。

```javascript
var link = document.getElementById("myLink");
link.onclick = function(){
    window.event.returnValue = false;
};
```

这个例子在 `onclick` 事件处理程序中使用 `returnValue` 达到了阻止链接默认行为的目的。与 DOM 不同的是，在此没有办法确定事件是否能被取消。

相应地，`cancelBubble` 属性与 DOM 中的 `stopPropagation()` 方法作用相同，都是用来停止事件冒泡的。由于IE不支持事件捕获，因而只能取消事件冒泡；但 `stopPropagatioin()` 可以同时取消事件捕获和冒泡。例如：

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    console.log("Clicked");
    window.event.cancelBubble = true;
};
document.body.onclick = function(){
    console.log("Body clicked");
};
```

通过在 `onclick` 事件处理程序中将 `cancelBubble` 设置为 `true`，就可阻止事件通过冒泡而触发 `document.body` 中注册的事件处理程序。结果，在单击按钮之后，只会显示一个警告框。

### 跨浏览器的事件对象

虽然 DOM 和 IE 中的 `event` 对象不同，但基于它们之间的相似性依旧可以拿出跨浏览器的方案来。IE中 `event` 对象的全部信息和方法 DOM 对象中都有，只不过实现方式不一样。不过，这种对应关系让实现两种事件模型之间的映射非常容易。可以对前面介绍的 `EventUtil` 对象加以增强，添加如下方法以求同存异。

```javascript
var EventUtil = {
    addHandler: function(element, type, handler){
        // 省略的代码
    },
    getEvent: function(event){
        return event ? event : window.event;
    },
    getTarget: function(event){
        return event.target || event.srcElement;
    },
    preventDefault: function(event){
        if (event.preventDefault){
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },
    removeHandler: function(element, type, handler){
        // 省略的代码
    },
    stopPropagation: function(event){
        if (event.stopPropagation){
            event.stopPropagation();
        } else {
            event.cancelBubble = true;
        }
    }
};
```

以上代码显示，我们为 `EventUtil` 添加了4个新方法。第一个是 `getEvent()`，它返回对 `event` 对象的引用。考虑到 IE 中事件对象的位置不同，可以使用这个方法来取得 `event` 对象，而不必担心指定事件处理程序的方式。在使用这个方法时，必须假设有一个事件对象传入到事件处理程序中，而且要把该变量传给这个方法，如下所示。

```javascript
btn.onclick = function(event){
    event = EventUtil.getEvent(event);
};
```

在兼容 DOM 的浏览器中，`event` 变量只是简单地传入和返回。而在 IE 中，`event` 参数是未定义的  `undefined`，因此就会返回 `window.event`。将这一行代码添加到事件处理程序的开头，就可以确保随时都能使用 `event` 对象，而不必担心用户使用的是什么浏览器。

第二个方法是 `getTarget()`，它返回事件的目标。在这个方法内部，会检测 `event` 对象的 `target` 属性，如果存在则返回该属性的值；否则，返回 `srcElement` 属性的值。可以像下面这样使用这个方法。

```javascript
btn.onclick = function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
};
```

第三个方法是 `preventDefault()`，用于取消事件的默认行为。在传入 `event` 对象后，这个方法会检查是否存在 `preventDefault()` 方法，如果存在则调用该方法。如果 `preventDefault()` 方法不存在，则将 `returnValue` 设置为 `false`。下面是使用这个方法的例子。

```javascript
var link = document.getElementById("myLink");
link.onclick = function(event){
    event = EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
};
```

以上代码可以确保在所有浏览器中单击该链接都不会打开另一个页面。首先，使用 `EventUtil.getEvent()` 取得 `event` 对象，然后将其传入到 `EventUtil.preventDefault()` 以取消默认行为。

第四个方法是 `stopPropagation()`，其实现方式类似。首先尝试使用DOM方法阻止事件流，否则就使用 `cancelBubble` 属性。下面看一个例子。

```javascript
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
    console.log("Clicked");
    event = EventUtil.getEvent(event);
    EventUtil.stopPropagation(event);
};
document.body.onclick = function(event){
    console.log("Body clicked");
};
```

在此，首先使用 `EventUtil.getEvent()` 取得了 `event` 对象，然后又将其传入到 `EventUtil.stopPropagation()`。别忘了由于 IE 不支持事件捕获，因此这个方法在跨浏览器的情况下，也只能用来阻止事件冒泡。

## 事件类型

Web 浏览器中可能发生的事件有很多类型。如前所述，不同的事件类型具有不同的信息，而 DOM3 级事件规定了以下几类事件。

- UI（User Interface，用户界面）事件，当用户与页面上的元素交互时触发；
- 焦点事件，当元素获得或失去焦点时触发；
- 鼠标事件，当用户通过鼠标在页面上执行操作时触发；
- 滚轮事件，当使用鼠标滚轮（或类似设备）时触发；
- 文本事件，当在文档中输入文本时触发；
- 键盘事件，当用户通过键盘在页面上执行操作时触发；
- 合成事件，当为IME（Input Method Editor，输入法编辑器）输入字符时触发；
- 变动（mutation）事件，当底层 DOM 结构发生变化时触发。
- 变动名称事件，当元素或属性名变动时触发。此类事件已经被废弃，没有任何浏览器实现它们，因此本章不做介绍。

除了这几类事件之外，HTML5 也定义了一组事件，而有些浏览器还会在 DOM 和 BOM 中实现其他专有事件。这些专有的事件一般都是根据开发人员需求定制的，没有什么规范，因此不同浏览器的实现有可能不一致。

DOM3 级事件模块在 DOM2 级事件模块基础上重新定义了这些事件，也添加了一些新事件。包括 IE9 在内的所有主流浏览器都支持 DOM2 级事件。 IE9 也支持 DOM3 级事件。

> 想要了解更多 DOM 和 HTML5 事件，请参见最新版的 W3C 规范：  
> https://www.w3.org/TR/uievents/

## 小结

事件是将 JavaScript 与网页联系在一起的主要方式。DOM3 级事件规范和 HTML5 定义了常见的大多数事件。即使有规范定义了基本事件，但很多浏览器仍然在规范之外实现了自己的专有事件，从而为开发人员提供更多掌握用户交互的手段。有些专有事件与特定设备关联，例如移动 Safari 中的 `orientationchange` 事件就是特定关联 iOS 设备的。

在使用事件时，需要考虑如下一些内存与性能方面的问题。

- 有必要限制一个页面中事件处理程序的数量，数量太多会导致占用大量内存，而且也会让用户感觉页面反应不够灵敏。
- 建立在事件冒泡机制之上的事件委托技术，可以有效地减少事件处理程序的数量。
- 建议在浏览器卸载页面之前移除页面中的所有事件处理程序。

可以使用 JavaScript 在浏览器中模拟事件。DOM2 级事件和 DOM3 级事件规范规定了模拟事件的方法，为模拟各种有定义的事件提供了方便。此外，通过组合使用一些技术，还可以在某种程度上模拟键盘事件。IE8 及之前版本同样支持事件模拟，只不过模拟的过程有些差异。