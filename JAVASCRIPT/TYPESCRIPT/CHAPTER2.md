# TypeScript "Hello, World"

1. .ts 파일 생성
- app.ts 파일을 생성
2. ts 파일 작성
```
let message: string = 'Hello, World';
console.log(message);
```
3. ts 파일 컴파일
```
tsc app.ts
```
4. app.js 파일 실행
- 컴파일된 app.js 파일 실행
```
node app.js
```
- ts-node가 설치되어있을 경우 ts 파일을 직접 실행할 수 있다.
```
ts-node app.ts
```
