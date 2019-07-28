# 《javascript 语言精粹》

#  原型

- 每个对象都链接到一个原型对象，并且它可以从中继承属性。

- 当创建一个对象的时候，可以选择某个对象作为它的原型




 # ```hasOwnProperty```

   * `hasOwnProperty`，如果对象拥有独特的属性，将返回```true```,`hasOwnProperty`方法不会检查原型链。

  

  # ```for in``` 枚举

*`for in`属性可遍历对象中的所有属性名，所有指的是也遍历原型中的属性。如果想要过滤掉原型中的值，可以采用`hasOwnproperty`方法，或`type of`来排除函数

   ```sh

    $ Object.toString //'function'

    $ Object.constructor //'function'

   ```

# ```detele```

  - 删除对象属性，但不删除原型链中的

# 四种调用

 -   方法调用

 -   函数调用

 -  构造器调用，`new`

 -  Apply 接受两个参数，第一个是将被绑定给this的值，第二个是参数数组

# 给基本类型增加方法

 - `Object.prototype.method`

 - `Funcution.prototype.method`

 - 函数、数组、字符串、数字、正则表达式、布尔值同样适用





 # javascript Dom 编程艺术
  ### 简介 
  - javascript是一种解释型语言。语言分为解释型和编译型（如java，先编译再执行），解释型语言不需要编译，只需要解释器，javascript 在web浏览器中完成解释并执行
  - 对象：是由一些彼此相关的属性和方法集合在一起而构成的数据实体
  - 实例是对象的具体表现：对象是同称，实例是个体。为给定对象创建一个新实例需要`new`关键字
  - 内建对象：比如数组`Array`，`Date`，`Math`
  - 宿主对象：有运行环境（web浏览器）提供的预定义对象m，比如`Form`、`Element`、 `Image`、 `document`
 # DOM
    - 即 document object model，文档对象模型，Dom把文档表示为
一棵节点树。
    - 节点分为不同的类型：元素节点、属性节点、文本节点等
    -  `getElementById`返回一个对象，可通过`document`d
    -  `getElementsByTagName`返回一个对象数组，可通过`document`调用
    -  `getAtrribute`、`setAtrribute`，只能通过元素节点调用，`setAttribute`方法可以对文档中的任何一个元素的任何一个属性做修改
    - Dom树 和 innerHtml属性的区别
     ```
      <div id='testDiv'>
      <p>This is <em>my</em>content</p>
      </div>
     ```
     - Dom可以看到元素的每个细节，需要`getElemntById`等来获取
                             div
          属性节点                            元素节点
         `id='textDiv' `                           ` p`
                            文本节点   元素节点    文本节点
                             `That is`    `em`        `content`
                                  
     - innerHtml是html字符串，无细节可言
                  ```         div    ```
         ```       <p>This is <em>my</em>content</p> ```
    -创建元素阶段 `createElement`,
    -创建文本节点 `createTextNode`
    - 父元素后面追加元素节点 `appendChild`
    - 插入元素 `insertBefore`
      - `parentElement.insertBefore(newElement,targetElement)`
    -`children()`和 `childNode`
# Dom + css
 - style对象的属性值必须放在引号里，单引号或双引号
  - `para.style.color='black'`
  - 如果没有引号，则认为是变量。
  - 怪异模式和标准模式差异很大，比较经典的就是IE对盒模型的解析，在怪异模式中，width本身就包括了padding和border的宽度，此外，标准模式下块级元素的经典居中方法-设定width，然后margin:auto-在怪异模式下也无法正常工作。触发怪异模式与DTD有关。
  - css spite
    >* 将多张图片合并成一张图片，减小http请求次数（原来一张图片需要一条http请求，http请求数越多，访问服务器的次数就越多，服务器压力就越大），利用background-position属性来在指定大小的容器里展示部分位置的背景图。
    >* 对图片位置精确度要求非常高，改变一个小图，可能印象到周边的其它图片，大大降低了可维护性

- relative、absolute和float
  >* position:relative position:absolute
float都可以改变元素在文档流的位置，absolute会脱离文档流，不影响其他元素，relative相对于原来的位置偏离（通过设置left、top、right、bottom值），float通过float:left、float:right 控制元素在同层里“左浮”和“右浮”
，float会改变正常的文档流排列，影响到周围元素。

- 水平居中
    >* 固定宽度
    >* 不固定宽度

# javascript 数据结构与算法
# java 设计模式

