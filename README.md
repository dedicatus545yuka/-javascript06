# -javascript06
Function对象，原型
### JSON 
- JSON 全称为 JavaScript Object Notation，译为 JavaScript 对象表示法。是一种`轻量级`的数据交换格式。 
- JSON 易于开发者阅读和编写，也易于计算机解析和生成。它原本是基于JavaScript的一个子集。
- JSON 采用完全独立于语言的文本格式，被 Java、C#、C++、PHP、OC 等几乎所有主流语言所支持。   
![数据交换格式](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/4.Raqs4EOfqiF4yO2GyieraRpR5HKuzUBoktUbC3L84!/m/dD8BAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)  
#### JSON格式
>字符串必须用双引号括起来。
1. 对象类型 
```json 
{
  "name" : "yuka",
  "age" : 29,
  "male" : true,
  "job" : "voice actor"
}
```
2. 数据类型  
```json
[
  "yuka",
  20,
  true,
  null
]
```
3. 类型的嵌套  
```json
{
  "wife" : [
    {
      "name" : "yuka",
      "age" : 29,
      "male" : true
    },
    {
      "name" : "saya",
      "age" : 14,
      "male" : false
    }
  ]
}
```
4. 在JavaScript中的Json格式
```json
// JavaScript中的对象
var json1 = {
    "name" : "yuka",
    "age" : 29,
    "male" : true,
    "job" : null
}
// JavaScript中的数组
var json2 = [ "yuka",29,true,null];
```
5. 符合JSON格式要求的字符串类型  
```js
var wife ='{"name" : "yuka","age" : 29,"male" : "girl","job" : "vioce artist"}';
var jsonString2 = '[ "张无忌",18,"girl","vioce artist"]';
```
* 符合JSON格式要求的字符串 - 不建议手动编写  
  * 当数据量较大时 - 编写比较麻烦
  * 构建数据内容 - 数据多来源于用户的输入(动态获取)
#### JSON的转换  
- JSON实际是JavaScript的标准规范中的一个子集(JavaScript支持JSON)
    * JavaScript提供了`JSON对象`,该对象具有两种方式 - 将JSON格式转换成字符串类型，将字符串类型转换成JSON格式
      * JSON.parse() - 将字符串转换成JSON
      * JSON.stringify() - 将JSON转换成字符串
* 注意 - JSON对象在 IE 8之前的版本不支持
    * 引入第三方的解决方案 - json2.js
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>JSON的转换</title>
        <!-- 引入第三方JSON的解决方案 : 解决IE8以下版本不支持JSON的问题 -->
        <script src="json2.js"></script><!-- 文档自己找 -->
        <script>
            console.log(JSON);
            var json = {
                "name" : "yuka",
                "age" : 29
            }
            // 将JSON转换成字符串
            var jsonString = JSON.stringify(json);
            console.log(jsonString);
            // 将字符串转换成JSON
            var jsonObj = JSON.parse(jsonString);
            console.log(jsonObj);
        </script>
    </head>
<body>
  请打开，开发者工具
</body>
</html>
```
![JSON对象的转换方式](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/TSFL8xlZBZZf2JZAxt6zu34CZMao9AvoViQNXHZ5wKc!/m/dPIAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)
#### eval()函数
- 将符合JSON格式的字符串转换成JSON
* 将符合JSON格式的字符串作为参数传递给eval()函数 -> 结果为报错 - SyntaxError: Unexpected token :
    * 注意 - 强制向传递的参数添加一对小括号() - 根据 eval() 的严格语法要求，其接收的参数只能是 string 类型，而不能是 String 类型！
      * 结果 -> 正常地将符合JSON格式的字符串转换成JSON
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>eval()函数</title>
    <script>
        var str = '{ "name" : "zhangwuji","age" : 18,"male" : true,"job" : null }';
        var json = eval('(' + str + ')');// 这里不加小括号就会报错
        console.log(json);
        /*
         JavaScript中大括号({})的作用
         * 大括号表示语句块 - eval()函数默认将解析为语句块 -> undefined
         * 大括号表示对象 - eval()函数强制添加小括号 -> 强制将其转换成对象
         */
        var json = eval('{}');// undefined
        console.log(json);
    </script>
</head>
<body>
  请打开，开发者工具！
</body>
</html>
```
### 函数和对象
1. 构造函数 
>目前，定义函数具有三种方式，这三种方式之间存在一定差别   

