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



    

  

 







