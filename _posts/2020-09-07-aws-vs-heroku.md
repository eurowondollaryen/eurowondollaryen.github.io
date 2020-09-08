---
title: AWS vs Heroku
author: Seho Kim
date: 2020-09-07 23:48:00 +0800
categories: [Tech]
tags: [AWS, Heroku]
pin: true
math: true
comments: true
---

## **AWS, Heroku 고려사항**

Heroku : 코드만 보내면 바로 된다. (PaaS)
AWS EC2 : 인프라를 위한 비용을 주고 인프라만 사용한다. 설정은 알아서 해야 함. (IaaS)

### 선택 시 고려 사항

1. 가격 : Heroku < AWS EC2
* Heroku는 AWS 위에서 돌아가므로, 더 비쌀수밖에 없다.

2. 시간 : Heroku > AWS EC2

3. 자유도 : Heroku < AWS EC2
* Heroku는 기술의 선택에 대한 자유도가 낮다.
* 하지만 AWS EC2는 컴퓨터 그 자체를 빌리는 것이기 때문에, 원하는 대로 할 수 있다.

#### 개인적인 생각
* Heroku는 토이프로젝트를 빨리빨리 배포하고 싶을 때 사용하면 좋을 것 같다.
* 그리고 AWS는 진짜 제대로 된 프로젝트를 만들고자 할 때 사용하면 좋을듯 