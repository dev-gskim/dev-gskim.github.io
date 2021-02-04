---
description: Git pull/push 시 Password 물어보지 않도록 설정하기
---

# pull, push 시 계정 물어보지 않도록

### 계정을 물어보지 않도록 하는 git 명령

```text
## 계정을 저장
$ git config credential.helper store

## 모든프로젝트에 적용
$ git config credential.helper store --global

## 계정정보를 임시로 저장
$ git config credential.helper cache

## 계정정보를 임시로 1시간 저장
$ git config credential.helper 'cache --timeout=3600'


```

* git : [https://git-scm.com/docs/git-credential-cache](https://git-scm.com/docs/git-credential-cache)

