---
title: "[JavaScript] Function & Method"
date: 2020-01-13T21:53:53+09:00
draft: true
author: "joowan kim"
description: ""
categories: 
Tags: ["method", "function"]
type: post
---

### 자바스크립에서의 함수
1. 어떤 작업을 수행하기 위해 필요한 statement들의 집합을 정의한 코드 블록.
1. 이름과 매개변수를 갖는다.
1. 일급 객체다.
    * 변수에 할당할 수 있다.
    * 매개변수로 전달할 수 있다.
    * 함수가 함수를 반환할 수 있다.
1. 간단히 말하면 JavaScript에서 모든 함수는 `Function` 객체이다.

### 함수 정의하기
함수를 정의하는 방법은 [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions)를 보면 자세히 알 수 있다.
그래서 몇가지만 간단히 소개하고 넘어가도록 하겠다.

소개에 앞서 선언문에 쓰이는 몇가지 요소에 대해 설명하겠다.
##### 용어
1. `name`: 별거 없다. 함수의 이름을 뜻한다.
1. `param`: 말그대로 parameter다. 함수에 전달되는 인수의 이름이다.
1. `statements`: 함수의 동작, body라고 할 수 있다.
1. `expression`: 연산자와 같이 하나 이상의 값으로 표현될 수 있는 코드라고 한다. 이것도 body라고 보면 될 듯하다.
1. `arg`: argument.., parameter와 비슷한 의미로 생각하면 될 듯하다.

##### 기호
1. `[]`: 생략이 가능하다는 뜻으로 이해하면 된다.
1. `()`: 모두가 알다시피 parameterㄴ나 arguments를 감싸는 용도
1. `{}`: 마찬가지로 모두가 아는 `body`를 감싸는 용도
1. `=>`: 화살표 함수 표현식에서 다시 언급하겠다.

#### 함수 선언문
```javascript
function name([param[,param[, ... param]]]){
    statements
}
```

#### 함수 표현식
```javascript
/******
 * 익명함수가 가능하다
 ******/
function [name]([param[,param[, ... param]]]){
    statements
}

/******
 *익명함수로 쓰일 때
 ******/
// 1.
var myFunction = function(){
    statements
}
// 2.
var myFunction = function namedFunction(){
    statements
}
// 3.
(function(){
    statements
})();
```

#### 화살표 함수 표현식
```javascript
([param[,param]]) => {
    statements
}
// 또는
param => expression
```

#### Function constructor
```javascript
new Function(arg1, arg2, ... argN, functionBody)
```

### method vs function
https://okky.kr/article/453415
https://m.blog.naver.com/PostView.nhn?blogId=byacj&logNo=120163659628&proxyReferer=https%3A%2F%2Fwww.google.com%2F

해당 function(method)을 수행하는 주체에 따라 달라진다.  
**method**: 수행하는 주체(this)가 method를 property로 가질 때  
**function**: 수행하는 주체(this)가 window일 때



### function
JavaScript에서 모든 함수는 `Fucntion` 객체
전역 `Function` 객체는 자신의 method 또는 속성(property)를 갖지 않는다


---
###### 참고 자료
![MDN-JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions)
![PoiemaWeb|JavaScript](https://poiemaweb.com/js-function)
![황준일님 블로그-1급객체](http://junil-hwang.com/blog/javascript-1%EA%B8%89%ED%95%A8%EC%88%98/)
![expression vs statement](https://shoark7.github.io/programming/knowledge/expression-vs-statement)

*부족한 점이 있다면 댓글로 알려주세요!*
