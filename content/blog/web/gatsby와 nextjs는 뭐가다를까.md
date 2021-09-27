---
title: 'Gatsby.js와 Next.js 간단 비교'
date: 2021-09-22 09:03:18
category: 'web'
draft: false
---

## 0. Gatsby.js와 Next.js

블로그를 만들기 위해 사용할 툴을 찾아보던 중 Gatsby와 Next를 두고 고민에 빠졌다.

두 프레임워크 모두 튜토리얼을 진행하면서 닮은 듯 다른 두 프레임워크의 차이점을 정리하기 위해 글을 작성해 보기로 했다.

## 1. Gatsby.js

### 1-1. Gatsby 소개

> Gatsby is a React-based open-source framework for creating websites and apps. - Gatsby.js 공식 문서

Gastby.js는 정적으로 HTML을 생성하는 웹 사이트를 구축하는 데 사용되는 React 프레임워크입니다.

React, GraphQl, react-router등을 결합하여 개발자가 직접 `webpack` 등의 개발환경을 설정할 필요없이 빠르게 웹 사이트를 구축하는데 도움을 줍니다.

Gatsby는 페이지 수를 예측할 수 있고 콘텐츠가 대부분 정적으로 유지되는 사이트를 구축하는데 주로 사용됩니다.(블로그, 포트폴리오 사이트 등)

### 1-2. Gatsby 장점

공식 문서에 있는 내용들을 가져왔습니다.

1. GraphQL을 기반으로 구축된 데이터 계층

   - 다른 소스의 데이터를 쉽게 결합하고 함께 렌더링할 수 있게 해준다.

2. 속도

   - 정적 페이지 생성과 지능형 페이지 렌더링을 결합하여 중요한 컨텐츠만 선택적으로 미리 로드하여 빠른 웹사이트를 제공한다.

3. 개발자 친화적

   - Javascript, Git, CI/CD 등과 같은 도구와 웹 기술들이 결합 된 Gatsby는 유지 관리 및 최적화에 드는 개발자의 시간을 줄여준다.

4. 방대한 생태계

   - 다양한 테마, 플러그인, 스타터가 존재하며, 이를 사용하여 간단하게 웹사이트를 구축할 수 있다.(ex. gatsby-starter-bee)

## 2. Next.js

### 2-1. Next.js 소개

> Next.js gives you the best developer experience with all the features you need for production: hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. No config needed. - Next.js 공식 문서

Next.js는 SSR를 구축하는데 사용됩니다. 그러면서도 정적 페이지 생성, CDN 캐싱 등 정적 페이지 생성에서 활용할 수 있는 모든 이점들을 지원합니다.

일반적으로 Next는 SSR과 정적 페이지 최적화를 모두 지원하는 사이트가 필요한 경우 사용됩니다.

### 2-2. Next.js 장점

공식 문서의 내용들을 가져왔습니다.

1. 이미지 최적화

   - 빌드 시 이미지를 자동으로 최적화 해줍니다. (`next/image`)

2. zero config

   - 자동 컴파일 및 번들링, 핫 리로드 등 Next.js에서 제공하는 기능은 좋은 개발자 경험을 얻을 수 있게 해줍니다.

3. 정적 페이지 생성

   - SSR 이외에도 정적 페이지 생성을 완벽하게 지원합니다.

## 3. 차이점

1. Next.js는 배포하기 위해 서버가 필요하지만(SSR을 사용하는 경우) Gatsby는 서버가 없어도 실행할 수 있다.
2. Next.js는 런타임에서 HTML/JS/CSS를 생성할 수 있지만 Gatsby는 빌드시에만 HTML/JS/CSS를 생성한다.

## 4. 어떤 것을 선택해야 할까?

### 4-1. Next.js를 사용할 때

콘텐츠가 많거나 시간이 지남에 따라 콘텐츠가 증가할 것으로 예상되는 경우 SSG는 최선의 선택이 아니다. 콘텐츠가 많아지면 사이트를 구축하는 데 시간이 많기 걸리기 때문이다.

따라서 시간이 지남에 따라 콘텐츠가 많아질 것으로 예상되는 사이트를 구축할 때는 SSR을 사용하는 것이 좋을거 같다.

### 4-2. Gatsby를 사용할 때

소규모 웹사이트와 블로그를 구축하면서 페이지의 수를 예상할 수 있다면 Gatsby를 사용하는 것이 좋을거 같다. Gatsby는 많은 스타터 템플릿과 테마, 플러그인을 가지고 있어 빠르게 개발이 가능하다.

## 참고자료

- [Next.js 공식 문서](https://nextjs.org/)
- [Gatsby 공식 문서](https://www.gatsbyjs.com/)
  - [Gatsby vs Next](https://www.gatsbyjs.com/features/jamstack/gatsby-vs-nextjs)
