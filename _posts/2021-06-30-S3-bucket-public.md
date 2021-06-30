---
title: django S3Boto3Storage를 이용하여 객체 public
tags: DJANGO S3 BOTO3
---

### django media를 s3에 publick으로 올리는 방법

```
models/video.py

from django.db import models
from video.storage ipmort MediaStorage

class Video(models.Model):
    source = models.FileField(upload_to='source', storage=MediaStorage)
    thumbnail = models.ImageField(upload_to='thumbnail', storage=MediaStorage)
```

```
video/storage.py

from sotrages.backends.s3boto3 import S3Boto3Storage

class MediaStorage(S3Boto3Storage):
    # base bucket location
    location = 'media/marketing/'

    # access authority
    default_acl = 'public-read'

```

- 기본적으로 settings에서 AWS에 대한 설정이 완료 된 후 S3Boto3Storage를 상속 받아 MediaStorage class를 생성하여 field를 원하는 대로 재정의 하여 django model 의 storage에 지정하면 됩니다.

- [Django Storage 공식 문서]('https://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html#usage')
