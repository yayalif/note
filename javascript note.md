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
 







