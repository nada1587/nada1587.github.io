---
layout: post
title: 자바스크립트 기초 정리 - 02. 데이터타입
subtitle : 원시타입, 참조타입
tags: [javascript]
author: Sohyun Kim
comments : False
---

<h3>#원시타입</h3>   
값의 타입은 typeof 연산자로 알수있음.   
<br>
**Number(숫자형)**   
<br>
<br>
- - -   
<br>   
<br>   
<h3>#참조타입</h3>   
변수와 마찬가지로 값을 할당받을 수 있지만, 한번 할당한 값은 바꿀수 없음.   
   
{% highlight javascript %}
  // 값을 다시 할당했을 때 오류
  const a = 10;
  a = 20; // Uncaught TypeError: Assignment to constant variable.
{% endhighlight %}