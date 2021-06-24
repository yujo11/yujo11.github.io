---
title: '[우테코]레벨2 학습로그'
date: 2021-06-22
category: '우아한 테크코스'
draft: true
---

![](./images/woowa.png)

### 1. Virtual DOM

- DOM(Document Object Model - 문서 객체 모델)

  - DOM은 웹 페이지에 대한 인터페이스다. 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 문서 구조, 스타일, 내용을 변경할 수 있게 돕는다.

- VDOM(Virtual DOM)

  - Virtual DOM (VDOM)은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념. 이 과정을 재조정이라고 한다.
  - 이 접근방식이 React의 선언적 API를 가능하게 한다. React에게 원하는 UI의 상태를 알려주면 DOM이 그 상태와 일치하도록 한다.

* Diffing Alogorithm

  - Virtual DOM이 업데이트 되면, React는 Virtual DOM을 업데이트 이전의 Virtual DOM 스냅샷과 비교하여 정확히 어떤 Virtual DOM이 바뀌었는지 검사한다.
  - 두 개의 트리를 비교할 때, React는 두 엘리먼트의 루트(root) 엘리먼트부터 비교합니다. 이후의 동작은 루트 엘리먼트의 타입에 따라 달라집니다.

- Virtual DOM은 항상 빠를까? NO

  - 유저 인터랙션이 발생하지 않는 페이지에서는 일반 DOM의 성능이 더 좋을 수 있다. -> SPA로 제작된 큰 규모의 웹 페이지에서는 Virtual DOM을 사용해서 브라우저의 연산을 줄여 성능을 개선할 수 있다.
  - Dan 트위터
    ![](./images/study-log/dan-tweet.png)

