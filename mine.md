# 原生js部分

## 方法总结
[参考文档](https://blog.csdn.net/Amanda_wmy/article/details/80524475)
> 判断数据类型 ==>  Object.prototype.toString.call(null) ==> [object Null] ==>  可以用在深拷贝、遍历等上
### 数组
> - 数组转成字符串 : arr.join("") 、arr.toString()
> - arr.push(); //向后添加，返回新数组个数 ,原数组是添加后的数组 
> - arr.pop(); //从后删除，返回删除的元素 
> - arr.unshift(); //向前添加，返回个数 
> - arr.shift(); //从前删除，返回删除的元素 
> - arr.reverse();//反转数组 
> - arr.sort();//排序 
> - arr.slice();拷贝,生成新的数组 
> - arr.splice()//截取 
> - arr.concat();//拼接，合并 
> - arr.indexOf();//寻找数组中的元素的索引，没有返回-1； 
> - Math.max.apply（null,arr）或 Math.max(…arr)//找到数组中的最大值 
> - Math.min.apply(null,arr)或 Math.min(…arr) //找到数组中的最小值 
> - 数组结构
```js
// 利用set集合简单实现数组去重
var arr = [1,2,3,3,2,1,21]
arr = Array.from(new Set(arr))
console.log(arr)
```
### 字符串
> - str.toUpperCase() //转大写 
> - str.toLowerCase() //转小写 
> - str.concat() // 拼接，合并 
> - str.indexOf() //寻找字符串中的元素，是否存在某个字符串，没有返回-1；
> - str.slice(beginSlice,endSlice) // 返回被操作字符的子字符串，第一个参数为开始位置，第二个参数为结束位置，前包后不包（不改变原字符串） 
> - str.split() //分隔符将一个字符串分割成多个字符串，转化成数组
> - str.trim() //删除元素前置及后缀的所有空格
> - str.startsWith("str") //检测字符串是不是以"str"开头的，根据判断返回true,false 
> - str.endsWith("str") //是不是以"str"结尾的 
> - 字符串模板
### 对象
> - Object.assign() // 浅拷贝，用于将所有可枚举属性的值从一个或多个源对象复制到目标对象，它将返回目标对象 
> - for...in //语句循环遍历对象的属性。

## 变量提升
- 声明统一提前，赋值原地不变   
- 函数声明格式的函数才会存在函数声明提前 ==>  函数整体提前而不止是只提前声明
- 函数表达式，构造函数，都不存在函数声明提前。
- 函数会首先被提升，然后才是变量  ==> 同一作用域下提前，函数会在更前面

## 面向对象

> `面向对象是一种思想，是基于面向过程而言的`，就是说面向对象是将功能等通过对象来实现，将功能封装进对象之中，让对象去实现具体的细节；这种思想是将数据作为第一位，而方法或者说是算法作为其次，这是对数据一种优化，操作起来更加的方便，简化了过程。

即 :  
> 1. 将复杂的事情简单化。
> 2. 面向对象将以前的过程中的执行者，变成了指挥者。
> 3. 面向对象这种思想是符合现在人们思考习惯的一种思想。
### 三大特性

#### 封装
只隐藏对象的属性和实现细节，仅对外提供公共访问方式

好处：将变化隔离、便于使用、提高复用性、提高安全性

原则：将不需要对外提供的内容隐藏起来；把属性隐藏，提供公共方法对其访问

#### 继承
继承的类就可以从被继承的类中获得一些属性和方法，提高代码复用性；继承是多态的前提
#### 多态

是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象

好处：提高了程序的扩展性

弊端：当父类引用指向子类对象时，虽提高了扩展性，但只能访问父类中具备的方法，不可访问子类中的方法；即访问的局限性。如果子类重写的父类的方法，那么调用的时候默认的是用子类重写的那个方法

前提：实现或继承关系；覆写父类方法。

### 五大原则
> 单一职责原则 、开放封闭原则、里式替换原则、依赖倒置原则、接口分离原则

## 继承
>继承是面向对象中一个非常重要的特征。指的是：子类继承父类的属性和方法。

在父类的属性和方法基础上, 让子类也拥有这些属性和方法, 并可以扩展

### 继承的优点 
- 子类拥有父类所有的属性和方法（代码复用）
- 子类可以扩展自己的属性和方法（更灵活）
- 子类可以重写父类的方法

### 继承的方式
- 原型链继承

> 1. 核心 : 拿父类实例来充当子类原型对象
```js
//  核心 : 拿父类实例来充当子类原型对象
// 缺点：
// 1. SuperType中的属性(不是方法)也变成了SubType的prototype中的公用属性,也可能被实例对象所修改
    // 其实原型对象上任何类型的值，都不会被实例所重写/覆盖。在实例上设置与原型对象上同名属性的值，只会在实例上创建一个同名的本地属性。
    //但是，原型对象上引用类型的值可以通过实例进行修改，致使所有实例共享着的该引用类型的值也会随之改变。
// 2. 创建子类型的时候，不能像父类型的构造函数中传递参数。
function SuperType(){
    this.colors = ["red", "blue", "green"];
}
SuperType.prototype.Fun = function(){
 console.log("Fun")
};
function SubType(){
}
//SubType继承了SuperType ==> 将 SubType 的原型对象替换成了 SuperType的实例对象
SubType.prototype = new SuperType();
// 给原型添加方法的语句一定要放在原型替换SubType.prototype = new SuperType()之后

// 通过 SubType 来构造实例对象
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green,black"
```
- 借用构造函数

```js
// 核心：将父类的构造函数拿到子类的构造函数中，改变this的指向(bind,apply,call)，返回新函数同时执行新函数(bind只会返回一个新函数，不会自动执行),记得传参。(即 在子类构造函数的内部调用父类构造函数)
// 优点: 解决了superType中的私有属性变公有的问题，可以向父类构造函数传递参数
// 缺点：每个子类实例都会拷贝一份父类构造函数中的方法，作为实例自己的方法
    // 每个实例都拷贝一份，占用内存大，尤其是方法过多的时候(即做不到 "函数复用",一般是通过"prototype"来调用某一方法)
    // 构造函数的方法都作为了实例自己的方法，当需求改变，要改动其中的一个方法时，之前所有的实例，他们的该方法都不能及时作出更新。只有后面的实例才能访问到新方法。
function SuperType(){
    this.colors = ["red", "blue", "green"];
}
function SubType(){
    //继承了SuperType
    SuperType.call(this);
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
//=================================================
function SuperType(name){
    this.name = name;
}
function SubType(){
    //继承了SuperType，同时还传递了参数
    SuperType.call(this, "Nicholas");
    //实例属性
    this.age = 29;
}
var instance = new SubType();
alert(instance.name); //"Nicholas";
alert(instance.age); //29
```
- 组合式继承

> 1. `核心`:原型链继承方法+借用构造函数拷贝属性
    > - 在构造函数中定义属性 把所有的方法写入原型对象
> 2. 缺点：两次调用父构造器函数，浪费内存。
```js
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
    alert(this.name);
};
function SubType(name, age){
    SuperType.call(this, name);//借用构造函数继承属性，第二次调用
    // 在实例上设置与原型对象上同名属性的值，只会在实例上创建一个同名的本地属性。
    this.age = age;
}
SubType.prototype = new SuperType();//借用原型链继承方法，第一次调用
SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
    alert(this.age);
};
var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
instance1.sayName(); //"Nicholas";
instance1.sayAge(); //29
var instance2 = new SubType("Greg", 27);
alert(instance2.colors); //"red,blue,green"
instance2.sayName(); //"Greg";
instance2.sayAge(); //27
```
- 原型式继承

> 1. `核心`:先创建了一个临时性的空的构造函数，然后将传入的`对象`作为这个构造函数的原型，最后返回了这个临时类型的一个新实例 ==> 就是 ES5 Object.create 的模拟实现
> 2. 可以不用创建构造函数
```js
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}
//执行: 子类的原型对象 = object(父类的原型对象);
```
- 寄生组合继承法

> 1. 完美的继承方法., 原型式继承方法+借用构造函数拷贝属性 ，原型链上不存在多余的属性
> 2. 核心：继承属性：借用构造函数 ; 继承方法：原型式继承
```js
// 父类构造函数
function Person( uName ){
    this.skills = [ 'php', 'javascript' ];
    this.userName = uName;
}
Person.prototype.showUserName = function(){
    return this.userName;
}
//子类构造函数
function Teacher ( uName ){
    Person.call( this, uName );
}
//空的构造函数
function object( o ){
    var G = function(){};
    G.prototype = o;
    return new G();
} 
// 该函数的意义是将 子类的原型对象  替换成 父类的原型对象
function inheritPrototype( subObj, superObj ){
    var proObj = object( superObj.prototype ); //复制父类superObj的原型对象
    proObj.constructor = subObj; //constructor指向子类构造函数
    subObj.prototype = proObj; //再把这个对象给子类的原型对象
}

inheritPrototype( Teacher, Person );

var oT1 = new Teacher( 'ghostwu' );
oT1.skills.push( 'linux' );
var oT2 = new Teacher( 'ghostwu' );
console.log( oT2.skills ); //php,javascript
console.log( oT2.showUserName() ); //ghostwu
```

### ES6继承
[文档](https://blog.csdn.net/gao_xu_520/article/details/80106671)
- class定义类
    > 写在类里面的方法实际是给其`prototype`（原型对象）里添加方法,定义方法时，前面不用加function。`constructor`方法是类的默认方法，相当于在构造函数内生成属性。
    - 类不存在变量提升,定义在前 使用在后，否则会报错
    - 类必须使用`new`调用，否则会报错
    - class内部只允许定义方法,不允许定义属性,属性定义在`constructor`里
    - `constructor`方法是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。一个类必须有`constructor`方法,如果没有显式定义，一个空的`constructor`方法会被默认添加。
    - 可以通过实例的`__proto__`属性为Class添加方法。但是不建议使用，因为这会改变Class的原始定义，影响到所有实例

- extends继承
    >子类继承了父类，在子类构造函数中必须调用`super`方法。(借用构造函数)。子类的`constructor`方法没有调用`super`之前，不能使用this关键字，否则报错，而放在super方法之后就是正确的。

- 静态方法
    >如果在一个方法前，加上`static`关键字，这就称为"静态方法"。静态方法方法不会被实例继承，而是直接通过类来调用。父类的静态方法，可以被子类继承
```js
class A{
    constructor(x,y){
        this.x = x
        this.y = y
    }
    static C() {
        console.log("CCC")
    }
}
class B extends A {
    constructor(m,x,y){
        super(x,y)
        this.m = m
    }
    static D() {
        console.log("DDD")
    }
    E(){
        console.log("EEE")
    }
}
var a = new B(1,2,3)
console.log(a)
a.E(); B.C(); B.D(); A.C();
// 非静态方法会被实例对象继承，不能再通过类来调用，否则会报错 ==>B.E()
// 静态方法不会被实例对象继承，只能通过类来调用，通过实例对象调用会报错 ==> a.D()
// 父类的静态方法，可以被子类继承,可以通过子类来调用 ==> B.C()
// constructor ==> ES6类的constructor函数相当于ES5的构造函数 , this指实例对象 

```



## 原型链
> 实例对象与Object原型对象之间的链条(`__proto__`)称为原型链
- 构造函数
    - new的四大隐藏步骤 
    >  1. 在构造函数内部声明了一个对象o(在内部隐式调用了new Object() )
    >  2. 将构造函数的this指向上面声明的对象o
    >  3. 给this绑定属性及方法，相当于给对象o绑定
    >  4. 将this对象返回出去
    - this的指向
    >   1. 函数自执行：this指的是执行函数的对象
    >   2. 事件驱动函数:this指的是函数绑定的元素对象
    >   3. new 构造函数()的this指的就是当前实例对象
    - 通过`prototype`指向原型对象
    ```js
    function YiWu(n,m){
        //var o = new Object()
        //YiWu.bind(o)
        this.n = n
        this.m = m
        this.aa = ()=>{
            console.log("aa")
        }
        //return o
    }
    ```
- 原型对象
    > 1. 任何写在原型对象中的属性和方法，都可以让所有实例对象共享
    ```js
    YiWu.prototype.bb = ()=>{
        console.log("bb")
    }
    //(个人理解：就是写在构造函数的prototype上的属性及方法所组成的”对象”)

    //(如果构造函数的某个方法不需要访问构造函数内部的私有属性，那么就可以将这个方法挂载到它的原型链上，原型对象上的某个方法发生了改变，那么所有的实例对象的该方法也随之改变,原型对象上增加了某个方法，所有的实例对象也会随之增加该方法)
    ```
    > 2. 原型对象通过`constructor`(构造器)指向构造函数
- 实例对象
    > 1. 通过`new 构造函数`产生的对象称为实例对象
    > 2. 实例对象能拷贝构造函数的所有属性及方法
    > 3. 实例对象可以使用其原型对象的所有方法
    > 4. 可以通过实例对象获取原型对象 
    ```js
    var C = new YiWu(e,f)
    console.log(C.__proto__)
    // Frefox, Chrome等浏览器通过私有属性获取
    console.log(Object.getPrototypeOf(C))
    // ES5方式去获取
    ```

> 原型搜索机制 : 实例对象属性-->其原型对象-->原型对象的原型对象--...>Object的原型对象 。`如果在Object的原型对象中还搜索不到，则抛出错误`


## 闭包
使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。

闭包有三个特性:

> 函数嵌套函数

> 函数内部可以引用外部的参数和变量

> 参数和变量不会被垃圾回收机制回收 

## 其他

### ajax原理
```js
var request = new XMLHttpRequest(); //  1.新建XMLHttpRequest对象
//4.判断请求响应结果
request.onreadystatechange = function () { // 状态发生变化时，函数被回调
    if (request.readyState === 4) { // 成功完成
        // 判断响应结果:
        if (request.status === 200) {
            // 成功，通过responseText拿到响应的文本:
            return success(request.responseText);
        } else {
            // 失败，根据响应码判断失败原因:
            return fail(request.status);
        }
    } else {
        // HTTP请求还在继续...
    }
}
// 2.选择请求方式及请求地址
request.open('GET', '/api/categories');
//3.发送请求
request.send();

```
### axios原理及其请求拦截机制

### promise及async、await
> 1. 同步 : 阻塞  ; 同步方法调用一旦开始，调用者必须等到方法调用返回后，才能继续后续的行为。
> 2. 异步 : 非阻塞 ; 不需要等待结果，直接执行下一步
#### promise
> promise 是一种承诺

>1. `Promise`主要是为了解决回调地狱问题
>2. `Promise`的实例有三个状态: Pending（进行中）、Resolved（已完成）、Rejected（已拒绝）。当你把一件事情交给promise时，它的状态就是`Pending`，任务完成了状态就变成了`Resolved`、没有完成失败了就变成了`Rejected`。

```js
var data = new Promise((resolve, reject)=>{
    if(1>2){
        reject("123")
        // 失败回调
    }else{
        resolve("456")
        // 成功回调
    }
}).then((res)=>{
    // res是成功回调时传进的参数
    console.log('成功_1：' + res)
    // 在then中return出的值是传递给下一个then的参数
    return "789"
}).then(
    (res)=>{
    console.log('成功_2：' + res)
}).catch((reason) => {
    console.log('失败：' + reason);
})
```
>3. `Promise.all` 与 `Promise.race`
    >- `Promise.all`: 接收一个数组，数组的每一项都是一个promise对象。如果有一个状态变成了rejected，那么Promise.all的状态就会变成rejected（任意一个失败就算是失败）

```js
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
    // 定时器的第三个参数及以后的参数都是作为"resolve"的参数
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});
// 同时执行p1和p2，并在它们都完成后执行then:
Promise.all([p1, p2]).then(function (results) {
    console.log(results); // 获得一个Array: ['P1', 'P2']
});
```
>- `Promise.race` 竞速模式 : 接受一个每一项都是promise的数组。但是与all不同的是，第一个promise对象状态变成resolved时自身的状态变成了resolved，第一个promise变成rejected自身状态就会变成rejected。`第一个变成resolved的promsie的值就会被使用`。
```js
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});
Promise.race([p1, p2]).then(function (result) {
    console.log(result); // 'P1'
});
```
#### async、await
> 主要用`async/await`来发送异步请求，从服务端获取数据，代码非常简洁

- async
>它作为一个关键字放到函数前面，用于表示函数是一个异步函数，因为async就是异步的意思， 异步函数也就意味着该函数的执行不会阻塞后面代码的执行。
- await
>  只有在async函数体内部使用，而且这个作用范围是不可以继承下去的。
>  只有await后面的代码执行完毕才会继续向下执行
```js
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve('done!'), 1000)
    })
    let result = await promise // 直到promise返回一个resolve值（*）
    alert(result) // 'done!' 
}
f()
```

### 垃圾回收机制

> 在JS垃圾回收机制中，如果一个对象不再被引用，那么这个对象就会被垃圾机制回收，如果两个对象相互引用，而不在被第三方引用，那么这两个对象就会被垃圾回收机制回收。

> 垃圾回收机制是为了以防内存泄漏，(内存泄漏: 当已经不需要某块内存时这块内存还存在着),  垃圾回收机制就是间歇的不定期的寻找到不再使用的变量，并释放掉它们所指向的内存。

> JS有两种变量: 全局变量和在函数中产生的局部变量。局部变量的生命周期在函数执行过后就结束了
此时便可将它引用的内存释放（即垃圾回收），但全局变量生命周期会持续到浏览器关闭页面。

> JS执行环境中的垃圾回收器有两种方式：标记清除（mark and sweep）、引用计数(reference counting)。

> - 标记清除:  垃圾收集器给内存中的所有变量都加上标记，然后去掉环境中的变量以及被环境中的变量引用的变量的标记。
在此之后再被加上的标记的变量即为需要回收的变量，因为环境中的变量已经无法访问到这些变量。

> - 引用计数(reference counting):  这种方式常常会引起内存泄漏，低版本的IE使用这种方式。
机制就是跟踪一个值的引用次数，当声明一个变量并将一个引用类型赋值给该变量时该值引用次数加1，
当这个变量指向其他一个时该值的引用次数便减一。当该值引用次数为0时就会被回收。

### localStorage、sessionStorage、Cookie的区别及用法
### 原生节点操作
### git 命令
### rem和px
### 正则
### for循环
[链接](https://www.cnblogs.com/littlewriter/p/6789873.html)
### 常见状态码
> - 200: 请求成功 处理方式: 获得响应的内容，进行处理
> - 304: 请求的资源未更新 处理方式: 丢弃
> - 403: 禁止 处理方式: 丢弃
> - 404: 没有找到 处理方式: 丢弃
> - 500: 服务器内部错误 服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。一般来说，这个问题都会在的源代码出现错误时出现。
> - 503: 服务出错 由于临时的维护或者过载，服务器当前无法处理请求。这个状况是临时的，并且将在一段时间以后恢复。
# jQ部分

## 优点 

- 链式调用
- 隐式迭代
- 完善的ajax
- 有可靠的事件处理机制

## 常用api

### 事件
用`.on()`来为节点添加事件, 用`.off()` 方法移除用`.on()`绑定的事件处理程序
- 鼠标事件
    - click  ==> 点击事件
    - dblclick ==> 双击事件
    - mousedown ==> 鼠标按键按下
    - mouseup ==> 鼠标按键松开
    - mouseover ==> 鼠标移入
    - mouseout ==>鼠标移出
    - mousemove ==> 鼠标移动
    - ...
- 表单事件
    - blur ==> 表单失焦时触发
    - focus ==> 表单聚焦时触发
    - change
    - input 
- 键盘事件
    - keydown ==> 某个键盘按键被按下
    - keyup ==> 某个键盘按键被松开
### 节点操作
- 增
    - append()  ==> A.append(B) 将B追加到A中 追加到A原本部分之后 为A的子元素
    - appendTo() ==> A.appendTo(B) 将A追加到B中
    - prepend() ==> 追加到A原本部分之前
    - prependTo()
    --------------
    - after() ==> A.after(B) 将B加到A元素之后 为A的兄弟元素
    - insertAfter() ==> A.insertAfter(B) 将A加到B元素之后 为A的兄弟元素
    - before() ==> A.before(B) 将A加到B元素之前 为A的兄弟元素
    - insertBefore()
- 删
    - reomve()
- 复制
    - clone()
### 动画效果

### ajax请求


# Vue

> 组件化开发、数据驱动、双向数据绑定;两大核心是`组件系统、数据驱动`

##双向数据绑定原理
> 主要利用的是`Object.defineProperty`来劫持数据(如放入`data`中的值,利用了`for`循环)，其中有`setter`和`getter`方法,结合`发布者-订阅者模式`(在数据变动时发布消息给订阅者，触发相应监听回调。) ,从而实现了双向数据绑定

> vue 3.0 会改用`proxy`来劫持数据，因为`proxy`可以劫持所有数据类型,而`Object.defineProperty`只能劫持基本数据类型

## 组件传值
> 1. 父组件与子组件传值
父组件传给子组件：子组件通过props方法接受数据;
子组件传给父组件：$emit方法传递参数
> 2. 非父子组件间的数据传递，兄弟组件传值
eventBus，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适。（虽然也有不少人推荐直接用VUEX，具体来说看需求咯。技术只是手段，目的达到才是王道。）

## 生命周期钩子
> “钩子” 简单理解就是“到什么时候，做什么事”

> 分为四大步:编译、挂载、更新、销毁
## 过滤器

## 路由
> hash模式 和 history模式

> 1. hash模式 :在浏览器中符号`#`，#以及#后面的字符称之为hash，用`window.location.hash`读取；
> - 特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.xxx.com，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。

> 2. history模式 : history采用`HTML5的新特性`；且提供了两个新方法：`pushState（）、replaceState（）`可以对浏览器历史记录栈进行修改，以及`popState`事件的监听到状态变更。
> - 特点:history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 `http://www.xxx.com/items/id`。后端如果缺少对 `/items/id` 的路由处理，将返回 404 错误。Vue-Router 官网里如此描述：“不过这种模式要玩好，还需要后台配置支持……所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。”

 > - 路由守卫

 > - 路由匹配(嵌套路由、路由重定向)

 > - 路由钩子 : `afterEach`、`beforeEach`(全局钩子)、`beforeEnter `、`beforeLeave`(某一路由独享的钩子)、

## VueX
> `Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式`; 是为了更好的解决 vue 数据传输，比如当多个视图依赖同一个状态或者来自不同视图的行为需要变更同一状态。

> 核心思想 : `所有的状态变更都是由于数据变化引起的`

> - `store` :一个容器，放着所有公共的 `state` ; Vue 组件从 store 中读取状态，相应组件也跟着动态变化；改变 store 的唯一方法是 `commit mutation`，这样可以明确的追踪到状态的变化
> - `state` : 单一状态树，读取方法：计算属性中直接返回 ; mapState（辅助函数）生成计算属性，避免应该一个组件获取多个状态的时候，每个状态都声明为计算属性造成冗余
> - `Getter`: sotre 的计算属性; 当某个属性被多个组件频繁调用的时候，可以用 getter 抽取出来，其它组件直接调用，不需要计算 ; mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性
> - `Mutation` : 唯一改变 store 的计算属性; 有一个字符串的事件类型（type） 和回调函数（handler），回调函数状态更改的地方，并且 state 作为第一个参数; store.commit 的方法调用 mutation; 是同步方法
> - `Action` : Action 提交的mutation，而不是直接变更状态；Action 可以包含任意异步操作；Action 可以通过 store.dispath 方法触发
> - `Module` : 所有状态集中在一起非常臃肿，所以允许 store 分割模块。`modules = { state: { ... }, mutations: { ... }, actions: { ... }, getters: { ... } } `

```js
// 将仓库分离出 => stroe.js ,在main.js中引入、挂载
// 状态管理
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

// 实例化Vuex，创建一个仓库
// 库
const store = new Vuex.Store({
    // 该库存数据的地方
    state: {
        NewsUrl: "", //新闻文章地址 => 新闻详情页
        NewsType: "top",//新闻类别
        MovieId: 0,//电影id => 电影详情页
        MovieType: "in_theaters",//电影类别
    },
    // 修改数据的方法 真正改数据的操作
    mutations: {
        // 修改仓库中state中的NewsUrl
        editNewsUrl(state, url) {
            state.NewsUrl = url
        },
        editNewsType(state, type) {
            state.NewsType = type
        },
        editMovieId(state, id) {
            state.MovieId = id
        },
        editMovieType(state, type) {
            state.MovieType = type
        }
    },
    // 获取数据的方法
    getters: {
        // 获取NewsUrl的方法
        getNewsUrl(state) {
            return state.NewsUrl
        },
        getNewsType(state) {
            return state.NewsType
        },
        getMovieId(state) {
            return state.MovieId
        },
        getMovieType(state) {
            return state.MovieType
        }
    },
    // 异步的方法放这里
    // 触发多个数据的改变才使用
    // 触发mutations，其实就是把刚才commit从组件放出来，换个地方放到actions
    // actions: {
    //     setAuthor(context, data) {
    //         context.commit('editAuthor', data)
    //         // context.commit('editCount')
    //     },
    //     setGallery(context, obj) {
    //         setTimeout(() => {
    //             context.commit('editGallery', obj)
    //         }, 1000)
    //     }
    // }
})
// 暴露store仓库到`main.js`的根容器里面
// console.log(Vuex,store)
export default store
//=在相应的组件里使用vuex(已经在main.js上挂载在了实例上)=====================================================

// 把type存进去仓库里面
      this.$store.commit("editMovieType", "in_theaters");
// 取值
       var type =  this.$store.getters.getNewsType;
```

## 坑
 Q1:在某一组件内定义了某一事件(如下拉刷新事件)，在事件进行但还未完成时，路由跳转使该组件销毁，该下拉刷新事件仍会继续执行，未被销毁 

> 需要在该组件的销毁阶段将该事件手动销毁 `window.removeEventListener` ; 自己写的事件监听也需要销毁`off`。

# React
[文档](https://blog.csdn.net/junjun0501/article/details/81221799)

> 组件系统、单向数据流、操作虚拟DOM、JSX 语法、数据驱动、函数式编程
> 1. react最核心的思想是将页面中任何一个区域或者元素都可以看做一个组件 component
> - 我一般通过es6的class定义类的来声明组件(分治，方便管理，减少耦合、复用，提高效率，性能)


## Redux
> Redux 实现了跨组件通信和逻辑分层

> Redux 试图让 state 的变化变得可预测 : `state 在什么时候，由于什么原因，如何变化`

### 三大原则 

> 1. 单一数据源
> - 所有的状态，保存在一个对象里面

> 2. State 是只读的
> - 唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。

> 3. 使用纯函数来执行修改
> - Reducer 只是一些纯函数，它接收先前的 state 和 action，并返回新的 state。

```js
//写在index.js里并挂载到实例上=============================================
// redux的核心文件
import {createStore} from 'redux';
// 提供对react支持的库
import {Provider} from 'react-redux';
// createStore是帮我们react创建一个存放数据的仓库
// createStore第一个参数是仓库里面的值，都放在state里面
// state,mutation,action,getter (Vue)
// state,action (React)
// createStore第二个参数是action，是触发state更改的函数，|| Vue : 异步放action,触发mutation
// action在react里面就是直接拿来定义更改state的函数
// 所有组件的全局变量，共有数据
// react是没有getters，也没有mutation，getters是用connect配合props来获取值得
let store = createStore((state = {
    author: "lemon",
    age: 19,
    skill: ['ps','css','js']
}, action) => {
    switch (action.type) {
        // 更改state里面的值，获取
        case 'setAuthor':
        // state.author = action.author
        // return state
        // 返回一个新的state，仓库更新了  ==> 返回出去的state会挂在取值组件的props 上
        return {
            // 首先继承原来的state仓库
            ...state,
            // 再更改仓库的author值
            author: action.author
        }
        case 'setAge':
        return {
            // 首先继承原来的state仓库
            ...state,
            // 再更改仓库的age值
            age: action.age
        }
        default:
        return state
    }
})
// 用Provider把整个<App />包裹，那现在整个react项目都可以调用store仓库里面的值  ==> 应该是App组件及其子组件 ？ 
// 把createStore创建的store放到Provider组件的store属性值里面
ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>
, document.getElementById('root'));

// 在组件中调用==================================================
//引入相应组件
import { connent } from 'react-redux'
// 将组件暴露并将store挂载到该组件的props上
export default connent(
    // connect的第一个函数是用来拿仓库的值到该组件的props上
    (state) => {
        console.log(state)
        return state
        //可以只返回需要的数据
    },
    // 第二个参数是创建更改仓库的函数放到该组件的props上 ==>  再在相应的地方调用该方法 ( this.props.aa.bind(this))==> 如果有参数，this.props.aa.bind(this,参数1,参数2...)
    (dispatch) => {
        return {
            //会把aa函数挂载到该组件的props上,this.props.aa()
            aa=() => {
                //依旧注意this的指向
                console.log(this)
                // dispatch的参数是个对象，对应store里面的那个action
                dispatch({
                    // type对应switch里面的case ，会执行相应的操作
                    type: setAge,
                    //传入新值,之前改变this的指向就是为方便拿到数值
                    age: this.state.age
                })

            }
        }
    }
)(Lao)
```

# 微信小程序

# 项目搭建流程 脚手夹命令 组件写法 配置文件
## vue
> 1. 利用脚手架搭建项目文件

全局安装
```bash
npm install -g @vue/cli
```
安装完，会在全局有vue命令
```bash
vue -V
```
创建项目
```bash
vue create weibo
```

定位到该文件夹
```
cd weibo
```

启动服务器
```
npm run serve
```
> 2. 开始编写组件

# Vue与React的生命周期对比
|生命周期|Vue|React|描述|
|-|-|-|-|
|编译前|beforeCreate|-|数据和虚拟DOM和真实DOM都没有|
|编译后|created|constructor|有数据|
|挂载前|beforeMount|componentWillMount|有数据，有虚拟DOM，但没挂载|
|挂载后|mounted|componentDidMount|有数据，有虚拟DOM，有挂载|
|更新前|beforeUpdate|componentWillUpdate|更新数据，并且更新了虚拟DOM，但没挂载|
|更新后|updated|componentDidUpdate|真实DOM更新了|
|销毁前|beforeDestory|-|虚拟DOM销毁了，但真实DOM没销毁|
|销毁后|destoryed|componentWillUnmount|真实DOM销毁了|
||-|shouldComponentUpdate|组件只要更新，就会触发这个生命周期，return 布尔值，为真DOM更新，否则不更新|


# 当不使用VueX及Redux时 , 可用发布订阅者模式替代
>发布/订阅模式就是字面意思：它定义了一种一对多的关系，让多个订阅者同时关注发布者，当发布者状态改变时，会通知所有订阅他的对象

> bus 事件总线
```js
// 在Vue的原型上挂载一个Vue实例
//因为每一个组件（实例）都是通过Vue类来创建的，而我们在Vue类的prototype上挂在了一个bus的属性。
Vue.prototype.bus = new Vue();
```
> emit 发布者
```js
//在methods中定义发布者方法
methods:{
    broadcast: function() { //广播
        this.bus.$emit('change', this.selfContent);
    }
}
```
> on  订阅者
```js
//在mounted（生命周期）中定义订阅者方法
mounted: function () {   //订阅
    var _this = this;
    this.bus.$on('change', function (msg) {    //订阅change事件
        _this.selfContent = msg;
    })
}
```
>创建订阅者本身会消耗内存,订阅消息后,也许,永远也不会有发布,而订阅者始终存在内存中.

# 200代码实现简单的vue

```js
class Vue {
            constructor(props) {
                // 在适当的部分执行生命周期函数

                // 数据和模板都没有 ==> 编译前
                this.beforeCreated = props.beforeCreated;
                this.beforeCreated()
                console.log(props)

                // 这个是Vue实例化的节点 Vue的作用域
                let el = this.$el = document.querySelector(props.el)
                // 获取实例化后，放进来的data
                // 方便在后面监听所有的这些数据
                let data = this.$data = props.data

                // 利用发布订阅模式把M和V  数据劫持和视图编译建立关系   ==> 事件总线
                let watch = this.$watch = new Observer()

                // 数据劫持  M
                // 比较简单的数据劫持，没有考虑到"data中数组"的劫持 
                Object.keys(data).forEach((key) => {
                    this.proxyData(key)
                })
                // 视图编译  V
                this.compile(el)

                //生命周期 ==> 挂载后
                this.mounted = props.mounted
                this.mounted()
            }
            // 遍历整个对象，并对所有的数据进行一次劫持
            proxyData(key) {
                let self = this
                // 在这里Vue选择劫持整个实例化后的对象，而非this.$data
                Object.defineProperty(self, key, {
                    // 数据一旦变动，我们触发了set的回调，视图就会发生改变
                    // 响应数据的改变触发对应的set和get完成对应逻辑
                    set(newValue) {
                        // 一旦值改变this.$data的值也响应改变
                        self.$data[key] = newValue;
                        console.log("值发生了更改", newValue)
                        // 发布者
                        this.$watch.emit(key, null)
                    },
                    get() {
                        console.log("我查看了该值")
                        return self.$data[key]
                    }
                })
            }
            // 编译模板
            // 就是把所有的el节点下的{{name}} v-for给编译解析，
            // {{name}} ===> laoyao
            compile(el) {
                let nodes = el.childNodes
                for (let node of nodes) {
                    // console.log(node)
                    // 区分文本节点还是元素节点
                    switch (node.nodeType) {
                        // 处理元素节点
                        case 1:
                            // 判断该节点是否有v-model这个属性值
                            if (node.hasAttribute('v-m')) {
                                let attrVal = node.getAttribute('v-m')
                                node.value = this[attrVal]
                                // 监听输入事件
                                node.addEventListener("input", () => {
                                    // 把v-model="name"  的 name值获取回来

                                    // 获取输入框的值
                                    // node.value = this[attrVal];
                                    this[attrVal] = node.value;
                                    // node.removeAttribute('v-m')
                                    console.log(attrVal)
                                    return () => {
                                        // 更新name的值，并把值放进this.name
                                        this[attrVal] = node.value
                                    }
                                })
                            } else if (node.hasAttribute('v-h')) {
                                let attrVal = node.getAttribute('v-h')
                                node.innerHTML = this[attrVal]
                            } else if (node.hasAttribute('v-f')) {
                                let attrVal = node.getAttribute('v-h')
                                node.innerHTML = this[attrVal]
                            }
                        // this.compileElement(node)
                        // 处理文本节点
                        case 3:
                            this.compileText(node, 'textContent')

                    }
                }
            }
            // 处理文本节点函数
            compileText(node, type) {
                let self = this;
                let reg = /\{\{((?:.|\r?\n)+?)\}\}/g;
                let txt = node.textContent
                console.log(txt)
                // 把所有的{{xxxx}}取出来xxxx
                // node.textContent = this[value]
                if (reg.test(txt)) {
                    // {{name}}  ->  laoyao
                    node.textContent = txt.replace(reg, (matched, value) => {
                        // 监听者，监听来自set回调函数的发布
                        this.$watch.on(value, () => {
                            node.textContent = self.$data[value]
                        })
                        console.log(matched, value)

                        // 监听者
                        return this[value]
                    })

                }
            }
        }
        //事件总线
        class Observer {
            constructor() {
                // 空的队列
                // 事件队列，发布者和订阅者的供需关系来去决定去向
                this.list = {
                    // 'eat':[()=>{
                    //     console.log('eat')
                    // }]
                }
            }
            // 监听 订阅者
            on(key, fn) {
                if (!this.list[key]) {
                    this.list[key] = [];
                }
                this.list[key].push(fn);
            }
            // 触发 发布者
            emit(key, params) {
                // 把所有存着回调函数的数组给取出来
                let fns = this.list[key];
                // 如果数组队列为空，则返回
                if (!fns || fns.length === 0) {
                    return false;
                }
                // 如果不为空，我就遍历所有的函数执行
                fns.forEach(fn => {
                    fn(params);
                });
            }
        }

        let vm = new Vue({
            el: "#demo",
            data: {
                name: "lemon",
                html: `<p style='color:red'>123</p>`
            },
            created() {

            },
            beforeCreated() {

            },
            mounted() {
                console.log("挂载之后")
                this.name = "laoxie"
            }
        })

        console.log(vm)
```

# 人事部分