## ES

[TOC]

## 6字符串: 

### 子串的识别

ES6 之前判断字符串是否包含子串，用 indexOf 方法，ES6 新增了子串的识别方法。

- **includes()**：返回布尔值，判断是否找到参数字符串。
- **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。

以上三个方法都可以接受两个参数，需要搜索的字符串，和可选的搜索起始位置索引。

let string = "apple,banana,orange"; string.includes("banana");     // true string.startsWith("apple");    // true string.endsWith("apple");      // false string.startsWith("banana",6)  // true

**注意点：**

- 这三个方法只返回布尔值，如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 。
- 这三个方法如果传入了正则表达式而不是字符串，会抛出错误。而 indexOf 和 lastIndexOf 这两个方法，它们会将正则表达式转换为字符串并搜索它。

### 字符串重复

repeat()：返回新的字符串，表示将字符串重复指定次数返回。

```
console.log("Hello,".repeat(2));  // "Hello,Hello,"
```

如果参数是小数，向下取整

```
console.log("Hello,".repeat(3.2));  // "Hello,Hello,Hello,"
```

如果参数是 0 至 -1 之间的小数，会进行取整运算，0 至 -1 之间的小数取整得到 -0 ，等同于 repeat 零次

```
console.log("Hello,".repeat(-0.5));  // "" 
```

如果参数是 NaN，等同于 repeat 零次

```
console.log("Hello,".repeat(NaN));  // "" 
```

如果参数是负数或者 Infinity ，会报错:

```
console.log("Hello,".repeat(-1));  
// RangeError: Invalid count value

console.log("Hello,".repeat(Infinity));  
// RangeError: Invalid count value
```

如果传入的参数是字符串，则会先将字符串转化为数字

```
console.log("Hello,".repeat("hh")); // ""
console.log("Hello,".repeat("2"));  // "Hello,Hello,"
```

### 字符串补全

- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

```
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"
```

如果指定的长度小于或者等于原字符串的长度，则返回原字符串:

```
console.log("hello".padStart(5,"A"));  // "hello"
```

如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

```
console.log("hello".padEnd(10,",world!"));  // "hello,worl"
```

常用于补全位数：

```
console.log("123".padStart(10,"0"));  // "0000000123"
```

### 模板字符串

模板字符串相当于加强版的字符串，用反引号 **`**,除了作为普通字符串，还可以用来定义多行字符串，还可以在字符串中加入变量和表达式。

**基本用法**

普通字符串

```
let string = `Hello'\n'world`; console.log(string);  // "Hello' // 'world"
```

多行字符串:

```
let string1 =  `Hey, can you stop angry now?`;
console.log(string1); // Hey, 
// can you stop angry now?
```

字符串插入变量和表达式。

变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式。

```
let name = "Mike"; 
let age = 27; 
let info = `My Name is ${name},I am ${age+1} years old next year.` console.log(info); 
// My Name is Mike,I am 28 years old next year.
```

字符串中调用函数：

```
function f(){  
	return "have fun!"; 
} 
let string2= `Game start,${f()}`;
console.log(string2);  // Game start,have fun!
```

**注意要点**

模板字符串中的换行和空格都是会被保留的

```
innerHtml = `<ul>
	<li>menu</li>  
	<li>mine</li> </ul> `
; 
console.log(innerHtml); // 输出 
<ul> 
	<li>menu</li> 
	<li>mine</li> 
</ul>
```



### 标签模板

标签模板，是一个函数的调用，其中调用的参数是模板字符串。

```
alert`Hello world!`;
// 等价于 
alert('Hello world!');
```

当模板字符串中带有变量，会将模板字符串参数处理成多个参数。

function f(stringArr,...values){ let result = ""; for(let i=0;i<stringArr.length;i++){  result += stringArr[i];  if(values[i]){   result += values[i];        }    } return result; } let name = 'Mike'; let age = 27; f`My Name is ${name},I am ${age+1} years old next year.`; // "My Name is Mike,I am 28 years old next year."  f`My Name is ${name},I am ${age+1} years old next year.`; // 等价于 f(['My Name is',',I am ',' years old next year.'],'Mike',28);

**应用**

过滤 HTML 字符串，防止用户输入恶意内容。

function f(stringArr,...values){ let result = ""; for(let i=0;i<stringArr.length;i++){  result += stringArr[i];   if(values[i]){     result += String(values[i]).replace(/&/g, "&amp;")               .replace(/</g, "&lt;")               .replace(/>/g, "&gt;");    } } return result; } name = '<Amy&MIke>'; f`<p>Hi, ${name}.I would like send you some message.</p>`; // <p>Hi, &lt;Amy&amp;MIke&gt;.I would like send you some message.</p>

**国际化处理（转化多国语言）**

i18n`Hello ${name}, you are visitor number ${visitorNumber}.`;   // 你好**，你是第**位访问者