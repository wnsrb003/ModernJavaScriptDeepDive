# ModernJavaScriptDeepDive
모던자바스크립트 Deep Dive 책 스터디

## 정리
> 변수 
1. 메모리 공간
2. 식별자(고유의 이름) - var result = 200 >> result = 식별자이면서 200이라는 값을 가르키는 메모리 주소가 저장된다.
3. 메모리 주소

> 변수 선언
자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차 실행 -> 런타임\
변수 선언은 런타임 이전 단계에서 실행된다!(변수(var, let, const), 함수, class등) - 호이스팅\
다만, 변수 선언과 값의 할당은 다른 단계(var a = 10 코드가 있다면 var a = undefined로 선언이 먼저 실행되지만, a = 10 이라는 값의 할당은 이뤄진 것은 아니고 런타임 단계에서 실행된다.)\

> 호이스팅
```
var s = 9
console.log(s)  -> 9
```
```
console.log(s)  -> undefined
s = 9
var s;
console.log(s)  -> 9
```

> 가비지 컬렉터

변수 값이 없는 경우 정리, 다만 랜덤\
참고) ES2021 -> Finalize\
WeakRef - 약한 참조를 걸어서 참조카운트가 0이면 정리하는 기능이 새로 나옴(찾아봐야 알듯)
```
var a = new WeakRef({ a:1 });
a.deref();
```

> 변수 이름 제한

숫자 시작, - 포함, 예약어(this,var등등)

> falsy
> 
falsy data : 0, '', null, undefined, false, NaN

> 변수 형

const 기본으로 데이터 변경 필요시에만 let 사용(거의 대부분 const 사용하여 개발 가능) 
-> var는 함수레벨스코프로 의도치않게 전역변수로 지정되어 오류 초래할 수 있다.

> 실행 컨테스트

