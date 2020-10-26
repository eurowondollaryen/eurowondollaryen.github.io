---
title: Java 알고리즘 문제 풀이 시
author: Seho Kim
date: 2020-10-26 23:57:00 +0800
categories: [Java]
tags: [algorithm]
pin: true
math: true
comments: true

---

**java algorithm snippet**
======================================
```java
Collections.sort(sizes, new Comparator<Integer>() {
			@Override
			public int compare(Integer a, Integer b) {
				return a.compareTo(b);
			}
		});
```