接口 （interface.js）
--

```
//Constuctor
 var Interface = function(name,methods) {
    if(arguments.length != 2){
        throw new Error("Interface constructor called with"+ arguments.length+
        "arguments,but expected exactly 2.")
    }
    this.name = name;
    this.methods=[];
    for(var i = 0, len=methods.length;i<len;i++){
        if(typeof methods[i] !== 'string'){
            throw new Error("Interface constructor expect method names to be"+
            "passed in as a string.")
        }
        this.methods.push(methods[i])
    }
}
// Static class method
Interface.ensureImplements = function(object){
    if(arguments.length<2){
        throw new Error("Function Interface.ensureImplements called with" +
         arguments.length + "arguments,but expected at least 2.")
    }
    for(var i=1,len=arguments.length;i<len;i++){
        var interface = arguments[i];
        if(interface.constructor != Interface){
            throw new Error("Function Interface.ensureImplements expects arguments"
            +"two and above to be instances of interface.")
        }
        for(var j=0,methodsLen = interface.methods.length;j<methodsLen;j++){
            var method = interface.methods[j];
            if(!object[method] || typeof object[method]!=='function'){
                throw new Error("Function Interface.ensureImplements:object"
                +" does not implements the "+ interface.name
                +" interface.Method "+ method+" was not found")
            }
        }
    }
}
exports.interface = Interface
```
## 封装和隐藏信息 ##
- (1) 门户大开型
    >*变量和方法用this公开
```
var Interface = require('./interface').interface //commonjs
//创建接口
var Publication = new Interface("Publication",['getIsbn','setIsbn',
'display']);
var Book = function(isbn){ //构造函数    采用this公开
     
}
Book.prototype = {
}
function displayBook(book){
    Interface.ensureImplements(book,Publication)//book实现publication接口
    //...
}
displayBook(new Book())//构造函数的实例
```
-  (2)利用闭包创建私有属性和方法
 >* 变量和方法用var限制作用域
 >* 这种对象创建模式不利于派生子类，因为派生出的子类不能访问
的任何私有属性或方法,用闭包实现私有成员导致的派生问题被称为“继承破坏封装”
 ```
    // 私有变量和方法
var Book = function(newIsbn){//构造函数 不采用this公开
    //private attributes 私有属性
    var isbn;  // var 声明
    //private method 私有方法
    var checkIsbn = function(isbn){
    }
    //privileged methods //特权方法：只有以下这些方法可以访问私有属性和方法,
    //由于每个对象实例都会包含这些方法的副本，因此特权方法太多会占用过多内存（弊端）
    //公共方法的前面都被加上了关键字this
    this.getIsbn = function(){
    }
    this.setIsbn = function(newIsbn){
    }
    //constructor code
    this.setIsbn(newIsbn)
}
Book.prototype={//任何不需要直接访问私有属性的方法可以直接声明在原型中。
    display:function(){//其不需要直接访问isbn属性，
    }
}
console.log(new Book(23).getIsbn())

 ```
##  继承 ##
- 类式继承
```
function extend(subclass,superclass){
    var F = function(){};//添加一个空函数
    F.prototype = superclass.prototype//
    subclass.prototype =  new F();//并用F创建的对象实例插入原型链中，
    //这样做可以避免创建超类的新实例，因为他可能会比较庞大，而且有时候
    //超类的构造函数有一些副作用，或者会执行一些需要进行大量计算的任务
    subclass.prototype.constructor = subclass;
}
//父类
function EditInPlaceField(id, parent, value) {
}
extend(EditInPlaceArea,EditInPlaceField);//继承
function EditInPlaceArea(id,parent,value){//调用父类构造函数
    EditInPlaceField.call(this,id,parent,value)
}
```
- 原型式继承
```
function clone(object){//clone函数首先创建一个新的空函数F
    //然后将F的prototype属性设置为作为参数object传入的原型对象
    var F = function(){}
    F.prototype = object;
    return new F();//以一个给定的对象为原型对象的空对象
}

EditInPlaceField = {//字面量方式
    configure: function(id,parent,value){
    },
}
//调用方式
var titlePrototypal = clone(EditInPlaceField)//继承
titlePrototypal.configure('titlePrototypal','body','Title Here')//调用父类

```

