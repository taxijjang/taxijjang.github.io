---
title: drf serializer에서 instance 유무의 차이
tags: django
---

serializer.save를 호출시

serializer안에 instance가 있다면 serializer.save는 update를 호출하고

serializer안에 instance가 없다면 serializer.save는 create를 호출한다

---