- 참고 문서
  - [Virtual DOM and Internals / React 공식 문서 ](https://reactjs.org/docs/faq-internals.html)
  - [Introduction to the DOM / MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
  - [문서 객체 모델(Document Object Model) / poiemaweb](https://poiemaweb.com/js-dom)
  - [[10분 테코톡]지그의 Virtual DOM / Youtube](https://www.youtube.com/watch?v=PN_WmsgbQCo)
  - [React and the Virtual DOM / Youtube](https://www.youtube.com/watch?v=BYbgopx44vo)

### 2. JSX

- JSX란?

  - JSX는 Javascript 언어 구문의 확장.

- JSX는 표현식이다.

  - JSX를 컴파일하면 JSX 표현식이 자바스크립트의 함수를 호출한다.
  - 따라서 if나 for 문 내에 JSX를 사용할 수 있고, 변수에 할당하거나 매개 변수로 전달하는 것 또한 가능하다.

  ```jsx
  const sayHello = name => {
    if (name) {
      return <h1>hello {name}!</h1>
    }

    return <h1>hello</h1>
  }
  ```

- JSX의 변환 과정

  1. JSX 코드

  ```jsx
  const element = <h1 className="greeting">Hello, world!</h1>
  ```

  2. React.createElement로 변환

  ```jsx
  const element = React.createElement(
    'h1',
    { className: 'greeting' },
    'Hello, world!'
  )
  ```

  3. Object로 변환

  ```jsx
  const element = {
    type: 'h1',
    props: {
      className: 'greeting',
      children: 'Hello, world',
    },
  }
  ```

* React에서는 반드시 JSX를 사용해야 하는가? NO

  - React는 JSX 사용을 필수로 하지 않는다. 하지만 자바스크립트 코드 내부의 UI로 작업할 때 시각적으로 더 도움된다고 생각한다.
  - 또한, React가 도움이 되는 에러 및 경고 메세지를 표시해준다.

* 참고 문서
  - [JSX 이해하기 / React 공식 문서](https://ko.reactjs.org/docs/jsx-in-depth.html)

### 3. Component

- Component란?

  - 최신 사용자 인터페이스는 복잡핟. 하나의 거대한 UI는 깨지기 쉽고 디버깅 또한 어렵다. 이를 모듈 식으로 분리하면 더욱 강력하고 유연한 UI를 쉽게 구현할 수 있다.
  - React는 Component를 통해 UI를 재사용 가능한 여러 조각으로 나눈다.

- Class Component, Function Component

  - 클래스 컴포넌트는 인스턴스를 생성하고 유지된다.
  - 함수 컴포넌트는 render될 때마다 호출된다.
  - 따라서 상태관리에서 클래스 컴포넌트가 이점이 있었으나 Hooks가 등장하면서 함수 컴포넌트에서도 클래스 컴포넌트의 생명주기를 따라할 수 있게 되었다.
  - 함수 컴포넌트는 클래스 컴포넌트에 비해 코드양이 줄어들고 구현 및 사용이 간단하다는 이점이 있다.

* 참고 문서
  - [Components and Props](https://ko.reactjs.org/docs/components-and-props.html#gatsby-focus-wrapper)
  - [How Are Function Components Different from Classes?](https://overreacted.io/how-are-function-components-different-from-classes/)
  - [웹 컴포넌트 / MDN](https://developer.mozilla.org/ko/docs/Web/Web_Components)
  - [탄력적인 컴포넌트 작성하기 / overreacted](https://overreacted.io/ko/writing-resilient-components/)

### 4. CDD(Component Driven Development)

- CDD란?

  - Component를 중심으로 개발하는 방법론. Bottom Up 방식으로 UI를 구축한다.
    - ex) Input Component + Button Component => Sign Up Page

- StoryBook

  - UI 개발을 위한 도구
  - 컴포넌트를 분리하여 개발할 때 UI를 쉽게 Test할 수 있게 한다.

* 참고 문서
  - [Component-Driven Development / Chromatic Blog](https://www.chromatic.com/blog/component-driven-development/)
  - [airbnb date range picker storybook](https://airbnb.io/react-dates/?path=/story/daterangepicker-drp--default)

### 5. Controlled & Uncontrolled Component

- Controlled Component(제어 컴포넌트)

  - React에 값이 완전히 제어되는 Component(ex. Input, Textarea)
  - State를 값으로 넘기고 State를 다룰 수 있는 핸들러를 콜백으로 넘긴다.

- Uncontrolled Component(비제어 컴포넌트)
  - 전통적인 HTML처럼 DOM에 제어되는 Component(ex. Input, Textarea)
  - 오적 사용자의 값만 상호작용

### 6. Custom Hook (Custom Hook VS Util Function)

- Custom Hook의 장점

  - Component 로직을 함수로 뽑아내어 재사용할 수 있음.

- Custom Hook과 Util 함수의 차이

  - Custom Hook은 Component 내부에 존재해야 함.(상태를 이용)
  - Util은 Component 외부에 존재해도 상관이 없음.(상태를 이용하지 않음)

- 참고 문서
  - [자신만의 Hook 만들기 / React 공식 문서](https://ko.reactjs.org/docs/hooks-custom.html)

### 7. Context API

- 장점

  - Context를 이용하면 단계마다 일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있음.
  - 다양한 레벨에 네스팅 된 많은 컴포넌트에 데이터를 손쉽게 전달할 수 있음.

- 단점

  - 컴포넌트를 재사용하기 어려워진다.

- 참고 문서
  - [Context / React 공식 문서](https://ko.reactjs.org/docs/context.html)

### 8. Redux

- Redux의 특징

  - Store는 단 한개만 존재한다.
  - 상태를 직접 변경할 수 없다. 상태를 변경하기 위해서는 Action 객체를 전달하는 방법 밖에 없다.
  - Action 객체는 reducer에 의해 처리 된다. reducer는 반드시 순수 함수로 작성되어야 한다.
  - Store
    - Redux를 구성하는 여러가지 메서드 제공
    - 애플리케이션의 모든 상태는 하나의 Store 안에 하나의 객체 트리 구조로 저장
  - Action
    - 상태 변경에 대한 정보를 담고 있는 Object
    - 어떤 타입의 액션이 실행될지에 대한 type을 가져야 한다.
  - Reducer
    - 이전 상태와 Action을 받아 다음 상태를 반환하는 순수 함수.
    - API호출, 라우팅 전환 같은 사이드 이펙드를 발생시키면 안 된다
  - Dispatch
    - Application의 어디에서든 호출 가능
    - 상태 변경을 일으키기 위한 유일한 방법, Action을 발행한다.

- Redux의 장점
  - 단방향 데이터 흐름에 따라 오류 제어와 상태관리에 이점

### 9. Redux Thunk

- Redux Thunk 특징

  - 간단한 코드와 간단한 사용법

- Redux Thunk의 장점

  - Redux Thunk Code

  ```js
  function createThunkMiddleware(extraArgument) {
    return ({ dispatch, getState }) => next => action => {
      if (typeof action === 'function') {
        return action(dispatch, getState, extraArgument)
      }

      return next(action)
    }
  }
  const thunk = createThunkMiddleware()
  thunk.withExtraArgument = createThunkMiddleware

  export default thunk
  ```

  - 코드가 간단한만큼 사용이 간단하다.

### 10. Redux Toolkit

- Redux Toolkit 특징

  - Redux에서 공식적으로 추천하는 Redux를 사용하는 방법.

- Redux Toolkit의 장점

  - immer, thunk 등 Redux를 간단하게 사용할 수 있는 라이브러리들이 내장되어 있다.
