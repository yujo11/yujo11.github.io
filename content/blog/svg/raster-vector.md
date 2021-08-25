---
title: '래스터 파일(JPG, PNG)와 벡터 파일(SVG)의 차이'
date: 2021-08-20 09:03:18
category: 'svg'
draft: false
---

### 1. 서론

웹 서핑이나 개발을 하다 보면 JPG, PNG, SVG 등 다양한 이미지 파일 형식들을 만나게 됩니다.

이 파일들은 크게 래스터(비트맵) 파일과 벡터 파일로 분류할 수 있습니다.

### 2. 래스터(Raster) 파일 - PNG, JPG 등

래스터(Raster) 파일은 화소들을 모아 디지털로 이미지를 표시합니다. 화소들은 색상에 대한 정보를 가지고 있습니다. 래스터 파일들은 총 화소 수와 각 화소의 정보량(색상의 깊이)에 따라 화질이 결정 됩니다.

PNG와 JPG는 래스터(Raster) 파일을 사용하는 대표적인 예입니다. PNG는 비손실압축 방식을 사용해 원본이 훼손되지 않지만 JPG파일은 손실압축으로 원본 자체가 훼손되는 차이점이 있습니다. 또한 PNG는 투명한 배경을 포함할 수 있지만 JPG는 투명한 배경을 포함할 수 없다는 차이도 존재합니다.

따라서, 고퀄리티의 이미지나 투명한 배경을 가진 이미지가 필요한 경우 PNG를 사용하는게 좋습니다.

- PNG와 JPG 간단 정리

|                       |    PNG     |   JPG    |
| :-------------------: | :--------: | :------: |
|       압축 방식       | 비손실압축 | 손실압축 |
| 투명한 배경 포함 가능 |     O      |    X     |

### 3. 벡터(Vector) 파일 - SVG 등

벡터(Vector) 파일은 XML기반의 마크업 코드로 구성 된 파일입니다.

앞서 설명했던 래스터 파일과 다르게 벡터는 이미지를 나눠서 저장하지 않고, 하나의 선이나 도형으로 저장하게 됩니다. 때문에 래스터 파일과는 다르게 확대를 하더라도 모든 사이즈에서 깔끔하게 렌더링 됩니다.

- 래스터 파일과 백터 파일 간단 정리

|                   | 래스터(Raster) 파일 |   벡터(Vector) 파일    |
| :---------------: | :-----------------: | :--------------------: |
| 저장 및 표현 방식 |     화소의 집합     | XML 기반의 마크업 코드 |
|     파일 크기     |      비교적 큼      |      비교적 작음       |
|  확대 시 렌더링   |        깨짐         |        안 깨짐         |

### 4. PNG와 SVG의 렌더링 비교

#### case 1.

- code

```html
<div style="display: flex">
  <div>
    <p>PNG</p>
    <img
      src="./outline_settings_black_24dp.png"
      style="width: 24px; margin-right: 24px"
    />
  </div>
  <div>
    <p>SVG</p>
    <img src="./settings_black_24dp.svg" style="width: 24px" />
  </div>
</div>
```

- result

![](./images/24px.png)

#### case 2.

- code

```html
<div style="display: flex">
  <div>
    <p>PNG</p>
    <img
      src="./outline_settings_black_24dp.png"
      style="width: 240px; margin-right: 24px"
    />
  </div>
  <div>
    <p>SVG</p>
    <img src="./settings_black_24dp.svg" style="width: 240px" />
  </div>
</div>
```

- result

![](./images/240px.png)
