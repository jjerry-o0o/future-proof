---
title: "ES5와 ES6 비교하기, 예제 코드 정리"
date: 2024-09-04
---

<br/>

기존엔 ES5, ES6 버전에 따른 차이를 인지하지 못하고, 구글링해서 나오는 방법으로 코드를 작성했었다.

그러다 리액트를 공부하면서 두 버전에 따른 차이를 알게 되었고, 새로운 버전에 대해 공부하고 활용하는 것이 얼마나 중요한지 깨닫게 되어 정리해보았다.

## ES란 ?

ES5 보다 ES6가 높은 버전이라는건 알겠는데, 앞에 붙는 ES가 뭔지 잘 모르겠다면, 짤막하게라도 알고 가자.

- ES는 ECMAScript 의 줄임말로, Ecma 인터내셔널에서 정의한 표준 스크립트 문법이다.
- JavaScript는 스크립트 언어의 종류이며, ECMAScript 를 따른다.
- ECMAScript와 JavaScript는 서로를 기반으로 하기 때문에 용어를 혼용해서 사용한다.

<br/>

## ES5 와 ES6 의 차이점

<br/>

### 💡 **let 과 const 추가**

기존에 ES5에서는 var만 사용 가능했고 이는 몇 가지 문제가 있었는데…

<br/>

⚠️ var 없이도 변수 선언가능

```js
num = 10;

console.log(num);  // 10
```

<br/>

⚠️ 동일한 이름의 변수 선언 가능

```js
var name = 'Jerry';
var name = 'Tom';

console.log(name);  // Tom
```

<br/>

⚠️ 초기화 안 된 변수를 호이스팅 시에 undefined로 초기화

```js
console.log(age);  // undefined

var age = 15;
```

<br/>

⚠️ 하위 블록에서 선언한 변수를 상위 블록에서 사용시 전역 변수처럼 사용됨

```js
var text = 'Hello~!';

if(1 == 1) {
	var text = 'What the fxxx';
}

console.log(text);  // What the fxxx
```

<br/>

  

위 3가지 상황에서 에러가 나줘야 하는데 문제 없이 동작해버리기 때문에 개발자 입장에서 에러의 원인을 찾는데 많은 어려움이 있었다. ES6에 추가 된 let 과 const 를 사용하여 이 문제점을 해결할 수 있다. 표로 정리한 내용은 다음과 같다.

<br/>


> var, let, const 비교 👀

|   |   |   |   |
|---|---|---|---|
||**var**|**let**|**const**|
|**중복 선언**|가능|불가능|불가능|
|**재할당**|가능|가능|불가능|
|**Hoisting**|undefined|ReferenceError|ReferenceError|
|**Scope**|function|block|block|
|**우선순위**|3|2|1|

<br/>

---

<br/>
  
### 💡 **Arrow Function (화살표 함수)**

<br/>

화살표 함수는 ES5에서 함수 만들 때 사용하던 function 키워드를 생략할 수 있다.

<br/>

> 매개변수 표현
```js
// 매개변수가 없는 경우
const arrow1 = () => { console.log("arrow 1") }

// 매개변수가 한 개인 경우 (소괄호 생략 가능)
const arrow2 = funcName => { console.log(funcName) }

// 매개변수가 여러 개인 경우 (소괄호 생략 불가능)
const arrow3 = (x, y) => { console.log("arrow " + (x + y)) }
```

<br/>

> 함수 몸체 표현
```js
// 함수 몸체 내용이 한 줄이면 중괄호 생략 가능
const arrow4 = () => console.log("arrow 4");
```

<br/>

> 객체 리터럴 반환
```js
// 객체 리터럴 반환 (소괄호로 감싸줌)
const arrow5 = () => ({ name : 'jjerry'});
```

<br/>

---

<br/>

### 💡 **Spread Operator (전개 연산자)**

<br/>

전개 연산자는 배열이나 객체를 펼쳐주는데 마치 구조를 해체해서 알맹이만 꺼내주는 느낌이다.

배열이나 객체를 합칠 때, ES5 의 방식 보다 간결하게 표현 가능하기 때문에 수정하는 것이 훨씬 간단해졌다.

다차원 배열의 경우 중첩된 배열은 그대로 배열로 표기되어진다.

<br/>

> 배열에서 전개 연산자 활용

```js
// ES5
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];

console.log(arr1.concat(arr2));  // [1, 2, 3, 4, 5, 6]

// ES6
const arr3 = [1, 2, 3];
const arr4 = [4, 5, 6];

console.log(...arr3, ...arr4);  // 1 2 3 4 5 6

const two = ['둘'];
const count = ['헛', ...two, '셋'];

console.log(...count);  // 헛 둘 셋

const dog1 = ['진돗개', ['시바'], '포메라니언'];
const dog2 = ['말라뮤트', ...dog1, ];

console.log(dog2);  // [ '말라뮤트', '진돗개', [ '시바' ], '포메라니언' ]
```

<br/>

> 객체에서 전개 연산자 활용
```js
// ES6
const obj1 = { name : 'jjerry', age : 6 };
const obj2 = { color : 'white' };
const obj3 = {...obj1, ...obj2};

console.log(obj3);  // { name: 'jjerry', age: 6, color: 'white' }

const blueberry = { blueberry : 'purple' };
const fruits = { apple : 'red', banana : 'yellow', ...blueberry }

console.log({...fruits});  // { apple: 'red', banana: 'yellow', blueberry: 'purple' }
```

