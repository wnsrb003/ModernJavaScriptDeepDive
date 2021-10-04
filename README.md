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

> 함수

- 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르다 -> 호이스팅(함수 표현식은 변수 호이스팅이 일어나는 것)
- 매개 변수보다 인수가 더 많은 경우, 초과된 인수는 무시(다만, arguments에 들어가 있음)
- 매개변수의 원시타입과 객체타입 인수는 차이가 있다.
```
function a(p, obj) {
  p++;
  obj.a = 0;
  }
  
var num = 0;
var person = {a:"name"};

console.log(num)  //0
console.log(person). // {a:"name"}

a(num, person);

console.log(num)  //0.  --안바뀜
console.log(person)  // {a:"0"} --바뀜

```
- 콜백함수 : 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백 함수라고 하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수라고 한다.

> 실행 컨테스트


> 메소드

메소드는 자신을 바인딩한 객체를 가르키는 내부 슬롯을 가지고 그것으로 super 가능

> 화살표 함수
```
const arrow = (x,y) => x*y;
const mul = () => { return (x*y) };
```
```
[1,2,3].map(v => v * 2);  //[1,2,3].map(function(v) { return v*2;} 의 ES6 화살표 함수 표현
const redux = dispatch => action => action.dispatch(next(action)); //이런 식의 연속되게 가능
```
단, 중복되는 변수는 사용 금지 ( const x = (a,a) => (a*a) //에러 )

> 배열

희소배열 = [, 1, , 3] -> 희소배열의 길이는 실제 요소 개수 보다 많다. 사용 권장하지 않음\
원본 배열을 직접 변경하는 메소드와 원본 배열을 변경하지 않고 새로 생성하는 메소드가 있다. -> 배열 관련 함수를 사용할 때 필히 확인
```
a.push() -> 원본 배열 변경
a.concat() -> 새로 생성
```
unshift -> 앞에 밀어넣기 / shift -> 앞에 제거    // splice로 사용 권장

splice -> arr.splice('start', 'count', 'items') -> 배열 제거를 시작할 인덱스, 제거할 개수, 삽입할 요소

> Number

Number.EPSILON >> 자바 스크립트에서 오차\
```
0.1 + 0.2 === 0.3. > false
isEqual(0.1+0.2, 0.3) > true
``` 
Number.MAX_SAFE_INTEGER >> 자바 스크립트에서 integer 의 최대 값으로 넘어가면 정상 동작이 안될 수 있음.\
Number.MIN_SAFE_INTEGER >> 최소값

> Symbol

- 생성자로 생성 불가
- 다른 값과 절대 중복되지 않는 유일무이한 값

> Symbol Iterable 

- Symbol.iterator라고 하는 메서드를 가지고 있는 객체
- Symbol.iterator는 next 메서드를 가지고 있는 객체를 반환해야 함.
- next 메서드는 {value}가 포함되어 리턴해야 함.

> promise

- 비동기 함수로 reject(실패), resolve(성공) 리턴
- 상태 정보로는 pending(대기), fulfilled(수행완료 - resolved), rejected(수행 완료 - reject)

> promise 후속 처리 메서드

- .then : 첫번째 콜백함수는 fulfilled 상태일 때, 호출하고 두번째는 rejected 호출
- .catch : rejected일때만 호출
- .finally : 성공 or 실패 상관없이 무조건 한번 호출

> 마이크로태스크 큐 

- 프로미스는 마이크로태스크 큐에 드로 테스크큐보다 우선순위가 높다.
```
setTimeout(() => console.log(1), 0);
Promise.resolve()
.then(() => console.log(2))
.then(() => console.log(3))
// 순서 2 > 3 > 1
```
