## javascript中this的指向
* 在一个方法内部，this始终指向当前对象，例如：
~~~javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;//this指向xiaoming
    }
};

xiaoming.age; // function xiaoming.age()
xiaoming.age(); // 今年调用是25,明年调用就变成26了
~~~
~~~javascript
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;//this指向window,function是window对象的一个属性。当定义一个函数时，函数会自动被绑定到window上(window.getAge())。此时，window就是当前对象，this就相当于window，this.birth === window.birth，由于window中没有birth属性，故this.birth返回undefined。
}
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

console.log(xiaoming.age()); // 25, 正常结果
console.log(getAge()); // NaN
~~~
* 在一个方法内部嵌套一个函数，此时，this又会指向全局对象window。
~~~javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        function getAgeFromBirth() {
            var y = new Date().getFullYear();
            return y - this.birth;
        }
        return getAgeFromBirth();
    }
};
~~~
> 为解决方法内部嵌套函数指向this，首先用一个变量捕获this，例如：
~~~javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var that = this; // 在方法内部一开始就捕获this
        function getAgeFromBirth() {
            var y = new Date().getFullYear();
            return y - that.birth; // 用that而不是this
        }
        return getAgeFromBirth();
    }
};
~~~
* apply(需要绑定的this对象，[函数需要传入的参数]) 方法可以改变函数的this指向，例如：
~~~javascript
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};
xiaoming.age(); // 25
getAge.apply(xiaoming, []);
~~~
>call()方法与apply()方法类似，只是传参的时候略有不同，apply()方法是以数组形式传入，而call()方法是按顺序传入。