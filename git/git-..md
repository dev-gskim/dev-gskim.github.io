# git 이전 내용으로 되돌리기.

### git Desktop 사용

* git Descktop 을 사용하여 이전으로 되돌리기 
* history 에서 특정 이력으로 이동후 'Revert this commit' 을 클릭하면 된다.

![](../.gitbook/assets/image%20%282%29.png)

### 특정 파일만 되돌리기.

* git checkout {커밋아이디} {파일경로+파일}

![](../.gitbook/assets/image%20%283%29.png)

```text
> git checkout 543e7fb "readme.md"
> Updated 17 paths from 543e7fb 
```

* readme.md 파일이 이전으로 되돌아 간다. 