<br/>

---

<br/>

### 💡 **for ~ of 반복문**

<br/>

for ~ of 반복문의 경우 인덱스 없이 반복 가능한 객체를 순회하여 작업할 때 유용하다.

<br/>

```js
const arr = ['c', 'a', 't'];

for (let i of arr) {
	console.log(i);
}
// c a t
```

<br/>

> for 문 비교

|   |   |   |   |   |
|---|---|---|---|---|
||for 문|for ~ in|forEach|for ~ of|
|도입 시기|ES1|ES3|ES5|ES6|
|특징|가장 빠르다.|배열 보단 객체 순회 시에 적합하다.|코드가 간결하다.|for 문과 비슷한 성능을 갖는다.|
|제어 방법|continue / break|continue / break|불가능|continue / break|

<br/>

---

<br/>

### 💡 **Map 객체**

<br/>

ES5 에서 사용하던 Object 와 ES6 의 Map 은 둘 다 key-value 형태로 저장되는 형식이지만 Object 의 경우 key 값으로 String, symbol 만 올 수 있고, Map 은 key 값으로 모든 값이 올 수 있다. 그리고 Map 의 메서드를 사용하여 보다 명확하게 개발자의 의도를 보여줄 수 있다.

<br/>

```js
// ES5
var obj = {
	"200" : "Ok",
	400 : "Bad Request"
}

var objSize = Object.keys(obj).length;

// ES6
const map = new Map([
	[100, "Continue"],
	[400, "Bad Request"],
])

map.set(200, "Ok");
const mapSize = map.size;

console.log(obj[200]);  // Ok
console.log(map.get(200));  // Ok
// obj.400;  // SyntaxError: Unexpected number

console.log(objSize);  // 2
console.log(mapSize);  // 3
```

<br/>

---

<br/>

### 💡 **Set 객체**

<br/>

Set의 특징으로는 중복되지 않은 데이터를 순서 없이 저장한다는 점이다.

고유한 값을 다루어야 할 때 배열 등의 경우 중복되는 값이 있는지 매번 체크해야 했는데 이런 경우 Set을 사용하면 좋다.

<br/>

```js
const set = new Set();

set.add('jjerry');
set.add(6);
set.add(true).add("tom");

console.log([...set]);  // [ 'jjerry', 6, true, 'tom' ]

set.delete(true);

if(!set.has(true)) {
	console.log("This is fake");  // 출력
}

console.log(set.size);  // 3
```

<br/>

[Set 에 대해 더 알고 싶다면…](https://www.daleseo.com/js-set/ "Set 에 대해 더 알고 싶다면…")

<br/>

---

<br/>

### 💡 **Class**

<br/>

ES5 에서도 prototype 을 사용한 객체 지향 프로그래밍이 가능했지만 코드 작성 시 불편함이 있어 ES6 의 class 개념이 나오게 됐다. class 는 명확한 구조와 상속 개념을 제공하지만 사실상 class 는 prototype을 보다 쉬운 문법(syntactic sugar)으로 쓸 수 있게 해주는 것이다.

<br/>

> ES5 의 prototype
```js
function MyCat(name) {
	this.name = name;
}

MyCat.prototype.introduction = function() {
	console.log("My cat's name is " + this.name);
}

var cat1 = new MyCat("Tom");
cat1.introduction ();  // My cat's name is Tom
```

<br/>

> ES6 의 class
```js
class MyCat {
	constructor(name) {
		this.name = name;
	}
	
	introduction() {
		console.log("My cat's name is " + this.name);
	}
}

const cat2 = new MyCat("Jerry");
cat2.introduction();  // My cat's name is Jerry
```

<br/>

---

<br/>

### 💡 **매개변수 기본 값**

<br/>

함수의 매개변수에 default 값을 주어 함수 호출 시 매개변수를 깜빡한 경우에 default 값을 사용하여 함수를 오류 없이 실행되도록 한다.

<br/>

```js
const myCatInfo = (sex, age, name = 'secret') => {
	return `My cat's name is ${name} and ${sex} is ${age} years old.`;
}

console.log(myCatInfo("He", 6));  // My cat's name is secret and He is 6 years old.
```

<br/>

---

<br/>

### 💡 **Rest Parameter (나머지 매개변수)**

<br/>

함수에 전달된 모든 매개변수 또는 할당되지 않은 나머지 매개변수를 전달 받을 수 있다.

<br/>

```js
function count(...nums) {
	console.log(nums);  // [ 1, 2, 3, 4, 5 ]
}``

count(1, 2, 3, 4, 5);

function fruits(first, second, ...food) {
	console.log("My favorite fruits is " + first);  // My favorite fruits is orange
	console.log("Second is " + second);  // Second is mango
	console.log("the others " + food);  // the others melon,peach,apple
}

fruits('orange', 'mango', 'melon', 'peach', 'apple');
```

<br/>

---

<br/>

ES6 의 새로운 문법들이 처음 접해보면 다소 낯설 수는 있지만, 사용하다 보면 ES6 가 모던 자바스크립트 개발의 표준이 된 이유(간결한 코드, 효율성 증가 등)를 느낄 수 있을 것이다.