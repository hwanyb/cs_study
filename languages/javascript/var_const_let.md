# 📌 `var`, `const`, `let`
## ✅ `var`, `const`, `let`의 차이점에 대해 설명해 주세요.
- `var`는 `function-scoped`이고, `let`, `const`는 `block-scoped`입니다.
- `var`는 변수 재선언, 재할당 모두 가능합니다.
- `const`는 변수 재선언, 재할당 모두 불가능합니다.
- `let`은 변수 재선언은 불가능하고, 재할당은 가능합니다.

||let|const|var|
|----|:---:|:---:|:---:|
|유효범위|Block Scope|Block Scope|Function Scope|
|재할당|⭕|❌|⭕|
|재선언|❌|❌|⭕|

***
## 🔗 용어 설명
### ✔ `function-scope`
`function-scope`는 함수 내부 스코프를 의미하며, 함수 내부에서 선언된 변수는 함수 내부에서만 접근 가능합니다.
```javascript
function test() {
    for(var i=0; i<3; i++){
        console.log(i);
    }
    console.log('final:', i);
}
```
`i`를 `var`로 선언했기 때문에 함수 안에서만 접근하면 얼마든지 `i`에 접근할 수 있습니다.

### ✔ `block-scope`
`block-scope`는 블록 `{}` 내부의 스코프를 의미하며, 블록 내부에서 선언된 변수는 블록 내부에서만 접근이 가능합니다.
```javascript
function test() {
    for(let i=0; i<3; i++){
        console.log(i);
    }
    console.log('final:', i);
}
```
`i`를 let으로 선언했기 때문에 블록 {} 안에서만 사용이 가능합니다. 따라서 for() {}바깥에 위치한 `console.log('final:', i);`는 `i`에 접근할 수 없어 `ReferenceError`가 발생합니다.

***
## 🔗 참고
- [Scope, let/const/var의 차이점](https://joooing.tistory.com/entry/Scope)