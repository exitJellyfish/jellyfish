# JavaScript基础知识总结

## 1. JavaScript简介

- JavaScript 最开始是专门为浏览器设计的一门语言，但是现在也被用于很多其他的环境。
- 如今，JavaScript 已经成为了与 HTML/CSS 完全集成的，使用最广泛的浏览器语言。
- 有很多其他的语言可以被“编译”成 JavaScript，这些语言还提供了更多的功能。建议最好了解一下这些语言，至少在掌握了 JavaScript 之后大致的了解一下。

## 2. 变量

我们可以使用 var、let 或 const 声明变量来存储数据。

- let — 现代的变量声明方式。
- var — 老旧的变量声明方式。一般情况下，我们不会再使用它。但是，我们会在 旧时的 "var" 章节介绍 var 和 let 的微妙差别，以防你需要它们。
- const — 类似于 let，但是变量的值无法被修改。

变量应当以一种容易理解变量内部是什么的方式进行命名。

## 3. 数据类型

JavaScript 中有八种基本的数据类型（译注：前七种为基本数据类型，也称为原始类型，而 object 为复杂数据类型）。

- number 用于任何类型的数字：整数或浮点数，在 ±(253-1) 范围内的整数。
- bigint 用于任意长度的整数。
- string 用于字符串：一个字符串可以包含 0 个或多个字符，所以没有单独的单字符类型。
- boolean 用于 true 和 false。
- null 用于未知的值 —— 只有一个 null 值的独立类型。
- undefined 用于未定义的值 —— 只有一个 undefined 值的独立类型。
- symbol 用于唯一的标识符。
- object 用于更复杂的数据结构。

我们可以通过 typeof 运算符查看存储在变量中的数据类型。

- 两种形式：typeof x 或者 typeof(x)。
- 以字符串的形式返回类型名称，例如 "string"。
- typeof null 会返回 "object" —— 这是 JavaScript 编程语言的一个错误，实际上它并不是一个 object。

## 4. 类型转换

有三种常用的类型转换：转换为 string 类型、转换为 number 类型和转换为 boolean 类型。

字符串转换 —— 转换发生在输出内容的时候，也可以通过 String(value) 进行显式转换。原始类型值的 string 类型转换通常是很明显的。

数字型转换 —— 转换发生在进行算术操作时，也可以通过 Number(value) 进行显式转换。

数字型转换遵循以下规则：

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b53a298c6bb246999509c66a641cee97~tplv-k3u1fbpfcp-watermark.image)

布尔型转换遵循以下规则：布尔型转换 —— 转换发生在进行逻辑操作时，也可以通过 Boolean(value) 进行显式转换。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7d74bbe5e61a4e5896b762fe2e03eb24~tplv-k3u1fbpfcp-watermark.image)

对 undefined 进行数字型转换时，输出结果为 NaN，而非 0。上述的大多数规则都容易理解和记忆。人们通常会犯错误的值得注意的例子有以下几个：

- 对 "0" 和只有空格的字符串（比如：" "）进行布尔型转换时，输出结果为 true。

## 5. 值的比较

- 比较运算符始终返回布尔值。
- 字符串的比较，会按照“词典”顺序逐字符地比较大小。
- 当对不同类型的值进行比较时，它们会先被转化为数字（不包括严格相等检查）再进行比较。
- 在非严格相等 == 下，null 和 undefined 相等且各自不等于任何其他的值。
- 在使用 > 或 < 进行比较时，需要注意变量可能为 null/undefined 的情况。比较好的方法是单独检查变量是否等于 null/undefined。

## 6. 空值合并运算符 '??'

- 空值合并运算符 ?? 提供了一种从列表中选择第一个“已定义的”值的简便方式。

它被用于为变量分配默认值：

```
// 当 height 的值为 null 或 undefined 时，将 height 的值设置为 100
height = height ?? 100;
复制代码
```

- ?? 运算符的优先级非常低，仅略高于 ? 和 =，因此在表达式中使用它时请考虑添加括号。
- 如果没有明确添加括号，不能将其与 || 或 && 一起使用。

## 7. 循环：while 和 for

我们学习了三种循环：

- while —— 每次迭代之前都要检查条件。
- do..while —— 每次迭代后都要检查条件。
- for (;;) —— 每次迭代之前都要检查条件，可以使用其他设置。

通常使用 while(true) 来构造“无限”循环。这样的循环和其他循环一样，都可以通过 break 指令来终止。

如果我们不想在当前迭代中做任何事，并且想要转移至下一次迭代，那么可以使用 continue 指令。

break/continue 支持循环前的标签。标签是 break/continue 跳出嵌套循环以转到外部的唯一方法。

## 8. 函数

函数声明方式如下所示：

```
function name(parameters, delimited, by, comma) {
  /* code */
}
复制代码
```

- 作为参数传递给函数的值，会被复制到函数的局部变量。
- 函数可以访问外部变量。但它只能从内到外起作用。函数外部的代码看不到函数内的局部变量。
- 函数可以返回值。如果没有返回值，则其返回的结果是 undefined。

为了使代码简洁易懂，建议在函数中主要使用局部变量和参数，而不是外部变量。

与不获取参数但将修改外部变量作为副作用的函数相比，获取参数、使用参数并返回结果的函数更容易理解。

函数命名：

- 函数名应该清楚地描述函数的功能。当我们在代码中看到一个函数调用时，一个好的函数名能够让我们马上知道这个函数的功能是什么，会返回什么。
- 一个函数是一个行为，所以函数名通常是动词。
- 目前有许多优秀的函数名前缀，如 create…、show…、get…、check… 等等。使用它们来提示函数的作用吧。

## 9. 函数表达式

- 函数是值。它们可以在代码的任何地方被分配，复制或声明。
- 如果函数在主代码流中被声明为单独的语句，则称为“函数声明”。
- 如果该函数是作为表达式的一部分创建的，则称其“函数表达式”。
- 在执行代码块之前，内部算法会先处理函数声明。所以函数声明在其被声明的代码块内的任何位置都是可见的。
- 函数表达式在执行流程到达时创建。

在大多数情况下，当我们需要声明一个函数时，最好使用函数声明，因为函数在被声明之前也是可见的。这使我们在代码组织方面更具灵活性，通常也会使得代码可读性更高。

所以，仅当函数声明不适合对应的任务时，才应使用函数表达式。

## 10. 箭头函数，基础知识

对于一行代码的函数来说，箭头函数是相当方便的。它具体有两种：

1. 不带花括号：(...args) => expression — 右侧是一个表达式：函数计算表达式并返回其结果。
2. 带花括号：(...args) => { body } — 花括号允许我们在函数中编写多个语句，但是我们需要显式地 return 来返回一些内容。

## 11. 对象

对象是具有一些特殊特性的关联数组。

它们存储属性（键值对），其中：

- 属性的键必须是字符串或者 symbol（通常是字符串）。
- 值可以是任何类型。

我们可以用下面的方法访问属性：

- 点符号: obj.property。
- 方括号 obj["property"]，方括号允许从变量中获取键，例如 obj[varWithKey]。

其他操作：

- 删除属性：delete obj.prop。
- 检查是否存在给定键的属性："key" in obj。
- 遍历对象：for(let key in obj) 循环。

我们在这一章学习的叫做“普通对象（plain object）”，或者就叫对象。

JavaScript 中还有很多其他类型的对象：

- Array 用于存储有序数据集合，
- Date 用于存储时间日期，
- Error 用于存储错误信息。
- ……等等。

它们有着各自特别的特性，我们将在后面学习到。有时候大家会说“Array 类型”或“Date 类型”，但其实它们并不是自身所属的类型，而是属于一个对象类型即 “object”。它们以不同的方式对 “object” 做了一些扩展。

## 12. 对象引用和复制

对象通过引用被赋值和拷贝。换句话说，一个变量存储的不是“对象的值”，而是一个对值的“引用”（内存地址）。因此，拷贝此类变量或将其作为函数参数传递时，所拷贝的是引用，而不是对象本身。

所有通过被拷贝的引用的操作（如添加、删除属性）都作用在同一个对象上。

