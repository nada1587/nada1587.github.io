---
layout: post
title: 자바스크립트 기초 정리 - 04. Todo 토이프로젝트를 개발하며!
subtitle : arrow function, 유사배열, 이벤트위임 등 
tags: [javascript]
author: Sohyun Kim
comments : False
---

<h3>#함수, 화살표함수의 차이!</h3>   

**일반함수**   
함수는 자바스크립트에서 일급객체임. 일급객체는 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킴.   

함수가 가능한 동작들   
- 리터럴에 의해 생성   
- 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능   
- 함수의 인자로 전달 가능   
- 함수의 리턴값으로 리턴 가능   
- 동적으로 프로퍼티를 생성 및 할당 가능   

{% highlight javascript %}
  // 함수 선언식 : 호이스팅이 일어남
  function test1(params) {
    return;
  }

  // 함수 표현식
  var test2 = function(params) {
    return;
  }

  // 내부함수
  function test3(a, b) {
    // test4는 내부함수인데 함수내부에서 외부함수의 변수나 파라미터를 사용할수 있고 참조할수 있음
    function test4(x) {
      return x * x;
    }
    return test4(a) + test4(b);
  }
{% endhighlight %}
   
<br>
**화살표함수**   
화살표함수는 ES6에서 추가되었으며, 기존 함수를 간결하게 표현할수 있는 기능이 개선됨. 상위 컨텍스트에 바인딩됨.   

{% highlight javascript %}
  // 매개변수가 없는경우, 객체 반환시 소괄호 사용
  () => ({ a: 1 });

  // 매개변수가 한 개인 경우 () 생략, 함수몸체가 한줄일 경우 {} 생략가능하며, 암묵적으로 return됨
  a => a + 1;

  // 매개변수가 두 개 이상인 경우 () 생략 불가, 함수몸체에 {} 사용시 return 구문 필요, return 구문 생략시 undefined 반환
  (a, b) => { return a + b }
{% endhighlight %}
   
<br>
**일반함수와 화살표함수에서의 this**   
자바스크립트에서 this는 현재 실행문맥이라고 이해할 수 있음. 현재 함수를 부른 객체가 누구인지를 나타냄. 화살표함수 이전의 함수에서는 함수를 호출하는 자가 누구인지에 따라 this의 값이 결정되었음. 화살표함수는 자신을 포함하는 외부 scope에서 this를 계승받음.  

화살표함수를 사용하면 안되는 경우   
- 객체의 메서드로 선언하는 경우 : 메소드릴 소유한 객체가 아닌 상위 컨텍스트의 객체를 가리킴.   
- 생성자함수로 사용하는 경우 : 화살표함수는 prototype을 갖고 있지 않기 때문에 생성자함수로 사용하면 안됨.   
- addEventListener 함수의 콜백 함수로 사용되는 경우 : 전역객체로 window를 가리킴.   

<br>
**제이쿼리 안에서의 화살표함수**   
제이쿼리 안에서 화살표 함수는 제이쿼리 이벤트핸들러로 사용하면 this값으로 자기자신을 나타낼수 없고 window객체를 나타냄. 

<br>
- - -   
<br>
<br>
<h3>#유사배열!</h3>   

**유사배열이란?!**   
자바스크립트에서 몇몇 객체는 배열처럼 보이지만 실제로는 배열이 아닌데 이를 유사배열이라함. 배열처럼 인덱스로 접근이 가능하고, length 속성이 존재 하지만 실제배열 네이티브 메소드인 push, forEach, indexOf와 같은 메소드를 사용하지 못함.   
   
유사배열의 두가지 예   
- document.getElementsByClassName()와 같이 nodeList인 경우   
- arguments   
   
실제 배열이 아니기 때문에 대부분 배열 형태로 바꾸어 사용함.   

{% highlight javascript %}
  function fnc() {
    console.log(arguments[0] + " " + arguments[1]);
    arguments.indexOf(4);
  }
  fnc(1,2,3,4);
  // console에 1, 2가 찍히지만 indexOf 메소드는 사용이 불가.

  function list() {
    return Array.prototype.slice.call(arguments);
  }
  list(1,2,3);
  // 결과값 [1, 2, 3];
{% endhighlight %}
   
유사배열을 배열처럼 사용 하는 다른 방법   
- [...유사배열].메소드   
- [].메소드.call(유사배열, function(){})   
- Array.prototype.메소드.call(유사배열, function(){})

<br>
- - -   
<br>
<br>
<h3>#이벤트등록 -> 버블링, 캡쳐링, 위임!</h3>   

**이벤트 리스너**   
이벤트리스너란 이벤트가 발생했을때 그 처리를 담당하는 함수를 가리키며, 이벤트 핸들러 라고도 함. 지정된 타입의 이벤트가 특정 요소에서 발생하면, 웹 브라우저는 그 요소에 등록된 이벤트 리스너를 실행시킴.   
   
{% highlight javascript %}
  element.addEventListener("click", function () {
    // Some codes in here
  }, false);
  // 매개변수 : 이벤트명, 콜백함수, 캡쳐링 사용 유무(true는 캡쳐링 사용, false는 버블링 사용)
{% endhighlight %}

이벤트 버블링과 캡쳐링은 메모리 관리를 위해 사용함. 여러 요소에 이벤트를 걸어 두면 초기 렌더링시 많은 메모리를 할당하기 때문에 가장 상위의 요소에 이벤트를 걸어 캡쳐링하는 방법을 이용함.   
이벤트를 차단해야 할 경우 : e.stopPropagation()을 이용함.   
   
<br>   

**이벤트 버블링**   
자식요소에서 부터 부모요소로 이벤트가 전파됨.   
   
<br>   

**이벤트 캡쳐링**   
부모요소에서 부터 자식요소로 이벤트가 전파됨.   
   
<br>   

**이벤트 위임**   
웹 문서에 이벤트 리스너를 등록하려면 반드시 DOM요소가 존재해야함. 그렇기 때문에 동적으로 DOM이 생성된다면 이벤트 리스너를 등록할수 없음. 그래서 이벤트 위임을 통해 나중에 생기는 DOM에게도 이벤트가 걸리도록 이벤트위임을 사용함.   
- 제이쿼리의 .on() 이벤트리스너를 사용하면됨.   

{% highlight javascript %}
  // 상위 menu 요소에 이벤트를 걸고 하위 타겟의 id 값을 통해 다른 이벤트를 연결시킴
  document.getElementById("menu").addEventListener("click", function(e) {
    var target = e.target;
    if (target.id === "file") {
      // 파일 메뉴 동작
    } else if (target.id === "edit") {
      // 편집 메뉴 동작
    } else if (target.id === "view") {
      // 보기 메뉴 동작
    }
  });
{% endhighlight %}

<br>
- - -   
<br>
<br>
<h3>#타입확인 함수</h3>   
**입력된 값의 타입 확인하기!**   

{% highlight javascript %}
function getType (any) {
  return Object.prototype.toString.call(any).slice(8, -1);
}
// var toString = Object.prototype.toString;
// toString.call(new String); -> [object String] 반환
// toString은 모든 객체에 사용되어 해당 객체의 클래스를 가져옴
// call()을 사용해서 검사하고자 하는 객체를 첫번째 파라미터로 넘겨서 그 객체의 해당 객체클래스를 확인할수 있음
// 가져온 반환값의 앞 '[object '는 항상 동일함으로 이 인덱스 8이후부터 마지막 ']'을 제외한 -1 까지의 값을 slice 하면 원하는 객체클래스를 확인하고 타입을 반환할수 있음
{% endhighlight %}

<br>