## 单体模式
 - 普通型
    ```
  // 单体是一个只能被 实例化一次 并且可以通过一个众所周知的访问点访问的类
var myNamespace = {};
myNamespace.Singleton = (function(){
    //私有属性及方法
    var privateAttribute1 = false;
    var privateAttribute2 = [1,2,3];
    function privateMethod1(){
    }
    function privateMethod2(){
    }
    return{// public members
        publicAttributes1: true,
        publicAttributes2: 10,
        publicMethod1: function(){
            console.log("singleton")
        },
        publicMethod2:function(){

        }
    }
})()
//调用方式
myNamespace.Singleton.publicMethod1()
    ```
 - 懒惰型
  ```
  myNamespace.Singleton = (function(){
   function constructor(){//转化工作的第一步时把单体的所有代码移到一个
    //名为constructor的方法中：
    //私有属性及方法
    var uniqueInstance;//私有属性，用于判断该类是否已经被实例化过
    var privateAttribute1 = false;
    var privateAttribute2 = [1,2,3];
    function privateMethod1(){

    }
    function privateMethod2(){

    }
    return{// public members
        publicAttributes1: true,
        publicAttributes2: 10,
        publicMethod1: function(){
            console.log("lazy singleton")

        },
        publicMethod2:function(){

        }
    }
   }
   return {
       getInstance:function(){//公用方法getInstance实现
        //全权控制其调用时机
        if(typeof uniqueInstance == 'undefined'){//如果没有被实例化，则实例化
            uniqueInstance = constructor()
        }
        return uniqueInstance
       }
   }
})()
myNamespace.Singleton.getInstance().publicMethod1()
  ```
  ## 方法的链式调用
  ```
  (function(){
    function _$(els){
        // ...
    }
    /**
     * Events
     * addEvent
     * getEvent
     */
    _$.method('addEvent',function(type,fn){

    }).method('getEvent',function(e){
        //...
    })
    /**
     * DOM
     * addClass
     * removeClass
     * replaceClass
     * hasClass
     * getStyle
     * setStyle
     */
    .method('addClass',function(className){
        //...
    }).method('removeClass',function(className){
        //...
    }).method('replaceClass',function(oldClass,newClass){
        //...
    }).method('hasClass',function(className){
        //...
    }).method('getStyle',function(pro){
        //...
    }).method('setStyle',function(prop,val){
        //...
    })
    /**
     * AJAX
     */
    .method('load',function(url,method){
        //...
    })
})()
  ```
  ## 设计模式
  - 工厂模式
  - 桥接模式
  - 组合模式
  - 门面模式
  - 适配器模式
  - 装饰着模式
  - 享元模式
  - 代理模式
  - 观察者模式
  - 命令模式
  - 职责链模式
  

你不知道的javascript ## 
# this的理解
 - 学习this 的第一步是明白this既不指向函数自身也不指向函数的词法作用域。
 - this 实际上是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用。

```
function foo() {
var a = 2;
this.bar();
}
function bar() {
console.log( this.a );
}
foo(); // ReferenceError: a is not defined
## 首先，这段代码试图通过this.bar() 来引用bar() 函数,这是 绝对不可能成功的,调用bar() 最自然的方法是省略前面的this，直接使用词法引用标识符。
##编写这段代码的开发者还试图使用this 联通foo() 和bar() 的词法作用域，从而让bar() 可以访问foo() 作用域里的变量a。这是不可能实现的，你不能使用this 来引用一个词法作用域内部的东西。

```
 - this 是在运行时进行绑定的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。this 的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式，当一个函数被调用时，会创建一个活动记录（有时候也称为执行上下文）。这个记录会包含函数在哪里被调用（调用栈）、函数的调用方法、传入的参数等信息。this 就是记录的其中一个属性，会在函数执行的过程中用到。
 - 绑定规则
 >* 默认绑定:  非严格模式,不带任何修饰的函数引用进行调用的，只能使用默认绑定，严格模式下，this指向undefiend
