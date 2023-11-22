## TypeScript简单介绍

TypeScript 是 JavaScript 的一个超集，支持 ECMAScript 6 标准（ES6 教程）。

TypeScript 由微软开发的自由和开源的编程语言。

TypeScript 设计目标是开发大型应用，它可以编译成纯 JavaScript，编译出来的 JavaScript 可以运行在任何浏览器上。

TypeScript 是一种给 JavaScript 添加特性的语言扩展。

**增加的功能包括：**

- 类型批注和编译时类型检查

- 类型推断
- 类型擦除
- 接口
- 枚举
- Mixin
- 泛型编程
- 名字空间
- 元组
- Await 

**从 ECMA 2015 反向移植而来：**

- 类

- 模块
- lambda 函数的箭头语法
- 可选参数以及默认参数



## TypeScript 与 JavaScript 的区别

TypeScript 是 JavaScript 的超集，扩展了 JavaScript 的语法，因此现有的 JavaScript 代码可与 TypeScript 一起工作无需任何修改，

TypeScript 通过**类型注解**提供编译时的**静态类型检查**。

TypeScript 可处理已有的 JavaScript 代码，并只对其中的 TypeScript 代码进行编译。

 **第一个TypeScript实例：**

```typescript
const greet : string = "Hello World!"
console.log(greet)
```

- **TypeScript 会忽略程序中出现的空格、制表符和换行符**。
- **TypeScript 区分大写和小写字符**。
- **分号在 TypeScript 中是可选的**，建议使用。
- **注释与JavaScript使用一致。**



## TypeScript基础类型

- **any（任意类型**）：声明为 any 的变量可以赋予任意类型的值。

> Any
>
> 任意值是 TypeScript 针对编程时类型不明确的变量使用的一种数据类型，
>
> 它常用于以下情况。
>
> 1、变量的值会动态改变时，比如来自用户的输入，任意值类型可以让这些变量跳过编译阶段的类型检查，示例代码如下：
>
> ```js
> let flag: any = 1;    // 数字类型
> flag = 'my name is leo';    // 字符串类型
> flag = true;    // 布尔类型
> ```
>
> 2、定义存储各种类型数据的数组时，示例代码如下：
>
> ```js
> let list: any[] = ['leo',25,true];
> list[1] = 'lion';
> ```

- **number（数字类型）**：双精度 64 位浮点值。它可以用来表示整数和分数。
- **string（字符串类型）**：一个字符系列，使用单引号（'）或双引号（"）来表示字符串类型。反引号（`）来定义多行文本和内嵌表达式。
- **boolean（布尔类型）**：表示逻辑值：true 和 false。
- **数组类型、元组**。

​					*元组可以属于理解成一个任意类型并且长度有限的数组*

- **enum（枚举类型）**：枚举类型用于定义数值集合。
- **void**：用于标识方法返回值的类型，表示该方法没有返回值。
- **null**：表示对象值缺失。
- **undefined**：用于初始化变量为一个未定义的值。

> **null，在 JavaScript 中 null 表示 "什么都没有"。**
>
> null是一个只有一个值的特殊类型。
>
> 表示一个空对象引用。
>
> 用 typeof 检测 null 返回是 object。
>
> **undefined，在 JavaScript 中, undefined 是一个没有设置值的变量。**
>
> typeof 一个没有值的变量会返回 undefined。
>
> Null 和 Undefined 是其他任何类型（包括 void）的子类型，可以赋值给其它类型，即其他类型可以转成这两种类型，如字符串类型，
>
> 此时，赋值后的类型会变成 null 或 undefined。
>
> ```
> let num: number;
> num = 1; // 运行正确
> num = undefined;    // 运行正确，此时为undefined类型
> num = null;    // 运行正确，此时为null类型
> ```

- **never**：never 是其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。

