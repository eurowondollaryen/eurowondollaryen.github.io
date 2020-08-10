---
title: Javascript 정리 - (2)
author: Seho Kim
date: 2020-08-10 23:42:00 +0800
categories: [Javascript]
tags: [Javascript, Function]
pin: true
---


## **함수와 프로토타입 체이닝**
Javascript의 함수는 여느 언어의 함수와 마찬가지의 기능도 하지만, 다음 기능도 있다.
* 모튤화 처리
* 클로저
* 객체 생성
과 같이 Javascript의 근간이 되는 많은 기능을 제공하고 있다.

### **함수 선언 방법 3가지**
1. 함수 선언문
* 가장 일반적인 선언 방식이다. 이 방식의 경우, 반드시 함수명이 정의되어 있아야 한다.
```js
//함수 리터럴만 사용하여 선언하는 방식
function add(x, y) {
	return x + y;
}
```
2. 함수 표현식
* 함수도 하나의 값처럼 취급된다. 함수 리터럴을 사용하여 만든 함수를 변수에 집어넣는 방식
* 다른 변수에 대입하는 것도 가능하다. 이 때, 아래의 add, plus 변수는 동일 함수를 참조하게 된다.
```js
//익명 함수를 이용한 함수 표현식 방식 선언
var add = function (x, y) {//익명 함수(anonymus function)
	return x + y;
};
var plus = add;
console.log(add(3,4)); // 결과 : 7
console.log(plus(3,4)); //결과 : 7
```
3. `Function()` 생성자 함수