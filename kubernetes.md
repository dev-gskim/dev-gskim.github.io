# kubernetes

#### kubernetes 클러스터 구성을 위해 모든 노드에 아래의 패키지를 설치 해야 한다. 

* kubeadm : kubernetes 클러스터를 구축하기 위해 사용하는 툴이다. 
* kubelet : 클러스터의 모든 머신에서 실행되며 Pod 및 컨테이너 시작 등의 작업을 수행하는 구성 요소이다. 
* kubectl : 클러스터와 통신하는 커맨드라인 인터페이스 유틸이다.

### 

### kubectl install

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

### kubeadm install

* [site](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) 참조

```text
### k8s.conf 
$ cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

### 
$ sudo sysctl --system
* Applying /usr/lib/sysctl.d/00-system.conf ...
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-arptables = 0
* Applying /usr/lib/sysctl.d/10-default-yama-scope.conf ...
kernel.yama.ptrace_scope = 0
* Applying /usr/lib/sysctl.d/50-default.conf ...
kernel.sysrq = 16
kernel.core_uses_pid = 1
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.accept_source_route = 0
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.promote_secondaries = 1
net.ipv4.conf.all.promote_secondaries = 1
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
* Applying /usr/lib/sysctl.d/60-libvirtd.conf ...
fs.aio-max-nr = 1048576
* Applying /etc/sysctl.d/99-sysctl.conf ...
* Applying /etc/sysctl.d/k8s.conf ...
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
* Applying /etc/sysctl.conf ...

```





#### sysctl

> sysctl 은 버전 번호나 보안 설정 같은 시스템 [커널](https://ko.wikipedia.org/wiki/%EC%BB%A4%EB%84%90_%28%EC%BB%B4%ED%93%A8%ED%8C%85%29)의 속성들을 읽고 수정하는 몇몇 [유닉스 계열](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%89%EC%8A%A4_%EA%B3%84%EC%97%B4) 운영 체제의 기능이다.

