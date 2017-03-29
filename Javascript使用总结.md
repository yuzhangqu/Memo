# Javascript使用总结
这里记录了编写Javascript代码的过程中遇到的有趣的问题及解决方案。

## 如何定义对象？
```javascript
function Person(first, last) {
	this.first = first;
	this.last = last;
}

Person.prototype.greeting = function() {
	code here
}
```

## 如何继承父类？
```javascript
function Teacher(first, last, subject) {
	Person.call(this, first, last);
}
Teacher.prototype = Object.create(Person.prototype);
Teacher.prototype.constructor = Person;
```

## 为什么便利数组不建议用`for...in`？
这种用法一般用在遍历字典上。对于纯数字的数组，`for...in`这种遍历方法只会得到下标字符串。

## 有哪些好用的小工具？
- `jquery.number.js`: 可将数字格式化为千分位带逗号
- `string-format.js`: 可实现字符串的带参数格式化

	```javascript
	String.prototype.format = function(replacements) {
		replacements = (typeof replacements === 'object') ? replacements : Array.prototype.slice.call(arguments, 0);
		return formatString(this, replacements);
	}
	
	var formatString = function(str, replacements) {
		replacements = (typeof replacements === 'object') ? replacements : Array.prototype.slice.call(arguments, 1);
		return str.replace(/\{\{|\}\}|\{(\w+)\}/g, function(m, n) {
			if (m == '{{') {
				return '{';
			}
			if (m == '}}') {
				return '}';
			}
			return replacements[n];
		});
	};
	```
	
## Array如何优雅地求和？
```javascript
[1, 2, 3].reduce((a, b) => a + b, 0);
```

## 怎么实现链式`setTimeout`调用？
```javascript
setTimeout(function foo() {
	code here
	setTimeout(foo, millisec);
}, millisec);
```

## 怎么让`setTimeout`的执行函数可以接受参数？
- 全局变量 + 匿名函数封装
- 接受参数，返回无参数的函数