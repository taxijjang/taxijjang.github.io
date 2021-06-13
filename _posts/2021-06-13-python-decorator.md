---
title: python decorator
tags: PYTHON
---

## 데코레이터란
- 데코레이터란 무엇일까요? 사전적 의미로는 "장식가" 또는 "인테리어 디자이너" 등의 의미를 가지고 있습니다. 이름 그대로, 자신의 방을 예쁜 벽지나 커튼으로 장식을 하듯이, 기존의 코드에 여러가지 기능을 추가하는 파이썬 구문


- 데코레이터는 함수에 적용할 수 있으며, 둘러싸는 함수 전후에 실행하는 능력이 있다.
- 데코레이터는 입력 인자와 반환 값을 액세스하고 수정할 수 있으며, 여러 위치에서 유용할 수 있다.

### 몇 가지 예제
1. 비율 제한
2. 캐싱 값
3. 함수의 런타임 타이밍
4. 로깅 목적
5. 예외 수용 및 전달
6. 인증


### Flask 에서 decorator 사용
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hollo():
    return "Hello World"
```


### 문자열을 받아 대문자로 변환
```
* 전달된 func를 대문자로 변환 *
def to_upper_case(func):
    text = func()

    if not isinstance(text, str):
        raise TypeError("Not a string type")
    return text.upper()

def say():
    return "welcome"

def hello():
    return "hello"

>>> to_upper_case(say)
WELCOME

>>> to_upper_case(hello)
HELLO


* 데코레이터 사용 *
@to_upper_case
def say():
    return "welcome"

>>> say
WELCOME
```


### 데코레이터를 사용한 동작 수정
```
* 대문자 데코레이터 *
def to_upper_case(func):
    def wrapper():
        text = func()
        if not isinstance(text, str):
            raise TypeError("Not a string type")
        return text.upper()
    return wrapper

def add_prefix(func):
    def wrapper():
        text = func()
        result = " ".join([text, "Larry Page!"])
        return result
    return wrapper

@to_upper_case
@add_prefix
def say():
    return "hihihihihihi"

@add_prefix
@to_upper_case
def say2():
    return "hihihihihihi"

>> say()
WELCOME LARRY PAGE!

>> say2()
WELCOME Larry Page!
```

### 데코레이터 인자 허용
- 데코레이터 함수에 인자를 전달할 수 있다.

```
def to_upper_case(func):
    def wrapper(*args, **kwargs):
        text = func(*args, **kwargs)
        if not isinstance(text, str):
            raise TypeError("Not a string type")
        return text.upper()
    return wrapper

@to_upper_case
def say(greet):
    return greet

>> say("my name is taekyun")
MY NAME IS TAEKYUN
```


---