> never 是其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。
>
> 这意味着声明为 never 类型的变量只能被 never 类型所赋值，在函数中它通常表现为抛出异常或无法执行到终止点（例如无限循环），示例代码如下：
>
> ```
> let n: never;
> let num: number;
> 
> // 运行错误，数字类型不能转为never类型
> n = 123;
> 
> // 运行正确，never 类型可以赋值给never类型
> n = (()=>{ throw new Error('exception')})();
> 
> // 运行正确，never 类型可以赋值给数字类型
> num = (()=>{ throw new Error('exception')})();
> 
> // 返回值为never的函数可以是抛出异常的情况
> function error(message: string): never {
>     throw new Error(message);
> }
> 
> // 返回值为never的函数可以是无法被执行到的终止点的情况
> function loop(): never {
>     while (true) {}
> }
> ```





## TypeScript变量声明

#### TypeScript 变量的命名规则：

1、变量名称可以包含数字和字母。

2、除了下划线 _ 和美元 $ 符号外，不能包含其他特殊字符，包括空格。

3、变量名不能以数字开头。

**以下为四种声明变量的方式**

```js
//var [变量名] : [类型] = 值; 声明变量的类型及初始值
var uname:string = "leo";

//var [变量名] : [类型]; 声明变量的类型，但没有初始值，变量值会设置为undefined
var uname:string;

//var [变量名] = 值; 声明变量并初始值，但不设置类型，该变量可以是任意类型
var uname = "leo";

//var [变量名]; 声明变量没有设置类型和初始值，类型可以是任意类型，默认初始值为undefined
var uname;

//总结：声明时，没有类型，类型就是any；没有初始值，初始值就是undefined
```

**实例：**

```js
var uname:string = "leo";
var age:number = 25;

//对应js
var uname = "leo";
var age = 25;
```



**TypeScript 遵循强类型，如果将不同的类型赋值给变量会编译错误**，而JavaScript则不会，因为她是弱类型语言，

如下实例：

```typescript
var num:number = "leo"     // 编译错误

//对应的js
var num = 100
num = "leo"     // 编译不报错
```

#### **类型推断**

当类型没有给出时，TypeScript 编译器利用类型推断来推断类型。

如果由于缺乏声明而不能推断出类型，那么它的类型被视作默认的动态 any 类型。

```typescript
var num = 100;    // 类型推断为 number
num = "leo";      // 编译错误，相当于上例 var num:number = "leo"
```

#### 变量作用域

**TypeScript 有以下几种作用域：**

1. **全局作用域** − 全局变量定义在程序结构的外部，它可以在你代码的任何位置使用。

2. **类作用域** − 这个变量也可以称为 字段。

   类变量声明在一个类里头，但在类的方法外面。 

   该变量可以通过类的对象来访问。

   类变量也可以是静态的，静态的变量可以通过类名直接访问。

3. **局部作用域** − 局部变量，局部变量只能在声明它的一个代码块（如：方法）中使用。

如以下例子：

```typescript
var global_num = 10          // 全局变量
class Person { 
   age = 18;                 // 实例变量
   static score = 100;       // 静态变量
   eat():void { 
      var food = 'apple';    // 局部变量
   } 
}

console.log("全局变量为: " + global_num)  
console.log(Person.score)    // 静态变量，直接通过类名访问
var person = new Person(); 
console.log("实例变量: " + person.age)
```

#### TypeScript的运算符、条件语句、循环与JavaScript基本一致。

#### TypeScript函数

```typescript
function function_name()
{
    // 执行代码
}

//调用函数
function_name()
```

#### TypeScript函数返回值 

TypeScript的函数返回值与JavaScript的函数返回值略有不同。

**TypeScript的函数返回值的格式：**

```typescript
function function_name():return_type { 
    // 语句
    return value; 
}

//与js相比，ts的函数返回值需要指定 return_type返回值的类型。
//ts
function greet():string { // 返回一个字符串
    return "Hello World！" 
}

//js
function greet() {
    return "Hello World！" 
}
```



#### TypeScript带参数函数

```typescript
语法格式如下所示：

function func_name( param1 [:datatype], param2 [:datatype]) {   //datatype为参数类型
     //执行代码  
}
实例：

//ts
function add(x: number, y: number): number {  //函数返回值为number，参数的数据类型也为number
    return x + y;
}

//js
function add(x, y) {
    return x + y;
}
```

