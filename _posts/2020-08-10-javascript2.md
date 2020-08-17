---
title: Javascript 정리 - (2) 함수와 프로토타입 체이닝
author: Seho Kim
date: 2020-08-10 23:42:00 +0800
categories: [Javascript]
tags: [Javascript, Function]
pin: true
---


## **1. 함수**
Javascript의 함수는 여느 언어의 함수와 마찬가지의 기능도 하지만, 다음 기능도 있다.
* 모튤화 처리
* 클로저
* 객체 생성
과 같이 Javascript의 근간이 되는 많은 기능을 제공하고 있다.

### **1.1 함수 선언 방법 3가지**
1. 함수 선언문
* 가장 일반적인 선언 방식이다. 이 방식의 경우, 반드시 함수명이 정의되어 있아야 한다.
```js
//함수 리터럴만 사용하여 선언하는 방식
function add(x, y) {
	return x + y;
}
```
2. 함수 표현식(익명 함수 표현식/기명 함수 표현식)
* 함수도 하나의 값처럼 취급된다. 함수 리터럴을 사용하여 만든 함수를 변수에 집어넣는 방식
* 다른 변수에 대입하는 것도 가능하다. 이 때, 아래의 add, plus 변수는 동일 함수를 참조하게 된다.
```js
//익명 함수 표현식 선언
var add = function (x, y) {//익명 함수(anonymus function)
	return x + y;
};
var plus = add;
console.log(add(3,4)); // 결과 : 7
console.log(plus(3,4)); //결과 : 7
```
* 기명 함수 표현식으로 선언할 때 주의할 점은, 변수명이 아닌 함수 리터럴의 명칭을 사용하면 안된다는 것이다.
* 다만, **리터럴의 내부에서는** 함수 리터럴의 명칭을 사용할 수 있다.
```js
//기명 함수 표현식 선언
var add = function sum(x, y) {
	return x + y;
};
console.log(add(3,4)); // 결과 : 7
console.log(sum(3,4)); // 결과 : Uncaught ReferenceError : sum is not defined 에러
```

#### **Function statement(함수 선언문)와 Function expression(함수 표현식)에서의 세미콜론**
함수 선언문 방식에서는 닫는 중괄호 끝에 세미콜론을 붙이지 않지만, 함수 표현식에서는 붙인다. 왜일까?
* Javascript 인터프리터는 자동으로 세미콜론을 삽입시켜 주기 때문에, 웬만해서는 logical error가 발생하지 않는다.
* 그러나, Function expression 방식에서 세미콜론을 붙이지 않으면 의도치 않은 에러가 발생 가능하다.
```js
var func = function() {
	return 42;
} //no semicolon
(function() {
	console.log("function called");
})();
//실행 결과 : number is not a function
```
* 원인 : Javascript parser가 `func()` 함수 정의 시, `return 42;}`뒤의 `function()`을 보고, `func()`를 호출하도록 작동한 것.
3. `Function()` 생성자 함수로 함수 생성하기
* 이 문법은 자주 사용되는 문법은 아니지만, 위 두 가지 방식(함수 선언문/표현식) 모두 내부적으로는 이 생성자 함수를 통해 생성된다.
```js
new Function(arg1, arg2, arg3, ..., argN, functionBody);
var add = new Function('x', 'y', 'return x + y');
console.log(add(3,4));//결과 : 7
```
#### **함수 호이스팅 **
* 더글러스 크락포드라는 JS Guru는 **함수 표현식**만을 사용하는 것을 권장한다.
* 그 이유가 바로 함수 호이스팅이다.
* 함수 호이스팅이란? : 함수 선언문으로 선언하면 선언문 위에서도 사용할 수 있고, 함수 표현식으로 선언하면, 선언문 위에서는 사용할 수 없는 현상.
* 함수 호이스팅이 발생하는 이유? : JS의 **변수 생성**과 **초기화**의 작업이 분리되어 진행되기 때문이다.
```js
//선언문 방식
add(2, 3); //5
function add(x, y) {
	return x + y;
}
//표현식 방식
plus(2, 3);//uncaught type error
var plus = function(x, y) {
	return x + y;
};
```

### **1.2 함수 객체란?**
* JS에서는 함수도 객체로 취급된다. 함수도 객체처럼 property를 가질 수 있다.
* 내부에서는 어떻게 동작할까?
* `add()`함수 생성 시, JS는 add 객체의 **`[[Code]]` 내부 property에 자동으로 함수 코드를 저장한다.**
```js
function add(x, y) {
	return x + y;
}
add.result = add(1,2);
add.hello = 'hello';
console.log(add.result);// 3
console.log(add.hello);// 'hello'
```

### **1.3 일급 객체란?**
* 리터럴에 의해 생성
* 변수나 배열의 요소, 객체의 property등에 할당 가능
* 함수의 인자로 전달 가능
* 함수의 리턴값으로 전달 가능
* 동적으로 property를 생성/할당 가능
> 일급 객체의 특성을 이용하여 함수형 프로그램이 가능하다.
> JS의 함수는 다른 언어의 함수와 비슷하지만, JS의 함수를 제대로 이해하려면, 일반 객체처럼 값으로 취급된다는 것을 이해해야 한다.
> property, parameter, return value

### **1.4 함수 객체의 기본 property**
* JS에서는 함수도 객체다.
* 함수는 일반 객체와는 다르게, 함수 객체만의 표준 property가 존재한다.
```js
var add = function(a, b) {
	return a + b;
};
console.dir(add);
```
* 결과
* 함수 객체에는 기본적으로 arguments, caller, length, name 등이 생성되어 있는 것을 확인할 수 있다.
* ECMA5 Script 명세서에는 모든 함수가 `length`, `prototype` property를 가져야 한다고 기술하고 있다.
1. `arguments` : 함수의 parameter를 갖고있는 object
2. `caller` : 자신을 호출한 함수명
3. `length` : 함수의 parameter의 개수를 의미하는 property
```js
ƒ add(a, b)
arguments: null
caller: null
length: 2
name: "add"
prototype: {constructor: ƒ}
__proto__: ƒ ()
[[FunctionLocation]]: VM90:1
[[Scopes]]: Scopes[2]
```
* 함수 객체의 property 관련 특징
1. 모든 함수는 Function.prototype 이라는 prototype 객체를 갖는다.
2. Function.prototype 객체 또한 함수 객체이다.
3. Function.prototype 객체는 Object.prototype 객체를 상속받는다.

* Function.prototype 객체가 가져야 할 property(ECMAScript)
1. constructor property
2. toString() 메서드
3. apply(thisArg, argArray) 메서드 => 자주 활용되는 중요한 메서드
4. bind(thisArg, [arg1, [arg2,]]) 메서드
