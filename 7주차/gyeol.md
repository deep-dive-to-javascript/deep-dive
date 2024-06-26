# 7회차 정리(25장~26장)

# 25 - 클래스

## 25.1 클래스는 프로토타입의 문법적 설탕인가?

- 자바스크립트는 프로토타입 기반의객체지향 언어
- 프로토타입 기반 객체지향언어는 클래스가 필요없는 객체지향 프로그램이 언어
    
    (ES5에서는 클래스 없이도 생성자 함수와 프로토타입을 통해 객체지향 언어의 상속 구현 가능)
    
- ES6에서 도입된 클래스는 클래스 기반 객체지향 프로그래밍에 익숙한 프로그래머가 빠르게 학습할 수 있도록 클래스 기반 객체지향 프로그래밍 언어와 흡사한 새로운 객체 생성 메커니즘을 제시
- 클래스는 함수이며 기존 프로토타입 기반 패턴을 크래스 기반 패턴처럼 사용할 수 있도록 하는 문법적 설탕이라고 볼 수 있음
- 클래스와 생성자 함수의 차이
    
    
    |  | 클래스 | 생성자함수 |
    | --- | --- | --- |
    | new 연산자 없이 호출 | 에러 발생 | 일반 함수로서 호출됨 |
    | extends, super 키워드 제공 | 제공 ❌ | 제공 ⭕ |
    | 호이스팅  | 호이스팅이 발생하지 않는 것처럼 동작 | 함수 선언문으로 정의된 생성자 함수 → 함수 호이스팅 발생
    함수 표현식으로 정의한 생성자 함수 → 변수 호이스팅 발생 |
    | strict mode | 클래스 내 모든 코드에 암묵적으로 지정되어 실행. 해제 불가능 | 암묵적으로 지정되지 않음 |
    | 프로퍼티 [[Enumerable]] 값 | 클래스의 constructor, 프로토 타입 메서드, 정적 메서드 모두 프로퍼티 어트리뷰트 [[Enumerable]] 값이 false. 열거 ❌ |  |
- 생성자 함수와 클래스는 프로토타입 기반의 객체지향을 구현했다는 점에서 매우 유사
- 하지만 클래스는 생성자 함수 기반의 객체 생성방식보다 명료함.
    
    → 클래스의 extends와 super 키워드는 상속 관계 구현을 더욱 간결하고 명료하게함
    
- 결론
    - 클래스를 프토토타입 기반 객체 생성 패턴의 단순한 문법적 설탕이라고 보기보다 **새로운 객체 생성 메커니즘**으로 보는 것이 합당

## 25.2 클래스 정의

- 클래스는 class 키워드를 사용하여 정의
- 클래스 이름은 파스칼 케이스를 사용하는 것이 일반적
    
    ```jsx
    // 클래스 선언문
    class Person {}
    ```
    
- 클래스는 값으로 사용할 수 있는 일급 객체(표현식으로 정의가 가능)
- 일급객체 특징
    - 무명의 리터럴로 생성 가능 → 런타임에 생성 가능
    - 변수나 자료구조에 저장 가능
    - 함수의 매개변수에 전달 가능
    - 함수의 반환값으로 사용 가능
- 클래스 몸체에는 0개 이상의 메서드만 정의 가능
- 클래스 몸체에서 정의할 수 있는 메서드
    - constructor(생성자), 프로토타입 메서드, 정적 메서드
        
        ```jsx
        // 클래스 선언문
        class Person {
        	// 생성자
        	constructor(name){
        		// 인스턴스 생성 및 초기화
        		this.name = name; // name 프로퍼티는 public
        	}
        	// 프로토타입 메서드
        	sayHi(){
        		console.log(`hi my name is ${this.name}`);
        	}
        	// 정적 메서드
        	static sayHello(){
        		console.log('hello');
        	}
        }
        // 인스턴스 생성
        const me = new Person('Park');
        // 인스턴스의 프로퍼티 참조
        console.log(me.name); // Park
        // 프로토타입 메서드 호출
        me.sayHi(); // Hi! My name is Park
        // 정적 메서드 호출
        Person.sayHello(); // Hello!
        ```
        
    - 클래스와 생성자 함수의 정의 방식 비교
        
        ![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/460a5374-4538-4452-937d-1e00f723d223)


## 25.3 클래스 호이스팅

