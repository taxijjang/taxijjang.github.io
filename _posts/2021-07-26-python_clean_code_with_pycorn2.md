---
title: pycon - 우아하게 준비하는 테스트와 리팩토링 ( 테스트 코드 )
tags: PYTHON CLEANCODE TESTCODE
---
아래의 글은 PyCon을 참고 하였습니다.
[!https://www.youtube.com/watch?v=S5SY2pkmOy0&t=382s](https://www.youtube.com/watch?v=S5SY2pkmOy0&t=382s)

# 잠깐, 테스트 코드 작성이 정말 필요한가요?

-   생각보다 실제 환경에서 동작하는 코드는 복잡하다.
-   하나의 가장 적은 단위의 코드를 추가하거나 수정했다고 가정한다.
-   만약 그 코드가 문제가 있으면 그건 정말로 큰 부작용(Side-Effect)를 발생시킨다.
-   특정 조건에서만 발생하는 버그로 인해, 일부는 동작하고 일부는 동작하지 않는다면 사람이 검수로 버그를 발견하기도 힘들어진다.
-   이렇게 되면 코드 하나를 추가하는 것이 두려워지고 신뢰할 수 없게 된다.
-   테스트 코드는 이런 기능 추가와 수정이 발생할 때 발생할 수 있는 사이드 이펙트 탐지를 돕고 코드를 신뢰할 수 잏게 만들어준다.

# 일반적으로 고려하는 테스트

1.  단위 테스트 (Unit Test)

    > -   method, function을 테스트 세부적으로 테스트 할 수 있는 방법
    > -   함수와 메서드의 최소 단위와 각 비즈니스 코드의 테스트 등 일반적인 테스트 코드들에 해당

2.  통합 테스트 (Intergration Test)

    > -   DB, 이미 통합된 코드를 테스트
    > -   각종 함수와 메서드가 모여진 코드의 잡합을 전체적으로 테스트 실제 사용하는 사용자 기능 위주의 테스트 가능

3.  E2E 테스트 (End-To-End Test)

    > -   UI 관점에서 실제로 테스트 하는 방법 (Form에 데이터를 직접 입력 한다거나, 등등 사용자 입장에서 테스트 하는)
    > -   사용자가 실제로 사용하는 UI와 같은 복잡한 환경에서 테스트 코드와 관계없이, 사용자의 OS와 레지스트리, 메모리 등에 의한 모든 결함 탐지


# 테스트 코드 별 특징

1.  White Box Test

    > -   코드의 내부를 들여다보고 코드를 테스트하는 방식


-   구문 커버리지 (커버리지 Coverage)
-   조건/분기 커버리지 (커버리지 Coverage)
-   MC/DB 커버리지 (커버리지 Coverage)

2.  Black Box Test

    > -   코드의 내부를 모르는 상태에서 입력 값과 출력 값으로 코드를 테스트하는 방식


-   동등 클래스 분할 (테스트 케이스 TC)
-   경계 값 분석 (테스트 케이스 TC)

# 순수 함수 (Pure Function)

```
__VERSION__ = '0.0.1'
def sum(a, b):
    return a + b

def get_version():
    return __VERSION__
```

함수에 제공된 입력 값에 의해 출력 값이 결정되는 함수
입력 값 외에 어떤 상태나, 환경에 의해서 출력 값이 결정되지 않는 함수이기 때문에 테스트를 진행하기에 적절 하다.

# 단위 테스트 assert 함수들

-   assertEqual - 두 값의 일치 여부를 검증

-   assNotEqual - 두 값의 불일치 여부를 검증

-   assertTrue - 값이 참임을 검증

-   assertFalse - 값이 거짓임을 검증

-   assertIs - 두 값의 참조 일치 여부를 검증

-   assertIsNot - 두 값의 참조 불일치 여부를 검증

-   assertIsNotNone - 값이 None이 아님을 검증

-   assertIn - 값의 포함 관계를 검증

-   assertNotIn - 값의 비포함 관계를 검증

-   assertIsInstance - 값의 인스턴스 타입 일치 여부를 검증

-   assertNotIsInstance - 값의 인스턴스 타팁 불일치 여부를 검증

-   unittest 모듈에서 제공하는 주요 메소드들

-   단위 테스트를 작성할 때 위와 같은 검증 메소드를 사용할 수 있다.
