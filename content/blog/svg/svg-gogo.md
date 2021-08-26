---
title: 'SVG(Scalable Vector Graphics) 톺아보기'
date: 2021-08-21 09:03:18
category: 'svg'
draft: false
---

### 1. 서론

SVG는 벡터 기반의 XML 포맷을 가진 그래픽입니다.

벡터 파일 형식을 가지고 있기 때문에 모든 사이즈에서 깔끔하게 렌더링 되며, `CSS`, `DOM`, `JavaScript` 등 웹 표준과도 잘 동작하도록 설계 되었습니다.

> 백터 파일과 래스터 파일의 차이가 궁금하시면 아래 링크의 글을 참고하시면 좋을거 같습니다.1
>
> - [래스터 파일(JPG, PNG)와 벡터 파일(SVG)의 차이](https://yujo11.github.io/svg/raster-vector/)

### 2. SVG속성들

### 2-1. viewport & viewBox

- viewport

  - svg가 화면에 표시 될 영역을 정의합니다.
  - width, height로 결정됨
  - 도형이 viewport 영역을 넘어서면 화면에 나타나지 않고 잘림

- viewBox

  - svg를 그릴 영역을 정의합니다.
  - 도형요소의 좌표값은 viewBox를 기준으로 함
  - min-x min-y width height 순서로 작성
  - min-x min-y : 좌픅상단을 기준점으로 한 viewBox의 시작 좌표
  - width height : viewBox의 사이즈

- 아래 예시들을 보면 같은 크기의 `<circle />`이더라도 viewBox에 따라 다르게 표현되는걸 확인할 수 있습니다.

```xml
<svg viewBox="0 0 200 200" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>
```

<svg viewBox="0 0 200 200" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>

```xml
<svg viewBox="0 0 100 100" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>
```

<svg viewBox="0 0 100 100" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>

```xml
<svg viewBox="0 0 50 50" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>
```

<svg viewBox="0 0 50 50" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>

### 2-2. 도형 요소

#### rect

- 직사각형을 그릴 떄 활용됩니다.

```xml
<svg width="400" height="110">
  <rect width="300" height="100"" />
</svg>
```

<svg width="400" height="110">
  <rect width="300" height="100"" />
</svg>

#### circle

- 원을 그릴 때 활용됩니다.

```xml
<svg viewBox="0 0 100 100" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" />
</svg>
```

<svg viewBox="0 0 100 100" width="100" height="100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="60" r="40" />
</svg>

#### ellipse

- 타원을 그릴 때 활용됩니다.
- `<circle />` 과 `<ellipse />` 는 비슷한 도형입니다. 차이점은 `<circle />`의 경우 x, y 반경이 동일하고 `<ellipse />`는 x, y 반경이 동일하지 않다는 점입니다.
- `<ellipse />`의 x, y를 동일하게 변경하면 `<circle />`과 같은 모양을 만들 수 있습니다.

```xml
<svg height="140" width="500">
  <ellipse cx="200" cy="80" rx="50" ry="50" />
</svg>
```

<svg height="140" width="500">
  <ellipse cx="200" cy="80" rx="50" ry="50" />
</svg>

```xml
<svg height="140" width="500">
  <ellipse cx="200" cy="80" rx="100" ry="50" />
</svg>
```

<svg height="140" width="500">
  <ellipse cx="200" cy="80" rx="100" ry="50" />
</svg>

#### line

- 선을 그릴 때 활용됩니다.

```xml
<svg height="210" width="500">
  <line x1="0" y1="0" x2="200" y2="20" style="stroke:black;stroke-width:2" />
</svg>
```

<svg height="210" width="500">
  <line x1="0" y1="0" x2="200" y2="20" style="stroke:black;stroke-width:2" />
</svg>

#### polygon

- 3개 이상의 꼭짓점을 가진 도형을 그릴 때 활용 됩니다.

```xml
<svg height="210" width="500">
  <polygon points="200,10 250,100 100,100"  />
</svg>
```

<svg height="210" width="500">
  <polygon points="200,10 250,100 100,100"  />
</svg>

#### polyline

- 다각선을 그릴 때 활용 됩니다.

```xml
<svg height="200" width="500">
  <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
  style="fill:none;stroke:black;stroke-width:3" />
</svg>
```

<svg height="200" width="500">
  <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
  style="fill:none;stroke:black;stroke-width:3" />
</svg>

## 2-3. path

- `<path />`를 통해 경로를 지정하여 다양한 표현을 할 수 있습니다.
- 아래 예시는 w3c에 예제로 등록 된 `<path />`로 그린 베지어 곡선입니다.

```xml
<svg height="400" width="450">
  <path id="lineAB" d="M 100 350 l 150 -300" stroke="red"
  stroke-width="3" fill="none" />
  <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
  stroke-width="3" fill="none" />
  <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
  fill="none" />
  <path d="M 100 350 q 150 -300 300 0" stroke="blue"
  stroke-width="5" fill="none" />
  <!-- Mark relevant points -->
  <g stroke="black" stroke-width="3" fill="black">
    <circle id="pointA" cx="100" cy="350" r="3" />
    <circle id="pointB" cx="250" cy="50" r="3" />
    <circle id="pointC" cx="400" cy="350" r="3" />
  </g>
  <!-- Label the points -->
  <g font-size="30" font-family="sans-serif" fill="black" stroke="none"
  text-anchor="middle">
    <text x="100" y="350" dx="-30">A</text>
    <text x="250" y="50" dy="-10">B</text>
    <text x="400" y="350" dx="30">C</text>
  </g>
</svg>

```

<svg height="400" width="450">
  <path id="lineAB" d="M 100 350 l 150 -300" stroke="red"
  stroke-width="3" fill="none" />
  <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
  stroke-width="3" fill="none" />
  <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
  fill="none" />
  <path d="M 100 350 q 150 -300 300 0" stroke="blue"
  stroke-width="5" fill="none" />
  <!-- Mark relevant points -->
  <g stroke="black" stroke-width="3" fill="black">
    <circle id="pointA" cx="100" cy="350" r="3" />
    <circle id="pointB" cx="250" cy="50" r="3" />
    <circle id="pointC" cx="400" cy="350" r="3" />
  </g>
  <!-- Label the points -->
  <g font-size="30" font-family="sans-serif" fill="black" stroke="none"
  text-anchor="middle">
    <text x="100" y="350" dx="-30">A</text>
    <text x="250" y="50" dy="-10">B</text>
    <text x="400" y="350" dx="30">C</text>
  </g>
</svg>

### 참고 자료

- https://www.w3schools.com/graphics/svg_intro.asp
- https://developer.mozilla.org/ko/docs/Web/SVG
