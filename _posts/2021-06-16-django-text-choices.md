---
title: django models.TextChoices (enum)
tags: PYTHON DJANGO
---

### models.TextChoices에서 name, value, label
```
class Kind(models.TextChoices):
    BEST_NAME = 'best_value', 'best_label'
    SALE_NAME = 'sale_value', 'sale_label'
    NEW_NAME = 'new_value', 'new_label'
```
### 호출 방법
> Kind.{ name }.{ name, value, label }

> Kind.NEW_NAME.name = NEW_NAME

> Kind.NEW_NAME.value = new_value

> Kind.NEW_NAME.name = NEW_label
