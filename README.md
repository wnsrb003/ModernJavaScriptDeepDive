# ModernJavaScriptDeepDive
모던자바스크립트 Deep Dive 책 스터디

## 4장
> 변수 
1. 메모리 공간
2. 식별자(고유의 이름)
3. 메모리 주소

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