- 클래스는 함수로 평가됨
- 클래스 선언문으로 정의한 클래스는 함수 선언문과 같이 런타임 이전에 먼저 평가되어 함수 객체를 생성
    
    → 이 함수 객체는 생성자함수로서 호출할 수 있는 함수(constructor)임 
    
- 생성자 함수로서 호출할 수 있는 함수는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성됨
    
    → 프로토타입과 생성자 함수는 언제나 쌍으로 존재(단 클래스는 클래스 전의 이전에 참조 불가능)
    
- 클래스 선언문은 호이스팅이 발생함
    - 단, let과 const 키워드로 선언한 변수처럼 호이스팅되어 선언 이전에 일시적 사각지대에 빠져 호이스팅이 발생하지 않는 것처럼 동작
- var, let, const, function, function*, class 키워드를 사용하여 선언된 모든 식별자는 호이스팅됨
    
    → 모든 선언문은 런타임 이전에 먼저 실행되기 때문
    

## 25.4 인스턴스 생성

- 클래스는 생성자 함수이며 new 연산자와 함께 호출되어 인스턴스를 생성(반드시 new 연산자와 함께 호출해야함)
- 참고)함수는 new 연산자의 사용 여부에 따라 일반 함수로 호출되거나 인스턴스 생성을 위한 생성자 함수로 호출
    
    ```jsx
    // 클래스를 new 연산자 없이 호출하면 타입 에러가 발생
    class Person {}
    // 인스턴스 생성
    const me = Person();
    // TypeError: Class constructor Person cannot be invoked without 'new'
    ```
    
- 클래스 표현식으로 정의된 클래스의 경우 클래스를 가리키는 식별자를 사용해 인스턴스를 생성하지 않고 기명 클래스 표현식의 클래스이름을 사용해 생성하면 에러가 발생
    
    → 기명 함수 표현식과 마찬가지로 클래스 표현식에서 사용한 클래스의 이름은 외부 코드에서 접근이 불가능하기 때문
    
    ```jsx
    const Person = class MyClass{};
    const me = new Person1();
    // 클래스 이름 MyClass는 함수와 동일하게 클래스 몸체 내부에서만 유효한 식별자
    console.log(MyClass); // Uncaught ReferenceError: MyClass is not defined
    
    ```
    

## 25.5 메서드

- 클래스 몸체에는 0개 이상의 메서드만 선언 가능
- 클래스 몸체에서 정의할 수 있는 메서드 → constructor(생성자), 프로토타입 메서드, 정적 메서드

### 25.5.1 constructor

- 인스턴스를 생성하고 초기화하기 위한 특수한 메서드
- 이름 변경이 불가능
- constructor는 메서드로 해석되지 않고 클래스가 평가되어 생성한 함수 객체 코드의 일부가 됨
    
    → 클래스 정의가 평가되면 constructor의 기술된 동작을 하는 함수 객체가 생성
    
    참고) 클래스의 constructor 메서드와 프로토타입의 constructor 프로퍼티
    
    - 클래스의 constructor 메서드와 프로토타입의 constructor 프로퍼티는 이름은 같지만 직접적인 관련은 ❌
    - 프로토타입의 constructor 프로퍼티는 모든 프로토타입이 가지고 있는 프로퍼티이며 생성자 함수를 가리킴
- constructor와 생성자 함수의 차이
    - constructor는 클래스 내에 최대 한 개만 존재(2 개 이상인 경우 문법에러 발생)
    - constructor는 생략 가능
        
        → 생략하면 클래스에 빈 constructor가 암묵적으로 정의됨. constructor를 생략한 클래스는 빈 constructor 에 의해 빈 객체를 생성
        
    - 인스턴스 생성과 동시에 인스턴스 프로퍼티 추가를 통해 인스턴스의 초기화를 실행 → 인스턴스를 초기화하려면 constructor를 생략하면 안됨
    - constructor는 별도의 반환문을 갖지 않아야함
        
        → new 연산자와 함께 클래스가 호출되면 생성자 함수가 동일하게 암묵적으로 this(인스턴스)를 반환함.
        만약 this가 아닌 다른 객체를 명시적으로 반환하면 this(인스턴스)가 반환되지 못하고 return 문에 명시한 객체가 반환되기 때문에 클래스의 기본 동작을 훼손함 
        

### 25.5.2 프로토타입 메서드

