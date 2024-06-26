# 12 - 함수

## 12.1 함수란?

- 일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다.
    
    ![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/1bccd72d-436d-4946-8f08-f9b6f3674eca)

    - 매개변수 - 함수 내부로 입력을 전달받는 변수
    - 입력 - 인수
    - 출력 - 반환값
- 함수는 값이며 여러 개 존재할 수 있다.
→ 특정 함수를 구별하기 위해 식별자인 함수 이름을 사용할 수 있다.
- 함수는 함수 정의를 통해 생성한다.
    
    ```jsx
    // 함수 선언문을 통해 함수 정의 예시
    function add(x, y){
    	return x + y;
    }
    // 함수 호출
    var result = add(2, 5);
    // 함수 add에 인수 2,5 를 전달하면서 호출하면 반환값인 7을 반환한다.
    console.log(result);
    ```
    
- 함수를 실행시키기 위해서는 인수를 매개변수를 통해 함수에 전달하면서 함수의 실행을 명시적으로 지시해야하는데, 이를 **`함수호출`** 이라 한다.

## 12.2 함수를 사용하는 이유

- 함수는 코드의 중복을 억제하고 **재사용성**을 높이기 때문에 **유지보수의 편의성**을 높이고 **코드의 신뢰성**을 높이는 효과가 있다.

## 12.3 함수 리터럴

- 자바스크립트의 함수는 객체 타입의 값이다. 그러므로 함수 리터럴로 생성할 수 있다.
- 함수 리터럴은 function 키워드, 함수 이름, 매개 변수 목록, 함수 몸체로 구성된다.
    
    ```jsx
    // 변수에 함수 리터럴을 할당
    var f = function add(x, y){
    	return x + y;
    };
    ```
    
- 함수 리터럴의 구성 요소
    - 함수 이름
        - 함수 이름은 식별자이므로 식별자 네이밍 규칙을 준수해야함
        - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자
        - 함수 이름은 생략 가능. 
        이름이 있는 함수 - 기명함수
        이름이 없는 함수 - 익명함수
    - 매개변수 목록
        - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분
        - 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당 → 매개변수 목록은 순서에 의미가 있음
        - 매개변수는 함수 몸체 내에서 변수와 동일 취급 → 식별자 네이밍 규칙을 준수해야함
    - 함수 몸체
        - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행단위로 정의한 코드 블록
        - 함수 몸체는 함수 호출에 의해 실행
- **함수는 객체**지만 일반 객체와는 다르다.
    - **호출할 수 없는 일반 객체에 비해 함수는 호출이 가능**하다.
    - 함수는 일반객체에는 없는 **함수 객체만의 고유한 프로퍼티**를 갖는다.

## 12.4 함수 정의

- 함수 정의 방식
    - 함수 선언문, 함수 표현식, Function 생성자 함수, 화살표 함수(S6)

### 12.4.1 함수 선언문

```jsx
// 함수 선언문
function add(x, y){
	return x + y;
}
```

- 함수 리터럴과 동일한 형태이지만 함수 이름을 생략할 수 있는 함수 리터럴과 다르게 **함수 선언문은 함수 이름 생략이 불가능**하다.
- 함수 선언문은 표현식이 아닌 문이다.

### 12.4.2 함수 표현식

```jsx
// 함수 표현식
var add = function(x, y){
	return x + y;
};
// 기명 함수 표현식
var add2 = function foo(x, y){
	return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2,5)); // 7
```

- 함수는 일급 객체이므로 함수 리터럴로 생성한 함수 객체를 변수에 할당할 수 있는데, 이러한 방식을 함수 표현식이라 한다.
- 함수 리터럴의 함수 이름은 생략이 가능하다. 이러한 함수를 익명함수라 한다.
- 함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적이다.
- 함수 선언문은 **표현식이 아닌 문**이고, 함수 표현식은 **표현식인 문**이다.

### 12.4.3 함수 생성 시점과 함수 호이스팅

- 함수 선언문이 코드의 선두로 끌러 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라한다.
- **함수 표현식**으로 함수를 정의하면 함수 호이스팅이 발생하지 않고 **변수 호이스팅**이 발생한다.

### 12.4.4 Function 생성자 함수

