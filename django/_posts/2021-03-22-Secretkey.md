---
layout: post
title: "Secret_Key 분리하기(장고)"
tags:
  - [Secret_Key]
  - [django]
---

## 참고 자료

---

[[Django] Django secret key 분리하기](https://medium.com/iovsomnium/django-django-secret-key-%EB%B6%84%EB%A6%AC%ED%95%98%EA%B8%B0-74288462e2ff)

## Secrets.json 만들기

---

프로젝트 폴더(manage.py가 있는 곳)에 secrets.json 파일 생성 후

```python
{
    "SECRET_KEY" : "스크릿키"
}
```

작성

## setting.py

---

setting.py 파일에 다음 코드를 작성

```python
import os, json
from django.core.exceptions import ImproperlyConfigured

secret_file = os.path.join(BASE_DIR, 'secrets.json')

with open(secret_file, 'r') as f: #open as로 secret.
    secrets = json.loads(f.read())

def get_secret(setting, secrets=secrets):
    try:
        return secrets[setting]
    except KeyError:
        error_msg = "Set the {} environment variable".format(setting)
        raise ImproperlyConfigured(error_msg)

SECRET_KEY = get_secret("SECRET_KEY")
```

## .gitignore 파일 생성

.gitignore파일 생성 후 `secrets.json`작성

## github 올리기