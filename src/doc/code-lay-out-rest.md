# 코드 레이아웃 나머지

> [코드 레이아웃](./code-lay-out.md)과 합쳐질 문서다.

## 이항 연산자 앞뒤로 줄바꿈을 해야할까?

몇 십년 동안 권장된 스타일은 이항 연산자 이후에 줄바꿈을 하는 거였다.
하지만 이는 두 가지 이유로 가독성을 해칠 수 있다.
연산자들은 화면의 여러 열(columns)에 흩어져 있는 경향이 있다.
그리고 각 연산자는 피연산자로 부터 제거되어 이전 줄로 옮겨진다.
여기 어느게 더하는 것이고 빼는 것인지 말하기 위해
눈이 추가적인 일을 해야만 하는 예시가 있다.

```python
# Wrong:
# operators sit far away from their operands
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```

이 가독성 문제를 해결하기 위해, 수학자들과 그들의 퍼블리셔들은 반대의 컨벤션을 다른다.
Donald Knuth 는 그의 *Computers and Typesetting* 시리즈에서
다음의 전통적인 규칙을 설명한다.
"비록 단락 내의 공식은 항상 이항 연산 및 관계 뒤에 줄바꿈을 하지만,
표시된 공식은 항상 이항 연산 전에 줄바꿈을 한다."[^1]

수학으로 부터 온 전통을 따르는 것은 대게
더 가독성 있는 코드를 결과로 낸다.

```python
# Correct:
# easy to match operators with operands
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

Python 코드에선, 규칙이 국지적으로 일관성이 있는 한
이항 연산자 앞이나 뒤에 줄바꿈을 하는 것이 허용된다.
새로운 코드의 경우 Knuth의 스타일이 제안된다.

## 공백 줄

탑 레벨 함수와 클래스 정의 앞 뒤로는
두 개의 공백 줄로 감싸진다.

클래스 내의 메소드 정의 앞뒤로는
한 줄의 공백 줄로 감싸진다.

관련된 함수들의 모음을 분리하기 위해 추가적인 공백 줄이 (꼭 필요한 경우에만) 사용될 수 있다.
공백 줄은 관련된 여러 줄의 관련된 one-liner[^2] 사이에서 생략될 수 있다.
(예를 들면, 더미 구현의 집합)

논리적인 구역을 나타내기 위해 함수 내에서 공백줄을 꼭 필요한 경우에만 사용하자.

Python 은 컨트롤 + L (^L) 폼 피드(form feed) 문자를 공백으로 받아들인다.
많은 툴들 이 문자를 페이지 구분자로 취급한다. 그래서 파일 내 서로 관련 된 구역들의 페이지를
분리하기 위해 사용할 수 있다.
몇 에디터와 웹 기반 코드 뷰어에서는 컨트롤 + L 이 폼 피드로 인식되지 않을 수 있다는 점을 주의하자.
그리고 그 위치에 다른 글리프(glyph)[^3]를 보여줄 것이다.

## 소스 파일 인코딩

코어 Python 배포의 코드는 항상 UTF-8을 사용하여야 한다.
(또는 Python 2 에서는 ASCII)

(Python 2 에서) 아스키 또는 (Python 3 에서) UTF-8을 사용하는 파일들은
인코딩 선언(declaration)들을 소유하면 안된다.

표준 라이브러리에서는, 디폴트 값이 아닌 인코딩은
테스트 목적이나 주석이나 독스트링에서 아스키 문자가 아닌
문자를 포함하는 작성자의 이름을 언급할 때만 사용되어야 한다.
반면에 `\x`, `\u`, `\U`, `\N` 이스케이프를 사용하는 것은
문자열 리터럴 안의 아스키가 아닌 데이터를 포함하기 위한 바람직한 방법이다.

Python 3.0 과 그 이상은, 다음의 정책이 표준 라이브러리에 의해 규정되어있다.
([PEP 3131](https://www.python.org/dev/peps/pep-3131/)참고)
Python 표준 라이브러리 안의 모든 식별자들은 반.드.시. 아스키로만 이루어진 식별자들을 사용해야 하며,
가능한 한 영어를 사용해야한다.
(많은 경우에, 영어가 아닌 약어나 기술적인 용어만 영어가 아니어도 된다.)
덧붙여, 문자열 리터럴과 주석 또한 아스키여야한다. 다음의 경우만 예외인데,
(a) 아스키가 아닌 기능을 테스트하는 테스트 케이스 그리고,
(b) 라틴 알파벳(latin-1, ISO/IEC 8859-1 character set)에 기반하지 않은 작성자 명
일 땐, 반드시 이 문자 집합에서
이름의 전자(transliteration)[^4]을 제공해야 한다.

전세계의 사용자를 대상으로 하는 오픈 소스 프로젝트는 유사한 정책을 채택하길 권장한다.

## 가져오기

- 가져오기(Imports)는 분리된 줄에 사용해야 한다.

```python
    # 옳은 예
    import os
    import sys
