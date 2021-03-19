# docker user 추가

### 가장 간단한 방법

* group 에 사용자 추가하기

```text
## -a : add user into group
## -d : delete user from group
## -r : delete passwd on group
# gpasswd -a [user] [group]
```



### LINUX MINT

* linux mint 에서 docker 를 사용하려면 다음과 같이 입력한다.
* ```text
  $ sudo apt install docker.io
  # 사용자 추가
  $ sudo usermod -aG docker $USER
  ```
* 그런데 위의 명령으로는 $USER 에 그룹이 추가되지 않는다.

  ```text
  $ groups
  그래서 root 계정으로 그룹을 추가하도록 한다.
  ```

* 그러나 linux mint 에서는 설치시 root 에 패스워드가 없으므로 su - 명령으로 접속할 수 없다.

  ```text
  $ sudo grep root /etc/shadow
  root:!:17985:0:99999:7:::
  ```

* ! 부분이 password 부분이다.
* 아래와 같이 입력하여 password 를 입력한다.

  ```text
  $ sudo -i
  root@linuxmint: ~# passwd
  새 UNIX 암호 입력:
  새 UNIX 암호 재입력:
  passwd: 암호를 성공적으로 업데이트했습니다.
  ```

* 또 다른 방법으로는 ACL 권한을 부여하는 것이다.

  ```text
  $ sudo setfacl -m user:$USER:rw /var/run/docker.sock
  ```

