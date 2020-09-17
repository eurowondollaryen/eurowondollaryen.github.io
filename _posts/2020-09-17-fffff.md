---
title: Linux Commands
author: Seho Kim
date: 2020-09-17 23:48:00 +0800
categories: [Linux]
tags: [Linux]
pin: true
math: true
comments: true
---

## **Linux Commands**
### 최근 수정 파일 찾기
- `find [검색하려는 폴더] -type -f -mtime -30 -ls`
- `find . -type -f -mtime -30 -ls`

### Linux 캐릭터셋 확인 및 변경
- Charset 확인 명령어 : `locale`
- 현재 시스템에서 지원하는 locale 목록 확인 : `locale -a`

### Charset 변경 (파일에서 UTF-8, EUC-KR 변경 시)
- `vi /etc/sysconfig/i18n`

### 현재의 Shell에서 charset 변경
- `export LANG=ko_KR.euckr`

### os 종 확인
- `uname -a`

### os version
- `cat /etc/issue`

### shell type 확인
- `echo $SHELL`
- 결과 : `usr/bin/ksh`

### 참고) windows에서 작성한 shell script가 ksh에서 동작하지 않을 때
#### 증상
`ksh: [파일명.sh] : not found~~~`
#### 원인
- 윈도우는 줄바꿈을 CR-LF(DOS 개행문자)로 하지만, 유닉스는 LF로 줄바꿈을 한다.
- `vi 파일명.sh` 하면 각 문자열 끝에 ^M이라는 문자가 들어가 있음.(개행문자 CR이 깨진 흔적)
#### 해결방법
1. vi에서 :setff=unix 입력하여 DOS파일 타입을 UNIX 타입으로 세팅
2. vi에서 각 행의 끝에 있는 ^M 문자를 모두 공백으로 바꾸기
- `:%S/^M$//g` => ^M 쓰는 법 : Ctrl + v > Ctrl + m
