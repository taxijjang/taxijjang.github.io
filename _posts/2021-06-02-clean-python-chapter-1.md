---
title: 1장 - 파이써닉으로 생각하기
tags: python
---

### 올바른 함수 이름
```
# 잘못된 방법
def get_user_info(id):
    db = get_db_connection()
    user = execute_query_for_user(id)
    return user

# 올바른 방법
def get_user_by(user_id):
    db = get_db_connection()
    user = execute_user_query(user_id)
    return user
```

### 클래스의 이름은 카멜 케이스(camel case)
```
class UserInformation:
    det get_user(id):
        db = get_db_connection()
        user = execute_query_for_user(id)
        return user
```

### 함수 및 메서드 인자는 변수 및 메서드 이름과 동일한 규칙을 따라야 한다.
```
def calculate_tax(amount, yearly_tax):
    pass

class Player:
    deg get_total_score(self, player_name):
        pass
```

### 인플레이스 문자열 결합 대신 조인 사용
```
first_name = "Json"
last_name = "smart"

# 문자열 연결 시 권장하지 않는 방법
full_name = first_name + " " + last_name

# 더 뛰어난 성능과 가독성 향상
" ".join([first_name, last_name])
```

### 식별자 바인딩 시 람다 대신 함수 사용
```
# 추천하지 않는 방법
square = lambda x: x * x

# 추천하는 방법
def square(val):
  return val * val
```

### 비교 시 type() 대신 isinstance() 메서드 사용
```
# 추천하지 않는 방법
user_ages = {"Larry": 35, "Jon": 89, "Imli": 12}
if type(user_ages) == dict:
  pass

#추천하는 방법
user_ages = {"Larry": 35, "Jon": 89, "Imli": 12}
if isinstance(user_ages, dict):
  pass
```
---
