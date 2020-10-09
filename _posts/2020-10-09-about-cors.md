---
title: CORS란?
author: Seho Kim
date: 2020-10-09 01:12:00 +0800
categories: [Tech]
tags: [cors]
pin: true
math: true
comments: true
---

## **CORS란?**
- Cross-Origin Resource Sharing
- A 도메인의 프론트엔드 JS 코드가 B 도메인에 request를 날리면, 브라우저는 보안상의 이유로, 해당 요청을 제한한다.
- ajax, fetch api는 동일 출처 정책을 따른다.
- 다른 domain의 리소스를 불러오려면, 그 출처(B 도메인에 해당하는 웹서버)에서 올바른 CORS 헤더를 포함한 응답을 반환해야 한다.
