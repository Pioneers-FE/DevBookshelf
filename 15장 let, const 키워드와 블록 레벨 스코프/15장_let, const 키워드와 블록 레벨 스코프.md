이번장은 `var` 키워드의 문제점을 다루고 이를 보완한 `let`, `const`를 다루는 시간을 갖는다.

## var의 문제점

1. 변수 중복 선언이 가능함.

   ```jsx
   var a = 100
   var a
   var a = 200
   ```

   초기화 문이 없다면 엔진에 의해 무시되고 초기화 문이 있다면 var키워드가 없는 것처럼 동작한다.

2. 함수레벨 스코프이기 때문에 전역변수가 의도치 않게 생성될 수 있음

   ```jsx
   if (true) {
     var x = 10
   }
   ```

   블록문에 감싸서 표현했지만 전역 변수 x가 생겼다.

3. 변수 호이스팅으로 인해 예기치 못한 에러 발생 가능

## let의 차이점

1. 중복 선언을 방지한다.

   중복선언을 하게 되면 문법에러가 발생하게 된다.

2. 블록 레벨 스코프

   모든 코드 블록을 지역 변수로 인정한다.

3. 변수호이스팅이 일어나지 않는 것처럼 보이게 함.

   선언과 초기화의 분리. 런타임 이전에 선언단계가 실행되는 것은 동일 그러나 초기화는 코드문이 실행되기 전까지 일어나지 않는다.

   그래서 스코프 시작지점 부터 초기화 시작지점까지를 Temporal Dead Zone이라고 부른다.

   ```jsx
   let x = 100

   {
     console.log(x) // Reference Error

     let x = 1
   }
   ```

   만약 호이스팅이 일어나지 않는다면 해당 코드는 문제없이 100을 출력해야 한다. 그러나 스코프 마다 호이스팅이 일어났기 때문에 참조 오류가 발생한다.

4. 전역 변수를 선언해도 window 전역 객체의 프로퍼티가 되지 않는다.

   ```jsx
   var x = 20
   let y = 10
   function foo() {}

   window.x // 20
   window.y // undefined
   window.foo // function...
   ```

## const 키워드

const 키워드는 재할당이 금지된 변수다. 그래서 상수로 취급될 수 있다.

다만 객체의 경우에는 수정이 가능하다. 객체의 수정은 재할당과 관련이 없다.

따라서 const 키워드로 선언한 객체의 경우라도 재할당이 가능하다는 특징이 있다.
