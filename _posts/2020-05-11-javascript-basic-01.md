---
layout: post
title: 자바스크립트 기초 정리 - 01. 변수와 상수
subtitle : var, let, const
tags: [study javascript es6]
author: Sohyun Kim
comments : False
---

<h3>#변수(var, let)</h3>   
이름이 붙은 값. 언제든 바뀔수 있음.   
변수를 선언할때 초기값을 할당 하지 않으면 암시적으로 특별한 값 Undefined가 할당됨.   
{% highlight javascript %}
  var a; //undefined
  a = ['1','2','3'];
{% endhighlight %}
<br>
문 하나에 여러개의 변수 선언이 가능함.
{% highlight javascript %}
  var a = '가', b = '나';
  let c = '다', d = '라';
{% endhighlight %}
<br>
**var와 let의 차이점**   
- var는 동일 변수명으로 재선언이 가능하지만 let은 그렇지 않음.   
{% highlight javascript %}
  var a = 10;
  var a = 20;
  console.log(a) // 20
   
  // 똑같은 변수를 재선언할 때 오류
  let a = 10;
  let a = 20; // Uncaught SyntaxError: Identifier 'a' has already been declared
{% endhighlight %}
<br>
- var는 함수스코프를 가지며, let은 블록스코프를 가짐.   
{% highlight javascript %}
  // var의 유효범위 확인시 함수 밖의 a와 안의 a가 각자 다른 유효범위를 가짐. 
  var a = 100;
  function print() {
      var a = 10;
      console.log(a);
  }
  print(); // 10
  
  // for문에서의 변수 var의 유효범위.
  var a = 10;
  for (var a = 0; a < 5; a++) {
      console.log(a); // 0 1 2 3 4 5
  }
  console.log(a); // 6
  
  // for문에서의 변수 let의 유효범위.
  var a = 10;
  for (let a = 0; a < 5; a++) {
      console.log(a); // 0 1 2 3 4 5
  }
  console.log(a); // 10
{% endhighlight %}
<br>
- 호이스팅이 발생한 경우 let은 선언 전 호출하면 사각지대(TDZ:let으로 선언하는 변수는 선언하기 전까지 존재하지 않는다는 직관적 개념을 나타낸 표현)로 인해 에러가 발생함.   
{% highlight javascript %}
  console.log(a); //uncaught ReferenceError: a is not defined
  let a = 20;
{% endhighlight %}
<br>
<br>
- - -   
<br>
<br>
<h3>#상수(const)</h3>   
변수와 마찬가지로 값을 할당받을 수 있지만, 한번 할당한 값은 바꿀수 없음.   
단, 객체 {}또는 배열 []로 선언했을 때는 객체의 속성(property)과 배열의 요소(element)를 변경할 수 있음.   
{% highlight javascript %}
  // 값을 다시 할당했을 때 오류
  const a = 10;
  a = 20; // Uncaught TypeError: Assignment to constant variable.
{% endhighlight %}
<br>
일반적으로 상수를 지정할때는 대문자와 '_'를 사용함.   
{% highlight javascript %}
  const MAX_HIGH_TEMP = 36;
{% endhighlight %}