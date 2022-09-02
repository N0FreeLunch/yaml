## 한 파일에 여러 도큐먼트 정의하기
- 하나의 파일에 여러 단위의 yaml 도큐먼트를 정의한다.
- 하나의 도큐먼트는 데이터를 직렬화 할 수 있는 한 단위이다.
- 하나의 yaml 파일에 여러 도큐먼트를 정의한다는 것은 직렬화의 단위가 되는 대상이 여럿이라는 의미이다.
- 하나의 도큐먼트는 하나의 JSON으로 변환 가능하다.

### `---`
- 하나의 파일에서 여러 별도의 yaml 코드를 정의할 때, 각각의 yaml 코드 간의 구분을 위한 문법
- yaml 코드의 시작 지점을 만든다.
```
---
```
- 위 코드 다음의 yaml은 다음 `---` 또는 `...`이 나오기 전까지 하나의 yaml 코드 단위를 가진다.

#### 예제
```
# Ranking of 1998 home runs
---
- Mark McGwire
- Sammy Sosa
- Ken Griffey

# Team ranking
---
- Chicago Cubs
- St Louis Cardinals
```

### `...`
- 하나의 파일에서 여러 별도의 yaml 코드를 정의할 때, 각각의 yaml 코드 간의 구분을 위한 문법
- yaml 코드의 끝 지점을 만든다.

#### 예제
```
---
time: 20:03:20
player: Sammy Sosa
action: strike (miss)
...
---
time: 20:03:47
player: Sammy Sosa
action: grand slam
...
```

### 주석
- 주석은 `#`으로 사용할 수 있다.
- 한 행에서 `#`이 나온 뒤의 문자열은 주석이 되어 무시된다.

#### 예제
```
---
hr: # 1998 hr ranking
- Mark McGwire
- Sammy Sosa
# 1998 rbi ranking
rbi:
- Sammy Sosa
- Ken Griffey
```

```
---
hr:
- Mark McGwire
- Sammy Sosa
rbi:
- Sammy Sosa
- Ken Griffey
```
- yaml 파일을 파싱하여 직렬화를 하게 되면 위 두 문서는 동일한 직렬화 데이터를 갖는다.

### 노드의 반복 (Repeated nodes), 참조
- yaml의 한 단위의 자료의 형태를 Node라고 부르며 노드에는 스칼라, 시퀀스, 매핑으로 구성되어 있다.
- 한 단위의 노드는 재사용할 수 있는 단위로 만들 수 있다.
- 재사용하는 단위로 만들 때는 하나의 노드의 앞에 `&명칭`을 사용한다.
- `*명칭`을 사용하면 재사용 단위로 지정한 노드를 사용할 수 있다.

#### 예제
```
---
hr:
- Mark McGwire
# Following node labeled SS
- &SS Sammy Sosa
rbi:
- *SS # Subsequent occurrence
- Ken Griffey
```
- `- &SS Sammy Sosa`에서 스칼라 형태의 `Sammy Sosa`를 재사용 단위로 지정하였다.
- 이때, 재사용 대상의 명칭은 `&SS`이다.
- `&SS`로 재사용할 노드를 불러오면 스칼라 데이터를 저장 했으므로 스칼라 값인 `Sammy Sosa`가 `&SS` 부분에 할당된다.


