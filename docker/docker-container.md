---
description: docker container 자동실행
---

# docker container 자동실행

### docker container 자동실행 

* 참고 : [https://docs.docker.com/config/containers/start-containers-automatically/](https://docs.docker.com/config/containers/start-containers-automatically/)
* service 파일 생성

```text
# cd /etc/systemd/system
# vi [서비스명].service
[Unit]
Description=docker Service
Wants=docker.service
After=docker.service
Requires=docker.service
 
[Service]
RemainAfterExit=yes
#Restart=always
ExecStart=/usr/bin/docker start [실행할 docker container 이름]
ExecStop=/usr/bin/docker stop [실행할 docker container 이름]
 
[Install]
WantedBy=multi-user.target
```

* systemctl 명령어를 통해서 데몬으로 등록 

```text
# systemctl enable [서비스명].service
```



