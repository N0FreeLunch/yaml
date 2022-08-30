## 시퀀스
- 순서가 있는 나열을 의미함
- YAML에서 순서가 있는 대상은 대상을 순서대로 `-`을 붙여서 연속된 개행으로 차례로 나열한다.

### 스칼라 값의 시퀀스
```
- Mark McGwire
- Sammy Sosa
- Ken Griffey
```
- 축구 선수 이름이란 스칼라 값을 `-`으로 한 줄씩 나열하였다.
- 순서는 `Mark McGwire`, `ammy Sosa`, `Ken Griffey` 순이 된다.


## 매핑
- 키/벨류 형식으로 한 쌍을 만드는 것
- `키: 벨류` 방식으로 표현한다. 콜론은 키 바로 다음에 붙여주고 콜론과 벨류 사이에는 공백 문자가 위치할 수 있다.

## 스칼라 값과 스칼라 값을 매핑
```
hr:  65    # Home runs
avg: 0.278 # Batting average
rbi: 147   # Runs Batted In
```

## 서로 다른 구조 간의 결합
- 스칼라 값과 스칼라 뿐만 아니라 스칼라 값에 시퀀스를 매핑할 수 있다.

### 스칼라와 시퀀스의 매핑
```
american:
- Boston Red Sox
- Detroit Tigers
- New York Yankees
national:
- New York Mets
- Chicago Cubs
- Atlanta Braves
```

- `american` 이라는 스칼라 값을 키로 두면 `american:`이 되고 시퀀스를 대응한다. `american:` 다음에는 공백 문자가 올 수 있으므로 개행 문자가 와도 된다.

```
- Boston Red Sox
- Detroit Tigers
- New York Yankees
```
- 연속된 개행으로 이뤄진 문두에 하이픈 `-`이 붙은 형태로 `- New York Yankees` 다음에 `national:`가 오므로 시퀀스가 끝나는 지점을 알 수 있다. 곧, 시퀀스의 단위를 알 수 있다.


