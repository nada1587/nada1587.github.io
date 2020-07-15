---
layout: post
title: 자바스크립트 기초 정리 - 07. queryString
subtitle : 데이터방식
tags: [javascript]
author: Sohyun Kim
comments : False
---

<h3>#queryString</h3>
**쿼리스트링이란?**   
웹 클라이언트에서 서버로 전달하는 입력 데이터를 전달하는 방식을 말함. URL주소에 미리 협의된 데이터를 파라미터를 통해 변수=값으로 구성하여 넘기는 것을 의미함.   
(key1=value1&key2=value2&key3=value3...)   
- post 방식(요청) : form 형식 데이터 전달(submit을 클릭하면 queryString으로 만들어 서버로 전달)   
- get 방식(응답) : http://URL?key1=value1&key2=value2
- 특수문자 표시   
   
| 화면출력  | url문자 또는 코드 | 화면출력 | url문자 또는 코드 |
| :-------: | :-------: | :-------: | :-------: |
| 공백 | + , %20 | % | %25 |
| & | %26 | + | %2B |
| = | %3D | ? | %3F |

<br>
<br>