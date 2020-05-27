---
layout: post
title: javascript 구조 분해 할당(Destructuring assignment)
featured-img: javascript
mathjax: true
categories: [Devlog]
tags: [Javascript, ES6]
---


<br>

# 객체 **구조분해**
구조 분해 할당이란 배열이나 객체나 배열의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 합니다. 기존보다 짧은 표현식으로 호출이 가능해 편리합니다. 사용할 때마다 까먹어 저장해놓고 사용하려고 합니다.

## 기본할당 방법

```jsx
var member = {name: 'elsa', age: 20};
var {name, age} = member ;

console.log(name); // elsa
console.log(age); // 20
```

## 함수 파라미터에 넣기

```jsx
var member = {name: 'elsa', age: 20};
print(member);

function print({ name, age }) {
	console.log(name); // elsa
	console.log(age); // 20
}
```

## 기본값 할당
객체로부터 구조분해된 값이 undefined인 경우, 변수에 기본값을 할당할 수 있습니다.

```jsx
var {name = 'Unknown', age = 0} = {name: 'elsa', age: 20};
console.log(name); // elsa
console.log(age); // 20

var {name = 'Unknown', age = 0} = {name: 'elsa');
console.log(name); // elsa
console.log(age); // 0
```

## 변수 이름 바꾸기
해체된 값의 변수 이름을 바꿔줄 수 있습니다.

```jsx
var member = {name: 'elsa', age: 20};
var {name: nameis, age} = member;

console.log(nameis); // elsa
console.log(age); // 0
```

변수 이름을 바꿔줌과 동시에 기본값까지 할당해 줄 수 있습니다.

```jsx
var {name: nameis= 'Unknown', age: ageis = 0} = {name: 'elsa'};

console.log(nameis); // elsa
console.log(ageis); // 0
```


만약에 key 이름으로 선언된 값이 존재하다면, 바로 새로운 배열 key로 넣어 사용할 수도 있습니다.

```jsx
var member = {name: 'elsa', age: 20};
var background = {color: 'red', opacity: 50}

var {name, age} = member ;
var {color, opacity} = background;

const newValue = {
	name,
	age,
	color,
	opacity
}

console.log(newValue ); //{name: "elsa", age: 20, color: "red", opacity: 50}
```

이 코드는 아래와 같은 의미를 지닙니다.

```jsx
const newValue = {
	name: name,
	age: age,
	color: color,
	opacity: opacity
}
```

# 배열 구조분해

배열의 기존 구조를 분해하지 않고, 값을 호출하던 방식입니다.

```jsx
var number = ["one", "two", "three"];

console.log(number [0]); // one
console.log(number [1]); // two
```

## 기본할당 방법
구조분해해 호출하는 방식입니다.

```jsx
var number = ["one", "two", "three"];
var [one, two, three] = number;

console.log(one); // one
console.log(two); // two
console.log(three); // three
```

## 일부만 사용하기

```jsx
var number = ["one", "two", "three"];
var [x, y] = number;
console.log(x); // 1
console.log(y); // 2
```

필요하지 않은 값이 있을 중간에 무시할 수도 있습니다.

```jsx
function numbering() {
  return [1, 2, 3];
}

var [x, , y] = numbering();
console.log(x); // 1
console.log(y); // 3
```

모든 값을 무시할 수도 있습니다.

```jsx
[,,] = numbering();
```

## 나머지 값 할당하기
변수에 배열에 값을 할당하다가 한꺼번에 남은 값들을 할당해줄 수 있습니다. b에 남은 모든 값들이 할당됩니다.

```jsx
var [x, ...y] = [1, 2, 3];
console.log(x); // 1
console.log(y); // [2, 3]
```

```jsx
var [x=5, y=7] = [1];
console.log(a); // x
console.log(b); // y
```

<br><br>
참고 - [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
<br><br>