```

```python
    # 잘못된 예
    import sys, os
```

이것도 괜찮다.

```python
    # Correct:
    from subprocess import Popen, PIPE
```

- 가져오기는 항상 파일의 맨 위에 놓여져 있어야 한다.
  모듈 주석과 독스트링 바로 다음, 그리고 모듈 전역들과 상수들 전에 말이다.

  가져오기는 다음의 순서에 따라 구분되어야 한다.

  1. 표준 라이브러리 가져오기
  2. 관련 서드 파티 가져오기
  3. 로컬 어플리케이션/라이브러리의 특정한 가져오기

  각 가져오기 모음 사이에 공백줄을 넣어야한다.

- 절대 경로 가져오기가 권장된다. 가져오기 체계가 잘못 구성
- (예를 들면, 패키지 내부의 디렉토리가 `sys.path` 에서 끝나는 경우)된다면,
  더 가독성있으며 더 나은 행위를 하는 경향이 있다.
  (또는, 최소한, 더 나은 에러 메시지를 준다던가)

```python
import mypkg.sibling
from mypkg import sibling
from mypkg.sibling import example
```

  하지만, 명시적 상대경로 가져오기는 절대경로 가져오기의 허용 가능한 대안이다.
  특히, 불필요하게 장황한 복잡한 패키지 레이아웃을 처리 할 땐,
  절대경로 가져오기를 사용하는 것보다 나을 수 있다.

```python
from . import sibling
from .sibling import example
```

  표준 라이브러리 코드는 복잡한 패키지 레이아웃을 피하고,
  항상 절대경로 가져오기를 사용해야한다.

  암시적인 상대경로 가져오기는 *절대* 사용되어선 안되며,
  Python 3 에서는 제거되었다.

- 클래스를 갖고 있는 모듈에서 클래스를 가져오기 할때, 다음과 같이
  철자를 바꾸는 것은 괜찮다.

```python
from myclass import MyClass
from foo.bar.yourclass import YourClass
```

만약 이 철자가 로컬 이름 충돌을 야기한다면, 명시적으로 철자를 바꾸자.

```python
import myclass
import foo.bar.yourclass
```

  그리고 "myclass.MyClass"와 "foo.bar.yourclass.YourClass"를 사용하자.

- 와일드 카드 가져오기(`from <module> import *`) 는 피해야한다.
  이들은 네임스페이스 안에서 보여지는 이름들이 불분명하게 만들고,
  독자와 많은 자동화 툴들을 혼란시킨다.
  공개 API의 일부로 내부 인터페이스를 다시 게시(republishing)하는 와일드 카드 가져오기에 대한
  방어 가능한 사용 사례가 하나 있다.
  (예를 들어, 선택적 가속기 모듈(optional accelerator module)로 부터의 정의로,
  인터페이스의 순수 Python 구현을 덮어 쓰고,
  정확히 어떤 정의를 덮어 쓸지 미리 알 수 없을 때)

  이름을 이러한 방법으로 다시 게시할 때,
  [퍼블릭 그리고 내부 인터페이스에 관한 아래의 지침서](./naming-conventions.md#퍼블릭-그리고-내부-인터페이스)
  는 계속 적용된다.

## 모듈 레벨 던더 이름

던더들은 앞 뒤로 두개의 밑줄(underscore)로 감싸진 이름으로,
`__all__`, `__author__`, `__version__` 등이 있다.
모듈 레벨의 "던더들"은 모듈의 독스트링 다음, 가져오기 전에 위치해야한다.
*단*, `from __future__` 가져오기는 제외한다.
Python의 future-imports 명령(mandates)은 모듈내에서 반드시 독스트링을 제외한
어떠한 코드들 보다도 전에 위치해야한다.

```python
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

[^1]: Donald Knuth의 책 "The TeXBook", 195 ~ 196 쪽.
[^2]: [한줄로 끝내버리는 것들](https://wiki.python.org/moin/Powerful%20Python%20One-Liners)
[^3]: _역: 상형문자 같은 것_
[^4]: [위키피디아](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%9E%90_(%EC%96%B8%EC%96%B4%ED%95%99))