- 생성자 함수를 사용하여 인스턴스 생성시 프로토타입 메서드를 생성하기 위해서는 명시적으로 프로토타입에 메서드를 추가해야함
- 클래스 몸체에서 정의한 메서드는 생성자 함수에 의한 객체 생성 방식과 달리 클래스의 prototype 프로퍼티에 메섣르르 추가하지 않아도 기본적으로 프로토타입 메서드가 됨
- 생성자 함수와 마찬가지로 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이됨

    ![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/84393a44-9cd1-4364-b75c-affc6462f730)
    
    - 이처럼 클래스 몸체에서 정의한 메서드는 인스턴스 프로토타입에 존재하는 프로토타입 메서드가 됨
    - 인스턴스는 프로토타입 메서드를 상속받아 사용 가능
- 즉, 클래스는 생성자 함수와 같이 인스턴스를 생성하는 생성자 함(클래스는 생성자함수와 같이 프로토타입 기반의 객체 생성 메커니즘)

### 25.5.3 정적 메서드

- 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드
- 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 됨
- 정적 메서드의 프로토 타입 체인

    ![image](https://github.com/deep-dive-to-javascript/deep-dive/assets/66353188/52441311-0efe-442a-921f-faa6146f5cc6)
    
    - 정적 메서드는 클래스에 바인딩된 메서드가 됨
    - 정적 메서드는 클래스 정의 이후 인스턴스를 생성하지 않아도 호출 가능
    - 정적 메서드는 프로토타입 메서드처럼 인스턴스로 호출하지 않고 클래스로 호출
    - 정적 메서드는 인스턴스로 호출 불가능 
    → 정적 메서드가 바인딩된 클래스는 인스턴스의 프로토타입 체인상에 존재하지 않기 때문(인스턴스의 프로토타입 체인 상에는 클래스가 존재하지 않음 → 인스턴스로 클래스의 메서드 상속 받을 수 없음)

### 25.5.4 정적 메서드와 프로토타입 메서드의 차이

- 정적 메서드와 프로토타입 메서드는 자신이 속해있는 프로토타입 체인이 다름
- 정적 메서드는 클래스로 호출. 프로토타입 메서드는 인스턴스로 호출
- 정적 메서드는 인스턴스 프로퍼티 참조 불가능. 프로토타입 메서드는 인스턴스 프로토타입 참조 가능
- 프로토타입 메서드와 정적 메서드 내부 this 바인딩 차이
    
    <aside>
    💡 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다!
    
    </aside>
    
    - 프로토 타입 메서드는 인스턴스로 호출해야함 → 프로토타입 메서드 내부의 this는 프로토타입 메서드를 호출한 인스턴스를 가리킴
    - 정적 메서드는 클래스로 호출해야함 → 정적 메서드 내부의 this는 인스턴스가 아닌 클래스를 가리킴
    - 따라서 메서드 내부에서 인스턴스 프로퍼티를 참조할 필요가 있다면 this를 사용해야하며 이 경우 프로토타입 메서드로 정의 해야함
    - 메서드 내부에서 this를 사용하지 않고도 프로토타입 메서드로 정의가 가능 하지만 반드시 인스턴스 생성 후에 다음 인스턴스로 호출해야하므로 this를 사용하지 않는 메서드는 정적 메서드로 정의하는 것이 좋음
- 표준 빌트인 객체인 Math, Number 등은 다양한 정적 메서드를 가지고 있음. 이 정적 메서드들은 애플리케이션 전역에서 사용할 유틸리티 함수 
e.g. Math.max, Numeber.isNaN 등
→ 이렇게 클래스 또는 생성자 함수를 하나의 네임스페이스로 사용하여 정적 메서드를 모아두면 충돌 가능성을 줄여주고 관련 함수를 구조화 하기 좋음.
즉 정적 메서드는 애플리케이션 전역에서 사용할 유틸리티 함수를 전역 함수로 정의하지 않고 메서드로 구조화할 때 유용

### 25.5 클래스에서 정의한 메서드 특징

- function 키워드를 생략한 메서드 축약 표현을 사용
- 객체 리터럴과는 달리 클래스에 메서드를 정의할 때는 콤마가 불필요
- 암묵적으로 strict mode로 실행됨
- for … in 문이나 Object.keys 메서드 등으로 열거 불가능(프로퍼티 어트리뷰트 [[Enumerable]]의 값이  false
- 내부 메서드 [[Construct]]를 갖지 않는 non-constructor → new 연산자와 함께 호출 ❌

## 25.6 클래스의 인스턴스 생성 과정

**`1. 인스턴스 생성과 this 바인딩`**

- new 연산자와 함께 클래스 호출하면 constructor의 내부 코드가 실행되기 전에 암묵적으로 빈 객체 생성. 
(이 빈객체는 클래스가 생성한 인스턴스인데 아직 완성되지 않은 상태)
- 이 때 클래스가 생성한 인스턴스의 프로톹아ㅣㅂ으로 클래스의 prototype 프로퍼티가 가리키는 객체가 설정됨
- 암묵적으로 생성된 빈 객체(인스턴스)는 this에 바인딩됨

⇒ constructor  내부의 this는 클래스가 생성한 인스턴스를 가리킴

`2. 인스턴스 초기화`

- constructor의 내부 코드가 실행되어 this에 바인딩되어있는 인스턴스를 초기화
→ this에 바인딩되어있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로  전달 받은 초기값으로 인스턴스이 프로퍼티값을 초기화
- 만약 constructor가 생략되었다면 이 과정도 생략

`3. 인스턴스로 반환`

- 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됨

```jsx
class Person{
	// 생성자
	constructor(name){
		// 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩됨
		console.log(this); // Person {}
		console.log(Object.getPrototypeOf(this) === Person.prototype); // true
		// 2. this에 바인딩되어있는 인스턴스를 초기화
		this.name = name;
		// 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됨
	}
}
```

## 25.7 프로퍼티

### 25.7.1 인스터스 프로퍼티

- 인스턴스 프로퍼티는 constructor 내부에서 정의해야 함
- 생성자 함수에서 생성자 함수가 생성할 인스턴스의 프로퍼티를 정의하는 것과 마찬가지로 constructor 내부에서 this에 인스턴스 프로퍼티를 추가함
    
    → 클래스가 암묵적으로 생성한 빈 객체(인스턴스)에 프로퍼티가 추가되어 인스턴스가 초기화됨
    
- constructor 내부에서 this에 추가한 프로퍼티는 언제나 클래스가 생성한 인스턴스의 프로퍼티가 됨
- ES6의 클래스는 ㅈ버근제한자를 지원하지 않으므로 인스턴스 프로퍼티는 언제나 public함

### 25.7.2 접근자 프로퍼티

- 접근자 프로퍼티는 자체적으로 값([[Value]] 내부 슬롯)을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(getter 함수와 setter 함수)로 구성됨
- 접근자 프로퍼티는 클래스에서도 사용할 수 있음
- 클래스의 메서드는 기본적으로 프로토타입 메서드가 됨 → 클래스의 접근자 프로퍼티 또한 인스턴스 프로퍼티가 아닌 프로토타입의 프로퍼티가 됨

### 25.7.3 클래스 필드 정의 제안

- 클래스 필드(필드 or 멤버)는 클래스 기반 객체 지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어
- 2021년 1월 기준 TC39 프로세스의 stage3에서 자바스크립트에서도 인스턴스 프로퍼티를 클래스 기반 객체지향 언어의 클래스 필드처럼 정의할 수 있는 새로운 표준 사양인 `Class field declarations` 가 제안되었음(2022년 6월 기준 ECMAScript에 정식 표준으로 승급)
- 클래스 필드에 함수를 할당하는 것은 가능하지만 권장되지는 않음
→ 그 함수는 프로토타입 메서드가 아닌 인스턴스 메서드가 되기 때문
- 클래스 필드 정의 제안으로 인해 인스턴스 프로퍼티를 정의하는 방식은 두 가지가 됨
    - 인스턴스를 생성시 외부 초기값으로 클래스 필드를 초기화할 필요가 있다면 constructor에서 인스턴스 프로퍼티를 정의하는 기존 방식 사용
    - 인스턴스 생성시 외부 초기값으로 클래스 필드를 초기화할 필요가 없다면 기존방식, 클래스 필드 정의 방식 모두 사용 가능

### 25.7.4 private 필드 정의 제안

- 자바스크립트는 캡슐화를 완전하게 지원하지 않음 
→ 인스턴스 프로퍼티는 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있음(언제나 public!)
- 클래스 필드 정의 제안을 사용하더라도 클래스 필드는 기본적으로 public → 외부에 그대로 노출됨
- 이 또한 2021년 1월 기준 TC39 프로세스의 stage3에서 private 필드를 정의할 수 있는 새로운 표준 사양이 제안되었음
- private 필드의 선두에 #을 붙여서 정의. 참조할 때도 #을 붙여줘야함
- private 필드는 클래스 내부에서만 참조 가능

### 25.7.5 static 필드 정의 제안

- 클래스에서는 static 키워드를 사용해 정적 메서드를 정의할 수 있지만 static 키워드를 사용해 정적 필드는 정의할 수 없었음
- 2021년 1월 기준  TC39 프로세스의 stage3에서 static public필드, static private필드, static private 메서드를 정의할 수 있는 새로운 표준 사양인 `Static sclass features` 가 제안 되었음

## 25.8 상속에 의한 클래스 확장

### 25.8.1 클래스 상속과 생성자 함수 상속

- 프로토타입 기반 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속받는 개념이지만 **상속에 의한 클래스확장은 기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것**
- 클래스는상속을통해 다른 클래스를 확장할  수 있는 문법인 extends 키워드가 기본적으로 제공, extends 키워드를 사용한 클래스 확장은 간편하고 직관적
- 생성자 함수는 클래스와 같이 상속을 통해 다른 생성자 함수를 확장 할수 있는 문법이 제공되지 않음

### 25.8.2 extends 키워드

- 상속을 통해 클래스를 확장하기 위해 extends 키워드를 사용해 상속받을 클래드를 정의
- 서브 클래스(파생클래스, 자식클래스)
    - 상속을 통해 확장된 클래스
- 수퍼클래스(베이스 클래스, 부모 클래스)
    - 서브클래스에게 상속된클래스
- extends 키워드의 역할
    - 수퍼클래스와 서브클래스간의 상속 관계를 설정
- 수퍼클래스와 서브클래스는 인스턴스의 프로토타입 체인 뿐만 아니라 클래스간의 프로토타입 체인도 생성
→이를 통해 프로토타입 메서드, 정적 메서드 모두 상속 가능

### 25.8.3 동적 상속

- extends 키워드는 클래스 뿐만 아니라 생성자 함수를 상속받아 클래스 확장도 가능(단, extends 키워드 앞에 반드시 클래스가 와야함)
- extends 키워드 다음에는 클래스뿐만 아니라 [[Construct]] 내부  메서드를 갖는 함수 객체로 평가 가능한 모든 표현식 사용 가능하며 이를 통해 동적으로 상속 받을 대상 결정 가능

### 25.8.4 서브클래스의 constructor

- 서브클래스에서 constructor를 생략하면 클래스에 아래와 같은 constructor가 암묵적으로 정의됨
    
    ```jsx
    constructor(...args){super(...args);}
    // args는 new 연산자와 함께클래스를 호출할 때 전달할 인수의 리스트
    // super()는 수퍼클래스의 constructor(super-constructor)를 호출하여 인스턴스를 생성
    ```
    
- 수퍼클래스, 서브클래스 모두  constructor를 생략하면 빈 객체가 생성됨
    
    → 프로퍼티를 소유하는 인스턴스를 생성하려면 constructor내부에서 인스턴스에 프로퍼티를 추가해야함
    

### 25.8.5 super 키워드

- super 키워드는 함수처럼 호출이 가능하고 this와 같이 식별자처럼 참조할 수 있는 특수한 키워드

**`super호출`** 

- super를  호출하면 수퍼클래스의 constructor(super-constructor)를 호출
- 
- super 호출시 주의사항
    - 서브클래스에서 constructor를 생략하지 않은 경우 서브클래스의 constructor에서는 반드시 super를 호출해야함
    - 서브클래스의 constructor에서  super를 호출하기 전에는 this 참조 불가능
    - super는 반드시 서브클래스의 constructor에서만 호출. 서브클래스가 아닌 클래스의 constructor나 함수에서super를 호출하면 에러 발생

**`super 참조`**

- 메서드 내에서  super를 참조하면 수퍼클래스의 메서드 호출 가능

### 25.8.6 상속 클래스의 인스턴스 생성 과정

**`1. 서브클래스의 super 호출`**

- 자바스크립트 엔진은 클래스 평가시 수퍼클래스와 서브클래스의 구분을 위해 ‘base’ or ‘derived’ 를 값으로 갖는 내부 슬롯 [[ConstructorKind]] 를 가짐
- 다른 클ㄹ래스를 상속받지 않는 클래스(그리고 생성자 함수)는 내부 슬롯  [[ConstructorKind]]의 값이 ‘base’ 로 설정
다른클래스를 상속받는 서브클래스는 내부 슬롯 [[ConstructorKind]] 의 값이 ‘derived’로 설정
→ 이를 통해 수퍼클래스와 서브클래스는 new 연산자와 함께 호출되었을 때의 동작이 구분됨
- 다른 클래스를 상속받지 않는 클래스(그리고 생성자함수)는 new 연산자와 함께 호출시 암묵적으로 빈 객체(인스턴스)를 생성하고 이를 this에 바인딩
    
    **다른 클래스를 상속받는 서브 클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임 → 서브클래스의 constructor에서 반드시 super를 호출해야하는 이유**
    
- 서브 클래스가 new 연산자와 함께 호출되면 서브클래스 constructor 내부의 super 키워드가  함수처럼 호출 → 수퍼클래스의 constructor(super-constructor)가 호출 됨(수퍼 클래스가 평가되어 생성된 함수 객체의 코드가 실행)

**`2. 수퍼클래스의 인스턴스 생성과 this 바인딩`**

- 수퍼클래스의 constructor 내부의 코드가 실행되기 이전에 암묵적으로 빈 객체를 생성(이 빈객체는 클래스가 생성한 인스턴스이며 미완성상태)
- 암묵적으로 생성된 빈 객체(인스턴스)는 this에 바인딩됨 → 수퍼클래스의 constructor 내부의 this는 생성된 인스턴스를 가리킴
- 이 때 인스턴스는 수퍼클래스가 생성한 것이지만 new 연산자와 함께 호출된 클래스는 서브클래스 → new 연산자와 함께 호출된 함수를 가리키는 new.target은 서브 클래스를 가리킴(**인스턴스는 new.target이 가리키는 서브클래스가 생성한 것으로 처리됨**)

**`3. 수퍼클래스의 인스턴스 초기화`**

- 수퍼클래스의 constructor가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화함
즉, this에 바인딩 되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화함

**`4. 서브클래스 constructor로의 복귀와 this 바인딩`**

- super의 호출이 종료되고 제어 흐름이 서브클래스 constructor로 돌아옴
    
    **이 때 super가 반환한 인스턴스가 this에 바인딩됨. 서브클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용**
    
- **이처럼 super가 호출되지 않으면 인스턴스가 생성되지 않고 this 바인딩도 불가능해짐. 
→ 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없는 이유**

**`5. 서브클래스의 인스턴스 초기화`** 

- super 호출 이후 서브클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행됨
→ this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화함

**`6. 인스턴스반한`**

- 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됨

### 25.8.7 표준 빌트인 생성자 함수 확장

- extends 키워드 다음에는 클래스뿐만 아니라 [[Construct]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식 사용  가능
- String, Number, Array 같은표준 빌트인 객체도 [[Construct]] 내부  메서드를 갖는 생성자 함수이므로 extends 키워드를 사용하여 확장 가능

# 26 - ES6 함수의 추가 기능

## 26.1 함수의 구분

- ES6 이전의 모든 함수는 사용 목적에 따라 명확히 구분되지 않음 
→ 일반 함수로서 호출이 가능하고 생성자함수로서의 호출도 가능함(ES6 이전의 모든 함수는 callable이면서 constructor)
- 호출 방식에 특별한 제약이 없고 생성자 함수로 호출되지 않아도 프로토 타입 객체를 생성 → 실수를 유발할 가능성이 있고 성능에도 좋지않음
- 이런  문제를 해결하기 위해 ES6에서 함수를 사용 목적에 따라 세 가지 종류로 구분함
    
    
    | ES6 함수의 구분 | constructor | prototype | super | arguments |
    | --- | --- | --- | --- | --- |
    | 일반 함수 | ⭕ | ⭕ | ❌ | ⭕ |
    | 메서드 | ❌ | ❌ | ⭕ | ⭕ |
    | 화살표 함수 | ❌ | ❌ | ❌ | ❌ |
    - 일반 함수는 함수 선언문이나 함수 표현식으로 정의한 함수이며 ES6 이전의 함수와 차이 ❌
    - ES6의 메서드와 화살표 함수는 ES6 이전의 함수와 명확한 차이 ⭕
        
        → 일반함수는 constructor / ES6의 메서드와 화살표 함수는 non-constructor 
        

## 26.2 메서드

- ES6 이전 사양에서는메서드에 대한 명확한 정의 ❌
- **ES6 사양에서 메서드는 메서드 축약 표현으로 정의된 함수만을 의미**
- **ES6 메서드는 인스턴스를 생성할 수 없는 non-constructor** 
→ 생성자 함수로서 호출 불가능하며 prototype 프로퍼티가 없고 프로토타입 생성 ❌
- **ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]] 를 가짐**
    
    → super 키워드 사용 가능(ES6 메서드가 아닌 함수는 super 키워드 사용 불가능)
    
- ES6 메서드는 본연의 기능(super)을 추가하고 의미적으로  맞지 않는 기능(constructor)은 제거 
→ 메서드 정의시 프로퍼티 값으로 익명 함수 표현식을 할당하는 ES6 이전의 방식은 사용하지 않는 것이 좋음

## 26.3 화살표 함수

- 화살표 함수는 function 키워드 대신 화살표(⇒, fat arrow)를 사용해 기존의 함수 정의 방식보다 간략하게 함수 정의 가능(내부 동작도 기존 함수보다 간략)
- 특히 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로서 유용

### 26.3.2 화살표 함수와 일반 함수의 차이

- 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor
    
    → 인스턴스 생성이 불가능하므로 prototype 프로퍼티가 없고 프로토타입도 미생성
    
- 중복된 매개변수 이름 선언 불가능
    
    → 일반함수는 중복된 매개변수 이름 선언시 에러 발생하지 않음
    
- 화살표 함수는 함수  자체의 this, arguments, super, [new.target](http://new.target) 바인딩을 갖지 않음
    
    → 화살표 함수  내부에서 this, arguments, super, [new.target](http://new.target) 참조시 스콬프 체인을 통해 상위 스코프의 arguments, super, [new.target](http://new.target)를 참조함
    

### 26.3.3 this

- 화살표 함수의 this는 일반 함수의 this와 다르게 동작
    
    → 콜백 함수 내부의 this문제(콜백 함수 내부의 this가 외부 함수의 this와 다르기 때문에 발생하는 문제)를 해결하기 위해 의도적으로 설계된 것
    
- **화살표 함수는 함수 자체의 this 바인딩을 갖지 않음 → 화살표 함수 내부에서 thisㄹㄹ참조하면 상위 스코프의 this를 그대로 참조. 이게 바로 `lexical this`**
- 위와 같은 이유로 Function.prototype.call, Function.prototype.apply, Function.prototype.bind 메서드를 사용해도 화살표 함수 내부의 this 교체 불가능(메서드는 호출이 가능하나 this 교체가 불가능)
- ES6가 아닌 일반적인 의미의 메서드를 화살표 함수로  정의하는 것은 피해야함
    
    ```jsx
    // bad
    const person = {
    	name: 'Park',
    	sayHi: () => console.log(`Hi ${name}`}
    };
    person.sayHi(); // Hi
    // sayHi 프로퍼티에 할당된  화살표 함수 내부의 this는 상위 스코프인 전역 this가 가리키는
    // 전역 객체를 가리키므로 이 예제를 브라우저에서 실행하면 this.name은 빈 문자열을 갖는 window.name과 같음
    // 전역 객체 window에는 빌트인 프로퍼티 name이 존재
    ```
    

### 26.3.4 super

- 화살표 함수는 함수 자체의 super 바인딩을 갖지 않음 → 화살표 함수 내부에서 super 참조시 this와 마찬가지로 상위스코프의 super를 참조

### 26.3.5 arguments

- 화살표 함수는 함수 자체의 arguments 바인딩을 갖지 않음 → 화살표 함수 내부에서 arguments 참조시 this와 마찬가지로 상위스코프의 arguments 를 참조

## 26.4 Rest 파라미터

### 262.4.1 기본문법

- Rest 파라미터(나머지 매개변수)는 매개변수 이름 앞에 세개의 점 … 을 붙여서 정의한 매개변수를 의미
- **Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받음**

# 💭느낀점

자바스크립트 클래스를 이렇게 깊이있게 공부한 경험이 있었던가…하고 돌이켜보니 제대로 공부해본적이 없는 것 같다ㅎㅎ;; 
클래스를 실제로 사용해 본적도 많지 않고…클래스하면 딱 떠오르는 것이 자바의 클래스라 자바스크립트의 클래스는 뭔가 어색한 느낌이다.

그래서인지 이번 챕터는 읽기가 어려웠다 😭 나중에 시간을 내어 다시 보는걸로..!
