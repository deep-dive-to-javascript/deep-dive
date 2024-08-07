# Morden JavaScript Deep Dive

Dasom, 2024.07.07

※ 메서드는 자주 사용하거나 특이점이 있는 것 위주로 정리함

## 27장 배열

> 배열은 객체이지만, 객체와 구별되는 특징이 존재한다.
>
> 즉, 자바스크립트 배열은 배열이 아니다.

### 자바스크립트의 배열은 배열이 아니다

* 자료구조의 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말함 (밀집 배열)
  * 따라서, 자바스크립트 배열은 인덱스로 배열 요소에 접근하는 경우, 일반적인 배열보다 느림
  * 하지만 배열 요소를 삽입 또는 삭제하는 경우 성능이 더 빠름



### length 프로퍼티와 희소 배열

* 현재 length 프로퍼티 값보다 작은 숫자 값을 할당하면 배열의 길이가 줄어듦

  ```js
  const arr  = [1, 2, 3, 4, 5];
  arr.length = 2;
  console.log(arr); //[1, 2]
  ```

  * 단, 더 큰 숫자값을 할당한다고 배열의 길이가 늘어나지는 않음

* 희소배열

  ```js
  const sparse = [, 2, , 4];
  console.log(sparse.length) // 4
  
  // 배열 요소에는 인덱스가 0, 2인 요소가 존재하지 않음. 따라서 배열의 길이 !== 요소의 길이
  console.log(Object.getOwnPropertyDescriptors(sparse));
  /*
  {
  '1': {value: 2, ...중략},
  '3': {value: 4, ...중략},
  length: {value: 4, ...중략}
  }
  */
  ```



### 배열 메서드

**포함 여부** 

* indexof
  * 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환
* includes
  * 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환

* some
  * 배열에 특정 조건을 만족하는 요소가 하나라도 참이면 true를 반환
* find
  * 조건을 만족하는 첫 번째 요소를 반환

> 성능의 차이
>
> 모두 배열에서 해당하는 요소를 찾았을 때 탐색을 중단하므로 성능차이는 미미함.
>
> 단순히 배열의 포함 여부만 검사할 때는 includes를 사용하는 것이 더 직관적일 수 있음.



**정렬**

* sort

  ```js
  // 자바스크립트의 정렬
  let mixedArr = [10, "banana", 5, "apple", 8, "cherry"];
  
  // 내림차순 정렬을 위한 비교 함수 제공
  mixedArr.sort((a, b) => {
    if (typeof a === "number" && typeof b === "number") {
      return b - a; // 숫자는 숫자끼리 비교
    } else if (typeof a === "string" && typeof b === "string") {
      return b.localeCompare(a); // 문자열은 문자열끼리 비교
    } else {
      return typeof a === "number" ? -1 : 1; // 숫자를 문자열보다 우선
    }
  ```

  > sort 메서드는 quicksort 알고리즘을 사용했었으나, 동일한 값의 요소가 중복되어 있을 때 초기 순서와 변경될 수 있는 문제가 존재해, ES10 이후부터 timsort 알고리즘을 사용하도록 바뀜



**배열 순회**

* foreach 
  * 원본 배열을 변경하지 않음
  * 반환 값은 언제나 undefined

* map
  * 원본 배열을 변경하지 않음
  * 콜백 함수의 반환값들로 구성된 새로운 배열을 반환

```js
// Q. 배열을 순회하며 컴포넌트를 렌더링 할 때, map과 foreach 중 어떤 것을 사용하시나요?
const Component = () => {
 const arr = [1, 2, 3];

  return(
    arr.map((item) => 
			<p>{item}</p>       
		)
)}
```



## 28장 Number

### Number 메서드

* toExponential

  * 숫자를 지수 표기법으로 변환하여 문자열로 반환

  > 지수 표기법이란?
  >
  > e앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 나타내는 방식
  >
  > 매우 크거나 작은 숫자를 표기할 때 주로 사용



## 29장 Math

### Math 프로퍼티

* Math.PI: 원주율
* Math.abs: 절대값
* Math.round: 반올림
* Math.ceil: 올림
* Math.floor: 내림
* Math.sqrt: 제곱근
* Math.random: 임의의 난수
* Math.pow(a, b): a의 b제곱
* Math.max
* Math.min



## 30장 Date

Date 생성자 함수로 생성한 Date 객체는 기본적으로 현재 날짜와 시간을 나타내는 정수값을 가짐

```js
const date = new Date()
console.log(date) // Sun Jul 07 2024 18:07:46 GMT+0900 (한국 표준시)
```



### Date 메서드

* getDay
  * 요일을 0~6까지의 정수로 표기해 반환함 (cf. 일요일: 0)
* toISOString
  * ISO 8601형식으로 날짜와 시간을 표현한 문자열을 반환

* toLocaleString
  * locale을 기준으로 날짜와 시간을 표현한 문자열을 반환

```js
console.log(date.toString()) // Sun Jul 07 2024 18:07:46 GMT+0900 (한국 표준시)
console.log(date.toISOString()) //2024-07-07T09:07:46.744Z
console.log(date.toLocaleString()) //2024. 7. 7. 오후 6:07:46

```



**서버에 저장하는 date 형식에 대해** (with Chat GPT)