#### 可选参数和默认参数

```typescript
可选参数，在 TypeScript 函数里，如果我们定义了几个参数，则我们必须传入几个参数，除非将这些参数设置为可选，可选参数使用问号标识 ？。

function fullName(firstName: string, lastName: string) {  //调用函数必须传入两个参数，否则报错
    return firstName + " " + lastName;
}

let name1 = buildName("leo");                  // 错误，缺少参数
let name2 = buildName("leo", "lion", "gao");   // 错误，参数太多了
let name3 = buildName("leo", "lion");          // 正确
```

修改为可选参数之后:

```typescript
function fullName(firstName: string, lastName?: string) { //此时lastName为可选参数，非必传
    if(lastName){
        return firstName + " " + lastName;
    }else {
        return firstName;
    }

}

let name1 = buildName("leo");                  // 正确
let name2 = buildName("leo", "lion", "gao");   // 错误，参数太多了
let name3 = buildName("leo", "lion");          // 正确

//ts函数设置可选参数时，只能少传，不能多传，相比之下，js函数的参数可以多传，按顺序取参数。
默认参数，可以设置参数的默认值，这样在调用函数的时候，如果不传入该参数的值，则使用默认参数，语法格式为：

function function_name(param1[:type],param2[:type] = default_value) {
      //执行代码
}

//default_value为默认值，当不传入该参数时，取默认值。
注意：参数不能同时设置为可选和默认。 
以下实例函数的参数lastName设置了默认值为'lion'，调用该函数时如果未传入参数则使用该默认值：

function fullName(firstName:string,lastName:string = 'lion') {  
    console.log(firstName + " " + lastName); 
}

fullName('leo')         //leo lion，lastName取默认值
fullName('leo','gao')   //leo gao

//剩余参数

有一种情况，我们不知道要向函数传入多少个参数，这时候我们就可以使用剩余参数来定义。剩余参数语法允许我们将一个不确定数量的参数作为一个数组传入。

function fullName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}

let uname = fullName("leo", "lion", "ggj", "gao");
```

#### 匿名函数

```typescript
// 匿名函数是一个没有函数名的函数。
// 匿名函数在程序运行时动态声明，除了没有函数名外，其他的与标准函数一样。
// 我们可以将匿名函数赋值给一个变量，这种表达式就成为函数表达式。

var greet = function() {  //不带参数的匿名函数
    return "hello world！";  
} 
console.log(msg())


var add = function(a,b) {  //带参数的匿名函数
    return a + b;  
} 
console.log(add(2,3))

//匿名函数自调用
(function () { 
    var str = "Hello World！";   
    console.log(str)     
 })()
```

#### 构造函数

TypeScript 也支持使用 JavaScript 内置的构造函数 Function() 来定义函数：

```typescript
var res = new Function ([arg1[, arg2[, ...argN]],] functionBody)
var myFunction = new Function("a", "b", "return a * b"); 
var x = myFunction(4, 3); 
console.log(x);
```

#### 箭头函数

( [param1, parma2,…param n] )=>statement;
var add = (x:number)=> {    
    x = 10 + x 
    console.log(x)  
} 
foo(100)
我们可以不指定函数的参数类型，通过函数内来推断参数类型：

var func = (x)=> { 
    if(typeof x=="number") { 
        console.log(x+" 是一个数字") 
    } else if(typeof x=="string") { 
        console.log(x+" 是一个字符串") 
    }  
} 
func(12) 
func("Tom")
 更多例子

var display = x => {      //单个参数 () 是可选的
    console.log("输出为 "+x) 
} 
display(12)


var disp =()=> {     //无参数时可以设置空括号
    console.log("Function invoked"); 
} 
disp();
函数重载

重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

//参数类型与参数数量不同
function disp(s1:string):void; 
function disp(n1:number,s1:string):void; 

function disp(x:any,y?:any):void { 
    console.log(x); 
    console.log(y); 
}
TypeScript中的Number、String、Array（数组）类型语JavaScript基本一致。

