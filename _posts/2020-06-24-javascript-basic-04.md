---
layout: post
title: 자바스크립트 기초 정리 - 04. class 알아보기
subtitle : 생성자함수, class
tags: [javascript]
author: Sohyun Kim
comments : False
---

<h3>#생성자함수?!</h3>   
생성자함수는 객체를 생성하는 함수를 의미함. 사람 생성자함수를 만들면 다음과 같이 작성할수 있음.   

{% highlight javascript %}
// 생성자함수를 정의할땐 일반 함수와 구분하기 위해 함수명을 대문자로 시작함.
function Person(name, height) {
  this.name = name;
  this.height = height;
  this.sayHello = function() {
    alert(this.name + 'said "hello!"');
  }

  // 이렇게 생성자함수 내에 this.smile로 메서드를 작성하면 new 키워드를 통해 새로운 객체를 만들때마다 smile 메서드가 반복생성되어 메모리낭비를 불러옴.
  this.smile = function() {
    alert('hoho!');
  }
}

const sohyun = new Person('sohyun', '174');
{% endhighlight %}  
   
<br>
- 생성자함수는 new 키워드를 통해 호출하여 객체를 생성할수 있음.(const sohyun = new Person('sohyun','174');)   
- Person.prototype.smile = function(){}; 이처럼 Person이라는 생성자함수의 prototype(원형객체)에 메서드를 추가하면 new 키워드로 객체 생성시 원형 하나의 메서드를 공유받기때문에 메모리소비를 줄일수 있음.   
- new 키워드로 생성된 객체의 내부를 보면 _ _proto_ _ 가 들어있는데 이는 생성자의 prototype이 참조되었음을 의미함.    

<br>
<br>
- - -   
<br>
<br>
<h3>#class란?!</h3>   
es6부터 새롭게 추가된 class 키워드를 통해 클래스를 정의할수 있음. 클래스는 별도 타입의 객체를 생성하는 설계 도면이라고 생각하면됨. 기본 속성(모양, 형태 등등)을 가진 붕어빵을 클래스라고 하면, 이를 기반으로 팥이 들어있는 붕어빵, 슈크림이 든 붕어빵등 다양한 객체를 만들어 낼 수 있음. 즉, 클래스를 통해 객체가 가져야할 상태와 행위들을 속성과 메서드로 정의해 놓고 **인스턴스를 생성하여 각각의 상태를 관리할수 있음**.   
   
<br>
- 클래스(추상화:자동차), 인스턴스(구체화:특정자동차)   
- 클래스는 생성자를 통해 객체 인스턴스를 초기화 시킴.   
- instanceOf()를 사용하여 클래스의 인스턴스 인지 확인가능함.   
- extends 키워드를 사용하여 상속받은 클래스의 생성자 호출은 super()를 이용.

<br>
<br>
- - -   
<br>
<br>
<h3>#예제</h3>   
**Todo 리스트 코드 작성시 사용한 class 예시**   

{% highlight javascript %}
const List = require('./List');

const incompletedList = new List({
  data: listData.incompleted,
  type: 'incompleted',
  option: 'title',
  container: '[data-list=incompletedList]',
  isDone: false,
});
{% endhighlight %}

{% highlight javascript %}
'use strict';

const $ = require('jquery');
const tmplTodoItem = require('../templates/partials/todoItem.hbs');
const dataAttrs = {
  sortSelect: 'data-select="select"',
};

class List {
  constructor({ data, type, option, container, isDone }) {
    if (!container || typeof container !== 'string') {
      throw new Error('container is not valid');
    }
    this.data = data || [];
    this.type = type;
    this.option = option || null;
    this.$container = $(container);
    this.isDone = isDone;
    this.sortedData = [];
  }

  init() {
    console.log('List init!');
  }

  // 리스트 다시그리기
  render(
    data = this.data
  ) {
    if (!this.data) {
      throw new Error('data is not defined.');
    }
      
    this.option = $(`[${dataAttrs.sortSelect}]`).val();

    if (this.type === 'incompleted') {
      this.sortData = this.getSortData(data, this.option);
      data = this.sortData;
    }
    this.$container.empty().append(tmplTodoItem({
      data,
      isDone: this.isDone,
    }));
  }

  // 날짜 업데이트
  dateFormat() {
    const date = new Date();
    function updateDate(format) {
      const yyyy = format.getFullYear();
      const mm = format.getMonth() < 9 ? `0${format.getMonth() + 1}` : format.getMonth() + 1;
      const dd = format.getDate() < 10 ? `0${format.getDate()}` : format.getDate();
      const h = format.getHours() < 10 ? `0${format.getHours()}` : format.getHours();
      const m = format.getMinutes() < 10 ? `0${format.getMinutes()}` : format.getMinutes();
      return `${yyyy}-${mm}-${dd} ${h}:${m}`;
    }
    const formatDate = updateDate(date);
    return formatDate;
  }

  // 리스트정렬
  getSortData(obj, key) {
    if (key === 'title') {
      obj.sort( function (a, b) { 
        return a[key] < b[key] ? -1 : 1;
      });
    } else {
      obj.sort( function (a, b) { 
        return a[key] > b[key] ? -1 : 1;
      });
    }
    return obj;
  }

  // 선택된 요소를 data에 푸시해서 다시 리스트 그리기
  addList($target) {
    const targetList = $target.parent().siblings('[data-group="list"]').find('[data-list="item"]');

    // 선택된 요소찾음
    targetList.each((i, el) => {  
      if ($(el).hasClass('active')) {
        this.data.push({
          title: $(el).find('h5').text(),
          updateDate: this.dateFormat(),
        });
      }
    });
    this.render(this.data);
  }

  // 선택된 안된 요소로 새배열만들어서 다시 리스트 그리기
  removeList($target) {
    const targetList = $target.parent().siblings('[data-group="list"]').find('[data-list="item"]');

    // 선택안된 요소찾음
    const inactiveListArr = [];
    targetList.each((i, el) => {  
      if (!$(el).hasClass('active')) {
        inactiveListArr.push({
          title: $(el).find('h5').text(),
          updateDate: $(el).find('small').text(),
        });
      }
    });
    this.data = inactiveListArr;
    this.render(this.data);
  }
}

module.exports = List;
{% endhighlight %}
<br>