---
title: Javascript 정리 - (1)
author: Seho Kim
date: 2020-08-08 01:20:00 +0800
categories: [Javascript]
tags: [Javascript, Variables]
pin: true
---


## **Javascript 개요 ~ Javascript 객체**
아래 4가지 개념은 제대로 알아야 Javascript 개발자라고 말할 수 있다고 생각하기 때문에, 이를 정리하고자 한다.
1. 객체
2. 함수
3. 프로토타입
4. 실행 컨텍스트, 클로저

#### **1. 객체**
Javascript에서 객체는 무엇일까?
* 기본 데이터 타입 : `boolean`, `number`, `string`, `null`, `undefined`

위 5가지를 제외한 모든 것이 객체이다.

#### **2. 함수**
- Javascript에서는 함수도 객체(일급 객체)로 취급한다.

#### **3. 프로토타입**
- 모든 객체는 숨겨진 링크인 prototype을 가진다.
- 이 링크는 해당 객체를 생성한 생성자의 프로토타입 객체를 가리킨다.
- 이 링크로 Javascript는 훨씬 더 다양하게 자신만의 자료 구조를 작성할 수 있다.
- 또한, 프로토타입을 이용하여 객체지향의 상속도 구현할 수 있다.

#### **4. 실행 컨텍스트, 클로저**
- js는 실행 컨텍스트를 만들고 그 안에서 실행이 이루어진다.
- 실행 컨텍스트는 자신만의 유효 범위를 갖는데, 이 과정에서 클로저를 구현할 수 있다.

#### **Javascript의 단점**
1. 유연하고 타입 체크가 느슨하기 때문에, 컴파일 에러는 런타임 에러로 넘어가게 되어 디버깅이 어렵다.
2. 최상위 레벨의 객체들은 모두 전역 객체 안에 위치하는데, 이는 충돌의 위험성이 있다.


### **1. Javascript Data type & Operator**
Javascript의 Data type은 총 2가지로 나뉜다.
* 기본 타입 : `Number`, `String`, `Boolean`, `undefined`, `null`
* 참조 타입(객체 타입) : `Object` - `Array`, `Function`, ``Regular Expression``

#### **1.1 Javascript 기본 타입**
1. Number
* Javascript에는 `Number`라는 하나의 타입만 존재한다.
* Javascript에서는 모든 숫자를 64비트 부동 소수점 형태로 저장하기 때문이다.
* Number 연산 시 주의사항 : 나눗셈 연산 결과를 정수로 받고 싶으면, Math.floor() 함수를 사용
```js
var num = 5 / 2;
console.log(num); // result : 2.5
console.log(Math.floor(num)); // result : 2.5
```

2. String
* C언어처럼 문자 하나만을 담는 타입은 없음.
* String 타입 주의사항 : 한 번 정의된 문자열은 C처럼 개별 문자를 수정할 수 없다.
```js
var str = 'hello';
console.log(str);
str[0] = 'a';
console.log(str); //예상 결과 : 'aello', 실제 결과 : 'hello'
str = 'bye';
console.log(str); //결과 : 'bye'
```
* Javascript에서는 한 번 생성된 문자열은 읽기만 가능하며, 수정은 불가능하다.
* 생성된 문자열을 굳이 다른 값으로 수정하고자 한다면, 문자열 자체를 String 변수에 대입해야 한다.

3. Boolean
* true/false 값을 나타냄. 특이사항 없음.

4. null & undefined
* 이 두 타입은 모두 Javascript에서 **"값이 비어있음"** 을 나타낸다.
* Javascript 환경 내애서 값이 할당되지 않은 변수는 `undefined` 타입이다.
* null은 값이 비어있음을 나타내는 데 사용한다.
* null, undefined 타입 주의사항 : null 타입을 체크할 때, typeof를 사용하지 말 것
```js
console.log(typeof null); //결과 : 'object'
console.log(typeof undefined); //결과 : 'undefined'
var nullVariable = null;
console.log(typeof nullVariable === null); //예상 결과 : true, 실제 결과 : false
console.log(nullVar === null); //결과 : true
```
정리
* `undefined`는 타입이자, 값을 나타낸다.
* `null`은 명시적으로 값이 비어있음을 나타낼 때 사용한다.
* `null`의 typeof 결과는 `Object`이다.

#### **1.2 Javascript 참조 타입(객체 타입)**
* Javascript에서 객체란 단순히 key:value 형태의 property들을 저장하는 컨테이너임.
* 이는 Hash 자료구조와 유사하다.
* 객체의 property는 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있다.

* 객체 생성 방법 3가지
1. Object() 생성자 함수
```js
//빈 객체를 생성하여 객체에 property를 집어넣는 방식
var obj = new Object(); // var obj = {} 로도 표기 가능
obj.prop1 = 'aaa';
obj.prop2 = 10;
console.log(typeof obj); //결과 : 'object'
console.log(obj); //결과 : { prop1 : 'aaa', prop2 : 10 }
```
2. 객체 리터럴 방식
```js
//변수 선언 시 객체의 property와 함께 초기화하는 방식
var obj = {
	prop1 : 'aaa',
	prop2 : 10
}
console.log(typeof obj); //결과 : 'object'
console.log(obj); //결과 : { prop1 : 'aaa', prop2 : 10 }
//결과는 1번 방식과 동일하다.
```
3. 생성자 함수
    - 함수를 통해서 객체를 생성하는 방법. 이후에 추가 작성

* 객체의 property 읽기/쓰기/갱신하기
    - 객체의 property 표기 방식은 2가지가 있다.
        1. 대괄호 표기법
        2. 마침표 표기법