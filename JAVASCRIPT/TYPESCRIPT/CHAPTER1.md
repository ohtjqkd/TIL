# TYPESCRIPT TUTORIAL

## TYPESCRIPT란?
typescript의 목적은
- 데이터의 type을 javascript에 도입
- ESMAScript Next or ES Next라고 하는 향후 javascript의 계획된 기능을 현재 javascript에 구현

## TypeScript의 장점
1. 버그를 피하면서 생산성을 향상시킨다.
type을 도입하면 런타임 버그가 발생하는 대신 컴파일 단계에서 버그를 잡을 수 있다.

```ex
function add(x, y) {
    return x + y;
}
```

HTML 요소들의 값을 가져와 함수에 전달하면 예기치 않은 결과가 나타날 수 있다.

```
let result = add(input1.value, input2.value);
console.log(result);
```
사용자가 10 input1에 10을 입력하고 input2에 20을 입력한 후 add를 호출한다면 예상했던 30이 아닌 1020이 반환되게 된다.
이는 input1과 input2가 string 타입이어서 발생하는 버그인데, javascript는 typetypesript에서는 type을 지정하여 컴파일 단계에서 오류를 발생시킬 수 있게 된다.
production 단계에서 런타임 버그가 발생하게 된다면 치명적이기 때문에 컴파일 단계에서 버그를 발견하고 해결할 수 있는 것은 typescript의 장점이라고 할 수 있다.


## npm 설치

```
npm install -g typescript
tsc --v
npm install -g ts-node
```
