---
layout: post
title: 제이쿼리 기초 정리 - 01. $.extend()
subtitle : Object 합치기
tags: [jQuery]
author: Sohyun Kim
comments : False
---

<h3>#객체를 합치는 3가지 방식</h3>
**$.extend(a, b)**   
a에 b, c를 합침을 의미함(가장 앞의 a는 타켓 객체를 의미함, extend함수에 파라미터는 갯수 제한이 없음)   
같은 프로퍼티가 있을 경우, 합쳐주는 b의 값으로 a값을 덮어주고, 새로운 프로퍼티가 b에 있을 경우 a에 추가함      

{% highlight javascript %}
  let a = {
    name: 'tubbi',
    age: 32
  } 
  let b = {
    name: 'tubbitung',
    hobby: 'bowling'
  }

  $.extend(a, b);

  console.log(a);
  /* let a = {
      name: 'tubbitung',
      age: 32,
      hobby: 'bowling'
  } */
{% endhighlight %}
<br>
**$.extend({}, a, b)**   
이 방식은 타겟 객체를 a가 아닌 빈 객체로 지정해 줌으로써, a 파라미터가 변하지 않도록 함   

{% highlight javascript %}
  let a = {
    name: 'tubbi',
    age: 32
  } 
  let b = {
    name: 'tubbitung',
    hobby: 'bowling'
  }

  let newObject = $.extend({}, a, b);

  console.log(newObject);
  /* let newObject = {
      name: 'tubbitung',
      age: 32,
      hobby: 'bowling'
  } */
{% endhighlight %}
<br>
**$.extend(true, a, b)**   
이 방식은 타겟 객체의 프로퍼티가 객체일 경우에 사용함   
true값을 첫번째 파라미터값으로 넣어주면 하위객체의 프로퍼티까지 합칠수 있음   

{% highlight javascript %}
  let a = {
    name: 'tubbi',
    age: 32,
    profile: {
      height: 175,
      weight: 'secret'
    }
  } 
  let b = {
    name: 'tubbitung',
    hobby: 'bowling',
    profile: {
      Waist: 'what?'
    }
  }

  $.extend(a, b);

  console.log(a);
  /* let a = {
      name: 'tubbitung',
      age: 32,
      hobby: 'bowling',
      profile: {
        Waist: 'what?'
      }
  } */



  let a = {
    name: 'tubbi',
    age: 32,
    profile: {
      height: 175,
      weight: 'secret'
    }
  } 
  let b = {
    name: 'tubbitung',
    hobby: 'bowling',
    profile: {
      Waist: 'what?'
    }
  }

  $.extend(ture, a, b);

  console.log(a);
  /* let a = {
      name: 'tubbitung',
      age: 32,
      hobby: 'bowling',
      profile: {
        height: 175,
        weight: 'secret',
        Waist: 'what?'
      }
  } */
{% endhighlight %}
<br>

<br>
<br>