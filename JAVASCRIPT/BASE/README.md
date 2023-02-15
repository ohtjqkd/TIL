## ES6에서 달라진 점

1. 변수 선언 방법의 변화(let, const)
- let은 블록 범위에서 유효함
- const 역시 블록 범위지만 값을 바꿀 수 없는 상수임

2. 템플릿 리터럴
- 다른 언어의 템플릿과 비슷함
- 백틱 `\``을 이용하여 표현할 수 있음
- 표현하고자 하는 데이터를 ${ 데이터 }로 표기하며 간단한 연산도 가능함

3. 반복문(for in, for of)
```
let array = ['a', 'b', 'c']
for (let i in array) {
    console.log(i) // 0, 1, 2 인덱스 값 출력
}
for (let i of array) {
    console.log(i) // a, b, c 값 출력
}
```

4. 기본 매개변수
- 함수의 매개변수에 기본값을 지정할 수 있음
```
function fun(a = 1, b = 2, c = 3) {
    return a + b + c;
}
console.log(fun()); // 20
```

5. 화살표 함수
- 화살표 함수는 기존의 함수를 간결하게 표현해주는 기능
- 일반함수와 화살표함수와의 가장 큰 차이는 일반함수는 자신만의 데이터를 가질 수 있는 반면, 화살표함수는 그렇지 못하다.
```
function fun(arg) {
    console.log(arg);
    return arg;
}
fun(1); // 1 출력

let fun2 = (arg) => {
    console.log(arg);
    return arg;
}
fun2(1); // 1 출력

function fun(arg) {
    this.name = arg;
}
new fun(1234).name; // 1234 출력
let fun2 = (arg) => {
    this.name = arg;
}
new fun(1234).name; // new 생성자를 통해 생성 불가, 에러 발생
```

6. 객체 정의 방법
- 무조건 key: value로 정의하던 부분을 생략할 수 있음
```
let width = 100;
let height = 200;
let fun = {
    width,
    height,
    print() { // 콜론 없이 표기 가능
        console.log(this.width);
    }
}
fun.print(); // 100;
console.log(fun); // { width: 100, height: 200, print: function 어쩌구 }
```

7. 객체 복사
- Object assign 함수가 추가됨
- 깊은 복사?

8. 계산된 속성 이름
- 객체의 key값을 동적으로 할당할 수 있다.
```
let key = 'name';
let data = {
    [key]: 'value',
    [`change_${key}`]: 'value2'
}
console.log(data); // { name: 'value1', change_name: 'value2' }
```

##### 수정 필요
9. 구조분해 할당(Destructing Assignment)

- 데이터를 할당하려면 대입 연산자를 통해서 할 수 있음. 예)  var a = 1; var b = a;
- 데이터를 할당 하는 기능을 간결하게 할 수 있게 됨.
- 배열 값은 대괄호[]를 사용해서 간단하게 할당 할 수 있으며, 객체값은 중괄호{}를 사용해 할당 할 수 있다.

```
//일반적인 사용 방법
let arr = ['1', '2', '3']
let [one, two, three] = arr
console.log(one) // 1
console.log(two) // 2
console.log(three) // 3

let [, , wow] = arr  //첫번째, 두번째를 빈값으로 선언
console.log(wow)  //3 


//////////////////////////////////////////////////
//값 할당(서로 바꾸기)
let num = 123;  
let text = 'hi'; 
[num, text] = [text, num]
console.log(num, text)


//////////////////////////////////////////////////
//객체의 값에 대해 적용
let data = {width : 100, height : 200}
let {width, height} = data
console.log(width)  //100
console.log(height)  //200

//////////////////////////////////////////////////
//다양한 변환
let param = {
    jsn : {
        name : 'hello',
        number : 1543
    },
    arr : [
        {arr_name : 'world', index : 4567},
        {arr_name : 'world record', index : 5513},
    ],
    param_text : 'im param_text'
}

let {jsn : {name : re_name}, arr : [{arr_name : new_name}], param_text} = param

//re_name은 param.jsn.name을 변환하여 별칭을 준 값
//new_name은 param.arr배열의 첫번째 arr_name을 변환하여 별칭을 준 값
//param_text는 param.param_text의 값을 변수명 그대로 사용한 값(별칭부여X)
console.log(re_name, new_name , param_text)
```

10. 전개구문 연산자(Spread operator)

 - 자바에서의 가변인자와 비슷한 기능 입니다.  * 앗차..자바를 안써보신분도 있겠구나..

 - 받으려는 데이터를 n개(가변)로 하여 받을 수 있습니다.

//일반 사용법
function numbers(...arg){
    console.log(arg)
}
numbers(1,2,3,4,5)  // 1,2,3,4,5  -> 배열 타입 입니다.


//////////////////////////////////////////////////
//대입하기
let number = [1, 2, 3, 4, 5]
let [one, two, ...nums] = number

console.log(one) // 1
console.log(two) // 2
console.log(nums) // [3, 4, 5]


//////////////////////////////////////////////////
//객체 복사
let obj1 = { string: 'bar', int: 42 }
let obj2 = { ...obj1 }
console.log(obj1, obj2)  


//////////////////////////////////////////////////
//배열 복사
let arr = [1,2,3,4,5]
let arr2 = [...arr]
arr[0] = 100
console.log(arr)  // 100,2,3,4,5
console.log(arr2) // 1,2,3,4,5
 

