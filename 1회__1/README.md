# 1-1. JavaScript Now

> 본 문서는 [코드스피츠 85](https://www.youtube.com/watch?v=0NsJsBdYVHI&list=PLBNdLLaRx_rImvbuZnfO-Ecv9OpuCNoCl) 의 내용을 바탕으로 작성되었습니다.

**목차**

1. [JavaScript Pipeline](#javascript-pipeline)
2. [ECMAScript Standard](#ecmascript-standard)
3. [ECMAScript 6](#ecmascript-6)
4. [ECMAScript 7](#ecmascript-7)
5. [ECMAScript 8](#ecmascript-8)
6. [ECMAScript 9](#ecmascript-9)
7. [Stage 3(ES11)](#stage-3es11)

## TL;DR

- 현대 자바스크립트를 대하는 방법과 ECMAScript 에 대해여 알아봅시다.
- ECMAScript 가 버전업이 되는 과정과 ES6 이후(~ES10) 표준이 된 스펙들 중 일부를 확인합니다.

# JavaScript Pipeline

ECMAScript 를 알아보기 이전에 현재 JavaScript 는 어떠한 처리 과정을 통해 출력되는 지 알아보겠습니다.

![JavaScript Pipeline](./img/Image001.png)

1. **Code**
   - 코드 작성.
   - ES3.1 ~ 5, 6 ~ | TypeScript | Kotlin | Dart | CoffeScript | ...
2. **Transpiler**
   1. 언어에 따라 컴파일을 수행.
      - TypeScript - tsc | Kotlin - kotlinc
   2. 작성한 코드를 JavaScript 로 번역. (babel)
3. **Packaging** : 최적화 과정 수행. (webpack)
4. **CI** : 테스트 등...
5. **Deploy** : 최종 배포.

기기 및 언어 호환성이나 코드 최적화는 Transpiler 와 Packaging 에서 책임지고 있습니다.
이러한 인프라를 바탕으로 우리는 상기의 문제에서 벗어나, 좀 더 좋은 코드를 작성하는것에 집중할 수 있습니다.

# ECMAScript Standard

1. 매년 상반기 새로운 버전을 출시.
   - 버전과 연도가 1 차이 (ES6 = ES2015).
   - (2019년 10월 기준) 현재 ES11 (ES2020)이 최종 조정중.
2. ES6 이후 급격한 변경을 지양하고 점진적인 버전업 진행.
   - 새롭게 반영될 사항은 Stage 0 ~ 3 까지의 단계별 승격을 거쳐, 정식 반영시 Stage 4 가 됨.
   - 최초 발제 시 Stage 0 에 등재되며 위원회의 회의를 통해 승격.
   - [현재 제안 중인 내용](https://github.com/tc39/proposals)
3. 그러나...
   - 승격은 c39 위원회에서 회의를 통해 결정되며, 각 제안의 담당자(챔피온)는 구글 관련 개발자가 많음.
   - Stage 4 기준 보다 구글이 원하는 순서대로 크롬에 빨리 반영되는 경우가 많음.

따라서 우리는 [크롬 업데이트](https://developers.goole.com/web/updates/capabilities) 문서 역시 확인해야할 필요가 있습니다.

# ECMAScript 6

- **Class**, Object Literal, getter, setter, ...
- Arrow
- **Iterator**, **Generator(Coroutine)**, **For of**
- const, let
- destructuring, rest, spread
- Template String
- (내장객체; Class Library)
  - Symbol, Promise, Map, Set, WeakMap, WeakSet, Proxy, Reflect

> **cf\_\_1) ES6 의 Class 는 설탕문법?**
>
> - ES5 : 생성자 함수, prototype 등을 사용하여 해당 객체와 연결.
> - ES6 : 연결된 생성자 객체 중 최상단의 생성자 객체를 생성.
>   - 이로 인해 함수나 배열을 상속받는 class 를 생성 가능.
> - 객체를 생성하는 근본적인 방식에서부터 사용하는 방식까지 ES5 와 다르다.
>   - [ES6 Class는 단지 prototype 상속의 문법설탕일 뿐인가?](https://gomugom.github.io/is-class-only-a-syntactic-sugar/)
>   - [JavaScript Classes, Inheritance, and Prototype Chaining (ES5 and ES6 Way)](https://medium.com/javascript-in-plain-english/javascript-classes-inheritance-and-prototype-chaining-es5-and-es6-way-4b8e9416702b)

# ECMAScript 7

- 중첩된 rest 해체

```javascript
const [a, …[b, …c] = [1, 2, 3, 4] // (a = 1, b = 2, c = [3, 4]
```

# ECMAScript 8

- **async / await**
- **shared memory**
- **atomics**

> **cf\_\_2) shared memory 와 atimics 의 등장배경**
>
> 1. JavaScript 는 worker thread pattern 에 기반한 web worker 를 통하여 멀티 쓰레드 환경에 대응
> 2. 허나 각 쓰레드간 새로운 객체를 생성해서 복제되기 때문에 처리가 느린 것이 단점
> 3. 이를 해결하기 위해...
>    - 메인 쓰레드와 데이터 공유를 위한 바이너리 데이터 버퍼인 [SharedArrayBuffer 객체](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) 등장
>    - 이와 동시에 동시성 문제를 해결하기 위해 [Atomics 객체](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics) 사용

# ECMAScript 9

- object 해체
- **asynchronous iterators**
  - generator의 장점과 async/await의 장점을 결합
  - 비동기적인 coroutine 을 만들 수 있는 구조를 제공

# ECMAScript 10

- optional catch

```javascript
try {
} catch {
  // 불필요한 error 인자 생략
}
```

# Stage 3(ES11)

- BigInt
- globalThis
- **top level await**
- class field
- private field | private method
  - `#` 을 선언해서 사용
- optional chaining
  - `?.` 을 사용
  - 객체 프로퍼티 값이 `null | undefined` 이라면 `undefined` 를 반환
- nullish coalescing
  - `??` 을 사용
  - 좌측 값이 `null | undefined` 이라면 우측 값 반환
- WeakReference

---

**참고자료**

1. [ES6 Class는 단지 prototype 상속의 문법설탕일 뿐인가?](https://gomugom.github.io/is-class-only-a-syntactic-sugar/)
2. [JavaScript Classes, Inheritance, and Prototype Chaining (ES5 and ES6 Way)](https://medium.com/javascript-in-plain-english/javascript-classes-inheritance-and-prototype-chaining-es5-and-es6-way-4b8e9416702b)
3. [2017년과 이후 JavaScript의 동향 - JavaScript(ECMAScript)](https://d2.naver.com/helloworld/2809766)
4. [2018년과 이후 JavaScript의 동향 - JavaScript(ECMAScript)](https://d2.naver.com/helloworld/7495331)
5. [2019년과 이후 JavaScript의 동향 - JavaScript(ECMAScript)](https://d2.naver.com/helloworld/4007447)
