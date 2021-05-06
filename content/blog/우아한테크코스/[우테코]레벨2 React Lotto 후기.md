---
title: '[우테코]레벨2 React Lotto 후기'
date: 2021-05-06
category: '우아한 테크코스'
draft: true
---

<p align="middle" >
  <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/javascript-lotto/main/src/images/lotto_ball.png"/>
</p>
<h2 align="middle">Level2 - 행운의 로또</h2>
<p align="middle">React 로또 어플리케이션</p>
</p>

## 📝 구현 요구사항

### 🚀 Step1

- [x] `Class Component`를 사용합니다.
- [x] 로또 구입 금액을 입력하면, 금액에 해당하는 로또를 발급해야 한다.
- [x] 로또 1장의 가격은 1,000원이다.
- [x] 소비자는 **자동 구매**만 할 수 있다.
- [x] 복권 번호는 번호보기 토글 버튼을 클릭하면, 볼 수 있어야 한다.
- [x] 결과 확인하기 버튼을 누르면 당첨 통계, 수익률을 모달로 확인할 수 있다.
- [x] 로또 당첨 금액은 고정되어 있는 것으로 가정한다.
- [x] 다시 시작하기 버튼을 누르면 초기화 되서 다시 구매를 시작할 수 있다.

### 🚀🚀 Step2

- [x] Step1의 Class Component를 Function Component로 마이그레이션 합니다.

## 1. 진행하며 고민한 점

### 1-1. CSS 라이브러리(Tailwind)

레벨 1에서 Vanilla Javascript로 미션을 수행할 때는 CSS에 대한 고민을 크게 하지 않았습니다. 미션들의 기본 UI가 짜여진 템플릿이 주어졌고 추가적으로 구현하는 UI는 제공 받은 템플릿을 바탕으로 간단하게 작성할 수 있었습니다.

그러나, 레벨 2부터는 모든 UI를 직접 작성하면서 과제를 수행해야 했습니다. 프론트엔드 진영에서 인기 있게 사용되는 라이브러리들이 있었고 어떤 라이브러리를 사용해서 CSS 스타일을 적용할지에 대한 고민이 많았습니다. 크게는 CSS in CSS(?)를 적용할지 CSS in JS를 적용할지부터 작게는 SCSS, Styled Component, Emotion, Tailwind CSS 등 여러 라이브러리들을 놓고 페어와 많은 고민을 했습니다.

결론적으로 선택한 라이브러리는 Tailwind였습니다. 다른 선택지와 비교했을 때 다음과 같은 장점들로 TailWind를 선택했습니다.

1. 스타일 적용을 위한 클래스 이름을 고민하지 않아도 된다.
   - Vanilla Javascript를 사용할 때 스타일을 위해 특정 클래스이름을 짓는 것은 시간을 꽤나 잡아먹는 일이었습니다.
   - Tailwind를 통해 이런 고민의 시간을 없앨 수 있었습니다.
2. 사용하는 곳과 스타일을 정의하는 곳이 바로 붙어있다.
   - Styled Component 같은 라이브러리와 비교헀을 때 큰 장점이라고 생각했던 부분입니다.
   - 해당 스타일을 적용하는 곳에 직접적으로 적용할 수 있어 어떤 스타일이 적용되고 있는지 한눈에 파악할 수 있어 좋았습니다.