11. 클래스(Class)

 - 클래스라는 기능은 1개의 영역 안에 다양한 함수, 변수 등을 집어넣고 사용 할 수 있게 해주는 기능 입니다.

 - 클래스는 new 연산자를 통해서 생성 할 수 있으며, 호이스팅이 되지 않으므로 유의하여야 합니다.

 - 클래스에서 함수는 function을 제거하고 선언 합니다.

 - 클래스에서 static 함수는 new로 생성된 변수에서 접근하는 것이 아니라 클래스에서 바로 접근해야 합니다.

 - 클래스는 다른 클래스를 상속 받아서 기존 클래스의 기능을 이어받을 수 있습니다.

//클래스 사용 방법
class Building {
    constructor(width, height) {
        this.width = width
        this.height = height
    }
    log(){  //function을 생략하고 함수를 사용
        console.log(this.width, this.height) 
    }
    static print(num){  //static 함수
        console.log(num) 
    }
}

let apt = new Building(100, 200)
console.log(apt.width, apt.height) //100, 200
Building.print(200)  //200  -> 오류 발생 : apt.print(200)


//////////////////////////////////////////////////
//상속받아 사용하는 방법
class Apart extends Building {  //상위클래스의 생성자를 구현해야 함.
    constructor(width, height) {  
        this.width = width
        this.height = height
    }
    //log, print 함수를 지니고 있음.
}

let apt2 = new Apart(100, 200)
console.log(apt2.width, apt2.height) //100, 200
Apart.print(200) 
 

12. 모듈(Modules)

 - export, import 를 통해 나누어서 개발된 파일(*.js)간의 관계를 유지하여 줍니다.

 - js파일에서 전달할 기능은 export, 사용하는 곳에서는 import를 선언하여 서로의 위치를 참조하게 합니다.

 - 기존에 html파일에서 <script />테그로 사용하는 경우 속성값인 type을 module로 해야 합니다.

* test.js
export const test_number = 1234

* test2.js
import * as testCode from "./test.js"

console.log(testCode.test_number)  //1234
 

13. 약속(Promise)

 - 비동기 프로세스의 순서를 보장할 때 사용합니다.

 - Ajax나 특정 파일 입출력 행위에 대해서 순서가 보장 될 때 주로 사용 합니다.

let prom = (num) => {
    return new Promise((res, fail) => {
        if (num > 4) {
            res(num)  //성공이면,
        } else {
            fail("err")  //에러발생
        }
    })
}

prom(5)
    .then(val => console.log(val)) // 5 출력
    .catch(err => console.log(err))

[https://lts0606.tistory.com/45]

## 화살표 함수(Arrow function)의 특징

1. this
:heavy_check_mark: 일반함수
자바스크립트에서 모든 함수는 실행될 때마다 함수 내부에 this라는 객체가 추가된다.
아래는 일반 함수에서 this가 바인딩 되는 상황이다.

함수 실행시에는 전역(window) 객체를 가리킨다.
메소드 실행시에는 메소드를 소유하고 있는 객체를 가리킨다.
생성자 실행시에는 새롭게 만들어진 객체를 가리킨다.
일반 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고,
함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정된다.


:heavy_check_mark: 화살표 함수
화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
화살표 함수의 this 언제나 상위 스코프의 this를 가리킨다.(Lexical this)
또한 call, apply, bind 메소드를 사용하여 this를 변경할 수 없다.

예를 들면

function fun() {
  this.name = "하이";
  return {
    name: "바이",
    speak: function () {
      console.log(this.name);
    },
  };
}

function arrFun() {
  this.name = "하이";
  return {
    name: "바이",
    speak: () => {
      console.log(this.name);
    },
  };
}

const fun1 = new fun();
fun1.speak(); // 바이

const fun2 = new arrFun();
fun2.speak(); // 하이
일반함수로 사용했을때는 바이가 찍히고 화살표함수를 사용했을때는 하이가 찍힌다.
일반 함수는 자신이 종속된 객체를 this로 가리키고 화살표 함수는 자신이 종속된 인스턴스를 가리킨다.


2. 생성자 함수로 사용 가능 여부
:heavy_check_mark: 일반 함수는 생성자 함수로 사용할 수 있다.
:heavy_check_mark: 화살표 함수는 생성자 함수로 사용할 수 없다. prototype 프로퍼티를 가지고 있지 않기 때문이다.

function fun() {
  this.num = 1234;
}
const arrFun = () => {
  this.num = 1234;
};

const funA = new fun();
console.log(funA.num); // 1234

const funB = new arrFun(); // Error
3. arguments 사용 가능 여부
:heavy_check_mark: 일반 함수 에서는 함수가 실행 될때 암묵적으로 arguments 변수가 전달되어 사용할 수 있다.
:heavy_check_mark: 화살표 함수에서는 arguments 변수가 전달되지 않는다.

function fun() {
  console.log(arguments); // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
}

fun(1, 2, 3);
일반함수는 arguments변수가 전달되어 [1,2,3]이 찍히지만

const arrFun = () => {
  console.log(arguments); // Uncaught ReferenceError: arguments is not defined
};

fun(1, 2, 3);
화살표함수는 arguments를 정의할 수 없다고 뜬다.

