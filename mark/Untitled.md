[TOC]

# AngularJS教程

## 1. angularJS资源

* [http://www.angularjs.org](http://www.angularjs.org)
* https://www.github.com/angular/
* http://www.angularjs.cn/
* http://www.ngnice.com/
* http://woxx.sinaapp.com/
* http://www.angularjs.net.cn/api/ng/

## 2. angularJS下载

* http://www.bootcdn.cn/angular.js/
* node.js服务器下载....
  * npm install angular

## 3. 简单演示

* ###### 例子一：使用模块方式单向绑定{#1}

```html
<!DOCTYPE html>
<html ng-app="module">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<script src="./1.3.6/angular.min.js"></script>
<script>
	var module = angular.module("module", []);
	module.controller("Aaa", function($scope) {
		$scope.name = "hello";
	});
</script>
</head>

<body>
	<div ng-controller="Aaa">
    	<p>{{name}}</p>
    </div>
    <div>
    </div>
</body>
</html>  
```

`angular.module("module", [])`当前页面没有依赖的模块**_参数二_**给空数组



* 例子二：双向数据绑定（MVVM）

```html
<!DOCTYPE html>
<html ng-app="module">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<script src="./1.3.6/angular.min.js"></script>
<script>
	var module = angular.module("module", []);
	module.controller("Aaa", ["$scope", function($scope) {
		$scope.name = "hello";
	}]);
</script>
</head>

<body>
	<div ng-controller="Aaa">
		<input type="text" ng-model="name">
    	<p>{{name}}</p>
    </div>
    <div>
    </div>
</body>
</html>
```
运行结果:![](F:\study\java\AngularJS\笔记\2.png)

相比第一个[例子一](#1),这里的controller的第二个参数为数组，这种写法可以解决代码压缩<font color="red">形式参数</font>丢失的情况



* 模版过滤器、函数监听、字段属性监听

```html
<!DOCTYPE html>
<html ng-app="module">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<script src="./1.3.6/angular.min.js"></script>
<script>
	var module = angular.module("module", []);
	module.controller("Aaa", ["$scope", function($scope) {
		$scope.iphone = {
			price : 5,
			num : 1,
			free : 10
		};
		/**
		* 计算总价
		*/
		$scope.sum = function() {
			return $scope.iphone.price * $scope.iphone.num;
		}
		
		/**
		* 满100包邮
		*/
		/*$scope.$watch("iphone", function() {
			if($scope.sum() >= 100) {
				$scope.iphone.free = 0;
			} else {
				$scope.iphone.free = 10;
			}
		}, true);*/
		
		/**
		* 写法2
		*/
		$scope.$watch($scope.sum, function(newValue, oldValue) {
			$scope.iphone.free = newValue >= 100 ? 0 : 10;
		});
		
	}]);
</script>
</head>

<body>
	<div ng-controller="Aaa">
    	<p>商品价格：<input type="text" ng-model="iphone.price"></p>
		<p>商品数量：<input type="text" ng-model="iphone.num"></p>
		<p>总价：{{sum() | currency:"￥"}}</p>
		<p>运费：{{iphone.free | currency:"￥"}}</p>
		<p>应付：{{sum() + iphone.free | currency:"￥"}}</p>
    </div>
    <div>
    </div>
</body>
</html>
```



## 4. 常用函数
### AngularJS `ng` 模块的 `function`组件

| 名称                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [angular.bootstrap](http://www.angularjs.net.cn/api/52.html) | 用于手动加载angularjs模板                                    |
| [angular.copy](http://www.angularjs.net.cn/api/53.html)      | 复制一个对象或者一个数组                                     |
| [angular.element](http://www.angularjs.net.cn/api/54.html)   | 包裹着一部分DOM element或者是HTML字符串，把它作为一个jQuery元素来处理 |
| [angular.equals](http://www.angularjs.net.cn/api/55.html)    | 比较两个值或者两个对象是不是相等                             |
| [angular.forEach](http://www.angularjs.net.cn/api/56.html)   | 循环对obj对象的每个元素调用iterator                          |
| [angular.fromJson](http://www.angularjs.net.cn/api/57.html)  | 把Json字符串转为对象                                         |
| [angular.identity](http://www.angularjs.net.cn/api/58.html)  | 返回它第一参数的函数                                         |
| [angular.extend](http://www.angularjs.net.cn/api/59.html)    | 复制src对象中的属性去dst对象中                               |
| [angular.injector](http://www.angularjs.net.cn/api/60.html)  | 创建一个injector对象, 调用injector对象的方法可以获得angular的service, 或者用来做依赖注入 |
| [angular.bind](http://www.angularjs.net.cn/api/51.html)      | 上下文，函数以及参数动态绑定                                 |
| [angular.isArray](http://www.angularjs.net.cn/api/61.html)   | 判断参数是否是数组                                           |
| [angular.isDate](http://www.angularjs.net.cn/api/62.html)    | 判断参数是否是时间类型                                       |
| [angular.isDefined](http://www.angularjs.net.cn/api/63.html) | 判断参数是否是定义引用                                       |
| [angular.isElement](http://www.angularjs.net.cn/api/64.html) | 判断参数是否是一个DOM元素（或用jQuery元素）                  |
| [angular.isFunction](http://www.angularjs.net.cn/api/65.html) | 判断参数是否是一个函数                                       |
| [angular.isNumber](http://www.angularjs.net.cn/api/66.html)  | 判断参数是否是一个Number                                     |
| [angular.isObject](http://www.angularjs.net.cn/api/67.html)  | 判断参数是否是一个对象                                       |
| [angular.isstring](http://www.angularjs.net.cn/api/68.html)  | 判断参数是否是一个字符串                                     |
| [angular.isUndefined](http://www.angularjs.net.cn/api/69.html) | 判断参数是否是一个Undefined                                  |
| [angular.lowercase](http://www.angularjs.net.cn/api/70.html) | 将指定的字符串转换为小写                                     |
| [angular.module](http://www.angularjs.net.cn/api/71.html)    | 注册或检索模块                                               |
| [angular.noop](http://www.angularjs.net.cn/api/72.html)      |                                                              |
| [angular.toJson](http://www.angularjs.net.cn/api/73.html)    | 把对象转为Json字符串                                         |
| [angular.uppercase](http://www.angularjs.net.cn/api/74.html) | 将指定的字符串转换为大写                                     |


> ### angular.bind()

可以改this指向，和`$.proxy()` 一样

```javascript
function show(n1, n2) {
    console.log(n1);
    console.log(n2);
    console.log(this);
}
//angular.bind(document, show, 3, 4)();

/*
function show(){
　　alert(this+"调用了show")
}
var c=angular.bind("c",show);
c();
// C 调用了show
*/

//调用了show方法，带3和4两个参数，this是指向window
angular.bind(window, show, 3)(4);

angular.bind(document, show, 2, 3)();
```

运行结果:
![](F:\study\java\AngularJS\笔记\QQ拼音截图未命名.png)



> ### angular.copy()

对象拷贝

```javascript
var a = {name : "hello"};
var b = {age : "20"};
var c = angular.copy(a,b);
console.log(b);
```

运行结果：

```
{name: "hello"}
```



> ### angular.clone()

用于深度复制对象

```js
var cloneObj=angular.clone(obj);
```



> ### angular.bootstrap()

动态初始化

```javascript
angular.bootstrap(document, "[myApp]");
```

等同于

```html
<html ng-app="myApp">
</html>
```

通常用法，如点击页面时初始化

```javascript
document.onclick = function() {
    angular.bootstrap(document, "myApp");
};
```

## 5. 服务

> ### $scope.$apply(function(){})

$apply可以使在源生js代码中使用angular

```javascript
var myApp = angular.module("myApp", []);
myApp.controller("Aaa", ["$scope", "$timeout", function($scope, $timeout) {
    $scope.name = "hello";
    setTimeout(function(){
        $scope.$apply(function() {
            $scope.name = "hi";
        });
    }, 2000);
}]);
```

