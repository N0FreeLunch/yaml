# Scalars

## 스칼라 개행
- yaml에서 문자열을 표기하는 방식은 스칼라, 시퀀스, 매핑을 이용하여 기술한다.
- 가장 기본적인 형태는 스칼라방식이다. 시퀀스는 스칼라 앞에 하이픈`-`을 붙여 표기하는 방식이고, 매핑을 구성하는 키, 벨류도 매핑의 형식에 스칼라 표현을 사용하는 방식이라고 볼 수 있다.
- 스칼라 방식은 개행을 허용한다. 단 행의 맨 앞에 하이픈`-`이 오거나 한 행에서 처음으로 콜론`:`이 나오는 등 yaml의 문법적인 요소로 인해 스칼라 표현이 끊기게 된다.

## 기본 스타일 / 리터럴 스타일 / 폴드 스타일
- 기본 스타일은 개행 및 들여쓰기를 하나의 공백으로 치환한다. 치환된 공백이 연속된 경우 중복 없이 하나의 공백으로 직렬화 된다.
- 리터럴 스트일은 일반 텍스트와 같이 개행이 개행으로 직렬화 되는 방식이다.
- 폴드 스타일은 들여쓰기와 빈 줄을 통해서 문자열의 개행으로 직렬화 되는 방식이다.

## 리터럴 스타일
- 줄 바꿈 문자를 포함하려면 스칼라 표현을 쓰기 전의 행에 `|`를 붙여주도록 한다.
- 줄 바꿈 문자를 포함하지 않고 직렬화에서 무시하려면 스칼라 표현을 쓰기 전의 행에 `|`를 붙여주지 않는다.
- 개행이 개행을 의미하기 때문에 리터럴 스타일에 해당한다.

### 예제
```
# ASCII Art
--- |
  \//||\/||
  // ||  ||__
```
- json 변환기로 변환을 하게 되면 `"\\//||\\/||\n// ||  ||__\n"`으로 개행을 `\n`으로 표기한 결과가 된다.
```
# ASCII Art
---
  \//||\/||
  // ||  ||__
```
- 기본 스타일의 예제로서 `---` 뒤에 `|`을 빼면 `"\\//||\\/|| // ||  ||__"`으로 개행을 무시한 결과가 된다.

## 줄바꿈 문자 공백화
- 줄바꿈이 공백을 의미한다.

### 예제
```
--- >
  Mark McGwire's
  year was crippled
  by a knee injury.
```
- json 변환기로 변환을 하게 되면 `"Mark McGwire's year was crippled by a knee injury.\n"`이다.
- 개행 이후로 이어지는 스칼라 표현이 동일한 들여쓰기로 되어 있을 경우 하나의 공백으로 표현된다.

## 폴드 스타일
- 빈 줄 또는 기본 들여쓰기 라인인 첫 번째 줄 보다 더 들여 쓰기 한 깊은 들여쓰기인 경우 개행 문자가 붙는다.
- 개행을 빈 줄 또는 들여쓰기로 표기하기 때문에 폴드 스타일에 해당한다.
- 폴드 스타일인 경우 스칼라 표현을 쓰기 전의 행에 `>`를 붙여준다.

```
--- >
 Sammy Sosa completed another
 fine season with great stats.

   63 Home Runs
   0.288 Batting Average

 What a year!
```
- json 변환기로 변환을 하게 되면 `"Sammy Sosa completed another fine season with great stats.\n\n  63 Home Runs\n  0.288 Batting Average\n\nWhat a year!\n"`이 된다.
```
 fine season with great stats.

   63 Home Runs
```
- 빈 줄은 하나의 개행을 의미한다. 깊은 들여 쓰기 또한 하나의 개행을 의미한다. 따라서 json 변환 결과는 `\n\n`로 두 개의 개행문자가 나온다.
```
   63 Home Runs
   0.288 Batting Average
```
- `Runs`와 `0.288` 사이도 깊은 들여쓰기이므로 개행 문자 하나를 포함한다.
```
   0.288 Batting Average

 What a year!
```
- `0.288 Batting Average` 다음 줄은 빈줄이므로 하나의 개행문자를 가진다.

## 들여쓰기로 스코프를 결정하기
```
name: Mark McGwire
accomplishment: >
  Mark set a major league
  home run record in 1998.
stats: |
  65 Home Runs
  0.278 Batting Average
```
- 매핑을 구성하는 `키: 벨류` 집합에서 키와 벨류는 각각 스칼라로 구성되어 있다.
- 따라서 키가 시작하는 위치 앞 또는 벨류가 시작하는 위치 앞에 `|` 또는 `>`를 붙여주면 기본 스타일의 스칼라 뿐만 아닌 리터럴, 폴드 스타일의 스칼라 값을 적어 줄 수 있다.

## 인용
- yaml에서 스칼라를 기술하는 방식을 flow scalar라고 한다.
- 스칼라를 표현하는 방식으로는 인용 부호를 쓰지 않는 방법(plain), 따옴표 인용 부호(single-quoted)를 사용하는 방법, 쌍 따옴표 인용 부호(double-quoted)를 사용하는 방법이 있다.
- 쌍따옴표 인용 부호를 사용하는 방식은 이스케이프 시퀀스를 이용할 수 있다. 따옴표 인용 부호를 사용하는 방법은 이스케이프 시퀀스를 사용할 수 없다.
- 모든 flow scalar는 여러 라인에 걸처 기술할 수 있다. 다음 줄에 스칼라를 이어 쓰깅 위해서는 상위노드의 들여쓰기 보다 더 깊은 들여쓰기 라인을 가져야 한다.

### 예제
```
unicode: "Sosa did fine.\u263A"
control: "\b1998\t1999\t2000\n"
hex esc: "\x0d\x0a is \r\n"

single: '"Howdy!" he cried.'
quoted: ' # Not a ''comment''.'
tie-fighter: '|\-*-/|'
```
- 인용 부호를 사용하여 스칼라 값을 표기할 수 있다.
- 쌍 따옴표 안에는 유니코드 이스케이프 시퀀스 `\u263A`, 벡스페이스 이스케이프 시퀀스 `\b1998`, 탭 이스케이스 시퀀스 `\t1999` `\t2000`, 16진수 핵스 이스케이프 시퀀스 `\x0d` `\x0a`가 사용되었다.
- 따옴표 안의 쌍 따옴표, 쌍 따옴표 안에 따옴표는 문자열 따옴표로 취급된다.

### 예제2
```
plain:
  This unquoted scalar
  spans many lines.

quoted: "So does this
  quoted scalar.\n"
```
```
  This unquoted scalar
  spans many lines.
```
- `plain`의 벨류는 스칼라이다. 스칼라 값이 개행을 하더라도 하나의 스칼라로 직렬화가 되기 위해서는 상위 노드인 `plain:`보다 더 깊은 들여쓰기여야 한다.
```
 plain:
   This unquoted scalar
   spans many lines.

 quoted: "So does this
quoted scalar.\n"
```
- `quoted`의 벨류는 따옴표로 감싸진 형태의 스칼라이다. 따옴표를 사용할 경우에는 다음 행의 이어지는 스칼라 값이 들여쓰기 위치에 상관없이 한 단위의 스칼라로 직렬화 될 수 있다.