为了创建“真正的拷贝”（一个克隆），我们可以使用 Object.assign 来做所谓的“浅拷贝”（嵌套对象被通过引用进行拷贝）或者使用“深拷贝”函数，例如 [_.cloneDeep(obj)](https://link.juejin.cn/?target=https%3A%2F%2Flodash.com%2Fdocs%23cloneDeep)。

## 13. 对象方法，"this"

- 存储在对象属性中的函数被称为“方法”。
- 方法允许对象进行像 object.doSomething() 这样的“操作”。
- 方法可以将对象引用为 this。
- this 的值是在程序运行时得到的。
- 一个函数在声明时，可能就使用了 this，但是这个 this 只有在函数被调用时才会有值。
- 可以在对象之间复制函数。
- 以“方法”的语法调用函数时：object.method()，调用过程中的 this 值是 object。

请注意箭头函数有些特别：它们没有 this。在箭头函数内部访问到的 this 都是从外部获取的。

## 14. 可选链 "?."

可选链 ?. 语法有三种形式：

1. obj?.prop —— 如果 obj 存在则返回 obj.prop，否则返回 undefined。
2. obj?.[prop] —— 如果 obj 存在则返回 obj[prop]，否则返回 undefined。
3. obj.method?.() —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。

正如我们所看到的，这些语法形式用起来都很简单直接。?. 检查左边部分是否为 null/undefined，如果不是则继续运算。

?. 链使我们能够安全地访问嵌套属性。

但是，我们应该谨慎地使用 ?.，仅在当左边部分不存在也没问题的情况下使用为宜。以保证在代码中有编程上的错误出现时，也不会对我们隐藏。

## 15. Symbol 类型

Symbol 是唯一标识符的基本类型

Symbol 是使用带有可选描述（name）的 Symbol() 调用创建的。

Symbol 总是不同的值，即使它们有相同的名字。如果我们希望同名的 Symbol 相等，那么我们应该使用全局注册表：Symbol.for(key) 返回（如果需要的话则创建）一个以 key 作为名字的全局 Symbol。使用 Symbol.for 多次调用 key 相同的 Symbol 时，返回的就是同一个 Symbol。

Symbol 有两个主要的使用场景：

1. “隐藏” 对象属性。 如果我们想要向“属于”另一个脚本或者库的对象添加一个属性，我们可以创建一个 Symbol 并使用它作为属性的键。Symbol 属性不会出现在 for..in 中，因此它不会意外地被与其他属性一起处理。并且，它不会被直接访问，因为另一个脚本没有我们的 symbol。因此，该属性将受到保护，防止被意外使用或重写。

因此我们可以使用 Symbol 属性“秘密地”将一些东西隐藏到我们需要的对象中，但其他地方看不到它。

1. JavaScript 使用了许多系统 Symbol，这些 Symbol 可以作为 Symbol.* 访问。我们可以使用它们来改变一些内置行为。例如，在本教程的后面部分，我们将使用 Symbol.iterator 来进行 [迭代](https://link.juejin.cn/?target=https%3A%2F%2Fzh.javascript.info%2Fiterable) 操作，使用 Symbol.toPrimitive 来设置 [对象原始值的转换](https://link.juejin.cn/?target=https%3A%2F%2Fzh.javascript.info%2Fobject-toprimitive) 等等。

从技术上说，Symbol 不是 100% 隐藏的。有一个内置方法 [Object.getOwnPropertySymbols(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FgetOwnPropertySymbols) 允许我们获取所有的 Symbol。还有一个名为 [Reflect.ownKeys(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FReflect%2FownKeys) 的方法可以返回一个对象的 所有 键，包括 Symbol。所以它们并不是真正的隐藏。但是大多数库、内置方法和语法结构都没有使用这些方法。

## 16. 数字类型

要写有很多零的数字：

- 将 "e" 和 0 的数量附加到数字后。就像：123e6 与 123 后面接 6 个 0 相同。
- "e" 后面的负数将使数字除以 1 后面接着给定数量的零的数字。例如 123e-6 表示 0.000123（123 的百万分之一）。

对于不同的数字系统：

- 可以直接在十六进制（0x），八进制（0o）和二进制（0b）系统中写入数字。
- parseInt(str，base) 将字符串 str 解析为在给定的 base 数字系统中的整数，2 ≤ base ≤ 36。
- num.toString(base) 将数字转换为在给定的 base 数字系统中的字符串。

要将 12pt 和 100px 之类的值转换为数字：

- 使用 parseInt/parseFloat 进行“软”转换，它从字符串中读取数字，然后返回在发生 error 前可以读取到的值。

小数：

- 使用 Math.floor，Math.ceil，Math.trunc，Math.round 或 num.toFixed(precision) 进行舍入。
- 请确保记住使用小数时会损失精度。

更多数学函数：

- 需要时请查看 [Math](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FMath) 对象。这个库很小，但是可以满足基本的需求。

## 17. 字符串

- 有 3 种类型的引号。反引号允许字符串跨越多行并可以使用 ${…} 在字符串中嵌入表达式。
- JavaScript 中的字符串使用的是 UTF-16 编码。
- 我们可以使用像 \n 这样的特殊字符或通过使用 \u... 来操作它们的 unicode 进行字符插入。
- 获取字符时，使用 []。
- 获取子字符串，使用 slice 或 substring。
- 字符串的大/小写转换，使用：toLowerCase/toUpperCase。
- 查找子字符串时，使用 indexOf 或 includes/startsWith/endsWith 进行简单检查。
- 根据语言比较字符串时使用 localeCompare，否则将按字符代码进行比较。

还有其他几种有用的字符串方法：

- str.trim() —— 删除字符串前后的空格 (“trims”)。
- str.repeat(n) —— 重复字符串 n 次。
- ……更多内容细节请参见 [手册](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FString)。

## 18. 数组

数组是一种特殊的对象，适用于存储和管理有序的数据项。

- 声明:

  // 方括号 (常见用法) let arr = [item1, item2...];

  // new Array (极其少见) let arr = new Array(item1, item2...);

调用 new Array(number) 会创建一个给定长度的数组，但不含有任何项。

- length 属性是数组的长度，准确地说，它是数组最后一个数字索引值加一。它由数组方法自动调整。
- 如果我们手动缩短 length，那么数组就会被截断。

我们可以通过下列操作以双端队列的方式使用数组：

- push(...items) 在末端添加 items 项。
- pop() 从末端移除并返回该元素。
- shift() 从首端移除并返回该元素。
- unshift(...items) 从首端添加 items 项。

遍历数组的元素：

- for (let i=0; i<arr.length; i++) — 运行得最快，可兼容旧版本浏览器。
- for (let item of arr) — 现代语法，只能访问 items。
- for (let i in arr) — 永远不要用这个。

比较数组时，不要使用 == 运算符（当然也不要使用 > 和 < 等运算符），因为它们不会对数组进行特殊处理。它们通常会像处理任意对象那样处理数组，这通常不是我们想要的。

但是，我们可以使用 for..of 循环来逐项比较数组。

## 19. 数组方法

数组方法备忘单：

- 添加/删除元素：
  - push(...items) —— 向尾端添加元素，
  - pop() —— 从尾端提取一个元素，
  - shift() —— 从首端提取一个元素，
  - unshift(...items) —— 向首端添加元素，
  - splice(pos, deleteCount, ...items) —— 从 pos 开始删除 deleteCount 个元素，并插入 items。
  - slice(start, end) —— 创建一个新数组，将从索引 start 到索引 end（但不包括 end）的元素复制进去。
  - concat(...items) —— 返回一个新数组：复制当前数组的所有元素，并向其中添加 items。如果 items 中的任意一项是一个数组，那么就取其元素。
- 搜索元素：
  - indexOf/lastIndexOf(item, pos) —— 从索引 pos 开始搜索 item，搜索到则返回该项的索引，否则返回 -1。
  - includes(value) —— 如果数组有 value，则返回 true，否则返回 false。
  - find/filter(func) —— 通过 func 过滤元素，返回使 func 返回 true 的第一个值/所有值。
  - findIndex 和 find 类似，但返回索引而不是值。
- 遍历元素：
  - forEach(func) —— 对每个元素都调用 func，不返回任何内容。
- 转换数组：
  - map(func) —— 根据对每个元素调用 func 的结果创建一个新数组。
  - sort(func) —— 对数组进行原位（in-place）排序，然后返回它。
  - reverse() —— 原位（in-place）反转数组，然后返回它。
  - split/join —— 将字符串转换为数组并返回。
  - reduce/reduceRight(func, initial) —— 通过对每个元素调用 func 计算数组上的单个值，并在调用之间传递中间结果。
- 其他：
  - Array.isArray(arr) 检查 arr 是否是一个数组。

请注意，sort，reverse 和 splice 方法修改的是数组本身。

这些是最常用的方法，它们覆盖 99％ 的用例。但是还有其他几个：

- [arr.some(fn)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Fsome)/[arr.every(fn)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Fevery) 检查数组。

与 map 类似，对数组的每个元素调用函数 fn。如果任何/所有结果为 true，则返回 true，否则返回 false。

这两个方法的行为类似于 || 和 && 运算符：如果 fn 返回一个真值，arr.some() 立即返回 true 并停止迭代其余数组项；如果 fn 返回一个假值，arr.every() 立即返回 false 并停止对其余数组项的迭代。

我们可以使用 every 来比较数组：

```
function arraysEqual(arr1, arr2) {
  return arr1.length === arr2.length && arr1.every((value, index) => value === arr2[index]);
}

alert( arraysEqual([1, 2], [1, 2])); // true
复制代码
```

- [arr.fill(value, start, end)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Ffill) —— 从索引 start 到 end，用重复的 value 填充数组。
- [arr.copyWithin(target, start, end)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2FcopyWithin) —— 将从位置 start 到 end 的所有元素复制到 自身 的 target 位置（覆盖现有元素）。
- [arr.flat(depth)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Fflat)/[arr.flatMap(fn)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2FflatMap) 从多维数组创建一个新的扁平数组。
- [Array.of(element0[, element1[, …[, elementN\]]])](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Fof) 基于可变数量的参数创建一个新的 Array 实例，而不需要考虑参数的数量或类型。

有关完整列表，请参阅 [手册](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray)。

## 20. Iterable object（可迭代对象）

可以应用 for..of 的对象被称为 可迭代的。

- 技术上来说，可迭代对象必须实现 Symbol.iterator 方法。
  - obj[Symbol.iterator]() 的结果被称为 迭代器（iterator）。由它处理进一步的迭代过程。
  - 一个迭代器必须有 next() 方法，它返回一个 {done: Boolean, value: any} 对象，这里 done:true 表明迭代结束，否则 value 就是下一个值。
- Symbol.iterator 方法会被 for..of 自动调用，但我们也可以直接调用它。
- 内置的可迭代对象例如字符串和数组，都实现了 Symbol.iterator。
- 字符串迭代器能够识别代理对（surrogate pair）。（译注：代理对也就是 UTF-16 扩展字符。）

有索引属性和 length 属性的对象被称为 类数组对象。这种对象可能还具有其他属性和方法，但是没有数组的内建方法。

如果我们仔细研究一下规范 —— 就会发现大多数内建方法都假设它们需要处理的是可迭代对象或者类数组对象，而不是“真正的”数组，因为这样抽象度更高。

Array.from(obj[, mapFn, thisArg]) 将可迭代对象或类数组对象 obj 转化为真正的数组 Array，然后我们就可以对它应用数组的方法。可选参数 mapFn 和 thisArg 允许我们将函数应用到每个元素。

## 21. Map and Set（映射和集合）

Map —— 是一个带键的数据项的集合。

方法和属性如下：

- new Map([iterable]) —— 创建 map，可选择带有 [key,value] 对的 iterable（例如数组）来进行初始化。
- map.set(key, value) —— 根据键存储值。
- map.get(key) —— 根据键来返回值，如果 map 中不存在对应的 key，则返回 undefined。
- map.has(key) —— 如果 key 存在则返回 true，否则返回 false。
- map.delete(key) —— 删除指定键的值。
- map.clear() —— 清空 map 。
- map.size —— 返回当前元素个数。

与普通对象 Object 的不同点：

- 任何键、对象都可以作为键。
- 有其他的便捷方法，如 size 属性。

Set —— 是一组唯一值的集合。

方法和属性：

- new Set([iterable]) —— 创建 set，可选择带有 iterable（例如数组）来进行初始化。
- set.add(value) —— 添加一个值（如果 value 存在则不做任何修改），返回 set 本身。
- set.delete(value) —— 删除值，如果 value 在这个方法调用的时候存在则返回 true ，否则返回 false。
- set.has(value) —— 如果 value 在 set 中，返回 true，否则返回 false。
- set.clear() —— 清空 set。
- set.size —— 元素的个数。

在 Map 和 Set 中迭代总是按照值插入的顺序进行的，所以我们不能说这些集合是无序的，但是我们不能对元素进行重新排序，也不能直接按其编号来获取元素。

## 22. WeakMap and WeakSet（弱映射和弱集合）

WeakMap 是类似于 Map 的集合，它仅允许对象作为键，并且一旦通过其他方式无法访问它们，便会将它们与其关联值一同删除。

WeakSet 是类似于 Set 的集合，它仅存储对象，并且一旦通过其他方式无法访问它们，便会将其删除。

它们都不支持引用所有键或其计数的方法和属性。仅允许单个操作。

WeakMap 和 WeakSet 被用作“主要”对象存储之外的“辅助”数据结构。一旦将对象从主存储器中删除，如果该对象仅被用作 WeakMap 或 WeakSet 的键，那么它将被自动清除。

## 23. 解构赋值

- 解构赋值可以立即将一个对象或数组映射到多个变量上。

- 解构对象的完整语法：

  let {prop : varName = default, ...rest} = object

这表示属性 prop 会被赋值给变量 varName，如果没有这个属性的话，就会使用默认值 default。

没有对应映射的对象属性会被复制到 rest 对象。

- 解构数组的完整语法：

  let [item1 = default, item2, ...rest] = array

数组的第一个元素被赋值给 item1，第二个元素被赋值给 item2，剩下的所有元素被复制到另一个数组 rest。

- 从嵌套数组/对象中提取数据也是可以的，此时等号左侧必须和等号右侧有相同的结构。

## 24. 日期和时间

- 在 JavaScript 中，日期和时间使用 [Date](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FDate) 对象来表示。我们不能只创建日期，或者只创建时间，Date 对象总是同时创建两者。
- 月份从 0 开始计数（对，一月是 0）。
- 一周中的某一天 getDay() 同样从 0 开始计算（0 代表星期日）。
- 当设置了超出范围的组件时，Date 会进行自我校准。这一点对于日/月/小时的加减很有用。
- 日期可以相减，得到的是以毫秒表示的两者的差值。因为当 Date 被转换为数字时，Date 对象会被转换为时间戳。
- 使用 Date.now() 可以更快地获取当前时间的时间戳。

和其他系统不同，JavaScript 中时间戳以毫秒为单位，而不是秒。

有时我们需要更加精准的时间度量。JavaScript 自身并没有测量微秒的方法（百万分之一秒），但大多数运行环境会提供。例如：浏览器有 [performance.now()](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FAPI%2FPerformance%2Fnow) 方法来给出从页面加载开始的以毫秒为单位的微秒数（精确到毫秒的小数点后三位）：

```
alert(`Loading started ${performance.now()}ms ago`);
// 类似于 "Loading started 34731.26000000001ms ago"
// .26 表示的是微秒（260 微秒）
// 小数点后超过 3 位的数字是精度错误，只有前三位数字是正确的
复制代码
```

Node.js 有 microtime 模块以及其他方法。从技术上讲，几乎所有的设备和环境都允许获取更高精度的数值，只是不是通过 Date 对象。

## 25. JSON 方法，toJSON

- JSON 是一种数据格式，具有自己的独立标准和大多数编程语言的库。
- JSON 支持 object，array，string，number，boolean 和 null。
- JavaScript 提供序列化（serialize）成 JSON 的方法 [JSON.stringify](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FJSON%2Fstringify) 和解析 JSON 的方法 [JSON.parse](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FJSON%2Fparse)。
- 这两种方法都支持用于智能读/写的转换函数。
- 如果一个对象具有 toJSON，那么它会被 JSON.stringify 调用。

## 26. 递归和堆栈

术语：

- 递归 是编程的一个术语，表示从自身调用函数（译注：也就是自调用）。递归函数可用于以更优雅的方式解决问题。

当一个函数调用自身时，我们称其为 递归步骤。递归的 基础 是函数参数使任务简单到该函数不再需要进行进一步调用。

- [递归定义](https://link.juejin.cn/?target=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FRecursive_data_type) 的数据结构是指可以使用自身来定义的数据结构。

例如，链表可以被定义为由对象引用一个列表（或 null）而组成的数据结构。

```
list = { value, next -> list }
复制代码
```

像 HTML 元素树或者本章中的 department 树等，本质上也是递归：它们有分支，而且分支又可以有其他分支。

就像我们在示例 sumSalary 中看到的那样，可以使用递归函数来遍历它们。

任何递归函数都可以被重写为迭代（译注：也就是循环）形式。有时这是在优化代码时需要做的。但对于大多数任务来说，递归方法足够快，并且容易编写和维护。

## 27. Rest 参数与 Spread 语法

当我们在代码中看到 "..." 时，它要么是 rest 参数，要么就是 spread 语法。

有一个简单的方法可以区分它们：

- 若 ... 出现在函数参数列表的最后，那么它就是 rest 参数，它会把参数列表中剩余的参数收集到一个数组中。
- 若 ... 出现在函数调用或类似的表达式中，那它就是 spread 语法，它会把一个数组展开为列表。

使用场景：

- Rest 参数用于创建可接受任意数量参数的函数。
- Spread 语法用于将数组传递给通常需要含有许多参数的列表的函数。

它们俩的出现帮助我们轻松地在列表和参数数组之间来回转换。

“旧式”的 arguments（类数组且可迭代的对象）也依然能够帮助我们获取函数调用中的所有参数。

## 28. 全局对象

- 全局对象包含应该在任何位置都可见的变量。
- 其中包括 JavaScript 的内建方法，例如 “Array” 和环境特定（environment-specific）的值，例如 window.innerHeight — 浏览器中的窗口高度。
- 全局对象有一个通用名称 globalThis。
- ……但是更常见的是使用“老式”的环境特定（environment-specific）的名字，例如 window（浏览器）和 global（Node.js）。
- 仅当值对于我们的项目而言确实是全局的时，才应将其存储在全局对象中。并保持其数量最少。
- 在浏览器中，除非我们使用 [modules](https://link.juejin.cn/?target=https%3A%2F%2Fzh.javascript.info%2Fmodules)，否则使用 var 声明的全局函数和变量会成为全局对象的属性。
- 为了使我们的代码面向未来并更易于理解，我们应该使用直接的方式访问全局对象的属性，如 window.x。

## 29. 函数对象，NFE

函数就是对象。

我们介绍了它们的一些属性：

- name —— 函数的名字。通常取自函数定义，但如果函数定义时没设定函数名，JavaScript 会尝试通过函数的上下文猜一个函数名（例如把赋值的变量名取为函数名）。
- length —— 函数定义时的入参的个数。Rest 参数不参与计数。

如果函数是通过函数表达式的形式被声明的（不是在主代码流里），并且附带了名字，那么它被称为命名函数表达式（Named Function Expression）。这个名字可以用于在该函数内部进行自调用，例如递归调用等。

此外，函数可以带有额外的属性。很多知名的 JavaScript 库都充分利用了这个功能。

它们创建一个“主”函数，然后给它附加很多其它“辅助”函数。例如，[jQuery](https://link.juejin.cn/?target=https%3A%2F%2Fjquery.com%2F) 库创建了一个名为 $ 的函数。[lodash](https://link.juejin.cn/?target=https%3A%2F%2Flodash.com%2F) 库创建一个 _ 函数，然后为其添加了 _.add、_.keyBy 以及其它属性（想要了解更多内容，参查阅 [docs](https://link.juejin.cn/?target=https%3A%2F%2Flodash.com%2Fdocs)）。实际上，它们这么做是为了减少对全局空间的污染，这样一个库就只会有一个全局变量。这样就降低了命名冲突的可能性。

所以，一个函数本身可以完成一项有用的工作，还可以在自身的属性中附带许多其他功能。

## 29. "new Function" 语法

语法：

```
let func = new Function ([arg1, arg2, ...argN], functionBody);
复制代码
```

由于历史原因，参数也可以按逗号分隔符的形式给出。

以下三种声明的含义相同：

```
new Function('a', 'b', 'return a + b'); // 基础语法
new Function('a,b', 'return a + b'); // 逗号分隔
new Function('a , b', 'return a + b'); // 逗号和空格分隔
复制代码
```

使用 new Function 创建的函数，它的 [[Environment]] 指向全局词法环境，而不是函数所在的外部词法环境。因此，我们不能在 new Function 中直接使用外部变量。不过这样是好事，这有助于降低我们代码出错的可能。并且，从代码架构上讲，显式地使用参数传值是一种更好的方法，并且避免了与使用压缩程序而产生冲突的问题。

## 30. 调度：setTimeout 和 setInterval

- setTimeout(func, delay, ...args) 和 setInterval(func, delay, ...args) 方法允许我们在 delay 毫秒之后运行 func 一次或以 delay 毫秒为时间间隔周期性运行 func。
- 要取消函数的执行，我们应该调用 clearInterval/clearTimeout，并将 setInterval/setTimeout 返回的值作为入参传入。
- 嵌套的 setTimeout 比 setInterval 用起来更加灵活，允许我们更精确地设置两次执行之间的时间。
- 零延时调度 setTimeout(func, 0)（与 setTimeout(func) 相同）用来调度需要尽快执行的调用，但是会在当前脚本执行完成后进行调用。
- 浏览器会将 setTimeout 或 setInterval 的五层或更多层嵌套调用（调用五次之后）的最小延时限制在 4ms。这是历史遗留问题。

请注意，所有的调度方法都不能 保证 确切的延时。

例如，浏览器内的计时器可能由于许多原因而变慢：

- CPU 过载。
- 浏览器页签处于后台模式。
- 笔记本电脑用的是电池供电（译注：使用电池供电会以降低性能为代价提升续航）。

所有这些因素，可能会将定时器的最小计时器分辨率（最小延迟）增加到 300ms 甚至 1000ms，具体以浏览器及其设置为准。

## 31. 装饰器模式和转发，call/apply

装饰器 是一个围绕改变函数行为的包装器。主要工作仍由该函数来完成。

装饰器可以被看作是可以添加到函数的 “features” 或 “aspects”。我们可以添加一个或添加多个。而这一切都无需更改其代码！

为了实现 cachingDecorator，我们研究了以下方法：

- [func.call(context, arg1, arg2…)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FFunction%2Fcall) —— 用给定的上下文和参数调用 func。
- [func.apply(context, args)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FFunction%2Fapply) —— 调用 func 将 context 作为 this 和类数组的 args 传递给参数列表。

通用的 呼叫转移（call forwarding） 通常是使用 apply 完成的：

```
let wrapper = function() {
  return original.apply(this, arguments);
};
复制代码
```

我们也可以看到一个 方法借用（method borrowing） 的例子，就是我们从一个对象中获取一个方法，并在另一个对象的上下文中“调用”它。采用数组方法并将它们应用于参数 arguments 是很常见的。另一种方法是使用 Rest 参数对象，该对象是一个真正的数组。

## 32. 函数绑定

方法 func.bind(context, ...args) 返回函数 func 的“绑定的（bound）变体”，它绑定了上下文 this 和第一个参数（如果给定了）。

通常我们应用 bind 来绑定对象方法的 this，这样我们就可以把它们传递到其他地方使用。例如，传递给 setTimeout。

当我们绑定一个现有的函数的某些参数时，绑定后的（不太通用的）函数被称为 partially applied 或 partial。

当我们不想一遍又一遍地重复相同的参数时，partial 非常有用。就像我们有一个 send(from, to) 函数，并且对于我们的任务来说，from 应该总是一样的，那么我们就可以搞一个 partial 并使用它。

## 33. 深入理解箭头函数

箭头函数：

- 没有 this
- 没有 arguments
- 不能使用 new 进行调用
- 它们也没有 super，但目前我们还没有学到它。我们将在 [类继承](https://link.juejin.cn/?target=https%3A%2F%2Fzh.javascript.info%2Fclass-inheritance) 一章中学习它。

这是因为，箭头函数是针对那些没有自己的“上下文”，但在当前上下文中起作用的短代码的。并且箭头函数确实在这种使用场景中大放异彩。

## 34. 原型继承

- 在 JavaScript 中，所有的对象都有一个隐藏的 [[Prototype]] 属性，它要么是另一个对象，要么就是 null。
- 我们可以使用 obj.__proto__ 访问它（历史遗留下来的 getter/setter，这儿还有其他方法，很快我们就会讲到）。
- 通过 [[Prototype]] 引用的对象被称为“原型”。
- 如果我们想要读取 obj 的一个属性或者调用一个方法，并且它不存在，那么 JavaScript 就会尝试在原型中查找它。
- 写/删除操作直接在对象上进行，它们不使用原型（假设它是数据属性，不是 setter）。
- 如果我们调用 obj.method()，而且 method 是从原型中获取的，this 仍然会引用 obj。因此，方法始终与当前对象一起使用，即使方法是继承的。
- for..in 循环在其自身和继承的属性上进行迭代。所有其他的键/值获取方法仅对对象本身起作用。

## 35. F.prototype

一切都很简单，只需要记住几条重点就可以清晰地掌握了：

- F.prototype 属性（不要把它与 [[Prototype]] 弄混了）在 new F 被调用时为新对象的 [[Prototype]] 赋值。
- F.prototype 的值要么是一个对象，要么就是 null：其他值都不起作用。
- "prototype" 属性仅在设置了一个构造函数（constructor function），并通过 new 调用时，才具有这种特殊的影响。

在常规对象上，prototype 没什么特别的：

```
let user = {
  name: "John",
  prototype: "Bla-bla" // 这里只是普通的属性
};
复制代码
```

默认情况下，所有函数都有 F.prototype = {constructor：F}，所以我们可以通过访问它的 "constructor" 属性来获取一个对象的构造器。

## 36. 原生的原型

- 所有的内建对象都遵循相同的模式（pattern）：
  - 方法都存储在 prototype 中（Array.prototype、Object.prototype、Date.prototype 等）。
  - 对象本身只存储数据（数组元素、对象属性、日期）。
- 原始数据类型也将方法存储在包装器对象的 prototype 中：Number.prototype、String.prototype 和 Boolean.prototype。只有 undefined 和 null 没有包装器对象。
- 内建原型可以被修改或被用新的方法填充。但是不建议更改它们。唯一允许的情况可能是，当我们添加一个还没有被 JavaScript 引擎支持，但已经被加入 JavaScript 规范的新标准时，才可能允许这样做。

## 37. 原型方法，没有 __proto__ 的对象

设置和直接访问原型的现代方法有：

- [Object.create(proto, [descriptors\])](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fcreate) —— 利用给定的 proto 作为 [[Prototype]]（可以是 null）和可选的属性描述来创建一个空对象。
- [Object.getPrototypeOf(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FgetPrototypeOf) —— 返回对象 obj 的 [[Prototype]]（与 __proto__ 的 getter 相同）。
- [Object.setPrototypeOf(obj, proto)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FsetPrototypeOf) —— 将对象 obj 的 [[Prototype]] 设置为 proto（与 __proto__ 的 setter 相同）。

如果要将一个用户生成的键放入一个对象，那么内建的 __proto__ getter/setter 是不安全的。因为用户可能会输入 "__proto__" 作为键，这会导致一个 error，虽然我们希望这个问题不会造成什么大影响，但通常会造成不可预料的后果。

因此，我们可以使用 Object.create(null) 创建一个没有 __proto__ 的 “very plain” 对象，或者对此类场景坚持使用 Map 对象就可以了。

此外，Object.create 提供了一种简单的方式来浅拷贝一个对象的所有描述符：

```
let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
复制代码
```

此外，我们还明确了 __proto__ 是 [[Prototype]] 的 getter/setter，就像其他方法一样，它位于 Object.prototype。

我们可以通过 Object.create(null) 来创建没有原型的对象。这样的对象被用作 “pure dictionaries”，对于它们而言，使用 "__proto__" 作为键是没有问题的。

其他方法：

- [Object.keys(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fkeys) / [Object.values(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fvalues) / [Object.entries(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2Fentries) —— 返回一个可枚举的由自身的字符串属性名/值/键值对组成的数组。
- [Object.getOwnPropertySymbols(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FgetOwnPropertySymbols) —— 返回一个由自身所有的 symbol 类型的键组成的数组。
- [Object.getOwnPropertyNames(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FgetOwnPropertyNames) —— 返回一个由自身所有的字符串键组成的数组。
- [Reflect.ownKeys(obj)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FReflect%2FownKeys) —— 返回一个由自身所有键组成的数组。
- [obj.hasOwnProperty(key)](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FhasOwnProperty)：如果 obj 拥有名为 key 的自身的属性（非继承而来的），则返回 true。

所有返回对象属性的方法（如 Object.keys 及其他）—— 都返回“自身”的属性。如果我们想继承它们，我们可以使用 for...in。

## 38. Class 基本语法

基本的类语法看起来像这样：

```
class MyClass {
  prop = value; // 属性

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 有计算名称（computed name）的方法（此处为 symbol）
  // ...
}
复制代码
```

技术上来说，MyClass 是一个函数（我们提供作为 constructor 的那个），而 methods、getters 和 settors 都被写入了 MyClass.prototype。

## 39. 类继承

1. 想要扩展一个类：class Child extends Parent：

- 这意味着 Child.prototype.__proto__ 将是 Parent.prototype，所以方法会被继承。

1. 重写一个 constructor：

- 在使用 this 之前，我们必须在 Child 的 constructor 中将父 constructor 调用为 super()。

1. 重写一个方法：

- 我们可以在一个 Child 方法中使用 super.method() 来调用 Parent 方法。

1. 内部：

- 方法在内部的 [[HomeObject]] 属性中记住了它们的类/对象。这就是 super 如何解析父方法的。
- 因此，将一个带有 super 的方法从一个对象复制到另一个对象是不安全的。

补充：

- 箭头函数没有自己的 this 或 super，所以它们能融入到就近的上下文中，像透明似的。

## 40. 静态属性和静态方法

静态方法被用于实现属于整个类的功能。它与具体的类实例无关。

举个例子， 一个用于进行比较的方法 Article.compare(article1, article2) 或一个工厂（factory）方法 Article.createTodays()。

在类生命中，它们都被用关键字 static 进行了标记。

静态属性被用于当我们想要存储类级别的数据时，而不是绑定到实例。

语法如下所示：

```
class MyClass {
  static property = ...;

  static method() {
    ...
  }
}
复制代码
```

从技术上讲，静态声明与直接给类本身赋值相同：

```
MyClass.property = ...
MyClass.method = ...
复制代码
```

静态属性和方法是可被继承的。

对于 class B extends A，类 B 的 prototype 指向了 A：B.[[Prototype]] = A。因此，如果一个字段在 B 中没有找到，会继续在 A 中查找。

## 41. 私有的和受保护的属性和方法

就面向对象编程（OOP）而言，内部接口与外部接口的划分被称为 [封装](https://link.juejin.cn/?target=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FEncapsulation_(computer_programming))。

它具有以下优点：

保护用户，使他们不会误伤自己

想象一下，有一群开发人员在使用一个咖啡机。这个咖啡机是由“最好的咖啡机”公司制造的，工作正常，但是保护罩被拿掉了。因此内部接口暴露了出来。

所有的开发人员都是文明的 —— 他们按照预期使用咖啡机。但其中的一个人，约翰，他认为自己是最聪明的人，并对咖啡机的内部做了一些调整。然而，咖啡机两天后就坏了。

这肯定不是约翰的错，而是那个取下保护罩并让约翰进行操作的人的错。

编程也一样。如果一个 class 的使用者想要改变那些本不打算被从外部更改的东西 —— 后果是不可预测的。

可支持性

编程的情况比现实生活中的咖啡机要复杂得多，因为我们不只是购买一次。我们还需要不断开发和改进代码。

如果我们严格界定内部接口，那么这个 class 的开发人员可以自由地更改其内部属性和方法，甚至无需通知用户。

如果你是这样的 class 的开发者，那么你会很高兴知道可以安全地重命名私有变量，可以更改甚至删除其参数，因为没有外部代码依赖于它们。

对于用户来说，当新版本问世时，应用的内部可能被进行了全面检修，但如果外部接口相同，则仍然很容易升级。

隐藏复杂性

人们喜欢使用简单的东西。至少从外部来看是这样。内部的东西则是另外一回事了。

程序员也不例外。

当实施细节被隐藏，并提供了简单且有据可查的外部接口时，总是很方便的。

为了隐藏内部接口，我们使用受保护的或私有的属性：

- 受保护的字段以 _ 开头。这是一个众所周知的约定，不是在语言级别强制执行的。程序员应该只通过它的类和从它继承的类中访问以 _ 开头的字段。
- 私有字段以 # 开头。JavaScript 确保我们只能从类的内部访问它们。

目前，各个浏览器对私有字段的支持不是很好，但可以用 polyfill 解决。

## 42. 类检查："instanceof"

让我们总结一下我们知道的类型检查方法：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5144219d331b48a982796a52aeffe3c8~tplv-k3u1fbpfcp-watermark.image)

当我们使用类的层次结构（hierarchy），并想要对该类进行检查，同时还要考虑继承时，这种场景下 instanceof 操作符确实很出色。正如我们所看到的，从技术上讲，{}.toString 是一种“更高级的” typeof。

## 43. Mixin 模式

Mixin — 是一个通用的面向对象编程术语：一个包含其他类的方法的类。

一些其它编程语言允许多重继承。JavaScript 不支持多重继承，但是可以通过将方法拷贝到原型中来实现 mixin。

我们可以使用 mixin 作为一种通过添加多种行为（例如上文中所提到的事件处理）来扩充类的方法。

如果 Mixins 意外覆盖了现有类的方法，那么它们可能会成为一个冲突点。因此，通常应该仔细考虑 mixin 的命名方法，以最大程度地降低发生这种冲突的可能性。

## 44. 错误处理，"try..catch"

try..catch 结构允许我们处理执行过程中出现的 error。从字面上看，它允许“尝试”运行代码并“捕获”其中可能发生的错误。

语法如下：

```
try {
  // 执行此处代码
} catch(err) {
  // 如果发生错误，跳转至此处
  // err 是一个 error 对象
} finally {
  // 无论怎样都会在 try/catch 之后执行
}
复制代码
```

这儿可能会没有 catch 部分或者没有 finally，所以 try..catch 或 try..finally 都是可用的。

Error 对象包含下列属性：

- message — 人类可读的 error 信息。
- name — 具有 error 名称的字符串（Error 构造器的名称）。
- stack（没有标准，但得到了很好的支持）— Error 发生时的调用栈。

如果我们不需要 error 对象，我们可以通过使用 catch { 而不是 catch(err) { 来省略它。

我们也可以使用 throw 操作符来生成自定义的 error。从技术上讲，throw 的参数可以是任何东西，但通常是继承自内建的 Error 类的 error 对象。下一章我们会详细介绍扩展 error。

再次抛出（rethrowing）是一种错误处理的重要模式：catch 块通常期望并知道如何处理特定的 error 类型，因此它应该再次抛出它不知道的 error。

即使我们没有 try..catch，大多数执行环境也允许我们设置“全局”错误处理程序来捕获“掉出（fall out）”的 error。在浏览器中，就是 window.onerror。

## 45. 自定义 Error，扩展 Error

- 我们可以正常地从 Error 和其他内建的 error 类中进行继承，。我们只需要注意 name 属性以及不要忘了调用 super。
- 我们可以使用 instanceof 来检查特定的 error。但有时我们有来自第三方库的 error 对象，并且在这儿没有简单的方法来获取它的类。那么可以将 name 属性用于这一类的检查。
- 包装异常是一项广泛应用的技术：用于处理低级别异常并创建高级别 error 而不是各种低级别 error 的函数。在上面的示例中，低级别异常有时会成为该对象的属性，例如 err.cause，但这不是严格要求的。

## 46. Promise 链

如果 .then（或 catch/finally 都可以）处理程序（handler）返回一个 promise，那么链的其余部分将会等待，直到它状态变为 settled。当它被 settled 后，其 result（或 error）将被进一步传递下去。

这是一个完整的流程图：

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82af525c1e2b451dafec052a56b53373~tplv-k3u1fbpfcp-watermark.image)

## 47. 使用 promise 进行错误处理

- .catch 处理 promise 中的各种 error：在 reject() 调用中的，或者在处理程序（handler）中抛出的（thrown）error。
- 我们应该将 .catch 准确地放到我们想要处理 error，并知道如何处理这些 error 的地方。处理程序应该分析 error（可以自定义 error 类来帮助分析）并再次抛出未知的 error（可能它们是编程错误）。
- 如果没有办法从 error 中恢复的话，不使用 .catch 也可以。
- 在任何情况下我们都应该有 unhandledrejection 事件处理程序（用于浏览器，以及其他环境的模拟），以跟踪未处理的 error 并告知用户（可能还有我们的服务器）有关信息，以使我们的应用程序永远不会“死掉”。

### 补充内容

#### Fetch 错误处理示例

让我们改进用户加载（user-loading）示例的错误处理。

当请求无法发出时，[fetch](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FAPI%2FWindowOrWorkerGlobalScope%2Ffetch) reject 会返回 promise。例如，远程服务器无法访问，或者 URL 异常。但是如果远程服务器返回响应错误 404，甚至是错误 500，这些都被认为是合法的响应。

如果在 (*) 行，服务器返回一个错误 500 的非 JSON（non-JSON）页面该怎么办？如果没有这个用户，GitHub 返回错误 404 的页面又该怎么办呢？

```
fetch('no-such-user.json') // (*)
  .then(response => response.json())
  .then(user => fetch(`https://api.github.com/users/${user.name}`)) // (**)
  .then(response => response.json())
  .catch(alert); // SyntaxError: Unexpected token < in JSON at position 0
  // ...
复制代码
```

到目前为止，代码试图以 JSON 格式加载响应数据，但无论如何都会因为语法错误而失败。你可以通过执行上述例子来查看相关信息，因为文件 no-such-user.json 不存在。

这有点糟糕，因为错误只是落在链上，并没有相关细节信息：什么失败了，在哪里失败的。

因此我们多添加一步：我们应该检查具有 HTTP 状态的 response.status 属性，如果不是 200 就抛出错误。

```
class HttpError extends Error { // (1)
  constructor(response) {
    super(`${response.status} for ${response.url}`);
    this.name = 'HttpError';
    this.response = response;
  }
}

function loadJson(url) { // (2)
  return fetch(url)
    .then(response => {
      if (response.status == 200) {
        return response.json();
      } else {
        throw new HttpError(response);
      }
    })
}

loadJson('no-such-user.json') // (3)
  .catch(alert); // HttpError: 404 for .../no-such-user.json
复制代码
```

1. 我们为 HTTP 错误创建一个自定义类用于区分 HTTP 错误和其他类型错误。此外，新的类有一个 constructor，它接受 response 对象，并将其保存到 error 中。因此，错误处理（error-handling）代码就能够获得响应数据了。
2. 然后我们将请求（requesting）和错误处理代码包装进一个函数，它能够 fetch url 并 将所有状态码不是 200 视为错误。这很方便，因为我们通常需要这样的逻辑。
3. 现在 alert 显示更多有用的描述信息。

拥有我们自己的错误处理类的好处是我们可以使用 instanceof 很容易地在错误处理代码中检查错误。

例如，我们可以创建请求，如果我们得到 404 就可以告知用户修改信息。

下面的代码从 GitHub 加载给定名称的用户。如果没有这个用户，它将告知用户填写正确的名称：

```
function demoGithubUser() {
  let name = prompt("Enter a name?", "iliakan");

  return loadJson(`https://api.github.com/users/${name}`)
    .then(user => {
      alert(`Full name: ${user.name}.`);
      return user;
    })
    .catch(err => {
      if (err instanceof HttpError && err.response.status == 404) {
        alert("No such user, please reenter.");
        return demoGithubUser();
      } else {
        throw err; // (*)
      }
    });
}

demoGithubUser();
复制代码
```

请注意：这里的 .catch 会捕获所有错误，但是它仅仅“知道如何处理” HttpError 404。在那种特殊情况下，它意味着没有这样的用户，而 .catch 仅仅在这种情况下重试。

对于其他错误，它不知道会出现什么问题。可能是编程错误或者其他错误。所以它仅仅是在 (*) 行再次抛出。

#### 其他

如果我们有加载指示（load-indication），.finally 是一个很好的处理程序（handler），在 fetch 完成时停止它：

```
function demoGithubUser() {
  let name = prompt("Enter a name?", "iliakan");

  document.body.style.opacity = 0.3; // (1) 开始指示（indication）

  return loadJson(`https://api.github.com/users/${name}`)
    .finally(() => { // (2) 停止指示（indication）
      document.body.style.opacity = '';
      return new Promise(resolve => setTimeout(resolve)); // (*)
    })
    .then(user => {
      alert(`Full name: ${user.name}.`);
      return user;
    })
    .catch(err => {
      if (err instanceof HttpError && err.response.status == 404) {
        alert("No such user, please reenter.");
        return demoGithubUser();
      } else {
        throw err;
      }
    });
}

demoGithubUser();
复制代码
```

此处的 (1) 行，我们通过调暗文档来指示加载。指示方法没有什么问题，可以使用任何类型的指示来代替。

当 promise 得以解决，fetch 可以是成功或者错误，finally 在 (2) 行触发并终止加载指示。

有一个浏览器技巧，(*) 是从 finally 返回零延时（zero-timeout）的 promise。这是因为一些浏览器（比如 Chrome）需要“一点时间”外的 promise 处理程序来绘制文档的更改。因此它确保在进入链下一步之前，指示在视觉上是停止的。

## 48. Promise API

Promise 类有 5 种静态方法：

1. Promise.all(promises) —— 等待所有 promise 都 resolve 时，返回存放它们结果的数组。如果给定的任意一个 promise 为 reject，那么它就会变成 Promise.all 的 error，所有其他 promise 的结果都会被忽略。
2. Promise.allSettled(promises)（ES2020 新增方法）—— 等待所有 promise 都 settle 时，并以包含以下内容的对象数组的形式返回它们的结果：
   - status: "fulfilled" 或 "rejected"
   - value（如果 fulfilled）或 reason（如果 rejected）。
3. Promise.race(promises) —— 等待第一个 settle 的 promise，并将其 result/error 作为结果。
4. Promise.resolve(value) —— 使用给定 value 创建一个 resolved 的 promise。
5. Promise.reject(error) —— 使用给定 error 创建一个 rejected 的 promise。

这五个方法中，Promise.all 可能是在实战中使用最多的。

## 49. 微任务（Microtask）

Promise 处理始终是异步的，因为所有 promise 行为都会通过内部的 “promise jobs” 队列，也被称为“微任务队列”（ES8 术语）。

因此，.then/catch/finally 处理程序（handler）总是在当前代码完成后才会被调用。

如果我们需要确保一段代码在 .then/catch/finally 之后被执行，我们可以将它添加到链式调用的 .then 中。

在大多数 JavaScript 引擎中（包括浏览器和 Node.js），微任务（microtask）的概念与“事件循环（event loop）”和“宏任务（macrotasks）”紧密相关。

## 50. Async/await

函数前面的关键字 async 有两个作用：

1. 让这个函数总是返回一个 promise。
2. 允许在该函数内使用 await。

Promise 前的关键字 await 使 JavaScript 引擎等待该 promise settle，然后：

1. 如果有 error，就会抛出异常 — 就像那里调用了 throw error 一样。
2. 否则，就返回结果。

这两个关键字一起提供了一个很好的用来编写异步代码的框架，这种代码易于阅读也易于编写。

有了 async/await 之后，我们就几乎不需要使用 promise.then/catch，但是不要忘了它们是基于 promise 的，因为有些时候（例如在最外层作用域）我们不得不使用这些方法。并且，当我们需要同时等待需要任务时，Promise.all 是很好用的。

## 51. Generator

- Generator 是通过 generator 函数 function* f(…) {…} 创建的。
- 在 generator（仅在）内部，存在 yield 操作。
- 外部代码和 generator 可能会通过 next/yield 调用交换结果。

在现代 JavaScript 中，generator 很少被使用。但有时它们会派上用场，因为函数在执行过程中与调用代码交换数据的能力是非常独特的。而且，当然，它们非常适合创建可迭代对象。

并且，在下一章我们将会学习 async generator，它们被用于在 for await ... of 循环中读取异步生成的数据流（例如，通过网络分页提取 (paginated fetches over a network)）。

在 Web 编程中，我们经常使用数据流，因此这是另一个非常重要的使用场景。

## 52. 异步迭代和 generator

常规的 iterator 和 generator 可以很好地处理那些不需要花费时间来生成的的数据。

当我们期望异步地，有延迟地获取数据时，可以使用它们的异步版本，并且使用 for await..of 替代 for..of。

异步 iterator 与常规 iterator 在语法上的区别：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3bf25f56fb0f4c578a5481bf8abc33b0~tplv-k3u1fbpfcp-watermark.image)

异步 generator 与常规 generator 在语法上的区别：

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/feee36c0682a455fade5479026419daa~tplv-k3u1fbpfcp-watermark.image)

在 Web 开发中，我们经常会遇到数据流，它们分段流动（flows chunk-by-chunk）。例如，下载或上传大文件。

我们可以使用异步 generator 来处理此类数据。值得注意的是，在一些环境，例如浏览器环境下，还有另一个被称为 Streams 的 API，它提供了特殊的接口来处理此类数据流，转换数据并将数据从一个数据流传递到另一个数据流（例如，从一个地方下载并立即发送到其他地方）。

## 53. 模块 (Module) 简介

下面总结一下模块的核心概念：

1. 一个模块就是一个文件。浏览器需要使用

- 默认是延迟解析的（deferred）。
- Async 可用于内联脚本。
- 要从另一个源（域/协议/端口）加载外部脚本，需要 CORS header。
- 重复的外部脚本会被忽略

1. 模块具有自己的本地顶级作用域，并可以通过 import/export 交换功能。
2. 模块始终使用 use strict。
3. 模块代码只执行一次。导出仅创建一次，然后会在导入之间共享。

当我们使用模块时，每个模块都会实现特定功能并将其导出。然后我们使用 import 将其直接导入到需要的地方即可。浏览器会自动加载并解析脚本。

在生产环境中，出于性能和其他原因，开发者经常使用诸如 [Webpack](https://link.juejin.cn/?target=https%3A%2F%2Fwebpack.js.org%2F) 之类的打包工具将模块打包到一起。

## 54. 导出和导入

- 在声明一个 class/function/… 之前：
  - export [default] class/function/variable ...
- 独立的导出：
  - export {x [as y], ...}.
- 重新导出：
  - export {x [as y], ...} from "module"
  - export * from "module"（不会重新导出默认的导出）。
  - export {default [as y]} from "module"（重新导出默认的导出）。

导入：

- 模块中命名的导出：
  - import {x [as y], ...} from "module"
- 默认的导出：
  - import x from "module"
  - import {default as x} from "module"
- 所有：
  - import * as obj from "module"
- 导入模块（它的代码，并运行），但不要将其赋值给变量：
  - import "module"

我们把 import/export 语句放在脚本的顶部或底部，都没关系。

因此，从技术上讲，下面这样的代码没有问题：

```
sayHi();

// ...

import {sayHi} from './say.js'; // 在文件底部导入
复制代码
```

在实际开发中，导入通常位于文件的开头，但是这只是为了更加方便。

请注意在 {...} 中的 import/export 语句无效。

像这样的有条件的导入是无效的：

```
if (something) {
  import {sayHi} from "./say.js"; // Error: import must be at top level
}
复制代码
```

## 55. Proxy 和 Reflect

Proxy 是对象的包装器，将代理上的操作转发到对象，并可以选择捕获其中一些操作。

它可以包装任何类型的对象，包括类和函数。

语法为：

```
let proxy = new Proxy(target, {
  /* trap */
});
复制代码
```

……然后，我们应该在所有地方使用 proxy 而不是 target。代理没有自己的属性或方法。如果提供了捕捉器（trap），它将捕获操作，否则会将其转发给 target 对象。

我们可以捕获：

- 读取（get），写入（set），删除（deleteProperty）属性（甚至是不存在的属性）。
- 函数调用（apply 捕捉器）。
- new 操作（construct 捕捉器）。
- 许多其他操作（完整列表请见本文开头部分和 [docs](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FProxy)）。

这使我们能够创建“虚拟”属性和方法，实现默认值，可观察对象，函数装饰器等。

我们还可以将对象多次包装在不同的代理中，并用多个各个方面的功能对其进行装饰。

[Reflect](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FReflect) API 旨在补充 [Proxy](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FProxy)。对于任意 Proxy 捕捉器，都有一个带有相同参数的 Reflect 调用。我们应该使用它们将调用转发给目标对象。

Proxy 有一些局限性：

- 内建对象具有“内部插槽”，对这些对象的访问无法被代理。请参阅上文中的解决方法。
- 私有类字段也是如此，因为它们也是在内部使用插槽实现的。因此，代理方法的调用必须具有目标对象作为 this 才能访问它们。
- 对象的严格相等性检查 === 无法被拦截。
- 性能：基准测试（benchmark）取决于引擎，但通常使用最简单的代理访问属性所需的时间也要长几倍。实际上，这仅对某些“瓶颈”对象来说才重要。

## 56. 遍历 DOM

给定一个 DOM 节点，我们可以使用导航（navigation）属性访问其直接的邻居。

这些属性主要分为两组：

- 对于所有节点：parentNode，childNodes，firstChild，lastChild，previousSibling，nextSibling。
- 仅对于元素节点：parentElement，children，firstElementChild，lastElementChild，previousElementSibling，nextElementSibling。

某些类型的 DOM 元素，例如 table，提供了用于访问其内容的其他属性和集合。

## 57. 搜索：getElement*，querySelector*

有 6 种主要的方法，可以在 DOM 中搜素节点：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c658adce682b4b8a9e1981b8dbbf9d18~tplv-k3u1fbpfcp-watermark.image)

此外：目前为止，最常用的是 querySelector 和 querySelectorAll，但是 getElement(s)By* 可能会偶尔有用，或者可以在旧脚本中找到。

- elem.matches(css) 用于检查 elem 与给定的 CSS 选择器是否匹配。
- elem.closest(css) 用于查找与给定 CSS 选择器相匹配的最近的祖先。elem 本身也会被检查。

让我们在这里提一下另一种用来检查子级与父级之间关系的方法，因为它有时很有用：

- 如果 elemB 在 elemA 内（elemA 的后代）或者 elemA==elemB，elemA.contains(elemB) 将返回 true。

## 58. 节点属性：type，tag 和 content

每个 DOM 节点都属于一个特定的类。这些类形成层次结构（hierarchy）。完整的属性和方法集是继承的结果。

主要的 DOM 节点属性有：

nodeType我们可以使用它来查看节点是文本节点还是元素节点。它具有一个数值型值（numeric value）：1 表示元素，3 表示文本节点，其他一些则代表其他节点类型。只读。

nodeName/tagName用于元素名，标签名（除了 XML 模式，都要大写）。对于非元素节点，nodeName 描述了它是什么。只读。

innerHTML元素的 HTML 内容。可以被修改。

outerHTML元素的完整 HTML。对 elem.outerHTML 的写入操作不会触及 elem 本身。而是在外部上下文中将其替换为新的 HTML。

nodeValue/data非元素节点（文本、注释）的内容。两者几乎一样，我们通常使用 data。可以被修改。

textContent元素内的文本：HTML 减去所有 。写入文本会将文本放入元素内，所有特殊字符和标签均被视为文本。可以安全地插入用户生成的文本，并防止不必要的 HTML 插入。

hidden当被设置为 true 时，执行与 CSS display:none 相同的事。

DOM 节点还具有其他属性，具体有哪些属性则取决于它们的类。例如， 元素（HTMLInputElement）支持 value，type，而 [元素（HTMLAnchorElement）则支持 href 等。大多数标准 HTML 特性（attribute）都具有相应的 DOM 属性。](https://link.juejin.cn/?target=undefined)

[59. 特性和属性（Attributes and properties）特性（attribute）— 写在 HTML 中的内容。属性（property）— DOM 对象中的内容。简略的对比：![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e71cdf90ae33415c8a675b184ac41e58~tplv-k3u1fbpfcp-watermark.image)elem.hasAttribute(name) — 检查是否存在这个特性。操作特性的方法：elem.getAttribute(name) — 获取这个特性值。elem.setAttribute(name, value) — 设置这个特性值。elem.removeAttribute(name) — 移除这个特性。elem.attributes — 所有特性的集合。在大多数情况下，最好使用 DOM 属性。仅当 DOM 属性无法满足开发需求，并且我们真的需要特性时，才使用特性，例如：我们需要一个非标准的特性。但是如果它以 data- 开头，那么我们应该使用 dataset。我们想要读取 HTML 中“所写的”值。对应的 DOM 属性可能不同，例如 href 属性一直是一个 完整的 URL，但是我们想要的是“原始的”值。60. 修改文档（document）创建新节点的方法：document.createElement(tag) — 用给定的标签创建一个元素节点，document.createTextNode(value) — 创建一个文本节点（很少使用），elem.cloneNode(deep) — 克隆元素，如果 deep==true 则与其后代一起克隆。插入和移除节点的方法：node.append(...nodes or strings) — 在 node 末尾插入，node.prepend(...nodes or strings) — 在 node 开头插入，node.before(...nodes or strings) — 在 node 之前插入，node.after(...nodes or strings) — 在 node 之后插入，node.replaceWith(...nodes or strings) — 替换 node。node.remove() — 移除 node。文本字符串被“作为文本”插入。这里还有“旧式”的方法：parent.appendChild(node)parent.insertBefore(node, nextSibling)parent.removeChild(node)parent.replaceChild(newElem, node)这些方法都返回 node。在 html 中给定一些 HTML，elem.insertAdjacentHTML(where, html) 会根据 where 的值来插入它："beforebegin" — 将 html 插入到 elem 前面，"afterbegin" — 将 html 插入到 elem 的开头，"beforeend" — 将 html 插入到 elem 的末尾，"afterend" — 将 html 插入到 elem 后面。另外，还有类似的方法，elem.insertAdjacentText 和 elem.insertAdjacentElement，它们会插入文本字符串和元素，但很少使用。要在页面加载完成之前将 HTML 附加到页面：document.write(html)页面加载完成后，这样的调用将会擦除文档。多见于旧脚本。61. 样式和类要管理 class，有两个 DOM 属性：className — 字符串值，可以很好地管理整个类的集合。classList — 具有 add/remove/toggle/contains 方法的对象，可以很好地支持单个类。要改变样式：](https://link.juejin.cn/?target=undefined)

- 

- 

  [style 属性是具有驼峰（camelCased）样式的对象。对其进行读取和修改与修改 "style" 特性（attribute）中的各个属性具有相同的效果。要了解如何应用 important 和其他特殊内容 — 在 ](https://link.juejin.cn/?target=undefined)[MDN](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh%2Fdocs%2FWeb%2FAPI%2FCSSStyleDeclaration) 中有一个方法列表。

- style.cssText 属性对应于整个 "style" 特性（attribute），即完整的样式字符串。

要读取已解析的（resolved）样式（对于所有类，在应用所有 CSS 并计算最终值之后）：

- getComputedStyle(elem, [pseudo]) 返回与 style 对象类似的，且包含了所有类的对象。只读。

## 62. 元素大小和滚动

元素具有以下几何属性：

- offsetParent — 是最接近的 CSS 定位的祖先，或者是 td，th，table，body。
- offsetLeft/offsetTop — 是相对于 offsetParent 的左上角边缘的坐标。
- offsetWidth/offsetHeight — 元素的“外部” width/height，边框（border）尺寸计算在内。
- clientLeft/clientTop — 从元素左上角外角到左上角内角的距离。对于从左到右显示内容的操作系统来说，它们始终是左侧/顶部 border 的宽度。而对于从右到左显示内容的操作系统来说，垂直滚动条在左边，所以 clientLeft 也包括滚动条的宽度。
- clientWidth/clientHeight — 内容的 width/height，包括 padding，但不包括滚动条（scrollbar）。
- scrollWidth/scrollHeight — 内容的 width/height，就像 clientWidth/clientHeight 一样，但还包括元素的滚动出的不可见的部分。
- scrollLeft/scrollTop — 从元素的左上角开始，滚动出元素的上半部分的 width/height。

除了 scrollLeft/scrollTop 外，所有属性都是只读的。如果我们修改 scrollLeft/scrollTop，浏览器会滚动对应的元素。

## 63. Window 大小和滚动

几何：

- 文档可见部分的 width/height（内容区域的 width/height）：document.documentElement.clientWidth/clientHeight

- 整个文档的 width/height，其中包括滚动出去的部分：

  let scrollHeight = Math.max( document.body.scrollHeight, document.documentElement.scrollHeight, document.body.offsetHeight, document.documentElement.offsetHeight, document.body.clientHeight, document.documentElement.clientHeight );

滚动：

- 读取当前的滚动：window.pageYOffset/pageXOffset。
- 更改当前的滚动：
  - window.scrollTo(pageX,pageY) — 绝对坐标，
  - window.scrollBy(x,y) — 相对当前位置进行滚动，
  - elem.scrollIntoView(top) — 滚动以使 elem 可见（elem 与窗口的顶部/底部对齐）。

## 64. 浏览器事件简介

这里有 3 种分配事件处理程序的方式：

1. HTML 特性（attribute）：onclick="..."。
2. DOM 属性（property）：elem.onclick = function。
3. 方法（method）：elem.addEventListener(event, handler[, phase]) 用于添加，removeEventListener 用于移除。

HTML 特性很少使用，因为 HTML 标签中的 JavaScript 看起来有些奇怪且陌生。而且也不能在里面写太多代码。

DOM 属性用起来还可以，但我们无法为特定事件分配多个处理程序。在许多场景中，这种限制并不严重。

最后一种方式是最灵活的，但也是写起来最长的。有少数事件只能使用这种方式。例如 transtionend 和 DOMContentLoaded（上文中讲到了）。addEventListener 也支持对象作为事件处理程序。在这种情况下，如果发生事件，则会调用 handleEvent 方法。

无论你如何分类处理程序 —— 它都会将获得一个事件对象作为第一个参数。该对象包含有关所发生事件的详细信息。

## 65. 冒泡和捕获

当一个事件发生时 —— 发生该事件的嵌套最深的元素被标记为“目标元素”（event.target）。

- 然后，事件从文档根节点向下移动到 event.target，并在途中调用分配了 addEventListener(..., true) 的处理程序（true 是 {capture: true} 的一个简写形式）。
- 然后，在目标元素自身上调用处理程序。
- 然后，事件从 event.target 冒泡到根，调用使用 on、HTML 特性（attribute）和没有第三个参数的，或者第三个参数为 false/{capture:false} 的 addEventListener 分配的处理程序。

每个处理程序都可以访问 event 对象的属性：

- event.target —— 引发事件的层级最深的元素。
- event.currentTarget（=this）—— 处理事件的当前元素（具有处理程序的元素）
- event.eventPhase —— 当前阶段（capturing=1，target=2，bubbling=3）。

任何事件处理程序都可以通过调用 event.stopPropagation() 来停止事件，但不建议这样做，因为我们不确定是否确实不需要冒泡上来的事件，也许是用于完全不同的事情。

捕获阶段很少使用，通常我们会在冒泡时处理事件。这背后有一个逻辑。

在现实世界中，当事故发生时，当地警方会首先做出反应。他们最了解发生这件事的地方。然后，如果需要，上级主管部门再进行处理。

事件处理程序也是如此。在特定元素上设置处理程序的代码，了解有关该元素最详尽的信息。特定于 的处理程序可能恰好适合于该 ，这个处理程序知道关于该元素的所有信息。所以该处理程序应该首先获得机会。然后，它的直接父元素也了解相关上下文，但了解的内容会少一些，以此类推，直到处理一般性概念并运行最后一个处理程序的最顶部的元素为止。

## 66. 事件委托

它通常用于为许多相似的元素添加相同的处理，但不仅限于此。

算法：

1. 在容器（container）上放一个处理程序。
2. 在处理程序中 —— 检查源元素 event.target。
3. 如果事件发生在我们感兴趣的元素内，那么处理该事件。

好处：

- 简化初始化并节省内存：无需添加许多处理程序。
- 更少的代码：添加或移除元素时，无需添加/移除处理程序。
- DOM 修改 ：我们可以使用 innerHTML 等，来批量添加/移除元素。

事件委托也有其局限性：

- 首先，事件必须冒泡。而有些事件不会冒泡。此外，低级别的处理程序不应该使用 event.stopPropagation()。
- 其次，委托可能会增加 CPU 负载，因为容器级别的处理程序会对容器中任意位置的事件做出反应，而不管我们是否对该事件感兴趣。但是，通常负载可以忽略不计，所以我们不考虑它。

## 67. 浏览器默认行为

有很多默认的浏览器行为：

- mousedown —— 开始选择（移动鼠标进行选择）。
- 在 上的 click —— 选中/取消选中的 input。
- submit —— 点击 或者在表单字段中按下 Enter 键会触发该事件，之后浏览器将提交表单。
- keydown —— 按下一个按键会导致将字符添加到字段，或者触发其他行为。
- contextmenu —— 事件发生在鼠标右键单击时，触发的行为是显示浏览器上下文菜单。
- ……还有更多……

如果我们只想通过 JavaScript 来处理事件，那么所有默认行为都是可以被阻止的。

想要阻止默认行为 —— 可以使用 event.preventDefault() 或 return false。第二个方法只适用于通过 on 分配的处理程序。

addEventListener 的 passive: true 选项告诉浏览器该行为不会被阻止。这对于某些移动端的事件（像 touchstart 和 touchmove）很有用，用以告诉浏览器在滚动之前不应等待所有处理程序完成。

如果默认行为被阻止，event.defaultPrevented 的值会变成 true，否则为 false。

## 68. 创建自定义事件

要从代码生成一个事件，我们首先需要创建一个事件对象。

通用的 Event(name, options) 构造器接受任意事件名称和具有两个属性的 options 对象：

- 如果事件应该冒泡，则 bubbles: true。
- 如果 event.preventDefault() 应该有效，则 cancelable: true。

其他像 MouseEvent 和 KeyboardEvent 这样的原生事件的构造器，都接受特定于该事件类型的属性。例如，鼠标事件的 clientX。

对于自定义事件，我们应该使用 CustomEvent 构造器。它有一个名为 detail 的附加选项，我们应该将事件特定的数据分配给它。然后，所有处理程序可以以 event.detail 的形式来访问它。

尽管技术上可以生成像 click 或 keydown 这样的浏览器事件，但我们还是应谨慎使用它们。

我们不应该生成浏览器事件，因为这是运行处理程序的一种怪异（hacky）方式。大多数时候，这都是糟糕的架构。

可以生成原生事件：

- 如果第三方程序库不提供其他交互方式，那么这是使第三方程序库工作所需的一种肮脏手段。
- 对于自动化测试，要在脚本中“点击按钮”并查看接口是否正确响应。

使用我们自己的名称的自定义事件通常是出于架构的目的而创建的，以指示发生在菜单（menu），滑块（slider），轮播（carousel）等内部发生了什么。

## 69. 鼠标事件

鼠标事件有以下属性：

- 按钮：button。
- 组合键（如果被按下则为 true）：altKey，ctrlKey，shiftKey 和 metaKey（Mac）。
  - 如果你想处理 Ctrl，那么不要忘记 Mac 用户，他们通常使用的是 Cmd，所以最好检查 if (e.metaKey || e.ctrlKey)。
- 窗口相对坐标：clientX/clientY。
- 文档相对坐标：pageX/pageY。

mousedown 的默认浏览器操作是文本选择，如果它对界面不利，则应避免它。

## 70. 移动鼠标：mouseover/out，mouseenter/leave

以下这些内容要注意：

- 快速移动鼠标可能会跳过中间元素。
- mouseover/out 和 mouseenter/leave 事件还有一个附加属性：relatedTarget。这就是我们来自/到的元素，是对 target 的补充。

即使我们从父元素转到子元素时，也会触发 mouseover/out 事件。浏览器假定鼠标一次只会位于一个元素上 —— 最深的那个。

mouseenter/leave 事件在这方面不同：它们仅在鼠标进入和离开元素时才触发。并且它们不会冒泡。

## 71. 事件：change，input，cut，copy，paste

数据更改事件:

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9e285fb7c2b4429187300847969003f1~tplv-k3u1fbpfcp-watermark.image)

[TOC]

