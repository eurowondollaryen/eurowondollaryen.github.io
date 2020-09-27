---
title: Oracle 대용량 파일 핸들링(FILE -> DB, DB -> FILE)
author: Seho Kim
date: 2020-09-20 23:03:00 +0800
categories: [Oracle]
tags: [oracle, sql loader]
pin: true
math: true
comments: true
---

## **1. FILE -> DB**
### **SQL LOADER**
- 파일 형태의 데이터를 Oracle DB에 구축하는 것을 도와주는 프로그램

### SQL LOADER 사용법
#### 준비물
- 컨트롤(.CTL)파일 (주의 : control 파일명은 영어로 시작해야함.. 숫자로 시작되면, memory fault 발생!)
- 데이터 파일 (.txt든 뭐든 내용에 구분자로 데이터가 나뉘어져 있으면 됨)
- 컨트롤 파일 내용 예시
```sql
LOAD DATA
INFILE [데이터 파일명].txt든
BADFILE [배드파일명].bad
DISCARDFILE [디스카드파일명].dsc
Append
INTO TABLE [데이터를 넣을 테이블]
FIELDS TERMINATED BY '\n' OPTIONALLY ENCLOSED BY '"'
(
	EMP_NO "REPLACE(TRIM(:EMP_NO),'-','')"
)
```

## **2. DB -> FILE**
- 내가 아는 DB TO FILE 추출 방법은 2가지가 있다.
1. 덤프 파일
2. SPOOL 기능
- 덤프는 해본 적이 없으므로.. SPOOL만 보자.
### **ORACLE SPOOL EXAMPLE**
```sql
SPOOL OFF --SPOOL 뜨기 전 버퍼를 비운다. 안 하면 SPOOL 내용이 끊겨 나올 수 있음.
SET TIMING OFF --명령어의 실행시간 표시여부 X
SET VERIFY OFF
SET ECHO OFF --명령이 표시되지 않게 세팅
SET FEEDBACK OFF --쿼리가 끝나고 N ROWS SELECTED 같은 문구가 뜨지 않음.
SET HEADING OFF --SELECT의 결과로 HEADER가 나오지 않게 세팅
SET PAGESIZE 0
SET LINES 3000
SET NUM 15
SET TERM OFF
SET TRIMSPOOL ON --TRIMSPOOL : SPOOL 결과에서 공백을 없앰(그냥 SPOOL 하면, 불필요한 공백이 생겨, 용량 잡아먹음)
SPOOL [내가 SPOOL할 파일명].txt
SELECT EMP_NO||'|'||EMP_NM||'|'||DEPT_NO
FROM EMPLOYEES;
SPOOL OFF
```
- 해당 명령이 끝나고, sqlplus를 종료하면, working directory에 [내가 SPOOL할 파일명].txt 파일에 조회된 SQL에 대한 내용이 추출된다.
