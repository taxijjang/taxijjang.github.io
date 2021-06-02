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

---
