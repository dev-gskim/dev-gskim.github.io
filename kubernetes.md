# kubernetes

### install

* [site](https://kubernetes.io/ko/docs/tasks/tools/install-kubectl/) 참
* 리눅스에서 curl을 사용하여 kubectl 바이너리 설치

```text
#### download
$ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

#### chmod
$ chmod +x ./kubectl

### 바이너리를 PATH가 설정된 디렉터리로 옮긴다.
### root 권한 필
$ sudo mv ./kubectl /usr/local/bin/kubectl

### version 확인
$ kubectl version --client
Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.2", GitCommit:"f5743093fd1c663cb0cbc89748f730662345d44d", GitTreeState:"clean", BuildDate:"2020-09-16T13:41:02Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}
```