- [Tailwind CSS 링크](https://tailwindcss.com/)

하지만 Tailwind를 적용하면서 다음과 같은 몇가지 단점을 느끼기도 했습니다.

1. 클래스명에 익숙해지기 위한 시간이 필요하다.
   - Tailwind에서는 Utility-First 컨셉을 통해 클래스명으로 스타일을 적용하고 있습니다.
   - ex) `<div mx-5 p-10></div>`
   - 기존 CSS를 축약해놓은 네이밍인데 대부분은 예상이 가능하지만(mt = margin top) 자주 사용하지 않는 Style의 경우 Tailwind 공식 홈페이지에서 매번 찾아가면서 사용했습니다.
   - 이 글을 보면서 Tailwind를 처음 적용하시려는 분들은 아래의 IntelliSense를 통해 시행착오를 조금이라도 줄이셨으면 좋겠습니다!
   - [Tailwind IntelliSense 링크](https://tailwindcss.com/docs/intellisense)
2. 복잡한 스타일을 적용할 때 클래스 이름이 굉장히 길어질 수 있다.
   - 클래스명을 통해 Style을 적용하다보니 Style을 많이 적용할 경우 클래스명이 길어져 조금은 지저분해 보일 수도 있는 코드가 나왔습니다. 아래는 실제로 사용한 코드입니다.
   ```js
   ;`<input className={'bg-gray-250 text-green-350 h-10 w-full text-left outline-none focus:border border-gray-400 rounded'}/>`
   ```
   - 클래스 이름이 길어질 경우 Prettier 플러그인을 활용해보시는 것도 추천드립니다!
   - [Prettier Plugin Tailwind](https://www.npmjs.com/package/prettier-plugin-tailwind)
3. 구체적인 스타일을 적용할 때 config에 추가해줄 일들이 생긴다.

   - Tailwind는 기본으로 제공하는 스타일 외에도 extends에 원하는 스타일을 정의하는 방식으로 확장해서 사용이 가능합니다.
   - 예를 들어 기본으로 제공되는 색깔 이외에 원하는 색깔을 Tailwind 스타일로 사용하기 위해서는 다음과 같은 작업이 필요합니다.

   ```js
   // tailwind.config.js
   module.exports = {
     extend: {
       colors: {
         gray: {
           150: '#e5e5e5',
           250: '#ECEBF1',
           350: '#d3d3d3',
         },
       },
     },
   }
   ```

   - CSS를 사용할 때 원하는 색의 RGB값을 적용해 바로 사용하는 것을 생각하면 조금은 번거롭게 느껴질 수도 있습니다.
   - 자주 사용하는 색의 경우 Styled Component를 사용하더라도 상수화해서 사용하기 때문에 큰 단점이라고 생각하지는 않습니다.
   - 하지만 다른 라이브러리의 경우 '선택사항'일 수 있는 부분이 Tailwind에서는 약간은 강제되는 모습이라 단점목록에 추가했습니다.

#### 결론

Tailwind를 사용해 Style을 적용했고 만족하면서 사용했습니다. 후에 프로젝트를 한다면 우선적으로 Tailwind 적용을 고민할거 같습니다.

### 1-2. CRA없이 React Boilerplate 만들기

정말 오랜만에 React를 접하게 됐습니다. React에 대해서는 정말 얕디 얕은 지식만 있었고 이전에 React를 사용할 당시에는 CRA 이외의 방법을 한번도 고민해보지 않았습니다. 하지만 지난 레벨 1미션들을 진행하면서 Webpack, Babel, eslint 등의 도구들에 익숙해진 상태였기 때문에 CRA없이 React Boilerplate를 만들어보기로 결정했습니다.

CRA없이 React를 빌드하면서 Webpack, Babel 세팅 등에서 시행착오를 겪기도 했지만 결과적으로 큰 어려움없이 React Boilerplate를 완성시킬 수 있었습니다.

이 과정에서 Webpack Loader, Plugin 뿐만 아니라 Babel 설정, eslint 설정까지 여러가지로 건드려보면서 기존에 사용하던 도구들에 대한 이해도를 높일 수 있었습니다.

아래는 Boilerplate를 만든 후의 `package.json`파일입니다.

```json
{
  "devDependencies": {
    "@babel/core": "^7.13.15",
    "@babel/eslint-parser": "^7.13.14",
    "@babel/eslint-plugin": "^7.13.15",
    "@babel/preset-env": "^7.13.15",
    "@babel/preset-react": "^7.13.13",
    "@pmmmwh/react-refresh-webpack-plugin": "^0.4.3",
    "@tailwindcss/postcss7-compat": "^2.1.0",
    "autoprefixer": "^9",
    "babel-loader": "^8.2.2",
    "css-loader": "^5.2.1",
    "eslint": ">=6.0.1",
    "eslint-config-prettier": "^8.2.0",
    "eslint-config-semistandard": "15.0.1",
    "eslint-config-standard": ">=14.1.0",
    "eslint-config-standard-jsx": "^10.0.0",
    "eslint-config-standard-react": "^11.0.1",
    "eslint-plugin-import": ">=2.18.0",
    "eslint-plugin-jsx-a11y": "^6.4.1",
    "eslint-plugin-node": ">=9.1.0",
    "eslint-plugin-promise": ">=4.2.1",
    "eslint-plugin-react": "^7.23.2",
    "eslint-plugin-standard": ">=4.0.0",
    "html-webpack-plugin": "^5.3.1",
    "husky": ">=6",
    "lint-staged": ">=10",
    "mini-css-extract-plugin": "^1.4.1",
    "postcss": "^7",
    "postcss-loader": "^5.2.0",
    "prettier": "2.2.1",
    "react-refresh": "^0.10.0",
    "tailwindcss": "npm:@tailwindcss/postcss7-compat",
    "webpack": "^5.32.0",
    "webpack-cli": "^4.6.0",
    "webpack-dev-server": "^3.11.2"
  },
  "dependencies": {
    "prop-types": "^15.7.2",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "tailwind": "^4.0.0"
  }
}
```

webpack, babel, eslint 등의 config가 궁금하시다면 아래의 링크를 통해 확인해보실 수 있습니다.

- [전체 코드 링크](https://github.com/yujo11/react-lotto/tree/step1)

## 2. 코드 리뷰 및 피드백

## 3. 링크

### 3-1. step1 링크

- [전체 코드 링크](https://github.com/yujo11/react-lotto/tree/step1)
- [PR 링크](https://github.com/woowacourse/react-lotto/pull/22)

### 3-2. step2 링크

- [전체 코드 링크](https://github.com/yujo11/react-lotto/tree/step2)
- [PR 링크](https://github.com/woowacourse/react-lotto/pull/57)
