# 주석

주석은 아얘 없는 것보다 코드와 상이한 것이 더 나쁘다.
항상 코드가 변경 될 때마다 주석을 최신 상태로 유지하는 것에
우선순위를 두자!

주석은 완전한 문장으로 쓰여져야 한다.
*(역: 영문으로 작성시)* 첫번째 글자는 대문자여야 한다.
단, 식별자(identifier)의 경우 첫글자의 대소문자를 변경하지 말아야 한다.

블록 주석은 주로 하나 이상의 단락으로 구성된다.
이를 구성하는 문장들은 마침표로 끝맺는다.

여러 문장으로 된 주석들은 문장들의 마침표 뒤에 2칸 공백을 사용해야한다.
단, 마지막 문장은 제외한다.

주석은 사용한 언어들이 명확해야하며,
다른 사용자가 이해하기 쉽게 작성되어야 한다.

비영어권 국가의 파이썬 코더들은 주석을 영어로 작성하자.
그렇게 하지 않을 경우 당신의 언어를 사용하지 않는 사람들은 코드를 절대로 읽지 않을 것을
120% 확실한다.

## 블록 주석

블록 주석은 주로 일반적으로 그 뒤에 오는 일부 (또는 전체) 코드에 적용되며,
해당 코드와 동일한 레벨로 들여쓰기 되야한다.
블록 코멘트의 각각의 줄은 `#` 하나와 한 칸 공백으로 시작한다.
(단, 주석 안에서 들여쓰기 된 경우를 제외한다.)

블록 주석 안의 단락들은 `#` 하나를 포함할 때마다 줄로 구분된다.

## 인라인 주석

인라인 주석을 적게 사용하자.

인라인 주석은 코드의 문(statement)과 같은 줄에 있는 주석이다.
인라인 주석은 최소 2칸 공백으로 코드의 문과 구분 되어야한다.
그들은 `#` 과 한 칸 공백으로 시작한다.

인라인 주석은 불필요하며, 실제로 상태를 명확히 나타내면 산만해진다. 다음과 같이 하지말자.

```python
x = x + 1                 # x 를 증가시킨다.
```

하지만, 이런 경우에는 때때로 유용하다.

```python
x = x + 1                 # 테두리 보정
```

## 문서화 문자열

좋은 문서화 문자열 (일명 "독스트링")을 작성하기위한 규칙은
[PEP 257](https://www.python.org/dev/peps/pep-0257/)
에서 영구화되었다.

- 모든 퍼블릭 모듈, 함수, 클래스, 그리고 메서드들에 대해서 독스트링을 작성하자.
  독스트링은 퍼블릭이 아닌 메서드에서는 필수가 아니지만,
  그 메서드가 무엇을 하는지는 설명해주어야한다.
  이 주석은 `def` 줄 다음에 작성되어야 한다.

- [PEP 257](https://www.python.org/dev/peps/pep-0257/)
  에 좋은 독스트링 컨벤션이 설명되어있다. 내용의 핵심은, 여러 줄의 독스트링을 끝낼 때,
  그 줄엔  `"""` 만 존재해야한다는 것이다.

```python
    """Return a foobang

    Optional plotz says to frobnicate the bizbaz first.
    """
```

- 한 줄로 된 독스트링의 경우, 닫는 ``"""`` 를 같은 줄에 유지해야한다.

```python
      """Return an ex-parrot."""
```