```
function foo() {
console.log( this.a );//根据调用栈，this指向全局。`use strict`下，this指向undefiend
}
var a = 2;
foo(); // 2 不带任何修饰的函数引用进行调用的
```
>* 隐式绑定：调用位置是否被某个对象拥有或者包含。
```
function foo() {
    console.log( this.a );
}
var obj = {
    a: 2,
    foo: foo
};
obj.foo(); // 2 调用位置会使用obj 上下文来引用函数，当函数引
//用有上下文对象时，隐式绑定规则会把函数调用中的this 绑定到这个上下文对象,因为调用foo() 时this 被绑定到obj，因此this.a 和obj.a 是一样的。
```
>* 默认绑定丢失
```
function foo() {
    console.log( this.a );
}
var obj = {
    a: 2,
    foo: foo
};
var bar = obj.foo; // 函数别名！
var a = "oops, global"; // a 是全局对象的属性
bar(); // "oops, global"
#虽然bar 是obj.foo 的一个引用，但是实际上，它引用的是foo 函数本身，因此此时的bar() 其实是一个不带任何修饰的函数调用，因此应用了默认绑定。
```
-  显示绑定
  - call
                bar.call(obj)
  - apply
                 bar.apply(obj)
  - 硬绑定 bind
  
- new 绑定
。在JavaScript 中，构造函数只是一些使用`new` 操作符时被调用的函数。它们并不会属于某个类，也不会实例化一个类
。 包括内置对象函数（比如Number(..)，详情请查看第3 章）在内的所有函数都可。以用new 来调用，这种函数调用被称为构造函数调用
。使用new 来调用函数，或者说发生构造函数调用时，会自动执行下面的操作。
>* 创建（或者说构造）一个全新的对象
>* 这个新对象会被执行[[ 原型]] 连接。
>* 这个新对象会绑定到函数调用的this。
>* 如果函数没有返回其他对象，那么new 表达式中的函数调用会自动返回这个新对象。
```
function foo(a) {
    this.a = a;
}
var bar = new foo(2);
console.log( bar.a ); // 2
```

```
function foo(something) {
    this.a = something;
}
var obj1 = {};
var bar = foo.bind( obj1 );
bar( 2 );
console.log( obj1.a ); // 2
var baz = new bar(3);//创建一个新对象baz
console.log( obj1.a ); // 2
console.log( baz.a ); // 3 修改了 baz.a 而没有修改
```

 - 绑定优先级
    >* 1、函数是否在new 中调用（new 绑定）？如果是的话this 绑定的是新创建的对象。
    var bar = new foo()
>* 2、函数是否通过call、apply（显式绑定）或者硬绑定调用？如果是的话，this 绑定的是指定的对象。
var bar = foo.call(obj2)
>* 3 函数是否在某个上下文对象中调用（隐式绑定）？如果是的话，this 绑定的是那个上下文对象。
var bar = obj1.foo()
>* 4 如果都不是的话，使用默认绑定。如果在严格模式下，就绑定到undefined，否则绑定到全局对象。
var bar = foo()

 - 箭头函数
 箭头函数的绑定无法被修改。（new 也不行！）
        
## 对象 ##
- 复制
```
function anotherFunction() { /*..*/ }
var anotherObject = {
    c: true
};
var anotherArray = [];
var myObject = {
    a: 2,
    b: anotherObject, // 引用，不是复本！
    c: anotherArray, // 另一个引用！
    d: anotherFunction
};
anotherArray.push( anotherObject, myObject );
```
 - 浅copy
       - Object.assign(目标对象，源对象，[源对象])
    

<pre>
   
            var newObj = Object.assign( {}, myObject );
            newObj.a; // 2
            newObj.b === anotherObject; // true
            newObj.c === anotherArray; // true
            newObj.d === anotherFunction; // true
    
</pre>

 - 深copy
      - Json（适用于部分情况）
       ```
        var newObj = JSON.parse( JSON.stringify( someObj ) );
        
       ```
- 数据
- - 描述符
```
Object.defineProperty( myObject, a, {
    enumerable: true,//决定可以出现在对象属性的遍历中
    writable: false, // 决定是否可更改
    configurable: true,
    value:2
}
Object.defineProperty( myObject, b, {
    enumerable: true,//决定不可以出现在对象属性的遍历中
    writable: false, // 决定是否可更改
    configurable: true,
    value:4
}
for(var k in myobject){//遍历对象，可遍历的属性enumerable为true
    console.log(k, myobject[k]) // a,2
}

```
- 属性描述符
    关心`get` `set` `enumerable` `configureable`
```
    var myObject = {
    // 给 a 定义一个getter
    get a() {
        return this._a_;
    },
    // 给 a 定义一个setter
    set a(val) {
        this._a_ = val * 2;
    }
    };
    myObject.a = 2;
    myObject.a; // 4
```
```
    var myObject = {
    // 给 a 定义一个getter
    get a() {
        return 2;
    }
    };
    myObject.a = 3;
    myObject.a; // 2 由于只定义了a 的getter，所以对a 的值进行设置时set 操作会忽略赋值操作， 而且即便有合法的setter，由于我们自定义的getter 只会返回2，所以set 操作是没有意义的。
```
- in 和 hasownproperty 区别
    `in` 查找原型链
    `hasownproperty`不查找原型链

