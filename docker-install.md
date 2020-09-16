---
description: docker install
---

# docker install

### centos7

* docker ce install

```text
# yum install -y yum-utils device-mapper-persistent-data lvm2
# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# yum install docker-ce
```

* 실행예

```text
[root@localhost ~]# yum install -y yum-utils device-mapper-persistent-data lvm2
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirror.kakao.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
Package yum-utils-1.1.31-54.el7_8.noarch already installed and latest version
Package device-mapper-persistent-data-0.8.5-2.el7.x86_64 already installed and latest version
Package 7:lvm2-2.02.186-7.el7_8.2.x86_64 already installed and latest version
Nothing to do
[root@localhost ~]# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
Loaded plugins: fastestmirror, langpacks
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
[root@localhost ~]# yum install docker-ce
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirror.kakao.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
docker-ce-stable                                                                         | 3.5 kB  00:00:00
(1/2): docker-ce-stable/x86_64/updateinfo                                                |   55 B  00:00:00
(2/2): docker-ce-stable/x86_64/primary_db                                                |  45 kB  00:00:00
Resolving Dependencies
--> Running transaction check
---> Package docker-ce.x86_64 3:19.03.12-3.el7 will be installed
--> Processing Dependency: container-selinux >= 2:2.74 for package: 3:docker-ce-19.03.12-3.el7.x86_64
--> Processing Dependency: containerd.io >= 1.2.2-3 for package: 3:docker-ce-19.03.12-3.el7.x86_64
--> Processing Dependency: docker-ce-cli for package: 3:docker-ce-19.03.12-3.el7.x86_64
--> Running transaction check
---> Package container-selinux.noarch 2:2.119.2-1.911c772.el7_8 will be installed
---> Package containerd.io.x86_64 0:1.2.13-3.2.el7 will be installed
---> Package docker-ce-cli.x86_64 1:19.03.12-3.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================================================
 Package                    Arch            Version                             Repository                 Size
================================================================================================================
Installing:
 docker-ce                  x86_64          3:19.03.12-3.el7                    docker-ce-stable           24 M
Installing for dependencies:
 container-selinux          noarch          2:2.119.2-1.911c772.el7_8           extras                     40 k
 containerd.io              x86_64          1.2.13-3.2.el7                      docker-ce-stable           25 M
 docker-ce-cli              x86_64          1:19.03.12-3.el7                    docker-ce-stable           38 M

Transaction Summary
================================================================================================================
Install  1 Package (+3 Dependent packages)

Total download size: 88 M
Installed size: 360 M
Is this ok [y/d/N]:

```

* 'y' 를 클릭하여 진행한다.
* docker start

```text
-- boot 시 자동실행하도록 등록
# systemctl enable docker.service

-- docker 실행
# systemctl start docker.service

-- docker 상태
# systemctl status docker.service

● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since 수 2020-09-16 18:11:56 KST; 8s ago
     Docs: https://docs.docker.com
 Main PID: 17086 (dockerd)
    Tasks: 18
   Memory: 44.2M
   CGroup: /system.slice/docker.service
           └─17086 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

 9월 16 18:11:54 epsvr5 dockerd[17086]: time="2020-09-16T18:11:54.662438492+09:00" level=info msg="scheme \"unix\" not registered, fallback t...dule=grpc
 9월 16 18:11:54 epsvr5 dockerd[17086]: time="2020-09-16T18:11:54.662495133+09:00" level=info msg="ccResolverWrapper: sending update to cc: {...dule=grpc
 9월 16 18:11:54 epsvr5 dockerd[17086]: time="2020-09-16T18:11:54.662540409+09:00" level=info msg="ClientConn switching balancer to \"pick_fi...dule=grpc
 9월 16 18:11:55 epsvr5 dockerd[17086]: time="2020-09-16T18:11:55.129760442+09:00" level=info msg="Loading containers: start."
 9월 16 18:11:55 epsvr5 dockerd[17086]: time="2020-09-16T18:11:55.916674576+09:00" level=info msg="Default bridge (docker0) is assigned with ... address"
 9월 16 18:11:56 epsvr5 dockerd[17086]: time="2020-09-16T18:11:56.342015415+09:00" level=info msg="Loading containers: done."
 9월 16 18:11:56 epsvr5 dockerd[17086]: time="2020-09-16T18:11:56.546052469+09:00" level=info msg="Docker daemon" commit=48a66213fe graphdriv...=19.03.12
 9월 16 18:11:56 epsvr5 dockerd[17086]: time="2020-09-16T18:11:56.546357647+09:00" level=info msg="Daemon has completed initialization"
 9월 16 18:11:56 epsvr5 dockerd[17086]: time="2020-09-16T18:11:56.801429819+09:00" level=info msg="API listen on /var/run/docker.sock"
 9월 16 18:11:56 epsvr5 systemd[1]: Started Docker Application Container Engine.
Hint: Some lines were ellipsized, use -l to show in full.

```



