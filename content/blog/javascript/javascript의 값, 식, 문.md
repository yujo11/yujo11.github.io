---
title: 'symc, async'
date: 2021-03-19 09:03:18
category: 'web'
draft: true
---

# symc, async

## sync

### Sync Flow

- Sync Flow: 메모리에 적재된 명령이 순차적으로 실행 됨. 한번 시작되면 멈출 수 없음
- Sync Flow Control: Goto를 통해 명령의 위치를 이동(ex - if 분기)
- Sub Flow: 함수 등을 통해 별도의 명령셋을 여러번 실행함.

### Blocking

- Blocking: Sync Flow가 실행되는 동안 다른 일을 할 수 없는 현상