## 混合对象“类” ##

- 面向类的设计模式
    **[1] 实例化**
    
    **[2] 继承**

    **[3] 多态**
## 原型 ##
- Object.create()
    可以创建一个对象m，并把这个对象的原型关联到指定的对象
```
    var myObject = Object.create( anotherObject );
    myObject.prototype 为anotherObject
```
- “构造函数”
javascript中，对于“构造函数”最准确的解释是，所有带`new`的函数调用，函数不是构造函数，但是当且仅当使用`new`时，函数调用会变成“构造函数调用”
 ***一些关于构造函数的误解和理解***
```
    function Foo(){
    }
    console.log(Foo.prototype.constructor === Foo)//true
    var a = new Foo()
    console.log(a.constructor === Foo)//true
```
- [ ] 错误理解一： a.constructor === Foo 为真意味着a确实有一个指向Foo的 .constructor 属性，但事实不是这样，实际上， .constructor引用被委托给了Foo.Prototype， 而Foo.prototype.constructor默认指向Foo
- Foo.prototype的.constructor属性只是Foo函数在声明时的默认属性，如果创建了一个**新对象**并替换了函数默认的.prototype对象引用，那么新对象不回自动获得.constructor属性。例如如下代码:
```
function Foo(){
}
Foo.prototype = {}//创建一个新原型对象
console.log(Foo.prototype.constructor === Foo)//false
var a = new Foo()
console.log(a.constructor === Foo)//false
```
```
function Foo(){
}
Foo.prototype.getName = function(){
 	return "meau"
}
console.log(Foo.prototype.constructor === Foo)//true
var a = new Foo()
console.log(a.constructor === Foo)//true
```

 - 原型继承
 
- [ ] 典型的“原型风格”
```
function Foo(name){
	this.name = name
}
Foo.prototype.myName = function(){
	return this.name
}
function Bar(name, label){
	Foo.call(this, name)
	this.label = label
}
//创建一个新的Bar.prototype对象并关联到Foo.prototype
Bar.prototype = Object.create(Foo.prototype) //重点
//注意，现在没有Bar.prototype.constructor了
//如果需要这个属性的话可以手动修复
Bar.prototype.constructor = Bar;

Bar.prototype.myLabel = function(){
	return this.label
}
var a= new Bar("a","Obj a")
console.log(a.myName())
console.log(a.myLabel())
```
>* 常见错误做法一：
```
Bar.prototype = Foo.protoType;
```
这种做法并不会创建一个关联到`Bar.prototype`的新对象，它只是让`Bar.prototype`直接引用`Foo.prototype`对象，因此当执行`Bar.prototype.myLable = ... `赋值语句的时候，会直接修改`Foo.prototype`对象本身
>* 常见错误做法二：
```
Bar.prototype = new Foo()
```
这种确实会创建一个关联到Bar.prototype的新对象，但是使用Foo的“构造函数”调用，如果函数Foo有一些副作用（比如写日志、修改状态、注册到其它对象、给this添加数据属性、等等）的话，就会影响到Bar()的“后代”（不理解什么意思，后期理解了在回来补充）

## 委托 ##
虽然`javascript`机制和传统面向类语言中的“类初始化”和“类继承”很相似，但是javascript中的机制有一个核心区别，那就是不会进行复制，对象之间是通过内部`prototype`链关联的。

## javascript 的两种思维模型 ##
- 模仿类行为（类
- ）
```
function Foo(who){
    this.me = who
}
Foo.prototype.identify = function(){
    return "I am " + this.me;

}
function Bar(who){
    Foo.call(this, who)
}
Bar.prototype = Object.create(Foo.prototype)
Bar.prototype.speak = function(){
    console.log("hello " + this.identify() + '.')
}
var b1 = new Bar('b1')
var b2 = new Bar('b2')

b1.speak()
b2.speak()
```
- 对象关联风格（行为委托）
```
Foo = {
    init: function(who){
        this.me = who
    },
    identify: function(){
        return "I am " + this.me;
    }
}

Bar = Object.create(Foo)
Bar.speak = function(){
    console.log("hello " + this.identify() + '.')
}

var b1 = Object.create( Bar );//注意区别
b1.init("b1")

var b2 = Object.create( Bar )
b2.init('b2')

b1.speak()
b2.speak()
```