1. `toString()`

   - 설명: `Date` 객체를 사람이 읽을 수 있는 문자열로 변환합니다.

   - 예시: `"Wed Jul 07 2024 14:48:00 GMT+0900 (Korean Standard Time)"`

   - 장점: 사람이 읽기 쉽다.

   - 단점: 표준화된 형식이 아니며, 타임존 정보가 명확하지 않아 일관성이 떨어진다.

2. `toLocaleString()`

   - 설명: 로컬 시간대와 로컬 형식을 사용하여 `Date` 객체를 문자열로 변환합니다.

   - 예시: `"7/7/2024, 2:48:00 PM"`

   - 장점: 로컬 시간대에 맞춰 출력되어 가독성이 좋다.

   - 단점: 로컬 설정에 따라 형식이 달라져 일관성이 없다.

3. `toISOString()`

   - 설명: `Date` 객체를 ISO 8601 형식의 문자열로 변환합니다.

   - 예시: `"2024-07-07T05:48:00.000Z"`

   - 장점: **표준화된 형식**으로, 타임존이 UTC로 고정되어 있어 일관성이 높다.

   - 단점: 사람이 읽기에는 불편할 수 있다.

4. `date.getTime()` (혹은 `date.valueOf()`)

   - 설명: `Date` 객체를 유닉스 타임스탬프로 변환합니다. (1970년 1월 1일 00:00:00 UTC 이후의 밀리초 수)

   - 예시: `1725590880000`

   - 장점: 숫자 형식으로 저장되어 비교 및 계산이 용이하다.

   - 단점: 사람이 읽기 어렵다.

5. `Date` 객체 그대로 저장

   - 설명: 자바스크립트의 `Date` 객체를 직접 저장합니다.

   - 장점: 자바스크립트 환경에서는 직관적이다.

   - 단점: **대부분의 데이터베이스가 `Date` 객체를 직접 저장할 수 없으므로** 문자열이나 숫자로 변환이 필요하다.

🧑🏻‍🔧 **추천 방법**: `toISOString()`

ISO 8601 형식은 표준화되어 있으며, 타임존을 UTC로 고정하기 때문에 시간대 차이에 따른 문제가 없기 때문



## 31장 RegExp

> 정규 표현식이란,
>
> 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어

* 정규표현식 리터럴

  * /: 시작, 종료 기호
  * // 사이에 패턴
  * 마지막 플래그 작성

  ```js
  // 정규표현식 예시
  // 패턴: is
  // 플래그: i (대소문자를 구별하지 않고 검색)
  const regexp = /is/i;
  ```

* 정규표현식 생성자 함수

  ```js
  /**
  * pattern
  * flages: 플래그 (g, i, m, u, y)
  */
  new Regexp(pattern[, flags])
  // 예시
  const regexp = new RegExp(/is/i);
  ```



### RegExp 메서드

* exec: 패턴을 검색하여 매칭 결과를 배열로 반환, 없으면 null
* **test**: 패턴을 검색하여 매칭 결과를 불리언 값으로 반환
* match: 대상 문자열과 정규 표현식의 매칭 결과를 배열로 반환



### 플래그

* i: 대소문자 구별X
* g: 모든 문자열 전역 검색
* m: 행이 바뀌더라도 계속 검색

-> 전체 문자열에서 대소문자를 구분하지 않고 모든 일치 항목을 찾으려면 `g`와 `i` 플래그를 함께 사용할 수 있음



### 자주 사용하는 정규 표현식

* 메일 주소 형식 검사

  `const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;`

* 비밀번호 조건 검사 (대소문자 1개 이상, 특수문자 1개 이상, 영어로만 작성)

  `const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[!@#$%^&*])[a-zA-Z!@#$%^&*]{8,}$/;`

* 핸드폰 번호 형식 검사

  `const phoneRegex = /^01[016789]-?\d{3,4}-?\d{4}$/;`



## 32장 String

### String 메서드

* trim: 문자열 앞 뒤 공백 제거





## 느낀점

배열나 문자열에서 포함 여부를 검색하는 코드를 짤 일이 많았는데, 그때마다 어떤 메서드를 쓰는 게 가장 빠르고 적합한가의 기준이 안 섰던 경험이 있다. 이번 기회를 통해 메서드의 보다 명확한 취지를 알게 된 것 같아 좋고, 혼용해서 사용하고 있던 기존 방식을 개선해야함을 다시 한 번 생각하게 되었다.

그리고 Date의 경우, ERD에 Date 형식이라고 되어있길래 막연히 Date 형식을 지원하는구나 라고 생각했는데, Date 객체를 직접 저장할 수 없다는 사실이 신기했다. 데이터 "타입"에 대해 합의를 본다고 해도 명확하게 정하지 않으면 각자가 생각하는 모양이 다를 수 있다는 걸 주의해야겠다.

cf. 실제로, 최근에 개발을 진행하면서 어떤 건 UTC타입으로 전달되고 어떤 건 new Date에서 생성되는 타입으로 전달이 되어서 api 에러가 발생했었는데, 아 그래서 그랬구나 하는 것을 알게 되었다. (왜냐면 프론트 로직에서는 문제 없이 동작했기 때문에... )