```jsx
// Function 생성자 함수
var add = new Function('x', 'y', 'return x+y');
```

- Function 생성자 함수로 함수를 생성하는 방식은 일반적이지 않고 바람직하지 않다.
- Function 생성자 함수로 생성한 함수는 클로저를 생성하지 않는 등 다른 방법으로 생성한 함수들과 다르게 동작한다.

### 12.4.5 화살표 함수

```jsx
// 화살표 함수(ES6)
var add = (x, y) => x + y;
```

- ES6에서 도입된 화살표 함수는 function 키워드 대신 화살표를 이용하여 간략한 방법으로 함수를 선언할 수 있다.
- 화살표 함수는 익명 함수로 정의한다.
- 화살표 함수는 생성자 함수로 사용할 수 없으며 기존 함수와 this 바인딩 방식이 다르고 prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.

## 12.5 함수 호출

- 함수는 함수를 가리- 키는 식별자와 한 쌍의 소괄호인 함수 호출 연산자로 호출한다.
- 함수는 매개변수의 개수와 인수의 개수가 일치하는지 체크하지 않는다. 
→ 함수를 호출할 때 매개변수의 개수만큼 인수를 전달하지 않아도 에러가 발생하지 않는다.

### 12.5.3 매개변수의 최대 개수

- 함수의 매개변수는 코드를 이해하는 데 방해되는 요소이므로 이상적인 매개변수 개수는 0개이며 적을 수록 좋다.
- **이상적인 함수는 한 가지 일만 해야하며 가급적 작게 만들어야한다.**
- 매개변수는 최대 3개 이상을 넘기지 않는 것을 권장한다. 만약 그 이상의 매개변수가 필요하다면 객체를 인수로 전달하는 것이 유리하다.

## 12.6 참조에 의한 전달과 외부 상태의 변경

```jsx
// 매개변수 primitive는 원시 값을 전달받고, 매개 변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj){
	primitive += 100;
	obj.name = 'Kim';
}

// 외부 상태
var num = 100;
var person = {name: 'Lee'};
console.log(num); // 100
console.log(person); // {name:"Lee"}

// **원시 값은 값 자체가 복사되어 잔달되고 객체는 참조 값이 복사되어 전달된다.**
changeVal(num, person);
// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100
// 객체는 원본이 훼손된다.
console.log(person); // {name:"Kim"}
```

- 원시 타입 인수를 전달 받은 매개변수 primitive의 경우 원시 값은 변경 불가능한 값이므로 직접 변경이 불가능하기 때문에 재할당을 통해 할당된 원시 값을 새로운 원시 값으로 교체
- 객체 타입 인수를 전달받은 매개변수 obj의 경우 객체는 변경 가능한 값이므로 직접 변경할 수 있기 때문에 재할당 없이 직접 할당된 객체를 변경
    
![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/e8b579b6-561c-4194-878f-3479728d8050)

    
- 의도치 않은 객체의 변경을 방지하기 위해서 객체를 불변 객체로 만들어서 사용할 수 있다. 
객체의 복사본을 새롭게 생성하는 비용은 들지만 객체를 원시 값처럼 변경 불가능한 값으로 동작하게 만들 수 있다.
    
    → 깊은 복사를 통해 새로운 객체를 생성하고 재할당을 통해 교체한다.
    

## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수

```jsx
// 익명 즉시 실행 함수
(function(){
	var a = 3;
	var b = 6;
	return a * b;
}());
```

- 함수 정의와 동시에 즉시 호출되는 함수
- 단 한번만 호출되며 다시 호출할 수 없다.
- 즉시 실행 함수는 함수 이름이 없는 익명함수를 사용하는 것이 일반적이다.
- 반드시 그룹 연산자 (…) 로 감싸야한다.

### 12.7.2 재귀 함수

- 재귀 호출을 수행하는 함수
- 재귀 함수는 자신을 무한 재귀호출하므로 재귀호출을 멈출 수 있는 탈출 조건을 반드시 만들어야한다.

### 12.7.3 중첩 함수

- 함수 내부에 정의된 함수를 중첩 함수 또는 내부 함수라 한다.
- 중첩 함수를 포함하는 함수는외부 함수라 부른다.

### 12.7.4 콜백 함수