![](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/RejDQUGaasOVbRkhGk4KH0BFHu0YM9y0Wr*0c8.bBDk!/m/dPIAAAAAAAAA&bo=nAMgAQAAAAADB5w!&rf=photolist)   
```js
// 创建对象
//对象初始化器方式（字面量）
var obj = {
    name : 'yuka',
    sayMe : function(){
        console.log('this is love');
    }
}
console.log(typeof obj);// object
console.log(obj instanceof Object);// true
//构造函数方式
var obj = new Object();

//创建函数
//函数定义语句
var fn = function(){};
//字面量表达式
function fn(){
    console.log('this is function');
}
console.log(typeof fn);// function
console.log(fn instanceof Function);// true
// 构造函数的方式
var fn = new Function();
console.log(typeof fn);// function
console.log(fn instanceof Function); //ture
```
2. 函数和Function对象
- 函数是这样的一段 JavaScript 代码，它只定义一次，但可能被执行或调用多次。 
- Function 类型是 JavaScript 提供的引用类型之一，通过 Function 类型创建 Function 对象。  
- 在 JavaScript 中，函数也是以对象的形式存在的。每个函数都是一个 Function 对象。 函数名，本质就是一个变量名，是指向某个 Function 对象的引用。
3. 函数的属性和方法  
> 由于每个函数都是一个 Function 对象，Function 类型也提供了一些属性和方法:

![](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/OQ5NIYAp8joBwr5BndhMN2IwxOgLWSUOVcV*ipVma3E!/m/dPMAAAAAAAAA&bo=AAXsAQAAAAADB8o!&rf=photolist)
#### Function对象 
- new Function()一定是 Function 类型的对象
- var 函数名 = new Function(形参,函数体);
- JavaScript中所有的函数都是一个Function对象
```js
var fn = new Function('a,b','return a+b;');
var result = fn(1,2);
console.log(result);// 3
console.log(fn instanceof Object);// true - fn是一个对象
console.log(fn);// [Function: anonymous] - fn是一个函数
// 调用函数的方式
fn();// 没有报错
```
#### 对象与构造函数 
构造函数 - 用来创建对象(属性和方法)，同样也具有参数 -> 形参和实参
* 定义属性 - this.属性名 = 值;
* 定义方法 - this.方法名 = function(){}
* 在方法中使用属性的话 -> this.属性名
* 注意 - this的用法本身就是JavaScript中的一大难点
* 含义 - 本身不具备任何含义(使用环境)
* this -> 代表将来要创建的对象
```js
function Wife(){
    // 定义属性
    this.name = 'yuka';
    // 定义方法
    this.sayMe = function(){
        console.log('this is love');
    }
}
// 通过构造函数方式创建对象
var wife = new Wife();//定义了一个小写wife
console.log(wife);

console.log(wife instanceof Object);// true
console.log(wife instanceof Function);// false

console.log(Wife instanceof Function);// true
```
### 原型
- 在 JavaScript 中，函数是一个包含属性和方法的 Function 类型的对象。而原型（Prototype）就是 Function 类型对象的一个属性。 
- 在函数定义时就包含了 prototype 属性，它的初始值是一个空对象。在 JavaScript 中并没有定义函数的原型类型，所以原型可以是任何类型。 
- 原型是用于保存对象的共享属性和方法的，原型的属性和方法并不会影响函数本身的属性和方法。  
#### 原型属性  
1. 所有的函数都是Function类型的对象
2. 所有Function类型的对象都具有`prototype`原型属性
3. 所有prototype原型属性的默认值都是一个空对象
    *  所有的对象都可以添加属性和方法