TypeScript Map对象
Map 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者原始值) 都可以作为一个键或一个值。Map 是 ES6 中引入的一种新的数据结构，可以参考 ES6 Map 与 Set。

TypeScript 使用 Map 类型和 new 关键字来创建 Map：

let myMap = new Map();
初始化 Map，可以以数组的格式来传入键值对：

let myMap = new Map([
    ["key1", "value1"],
    ["key2", "value2"]
]); 


let nameSiteMapping = new Map();

// 设置 Map 对象
nameSiteMapping.set("Google", 1);
nameSiteMapping.set("Runoob", 2);
nameSiteMapping.set("Taobao", 3);

// 获取键对应的值
console.log(nameSiteMapping.get("Runoob"));     // 2

// 判断 Map 中是否包含键对应的值
console.log(nameSiteMapping.has("Taobao"));       // true
console.log(nameSiteMapping.has("Zhihu"));        // false

// 返回 Map 对象键/值对的数量
console.log(nameSiteMapping.size);                // 3

// 删除 Runoob
console.log(nameSiteMapping.delete("Runoob"));    // true
console.log(nameSiteMapping);
// 移除 Map 对象的所有键/值对
nameSiteMapping.clear();             // 清除 Map
console.log(nameSiteMapping);
使用for...of来迭代Map对象。

let nameSiteMapping = new Map();

nameSiteMapping.set("Google", 1);
nameSiteMapping.set("Runoob", 2);
nameSiteMapping.set("Taobao", 3);

// 迭代 Map 中的 key
for (let key of nameSiteMapping.keys()) {
    console.log(key);                  
}

// 迭代 Map 中的 value
for (let value of nameSiteMapping.values()) {
    console.log(value);                 
}

// 迭代 Map 中的 key => value
for (let entry of nameSiteMapping.entries()) {
    console.log(entry[0], entry[1]);   
}
TypeScript元组
我们知道数组中元素的数据类型都一般是相同的（any[] 类型的数组可以不同），如果存储的元素数据类型不同，则需要使用元组。元组中允许存储不同类型的元素，元组可以作为参数传递给函数。

创建元组的语法格式如下：

var tuple_name = [value1,value2,value3,…value n]
实例

//声明一个元组并初始化
var mytuple = [10,'leo',25,true];


//也可以先声明一个空元组，然后再初始化
var mytuple = []; 
mytuple[0] = 10
mytuple[1] = 'leo'
mytuple[2] = 25
mytuple[3] = true


//访问元组，使用索引来访问
tuple_name[index]
元组运算

1、push() 向元组添加元素，添加在最后面。

2、pop() 从元组中移除元素（最后一个），并返回移除的元素。

var mytuple = [10,"Hello","World","typeScript"];

mytuple.push(25)  // [10,"Hello","World","typeScript",25]

mytuple.pop()  // [10,"Hello","World","typeScript"]
更新元组

元组是可变的，这意味着我们可以对元组进行更新操作：、

var mytuple = [10, "leo", "lion"]; // 创建一个元组

// 更新元组元素
mytuple[0] = 25     // [25, "leo", "lion"]
解构元组

我们也可以把元组元素赋值给变量，如下所示：

var user =[25,"leo"] 
var [age,uname] = user
console.log( age )       // 25
console.log( uname )     // 'leo'
TypeScript联合类型
联合类型（Union Types）可以通过管道(|)将变量设置多种类型，赋值时可以根据设置的类型来赋值。

注意：只能赋值指定的类型，如果赋值其它类型就会报错。

Type1|Type2|Type3
实例

//声明一个联合类型
var flag:string|number|boolean

flag = 25
console.log("数字为 ", flag)   // 数字为 25

flag = 'leo' 
console.log("字符串为 ", flag)   // 字符串为 leo

flag = true 
console.log("布尔值为 ", flag)   //布尔值为 true
如果赋值其它类型就会报错：

var flag:string|number

flag = true  //报错，联合类型不包括boolean
也可以将联合类型作为函数参数使用：