- 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백함수라고 한다.
- 고차함수
    - 매개변수를 통해 함수의 외부에서 콜백함수를 전달받은 함수를 고차함수라고 한다.
    - 고차함수는 콜백함수를 자신의 일부분으로 합성한다.
    - 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출시점을 결정해서 호출한다.
        
        → 콜백 함수는 고차 함수에 의해 호출되는데 이 때 고차함수는 필요에 따라 콜백함수에 인수를 전달할 수 있다.
        

### 12.7.5 순수 함수와 비순수 함수

- 어떤 외부 상태에 의존하지도 않고 변경하지도 않는, 즉 부수효과가 없는 함수를 순수함수라고 한다.
- 어떤 외부 상태에 의존하거나 외부 상태를 변경하는, 즉 부수효과가 있는 함수를 비순수함수라고 한다.
- 함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 외부 상태를 변경하는 부수 효과를 최소화 해서 불변성을 지향하는 프로그래밍 패러다임이다.

# 13 - 스코프

### 13.1 스코프란

- 모든 식별자(변수 이름, 함수 이름, 클래스 이름, 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정되는데, 이를 스코프라 한다. 
→ 스코프는 식별자가 유효한 범위를 뜻한다.
- 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고 말할 수있다.
- 만약 스코프라는 개념이 없다면 같은 이름을 갖는 변수는 충돌을 일으키므로 프로그램 전체에서 하나만 사용할 수 있을 것이다.
- var 키워드로 선언한 변수의 중복 선언
    - var 키워드로 선언된 변수는 가은 스코프 내에서 중복 선언이 허용되는데, 이는 의도치 않게 변수 값이 재할당되어 변경되는 부작용을 발생시킨다.
    - let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.

### 13.2 스코프의 종류

| 구분  | 설명 | 스코프 | 변수 |
| --- | --- | --- | --- |
| 전역 | 코드의 가장 바깥 영역 | 전역 스코프 | 전역 변수 |
| 지역 | 함수 몸체 내부 | 지역 스코프 | 지역 변수 |
- 전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역에서 선언된 변수는 지역 스코프를 갖는 지역 변수이다.
- 전역 변수는 어디서든지 참조할 수 있다.
- 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효하다

## 13.3 스코프 체인

- 스코프는 함수의 중첩에 의해 계층적 구조를 갖는다.
- 모든 스코프는 하나의 계층적 구조로 연결되며 모든 지역 스코프의 최상위 스코프는 전역 스코프다.
    - 이렇게 스코프가 계층적으로 연결된 것을 스코프 체인이라 한다.
- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색한다.
- 스코프는 식별자를 검색하는 규칙이다.

## 13.4 함수 레벨 스코프

- var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다. 이러한 특성을 함수 레벨 스코프라한다.

## 13.5 렉시컬 스코프

- 렉시컬 스코프는 함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 결정한다.
- 자바스크립트는 렉시컬 스코프를 따르므로 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의 했는지에 따라 상위 스코프를 결정한다.
- 함수의 상위 스코프는 언제나 자신이 정의된 스코프이다.
- 함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정된다. 함수 정의(함수 선언문 또는 함수 표현식)가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다.

# 14 - 전역 변수의 문제점

## 14.1 변수의 생명주기

### 14.1.1 지역 변수의 생명주기

![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/73c148a9-ab80-47b2-8117-3d8edd523f57)

- 지역 변수의 생명 주기는 함수의 생명주기와 일치한다.

### 14.1.2 전역 변수의 생명 주기

![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/9caf5cf7-baf6-4df6-85a6-fa8cdb10fb12)

- 전역 코드는 함수 호출과 같이 전역 코드를 실행하는 특별한 진입점이 없고 코드가 로드되자마자 곧바로 해석되고 실행된다.
- var 키워드로 선언한 전역 변수의 생명주기는 전역 객체의 생명주기와 일치한다.

## 14.2 전역 변수의 문제점

- **암묵적 결합**
    - 전역 변수를 선언한 의도는 코드 어디서든 참조하고 할당 가능한 변수를 사용하겠다는 것이다. 이는 **모든 코드가 전역 변수를 참조하고 변경할 수 있는 암묵적 결합을 허용**하는 것이다.
- **긴 생명 주기**
    - **전역 변수는 생명주기가 길다.** → 메모리 리소스를 오랜 기간 소비한다.
- **스코프 체인 상에서 종점에 존재**
    - 전역 변수는 스코프 체인 상에서 종점에 존재하기 때문에 변수를 검색할 때 가장 마지막에 검색된다.
    → **전역 변수의 검색 속도가 가장 느리다.**
- **네임스페이스 오염**
    - 자바스크립트에서는 파일이 분리되어있어도 하나의 전역 스코프를 공유한다. 
    → 다른 파일 내에서 동일한 이름으로 명명된 전역변수나 전역 함수가 같은 스코프 내에 존재할 경우 예상치 못한 결과를 가져올 수 있다.

## 14.3 전역 변수 사용을 억제하는 방법

- **전역 변수를 반드시 사용해야할 이유를 찾지 못한다면 지역변수를 사용해야한다.**
- **변수의 스코프는 좁을수록 좋다.**

### 14.3.1 즉시 실행함수

- 모든 코드를 즉시 실행함수로 감싸면 모든 변수는 즉시 실행함수의 지역 변수가 된다.

### 14.3.2 네임스페이스 객체

- 전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법

### 14.3.3 모듈 패턴

- 모듈패턴은 클래스를 모방해서 관련이 있는 변수와 함수를 모아 즉시 실행함수로 감싸 하나의 모듈을 만든다.
- 모듈 패턴을 자바스크립트의 클로저를 기반으로 동작한다.
- 모듈패턴은 전역 변수의 억제부터 캡슐화까지 구현할 수 있다.

### 14.3.4 ES6 모듈

- ES모듈을 사용하면 더는 전역 변수를 사용할 수 없다.
- ES6 모듈은 파일 자체의 독자적인 모듈 스코프를 제공한다.

# 15 - let, const 키워드와 블록 레벨 스코프

## 15.1 var키워드로 선언한 변수의 문제점

- 변수 중복 선언이 가능하다.
- 함수 레벨 스코프를 가지기 때문에 함수 외부에서 var키워드로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다.
- 변수 호이스팅에 의해 변수 선언문 이전에 참조할 수 있다.

## 15.2 let 키워드

- let 키워드로 이름이 같은 변수를 중복 선언하면 문법에러가 발생한다.
- let 키워드로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.
- let 키워드로 선언한 변수는  변수 호이스팅이 발생하지 않는 것처럼 동작한다. 
→ 변수를 변수 선언문 이전에 참조하면 참조에러가 발생한다.
- let 키워드로 선언한 변수는 “선언 단계”와 “초기화 단계” 가 분리되어 진행된다.
- let 키워드로 선언한 변수는 스코프의 시작 지점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없는데 이 구간을 일시적 사각지대라고 부른다.

## 15.3 const 키워드

- const 키워드는 상수를 선언하기 위해 사용한다.
- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야한다.
- const 키워드로 선언한 변수는 재할당이 금지된다.
    - const 키워드로 선언한 변수에 원시 값을 할당한 경우 원시 값은 변경할 수 없는 값이고  const 키워드에 의해 재할당이 금지되므로 할당된 값을 변경할 수 있는 방법은 없다.
- const 키워드로 선언한 변수에 객체를 할당한 경우 값을 변경할 수 있다.
- **const 키워드는 재할당을 금지할 뿐 불변을 의미하지는 않는다.**

✅ **자바스크립트는 ES6에서 도입된  let, const를 포함한 모든 선언이 호이스팅된다. 단 ES6 에서 도입된 let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.**

# 💬 느낀점
- 평소 다른 개발자분들이 함수프로그래밍에 대해 얘기하는 걸 보고 공부의 필요성을 느꼈었는데 이 책에서 순수함수, 비순수함수 등 함수 프로그래밍에 대한 내용을 조금이라도 공부할 수 있어서 좋았다!
- 책에서 바람직한 개발방법에 대해 이것저것 제시해줘서 평소에 내가 어떻게 개발을 하고 있었는지에 대해 다시 한 번 생각해볼 수 있었다. (그냥 개발하지 말고! 생각을 하며 개발을 하자!! )
- ES6 모듈은 평소에 자주 안 써봤기 때문에 시간을 내서 한번 더 공부 해보고 직접 사용해봐야겠다고 느꼈다!
