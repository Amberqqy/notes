# 学习ES6  
## ES6 就是ECMAScript 6是新版本JavaScript语言的标准。一直在更新中。  

### ES6开发环境的搭建  

1. 先建立一个项目的工程目录，并在目录下边建立两个文件夹：src和dist。  
> src：书写ES6代码的文件夹，写的js程序都放在这里。  
> dist：利用Babel编译成的ES5代码的文件夹，在HTML页面需要引入的时这里的js文件。  

2. 新建index.html文件，并在文件中引用dist文件下的index.js代码，代码如下：  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>学习es6</title>
    <script src="./dist/index.js"></script>
</head>
<body>
    Hello QQY ES6
</body>
</html>
```  
```
let a = 1;
console.log(a);

```  

3. 初始化项目  
打开终端，先用`npm init -y`初始化项目，然后就会在项目根目录下产生package.json文件，如下显示（默认值）：  
```
{
  "name": "es6",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```  

4. 全局安装Babel-cli  
终端上输入命令： `npm install -g babel-cli`  
尝试输入： `babel src/index.js -o dist/index.js`, 就会在dist文件夹下发现index.js。  

5. 如果在index.js中代码没有传过来，就本地安装babel-preset-es2015 和 babel-cli。
`npm install --save-dev babel-preset-es2015 babel-cli`    
并新建文件.babelrc,并写入代码：  
```
{
    "presets":[
        "es2015"
    ],
    "plugins":[]
}
```  
再次尝试输入： `babel src/index.js -o dist/index.js`即可。

6. 在package.json文件的scripts加上  
`"bulid": "webpack --mode development"`,即可使用npm run bulid 命令进行打包，然后`live-server`即可在浏览器中打开练习网页。  

### 新的声明方式  

三种声明：  
> var: es6中升级全局变量，var定义的变量可以修改，如果不初始化会输出undefined，不会报错。  
> let: 局部声明，let声明只在区块内起作用，外部不可以调用，好处就是防止数据污染。
> const: 声明常量，const定义的变量不可以修改，而且必须初始化。  

### 变量的解析赋值

1. 数组模式和赋值模式统一，如：`let [a,[b,c],d] = [1,[2,3],4];` 如果形式不一样。有可能获得undefined或者直接报错。  
2. 解析赋值允许使用默认值。  
3. 不仅可以用于数组，还可以用于对象。 
4. 对于圆括号的使用：如果解析前先定义了变量，在解析的时候得在解析语句外面加上圆括号。 
5. 字符串的解析：字符串将会被转换成了一个类似数组的对象。
> 注意： 对象的解析和数组的解析有一个重要的不同，数组的元素是按照次序排列的，变量的取值是由它的位置决定，而对象的属性是没有次序的，变量必须与属性同名，这样才能取到正确的值。  

### 扩展运算符和rest运算符（...）  

1. 当我们编写一个方法时，允许它传入的参数是不确定的。这就可以用对象扩展运算符来作参数： 如举例:  
```
function haha(...arg){
    console.log(arg[0]);//1
    console.log(arg[1]);//3
    console.log(arg[2]);//5
}
haha(1,3,5)
```  
再有一个例子： 
```
let arr1=['哈哈','qqy','欧耶'];
let arr2=arr1;
console.log(arr2);// ["哈哈", "qqy", "欧耶"]
arr2.push('新增');
console.log(arr1);// ["哈哈", "qqy", "欧耶", "新增"]
```
这样显示的结果表明我们在改变arr2的值时，arr1的值也被改变了。这不是我所想要的，这是对内存堆栈的引用，而不是真正的赋值。所以可以用到对象扩展运算符。如下显示：  
```
let arr1=['哈哈','qqy','欧耶'];
//let arr2=arr1;
let arr2=[...arr1];
console.log(arr2); //["哈哈", "qqy", "欧耶"]
arr2.push('新增');
console.log(arr2);//  ["哈哈", "qqy", "欧耶", "新增"]
console.log(arr1);// ["哈哈", "qqy", "欧耶"]
```  
2. 如何循环输出rest运算符（用for...of循环来进行）。
```
function qqy(first,...arg){
    for(let val of arg){
        console.log(val);//1 2 3 4 5 6 7
    }
}
qqy(0,1,2,3,4,5,6,7); 
``` 
### 字符串模板  
> 模板用连接号``来包括，且引用变量用${***}的形式插入即可。  
```
let my='美少女战士';
let blog = `非常高兴，我是你的老朋友${my}。学习字符串模版。`;
document.write(blog);
```  
**对运算符也支持：**   
```
let a=1;
let b=2;
let result=`${a+b}`;
document.write(result);//3
```  
**字符串的查找：**  
> indexof():（es5）返回所在位置长度；  
> includes():返回true(字符串存在) or false（字符串不存在）;  
> startsWith():判断开头是否存在  
> endsWith():判断结尾是否存在  

### es6数字操作  

1. 二进制声明：二进制的开始是0（零），然后第二个位置是b（注意这里大小写都可以实现），然后跟上二进制的值就可以了。
```
let binary = 0B010101;
console.log(binary);//21
```
2. 八进制声明：以0（零）开始的，然后第二个位置是O（欧），然后跟上八进制的值就可以了。
```
let octa=0o666;
console.log(b);//438
```  
**数字判断和转换**  

> 1. Number.isFinite()来进行数字验证，只要是数字，不论是浮点型还是整形都会返回true，其他时候会返回false。  
> 2. NaN是特殊的非数字，可以使用Number.isNaN()来进行验证。下边的代码控制台返回了true。`console.log(Number.isNaN(NaN));`  
> 3. 判断是否为整数Number.isInteger(xx)  
> 4. 整数转换Number.parseInt(xxx)  
> 5. 浮点型转换Number.parseFloat(xxx)  
> 6. 整数取值范围操作： 最大安全整数 `Number.MAX_SAFE_INTEGER`;最小安全整数 `Number.MIN_SAFE_INTEGER`
> 7. 安全整数判断isSafeInteger( )  
```
let m= Math.pow(2,53)-1;//取值范围：2的53次方
console.log(Number.isSafeInteger(m));//true
```  

### es6中新增的数组知识  

1. Array.from();
```
let  json = {
    '0': 'hi',
    '1': '你好',
    '2': '好好学习',
    length:3
}
 
let arr=Array.from(json);
console.log(arr)//  ["hi", "你好", "好好学习"]
```
将json代码转换成数组。  

2. Array.of()，负责把一堆文本或者变量（字符串也可以）转换成数组。 
```
let arr =Array.of(3,4,5,6);
console.log(arr);//[3, 4, 5, 6]
```  

3. find()实例方法：(在一个已知数组中查找)
参数：  
> value：表示当前查找的值。
> index：表示当前查找的数组索引。 
> arr：表示当前数组。  
```
let arr=[1,2,3,4,5,6,7,8,9];
console.log(arr.find(function(value,index,arr){
    return value > 1;//控制台上输出的是2
}))
```
在函数中如果找到符合条件的数组元素就进行return，并停止查找。如果找不到会显示undefined。  

4. fill()实例方法：(作用就是把数组进行填充)  
参数：  
> 第一个参数：填充的变量；  
> 第二个参数：开始填充的位置；从0开始计数  
> 第三个参数：填充到的位置；从1开始计数   
```
let arr=[0,1,2,3,4,5,6,7,8,9];
arr.fill('hi',2,5);
console.log(arr);
```  
把数组从第二位到第五位用hi进行填充。

5. 数组遍历：for...of循环。  
**for...of数组索引：**  
```
let k =['lala','Hi好','biubiu'];
for(let index of k.keys()){
    console.log(index)//0 1 2
}
```  
控制台输出0,1,2，输出数组的索引。  

**同时输出数组的内容和索引（entries()）**  
```
let k =['lala','Hi好','biubiu'];
for(let [index,val] of k.entries()){
    console.log(index)//0 1 2
    console.log(val)//lala Hi好 biubiu
}
``` 
控制台输出数组的索引和内容。

6. entries( )实例方法：  
entries()实例方式生成的是Iterator形式的数组，这种形式的数组好处就是可以让我们在需要时用next()手动跳转到下一个值。  
```
let arr =['lala','Hi好','biubiu'];
let list=arr.entries();
console.log(list.next().value);//[0,"lala"]
console.log(list.next().value);//[1, "Hi好"]
console.log(list.next().value);//[2, "biubiu"]
```

### es6中的箭头函数和拓展  

> 1. 箭头函数就是没有function关键字，而是一个类似箭头（=>）的函数。  
> 2. 箭头函数作为匿名函数,是不能作为构造函数的,不能使用new。   
> 3. 箭头函数不绑定arguments,取而代之用rest参数（…）解决。  
> 4. **箭头函数本没有this，绑定后不再多变**  
> 5. 根据上级的function中的this来做绑定,如果上级也是箭头函数，再上级查找，绑定以后就不再发生改变了,this不再多变。  
> 6. 箭头函数没有原型属性，箭头函数不能当做Generator函数,不能使用yield关键字。 
> 7. 箭头函数不能换行。如果在箭头函数中，方法体内如果是两句话，那就需要在方法体外边加上{}括号。  

**this指向的总结：**  

1. 箭头函数的this永远指向其上下文的 this，任何方法都改变不了其指向，如call(), bind(), apply()
2. 普通函数的this指向调用它的那个对象。  

### es6 数组的用法  

**in的用法：**in是用来判断对象或者数组中是否存在某个值的。
  
```
let obj={
    a:'haha',
    b:'have',
    c: ''
}
console.log('a' in obj);  //true
console.log('c' in obj);  //false
```  

**数组的遍历方法**  

1. **forEach**  
```
let oo =['ko','lplp','嘻嘻'];
oo.forEach((val,index)=>console.log(index,val))
//0 "ko"
//1 "lplp"
//2 "嘻嘻"
```
forEach循环的特点是会自动省略为空的数组元素，相当于直接给我们筛空了。  

2. **filter**,**some**,**map(起到一个替代的作用)**  
```
let oo =['ko','lplp','嘻嘻'];
oo.filter(l=>console.log(l))
oo.some(l=>console.log(l))
//ko
// lplp
// 嘻嘻
```  

**数组转换成字符串**  

1. **join（）方法**   
```
let oo =['ko','lplp','嘻嘻'];
console.log(oo.join())//ko,lplp,嘻嘻
```  
join()方法就是在数组元素中间，加了一些间隔:  
  
`console.log(oo.join('|'))//ko|lplp|嘻嘻`

2. **toString方法**  
```
let oo =['ko','lplp','嘻嘻'];
console.log(oo.toString())//ko,lplp,嘻嘻
```  

### es6中的对象  

**对象赋值**  

```
let name="qqy";
let skill= 'web';
var obj= {name,skill};
console.log(obj); //{name: "qqy", skill: "web"}
``` 

**对象Key值构建**  
```
let key='skill';
var obj={
    [key]:'web'
}
console.log(obj.skill);//web  
```
我们从后台取出key值，就可以运用这种[]形式的做法进行对象的构建。  

**自定义对象使用**  
```
var koko={
    ki:function(a,b){
        return a+b;
    }
}
console.log(koko.ki(1,6))//7
```

**Object.is()对象比较**  
```
var obj1 = {name:'哈哈'};
var obj2 = {name:'哈哈'};
console.log(+0 === -0);  //true 
console.log(NaN === NaN ); //false
console.log(Object.is(+0,-0)); //false
console.log(Object.is(NaN,NaN)); //true
console.log(Object.is(obj1.name,obj2.name)); //true
```
'==='是完全等于，数据和类型完全一致，则相等。  
'Object.is()'其行为与===基本一致，不过有两处不同：  
1. +0不等于-0。  
2. NaN等于自身。

**Object.assign()**  
```
var a={a:'wo'};
var b={b:'学习'};
var c={c:'web'};
 
let d=Object.assign(a,b,c)
console.log(d);//{a: "wo", b: "学习", c: "web"}
```  

### Symbol在对象中的运用  

Symbol,它的意思是全局标记。  
声明：`var s = Symbol()` 
```
var obja = { name: 'qqy', skill: 'web' };
var age = Symbol();
obja[age] = 18;
for (var item in obja) {
    console.log(obja[item]);//qqy web
}
console.log(obja);{ name: 'qqy', skill: 'web',age: '18' }
```