----------
## 你不知道的javascript（中） ##
# 类型和语法
- 其中内置类型
>[ ] null
```tyoeof null === 'object' //true```
这是一个由来以久的bug
```
    var a = null
    （！a!a && typeof a === 'object'）
```

>[ ] undefined
变量在未持有值时`undefined`
已在作用域中声明但还没有赋值的变量，是`undefined` 的
```
var a;
typeof a; // "undefined"
```
>[ ] boolean
>[ ] number
```
# NaN 有一个严重bug 如下：
var a = 2 / "foo";
var b = "foo";
a; // NaN
b; "foo"
window.isNaN( a ); // true
window.isNaN( b ); // true——晕！
# 修改方式
if (!Number.isNaN) {
    Number.isNaN = function(n) {
    return (
        typeof n === "number" &&
        window.isNaN( n )
    );
    };
}
# 修改方式二
if (!Number.isNaN) {
    Number.isNaN = function(n) {
        return n !== n;
    };
}
```
```
typeof 的返回值时字符串
NaN 是“不是数字的数字” nan是唯一一个自反不相等的值
var a = 2 / "foo"; // NaN
typeof a === "number"; // true
```
```
#tofixed(..) 方法可指定小数部分的显示位数：
var a = 42.59;
a.toFixed( 0 ); // "43"
a.toFixed( 1 ); // "42.6"
```
```
# toPrecision(..) 方法用来指定有效数位的显示位数：
var a = 42.59;
a.toPrecision( 1 ); // "4e+1"
a.toPrecision( 2 ); // "43"
```
>[ ] string
```
var a = 'foo'
var c = a
// 将a的值转换为字符数组
.split( "" )
// 将数组中的字符进行倒转
.reverse()
// 将数组中的字符拼接回字符串
.join( "" );
c; // "oof"
```
>[ ] object
`function` `array`都是object 的子类型
>[ ] symbol
JavaScript 中的变量是没有类型的，只有值才有。变量可以随时持有任何类型的值。

- 　值和引用
```
var a = 2;
var b = a; // b是a的值的一个副本
b++;
a; // 2
b; // 3
var c = [1,2,3];
var d = c; // d是[1,2,3]的一个引用
d.push( 4 );
c; // [1,2,3,4]
d; // [1,2,3,4]
```
  - 简单值（即标量基本类型值，scalar primitive）总是通过值复制的方式来赋值/ 传递，包括null、undefined、字符串、数字、布尔和ES6 中的symbol。
  - 复合值（compound value）——对象（包括数组和封装对象，参见第3 章）和函数，则总是通过引用复制的方式来赋值/ 传递。

- 内建函数
• String()
• Number()
• Boolean()
```
# 以下强制类型转换结果为false
    • undefined
    • null
    • false
    • +0、-0 和NaN
    • ""
```
• Array()
    `Array.prototype`是个空数组
• Object()
• Function()
    `Function.prototype(); // 空函数！`
• RegExp()
    `RegExp.prototype 是一个正则表达式`
• Date()
• Error()
• Symbol()——ES6 中新加入的！

- 相等比较
```
"0" == null; // false
"0" == undefined; // false
"0" == false; // true -- 晕！
"0" == NaN; // false
"0" == 0; // true
"0" == ""; // false


false == null; // false
false == undefined; // false
false == NaN; // false
false == 0; // true -- 晕！
false == ""; // true -- 晕！
false == []; // true -- 晕！
false == {}; // false

"" == null; // false
"" == undefined; // false
"" == NaN; // false
"" == 0; // true -- 晕！
"" == []; // true -- 晕！
"" == {}; // false

0 == null; // false
0 == undefined; // false
0 == NaN; // false
0 == []; // true -- 晕！
0 == {}; // false

[] == ![] // true
2 == [2]; // true
"" == [null]; // true
0 == "\n"; // true
```