```js
// 创建Function类型的对象
var fn = new Function();
// 测试prototype属性
console.log(fn.prototype);// {} - 空对象

// 定义函数
function n(){}
// 测试prototype属性
console.log(n.prototype);// {} - 空对象
```
#### 利用原型拓展属性和方法 
>通过如下两种方式可以设置原型的属性和方法:
>1. 原型的属性和方法单独进行定义。
>2. 直接为原型定义一个新对象。 
```js
function Hero(name){
    this.name = name;
    this.sayMe = function(){
        console.log(this.name);
    }
}

var hero = new Hero('张无忌');

 console.log(hero.name);
 hero.sayMe();

console.log(Hero.prototype);// 空对象 - Hero {}
// 将构造函数的prototype属性赋值给一个变量 -> 就是一个空对象
var obj = Hero.prototype;
// 为对象添加属性和方法
obj.age = 18;
obj.job = '教主';
obj.sayAge = function(){
    console.log('this is age');
}

var hero = new Hero('张无忌');

console.log(hero);// Hero { name: '张无忌', sayMe: [Function] }

console.log(hero.job);// 教主
hero.sayAge();// this is age
```
##### 一种特殊情况的思考
>原型的属性或方法与构造函数的属性或方法同名时 -> 构造函数的属性或方法的优先级更高  

```js
function Hero(){
    this.name = '张无忌';
}
var obj = Hero.prototype;
obj.name = '周芷若';

var hero = new Hero();
// 默认得到的是构造函数的属性
console.log(hero.name);// 张无忌

delete hero.name;
console.log(hero.name);// 周芷若
```
#### 隐式原型  
>隐性原型指__proto__属性  

```js
// 隐式原型是对象的属性
var obj1 = {
    name : 'zhangwuji'
}
console.log(obj1.__proto__);

var obj2 = new Object();
console.log(obj2.__proto__);

var obj3 = Object.create(obj2);
console.log(obj3.__proto__);
```
![对象的内存结构图](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/e3YJ9qeAXtsmkSCMQo4H47b8YMLSo9yJYrHGE9w6eao!/m/dPIAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)
#### 隐式原型和显式原型  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>显式原型与隐式原型</title>
    <script>
            // 构造函数
           function Hero(name){
               this.name = name;
               this.sayMe = function () {
                   console.log(this.name);
               }
           }
           //构造函数的原型属性
            var obj = Hero.prototype;
            obj.male = 'man';
           //通过构造函数的方式来构造对象
            var hero = new Hero();
            hero.name = '张无忌',
            hero.age = 18,
            hero.sayAge = function () {
                console.log('this is age');
            }
            // 继承函数Hero的属性 - Object { name: "张无忌", sayMe: Hero/this.sayMe(), age: 18, sayAge: hero.sayAge() }
            console.log(hero);
            // 继承了函数显式原型属性 Hero.prototype的属性 - Object { male: "man", 等 1 项… }
            console.log(hero.__proto__);

    </script>
</head>
<body>
    请打开，开发者工具！
</body>
</html>
```
![显式原型和隐式原型的关联图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/bK6X1B*DeazWQaKwm6OC7QfM0FhficYcm*RZWWDakQM!/m/dPMAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)
#### 原型链  
- 构造函数具或对象有`prototype` 属性，对象具有 `__proto__`属性，这就是上面所说的原型。 
- 如果构造函数或对象 A ，A 的原型指向构造函数或对象 B，B 的原型再指向构造函数或对象 C，以此类推，最终的构造函数或对象的原型指向 Object 的原型。由此形成一条链状结构，被称之为原型链。
- 按照上述的描述，在 B 中定义的属性或方法，可以直接在 A 中使用并不需要定义。这就是继承，它允许每个对象来访问其原型链上的任何属性或方法。 
- 原型链是 ECMAScript 标准中指定的默认实现继承的方式。
```js
function A(){
    this.a = 'a';
}
var a = new A();

console.log(a.a);// a
console.log(a.b);// undefined

function B(){
    this.b = 'b';
}

B.prototype = a;

var b = new B();

console.log(b.b);// b
console.log(b.a);// a
// 那么下面可以在构造N个函数来加长这条链（继承）
function C(){
    this.c = 'c';
}
C.prototype = b;
```
![原型链的示意图](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/a6kQ3PTzbUjC1bPrKa1hWafdgB*fadYf6maOwZ5DbYA!/m/dPIAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)