function fullName(name:string|string[]) {  //此时参数类型可以是字符串，也可以是字符串数组
    if(typeof name == "string") { 
        console.log(name) 
    } else {
        var i; 
        for(i = 0;i<name.length;i++) { 
        console.log(name[i])
        } 
    } 
}

fullName("leo")
fullName(["leo","lion","ggj","gao"])
也可以将数组声明为联合类型：

var arr:number[]|string[];  //数字数组或者字符串数组
TypeScript接口
接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

TypeScript 接口定义如下：

interface interface_name {

}
实例

以下实例中，我们定义了一个接口 IPerson，接着定义了一个变量 customer，它的类型是 IPerson。customer 实现了接口 IPerson 的属性和方法。

interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string 
} 

//实现接口
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"} 
}

//实现接口
var employee:IPerson = { 
    firstName:"Jim",
    lastName:"Blakes", 
    sayHi: ():string =>{return "Hello!!!"} 
}

联合类型和接口

以下实例演示了如何在接口中使用联合类型：

interface RunOptions { 
    program:string; 
    commandline:string[]|string|(()=>string); 
} 

// commandline 是字符串
var options:RunOptions = {program:"test1",commandline:"Hello"}; 
console.log(options.commandline)  

// commandline 是字符串数组
options = {program:"test1",commandline:["Hello","World"]}; 
console.log(options.commandline[0]); 
console.log(options.commandline[1]);
接口继承

接口继承就是说接口可以通过其他接口来扩展自己。Typescript 允许接口继承多个接口。继承使用关键字 extends。

//单接口继承
Child_interface_name extends super_interface_name

//多接口继承，继承的各个接口使用逗号 , 分隔。
Child_interface_name extends super_interface1_name, super_interface2_name,…,super_interfaceN_name
单实例继承 

interface Person { 
   age:number 
} 

interface Musician extends Person { 
   instrument:string 
} 

var drummer = <Musician>{}; 
drummer.age = 25 
drummer.instrument = "Drums" 
console.log("年龄:  "+drummer.age)
console.log("喜欢的乐器:  "+drummer.instrument)

// 年龄:  25
// 喜欢的乐器:  Drums
多实例继承

interface IParent1 { 
    v1:number 
} 

interface IParent2 { 
    v2:number 
} 

interface Child extends IParent1, IParent2 { } 
var Iobj:Child = { v1:12, v2:23} 
TypeScript类
TypeScript 是面向对象的 JavaScript。类描述了所创建的对象共同的属性和方法。TypeScript 支持面向对象的所有特性，比如 类、接口等。

TypeScript 类定义方式如下：

class class_name { 
    // 类作用域
}
定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：

1、字段 − 字段是类里面声明的变量。字段表示对象的有关数据。

2、构造函数 − 类实例化时调用，可以为类的对象分配内存。

3、方法 − 方法为对象要执行的操作。

实例，创建类的数据成员：

class Car { 
    // 字段 
    color:string; 

```
// 构造函数 
constructor(color:string) { 
    this.color = color
}  
 
// 方法 
show():void {
    console.log("颜色为 :   " + this.color) 
} 
```
}
我们使用 new 关键字来实例化类的对象，类实例化时会调用构造函数，例如：

var obj = new Car("blue")
类中的字段属性和方法可以使用 . 号来访问：

// 访问属性
obj.color 

// 访问方法
obj.show()
类的继承

TypeScript 支持继承类，即我们可以在创建类的时候继承一个已存在的类，这个已存在的类称为父类，继承它的类称为子类。类继承使用关键字 extends，子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他的都可以继承。TypeScript 一次只能继承一个类，不支持继承多个类，但 TypeScript 支持多重继承（A 继承 B，B 继承 C）。

实例

类的继承：实例中创建了 Shape 类，Circle 类继承了 Shape 类，Circle 类可以直接使用 Area 属性：

class Shape { 
   Area:number 

   constructor(a:number) { 
      this.Area = a 
   } 
} 

class Circle extends Shape { 
   show():void { 
      console.log("圆的面积:  "+this.Area) 
   } 
}

