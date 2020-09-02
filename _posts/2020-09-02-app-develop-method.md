---
title: 앱 개발 방식 3가지(하이브리드, 크로스플랫폼, 네이티브)
author: Seho Kim
date: 2020-09-02 23:50:00 +0800
categories: [tech]
tags: [mobile application]
pin: true
---

## **앱 개발 프레임워크 3가지 및 장단점**

### **1. 하이브리드앱**
* Apache Cordova(Ionic - ui를 위한 js 라이브러리이며, cordova가 내가 짠 웹페이지의 웹뷰를 감싸주는 역할을 한다.)
* PhoneGap(아는 바가 없음.)

  #### **동작 원리**
  * 웹뷰 위에서 돌아간다.
  * 마켓에 배포하는 것은 웹뷰임

  #### **장점**
  * native app에 대한 지식이 필요없다. 만들기 쉽다. html, css, js만 알면 된다.

  #### **단점**
  * UI를 한땀한땀 다 짜야한다.
  * OS단의 고급 기능을 사용할 수 없다. ex) 비디오 관련 기능 등..
  * 기본 카메라, 위치, 네트워크 정보, 연락처, 파일 시스템 까지는 지원함.

### **2. 크로스플랫폼앱**
* Flutter (Dart -> C/C++)
* Xamarin (C# -> IL(Intermediate Language, ios/android 둘 다 이해 가능한 언어))
* React Native

  #### **동작 원리**
  * 네이티브코드가 아닌걸로 코딩한 후 ios/android native로 변환함
  * 코드 작성 후, 이것을 js코드로 변환 후, 
  * 백엔드, java 개발자 등 다양한 개발자들이 할 수 있음
  * 그래도 네이티브가 아니라서 성능 이슈가 생길 수 있다.

  #### **장점**
  * 기존에 쓰던 언어 재탕 가능(하나의 언어로 두 플랫폼 배포 가능, 심지어 웹까지)
  * low cost
  * large reach
  * 관리 편함

  #### **단점**
  * 성능이슈
  * 그래픽 퀄리티
  * 네이티브 만의 기능 x
  * 느린 업데이트

### **3. 네이티브 앱**
* Java/Kotlin(Android Studio, Android IDE, Intellij IDEA)
* swift(XCode, AppCode, Atom)

  #### **동작 원리**
  * 별도 가공 과정을 거치지 않고 머신에서 컴파일되어 돌아간다.
  * 각 플랫폼마다의 구동 방식은 나중에..

  #### **장점**
  * 폰의 모든기능, 파워를 다 사용 가능(고급 기술을 사용하려면 필요함. 3d라든지..그래픽적으로)

  #### **단점**
  * 2가지 플랫폼의 언어를 배워야 하는 점
  * 맥북 사야함

### **내 생각**
> React Native는 써봤는데 느림.
> 간단한거는 Ionic & Cordova으로 만들고 각 잡고 만들거면 네이티브로 만드는 게 좋다고 생각함.

### **참조**
* [Mobile App Development Approaches Explained](https://railsware.com/blog/native-vs-hybrid-vs-cross-platform/)
* [youtube - 노마드 코더](https://www.youtube.com/watch?v=ksz_mSninEY)