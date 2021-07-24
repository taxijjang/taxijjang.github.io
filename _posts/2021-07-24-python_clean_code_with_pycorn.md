---
title: pycon - 우아하게 준비하는 테스트와 리팩토링 ( 클린코드 )
tags: PYTHON CLEANCODE
---
[https://www.youtube.com/watch?v=S5SY2pkmOy0&t=382s](https://www.youtube.com/watch?v=S5SY2pkmOy0&t=382s)

# 깨진 유리창 이론

-   만약 한 건물의 유리창이 깨진채로 방치되어 있다면 머지 않아 그 건물의 다른 유리창도 깨질 것이다.
-   만약 문제가 그대로 방치되어 있다면 머지 않아 돌이킬 수 없는 문제를 야기할 수 있다.

# 보이스카우트 규칙 (Boy Scout Rule)

-   깨진 유리창 이론을 막기 위함
-   언제나 처음 왔을 때보다 깨끗하게 해놓고 캠프장을 떠날 것

# 클린 코드의 원칙

### 가드 클러즈 (GuardClause)

-   가드 클러즈 (GuardClauses)는 여러분의 인덴트(Indent)를 줄여줍니다.

-   Before Refactoring

    ```
    def example():
      user = get_user()
      if user != None and user.type = 'anonymous':
          post = get_post(user)
          if post != None and post.title != None:
              comment = get_comment(post)
              status = do_wit_comment(comment)
              if status == False:
                  return Status.FAIL
              else:
                  return Status.SUCCESS
          return Status.FAIL
      return Status.FAIL
    ```

-   After Refactoring

    ```
    def example():
      user = get_user()
      if user == None of user.type == 'anonymous':
          return Status.FAIL
      post = get_post(user)
      if post == None or post.title == None:
          return Status.FAIL
      comment = get_comment(post)
      status = do_with_comment(comment)

      if status == False:
          return Status.FAIL

      return Status.SUCCESS
    ```

-   NoneObject는 코드의 복잡한 조건을 간단하게 만들어줍니다.

    ```
    def example():
      user = get_user()
      if user.get('type') == None:
          return Status.FAIL

      post = get_post(user)
      if post.get('title') == None:
          return Status.FAIL

      comment = get_comment(post)
      status = do_with_comment(comment)

      if status = False:
          return Status.FAIL

      return Status.SUCCESS
    ```

-   Bool, Object에서 None, False을 체크할 경우 `not` Syntax Sugar를 사용하세요

    ```
    def example():
      user = get_user()
      if not user.get('type'):
          return Status.FAIL

      post = get_post(user)
      if not post.get('title'):
          return Status.FAIL

      comment = get_comment(post)
      status = do_with_comment(comment)

      if not status:
          return Status.FAIL

      return Status.SUCCESS
    ```

-   각 함수에서 예외처리를 진행하거나 유효성 오류의 경우 NoneObject를 반환하세요

    ```
    def example():
      user = get_user()
      post = get_post(user)
      comment = get_comment(post)
      status = do_with_comment(comment)

      if not status:
          return Status.FAIL

      return Status.SUCCESS
    ```

-   짧은 조건은 삼항 연산자를 사용하세요

    ```
    def example():
      user = get_user()
      post = get_post(user)
      comment = get_comment(post)
      status = do_with_comment(comment)

      return Status.FAIL if not status else Status.SUCCESS
    ```


---

-   단순하나 형태의 IF, SWITCH는 Dict Accessing 형식으로 변경해주세요

    ```
    def get_user_permit(code):
        if cnode == 'A':
            return Permission.ADMIN
        elif code == 'U':
            return Permission.USER
        else:
            return Permission.ANONYMOUSE
    ---
    def get_user_permit(code):
        permissions = {
            'A': Permission.ADMIN,
            'U': Permission.USER,
            '_': Permission.ANONYMOUSE
        }
        return permissions.get(code, permissions['_'])
    ```

-   함수 이름은 snake\_case로 지정하고 행동(Action)을 이름의 가장 앞에 명명하세요

    ```
    def user_namd_find(name):
          #do sometiong
        pass

    def userPermissionChecking(permit):
        #do sometiong
        pass

    def CommentMessage(id, message):
        #do someting
        pass

    ---
    def find_user_name(name):
        #do someting
        pass

    def check_user_permit(permit):
        #do someting
        pass

    def do_comment(id, message):
        #do someting
        pass
    ```


-   주석이 필요한 복잡한 로직은 함수로 분리하고고, 함수 명을 주석 대신 사용하세요

    ```
    def example():
        user = getUser()
        post = getPost(user)

        if not post:
            return Status.FAIL

        # remove post with admin
        if is_user_admin(user):
            remove_post(post.id)
            send_log(user.id)
            send_log(post.owner)
        else:
            send_error(user.id)
        return Status.SUCCESS

    ---
    def example():
        user = getUser()
        post = getPost(user)

        if not post: return Status.FALE

        remove_post_with_admin(post, user)
        return Status.SUCCESS

    def remove_post_with_admin(post, user):
        if is_user_admin(user):
            remove_post(post.id)
            send_log(user.id)
            send_log(post.owner)
        else: send_error(user.id)
    ```


### 그 밖에도 많은 클린 코드 방법들이 존재합니다.

-   3줄 이상의 라인이 중복된 코드는 함수로 분리하세요 (그 이하는 인라인 함수 혹은 인라인 유지)
-   주석이 없는 코드가 제일 좋은 코드임을 명심하세요
-   클래스와 함수에 너무 많은 기능을 주지 마세요, 많은 기능이 묶인 함수면 코드 기능 별로 함수를 분리하세요
-   함수에 부여되는 인수는 4개를 넘지 않도록 하세요
-   복잡한 조건은 캡슐화를 하여 직관적인 이름을 명시하여 쉽게 만들어주세요
-   .py 파일에 두개 이상의 클래스를 정의하지 마세요 (클래스 별로 파일을 분리하세요)