var obj = new Circle(223); 
obj.show()        // 圆的面积:  223
需要注意的是子类只能继承一个父类，TypeScript 不支持继承多个类，但支持多重继承，如下实例：

class Root { 
   str:string; 
} 

class Child extends Root {} 
class Leaf extends Child {} // 多重继承，继承了 Child 和 Root 类
继承类的方法重写

类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写。其中 super 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。

class PrinterClass { 
   doPrint():void {
      console.log("父类的 doPrint() 方法。") 
   } 
} 

class StringPrinter extends PrinterClass { 
   doPrint():void { 
      super.doPrint() // 调用父类的函数
      console.log("子类的 doPrint()方法。")   //此处对父类方法进行重写
   } 
}
static关键字

上面提到，static 关键字用于定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用。

class StaticMem {  
   static num:number; 

   static disp():void { 
      console.log("num 值为 "+ StaticMem.num) 
   } 
} 

//直接通过类名调用静态属性和方法
StaticMem.num = 12     // 初始化静态变量
StaticMem.disp()       // 调用静态方法
扩展：instanceof 运算符用于判断对象是否是指定的类型，如果是返回 true，否则返回 false。

class Person { } 
var obj = new Person() 
var isPerson = obj instanceof Person;    //true
访问控制修饰符

TypeScript 中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。TypeScript 支持 3 种不同的访问权限。

1、public（默认） : 公有，可以在任何地方被访问。

2、protected : 受保护，可以被其自身以及其子类和父类访问。

3、private : 私有，只能被其定义所在的类访问。

以下实例定义了两个变量 str1 和 str2，str1 为 public，str2 为 private，实例化后可以访问 str1，如果要访问 str2 则会编译错误。

class Encapsulate { 
   str1:string = "Hello" 
   private str2:string = "World"
}

var obj = new Encapsulate() 
console.log(obj.str1)     // 可访问 
console.log(obj.str2)   // 编译错误， str2 是私有属性
类和接口

类可以实现接口，使用关键字 implements，并将 interest 字段作为类的属性使用。

以下实例红 AgriLoan 类实现了 ILoan 接口：

interface ILoan { 
   interest:number 
} 

class AgriLoan implements ILoan { 
   interest:number 
   rebate:number 

   constructor(interest:number,rebate:number) { 
      this.interest = interest 
      this.rebate = rebate 
   } 
} 

var obj = new AgriLoan(10,1) 
console.log("利润为 : "+obj.interest+"，抽成为 : "+obj.rebate )   // 利润为 : 10，抽成为 : 1
TypeScript与JavaScript中的对象基本一致。

TypeScript命名空间
命名空间一个最明确的目的就是解决重名问题。命名空间定义了标识符的可见范围，一个标识符可在多个名字空间中定义，它在不同名字空间中的含义是互不相干的。这样，在一个新的名字空间中可定义任何标识符，它们不会与任何已有的标识符发生冲突，因为已有的定义都处于其他名字空间中。

TypeScript 中命名空间使用 namespace 来定义，语法格式如下：

namespace SomeNameSpaceName { 
   export interface ISomeInterfaceName {      }  
   export class SomeClassName {      }  
}
以上定义了一个命名空间 SomeNameSpaceName，如果我们需要在外部可以调用 SomeNameSpaceName 中的类和接口，则需要在类和接口添加 export 关键字。

要在另外一个命名空间调用语法格式为：

SomeNameSpaceName.SomeClassName;
总结：以上为TypeScript的基础知识，可以看出TypeScript与JavaScript其中一些区别

1、TypeScript是JavaScript的超集，即你可以TypeScript在中使用原生JavaScript语法。

2、TypeScript是静态类语言（强类型），编译时进行类型检查；而JavaScript是动态类语言（弱类型）在运行时进行类型判断，相对更灵活。

3、TypeScript在JavaScript基础类型上，增加了void、never、any、元组、枚举、以及一些高级类型，还有类、接口、命名空间与更多面向对象的内容等。

4、JavaScript没有重载概念，TypeScript可以重载。

5、TypeScript最终仍要编译为弱类型，基于对象的原生的JavaScript，再运行。

