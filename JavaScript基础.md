# JS入门
## 一、==和===的区别
* 使用==比较时，会自动转换数据类型，比如
~~~
10 == '10';  //true
~~~
* 使用===比较时，则不会自动转换类型，如果比较前后数据类型不一致，直接返回 false,由于==会自动转换数据类型，所以大多数时候使用===比较。  
**注意**  NaN是一个特殊的Number，它与其他任何数都不等，包括它自己。  
~~~javascript
NaN === NaN;   //false
~~~
>唯一能判断NaN的方法是通过isNaN()方法:
~~~javascript
isNaN(NaN);  //true
~~~
>浮点数的比较很坑(因为计算机无法精确表示无限不循环小数)，比如：
~~~javascript
1 / 3 === (1 - 2 / 3);  //false
~~~
## 二、字符串中的常用方法
* toUpperCase() 将一个字符串全部变成大写  
~~~javascript
'Hello,World'.toUpperCase()  //返回"HELLO,WORLD"
~~~
* toLowerCase() 将一个字符串全部变成大写  
~~~javascript
'Hello,World'.toLowerCase()  //返回"hello,world"
~~~
* indexOf() 返回指定字符串出现的位置，如果原字符串没有指定字符串则返回-1，比如：
~~~javascript
var a = 'Hello,World';
a.indexOf('World');  //返回6
a.indexOf('world');  //返回-1
~~~
* substring() 返回指定索引区间的子串,比如：
~~~javascript
var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
~~~
## 三、数组中的常用方法
* indexOf() 搜索一个指定元素的位置，例如：
~~~javascript
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
~~~
* slice() 截取数组的部分元素，返回一个新的数组，例如：
~~~javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
~~~
>如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array：
~~~javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
~~~
* pop和push
>>push()向数组末尾添加若干元素，pop()则把数组最后一个元素删掉，例如：
~~~javascript
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
~~~
* unshift和shift
>>如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则把Array的第一个元素删掉：
~~~javascript
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
~~~
* sort()可以对当前数组进行排序，它会直接修改当前数组的元素位置，直接调用时，按照默认顺序排序：
~~~javascript
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
var arr1 = [3, 5, 1, 2, 4];
arr1.sort();
arr1;   //[1, 2, 3, 4, 5]
~~~
* reverse() 把整个数组的元素反转：
~~~javascript
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
~~~
* splice() 方法是从指定的索引开始删除若干元素，然后也可以从该位置添加若干元素：
~~~javascript
//Array.splice(start, number, ...需要删除的字符串),表示从start开始(包括start),删除number个元素
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素,注意,添加的时候是从start开始添加的:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
~~~
* concat() 方法把当前的数组和另一个数组连接起来，并返回一个新的数组：
~~~javascript
var arr1 = ['A', 'B', 'C'];
var arr2 = [1, 2, 3];
var added = arr1.concat(arr2);
added; // ['A', 'B', 'C', 1, 2, 3]
arr1; // ['A', 'B', 'C']
~~~
>**<font color="#f00">注意：</font>**concat()方法并没有修改当前数组，而是返回了一个新的数组。concat()方法也可以接收任意个元素和数组，并且自动把数组拆开，然后全部添加到新的数组里：
~~~javascript
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
~~~
* join()方法是把当前数组的每个元素都用指定的字符串连接起来，然后返回连接后的**<font color="#f00">字符串</font>**：
~~~javascript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
~~~
## 四、对象
* 如果要判断对象是否拥有某属性用in操作符，例如：
~~~javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
~~~
>**<font color="#f00">注意：</font>**in属性是判断对象中的所有属性，包括该对象继承的属性，例如：
~~~javascript
'toString' in xiaoming;   //true
~~~
>要判断一个属性是否是对象自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：
~~~javascript
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
~~~
## 五、循环
* for in：for循环的一个变体是for ... in循环，它可以把一个对象的所有属性依次循环出来，例如：
~~~javascript
var obj = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in obj) {
    console.log(key); // 'name', 'age', 'city'
}
~~~
## 六、Map
* 初始化Map需要一个二维数组，或者直接初始化一个空Map。Map具有以下方法：
~~~javascript
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59); // 添加新的key-value
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
~~~
由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值替换：
~~~javascript
var m = new Map();
m.set('Adam', 67);
m.set('Adam', 88);
m.get('Adam'); // 88
~~~
## 七、Set
* 创建Set可以传入一个数组或者不传入参数，例如：
~~~javascript
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
~~~
>**<font color="#f00">注意：</font>**重复元素在Set中自动被过滤
>Set中的常用方法
>
> * add()添加一个key,delete()删除一个key：
>~~~javascript
>var s = new Set([1, 2, 3, 3, '3']);
>s; // Set {1, 2, 3, "3"}
>s.add(4);
>s; // Set {1, 2, 3, "3", 4}
>s.add(4);
>s; // 仍然是 Set {1, 2, 3, "3", 4}
>s.delete(4);
>s; // 仍然是 Set {1, 2, 3, "3"}
>~~~
## 八、iterable
* Map、Set、Array都属于iterable类型。
* for...in 与 for...of 的区别
>for...in 遍历时遍历的是对象的属性，for...of 遍历的是对象的值，例如：
>~~~javascript
>var a = ['A', 'B', 'C'];
>a.name = 'Hello';
>for (var x in a) {
>    console.log(x); // '0', '1', '2', 'name'
>}
>for (var of in a) {
>    console.log(x); // '0', '1', '2'
>}
>~~~
## 九、变量提升
* JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部：
~~~javascript
function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}
foo();
//上面代码相当于
function foo() {
    var y; // 提升变量y的申明，此时y为undefined
    var x = 'Hello, ' + y;
    console.log(x);
    y = 'Bob';
}
~~~