# 异步和性能
- 事件循环队列和任务队列
事件循环队列类似于一个游乐园游戏：玩过了一个游戏之后，你需要重新到队尾排队才能再玩一次。而任务队列类似于玩过了游戏之后，插队接着继续玩。 
一旦有事件需要运行，事件循环就会运行，直到队列清空。事件循环的每一轮称为一个tick。用户交互、IO 和定时器会向事件队列中加入事件。
- 回调
- Promise

    固有行为属性
    >[] 每次对Promise调用 then(...)，它都会创建并返回一个新的Promise，我们可以将其链接起来
    >[] 在完成或拒绝处理函数内部，如果返回一个值或抛出一个异常，新返回的（可链接的）Promise 就相应地决议。
    >[] 如果完成或拒绝处理函数返回一个Promise，它将会被展开，这样一来，不管它的决议值是什么，都会成为当前then(..) 返回的链接Promise 的决议值。
    ```
        var p = Promise.resolve( 21 );
        var p2 = p.then( function(v){
            console.log( v ); // 21
            // 用值42填充p2
            return v * 2;
        } );
        //p2是一个new Promise
        // 连接p2
        p2.then( function(v){
            console.log( v ); // 42
        } );
    ```
    
    两个API
    >[ ] Promise.resolve
    
    ```
    # 可以传入非promise、非thenable的普通值
    var fulfilledPr = Promise.resolve( 42 );

    var rejectedTh = {
        then: function(resolved,rejected) {
            rejected( "Oops" );
        }
};
var rejectedPr = Promise.resolve( rejectedTh );// 对传入的thenable 则会展开。如果这个thenable 展开得到一个拒绝状态，那么从Promise.resolve(..) 返回的Promise 实际上就是这同一个拒绝状态。
Promise.resolve(..) 会将传入的真正Promise 直接返回
    ```
    
    > [ ]  Promise.reject
    ```
    var rejectedPr = Promise.reject( "Oops" );
    # 其和以下是等价的，
    var p = new Promise(function(resolve,reject)){
            reject( "Oops" )
    }
    
    ```
    
    > [ ] new Promise(...)构造器
     必须和`new`一起使用，并且必须提供一个函数回调，这个回调是同步的或立即调用的。这个函数接受两个函数回调，用以支持`promise`的决议。通常我们把两个函数称为`resovle` 和 `reject`
     
    ```
        var p = new Promise(function(resolve,reject)){
            //resolve()
            //reject()
        }
    ```
`reject(...)`拒绝这个`promise`，但是`resolve（...）`既可以完成`promise`， 也可以拒绝，要根据传入参数而定。如果传给`resolve（）`的是一个非promise、非thenable的立即值，这个promise就会用这个值完成，如果传给resolve（）的是一个promise或thenable的值，这个值就会被递归展开，并且（要构造的）promise将取用其最终决议值或状态。

>[] then 和 catch
 `then` 接受一个或两个参数，第一个用于完成回调，第二个用于拒绝回调，
 
 >[] P romise.all([]) 
 >[] Promise.race([])
 
 
- Generator 
> [X] 一个迭代器
```
function *boo(x){
	return x * (yield)
}

var it = boo(2)// 创建迭代器对象，并赋值给it

 it.next() //启动 foo
 res = it.next(7)
 console.log(res.value)//14
```
当执行boo()的时候，并不执行 generator 函数体，而是返回一个迭代器。迭代器具有next()方法，每次调用 next() 方法，函数就执行到yield语句的地方。next() 方法返回一个对象，其中value属性表示 yield **关键词后面表达式的值**，done 属性表示是否遍历结束

 - .next()调用时，返回一个对象 
 yield关键字将程序逻辑划分成几部分，每次.next()执行时执行一部分。.next()调用时，返回一个对象，这个对象具备两个属性。` {value: XX, done: XX} `
 
 - 可以通过向.next()传递参数
 通过.next()传递参数，可以赋值给***yield关键字前面的变量***。
 
 ```
     function *main(){
     var x = yield 'hello world'
     console.log(x)//oooooops
    
    }
    var it = main()
    console.log( it.next() )//{ value: 'hello world', done: false }
    console.log( it.next("oooooops") )//{ value: undefined, done: true } 
    // it.next()打印输出yield 之后表达式的值， 程序最后会打印ryield的返回值，没有return时，默认为undefined
 ```
 - 再理解下赋值给***yield关键字前面的变量***
 ```
    #和前一段代码进行对比
     function *main(){
     var x = yield 'hello world'
     console.log(x)//undefined
    
    }
    var it = main()
    console.log( it.next() )//{ value: 'hello world', done: false }
    console.log( it.next() )//{ value: undefined, done: true }
 ```
 
 
 
 
    

    
    
    
    
    
    
    
    
    



 
 

