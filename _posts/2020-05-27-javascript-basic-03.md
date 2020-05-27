---
layout: post
title: 자바스크립트 기초 정리 - 03. this를 지정하기
subtitle : call, apply, bind
tags: [javascript]
author: Sohyun Kim
comments : False
---

<h3>#call</h3>
call 메서드는 모든함수에서 사용이 가능함.   
첫번째 매개변수는 this로 사용할 값이고, 매개변수가 더 있으면 그 매개변수는 호출하는 함수로 전달됨.   

{% highlight javascript %}
const kim = { name: 'kim' };   
function greet() {
  return `hello, i'm ${this.name}!`;
}
greet.call(kim);  // "hello, I'm kim!"   
   
function update(birthYear, job){
  this.birthYear = birthYear;
  this.job = job;
}
update.call(kim, 1989, 'publisher');   
// const kim = { name: 'kim', birthYear: 1989, job: 'publisher' };
{% endhighlight %}

<br>
<br>
- - -   
<br>
<br>
<h3>#apply</h3>   
apply 메서드는 함수 매개변수를 처리하는 방법을 제외하면 call과 완전히 똑같음.   
call은 일반적인 함수와 마찬가지로 매개변수를 직접 받지만, apply는 매개변수를 **배열**로 받음.   

{% highlight javascript %}
update.apply(kim, [1990, 'actor']);
// const kim = { name: 'kim', birthYear: 1990, job: 'actor' };
{% endhighlight %}

apply로 흔히 배열의 최소값과 최대값을 구하는 예제를 사용함.   

{% highlight javascript %}
const arr = [2, 3, -5, 15, 7];
Math.min.apply(null, arr);  //-5
Math.max.apply(null, arr);  //15

// 이때 첫번째 매개변수로 null을 넣어주는 이유는 현재 사용하는 Math.min과 Math.max가 this와 관계없이 동작하기 때문에 임의로 넘겨주는 것임.
// ES6의 확산연산자를 사용해도 apply와 같은 결과를 얻을수 있음.

const newKim = [2002, 'artist'];
update.call(kim, ...newKim);  //update.apply(kim, newKim)과 같음.
{% endhighlight %}
<br>
<br>
- - -   
<br>
<br>
<h3>#bind</h3>   
this의 값을 바꿀수 있는 마지막 함수로 bind 메서드를 사용하면 함수의 this값을 영구히 바꿀수 있음.   
bind에 매개변수를 넘기면 항상 그 매개변수를 받으면서 호출되는 새 함수를 만들수 있음.   

{% highlight javascript %}
const updateKim = update.bind(kim);

updateKim(1940,'worker');
// const kim = { name: 'kim', birthYear: 1940, job: 'worker' };

updateKim.call(madeline, 1274, 'king');
// const kim = { name: 'kim', birthYear: 1274, job: 'king' };
{% endhighlight %}

<br>