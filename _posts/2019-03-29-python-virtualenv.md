## python 가상환경 

* 독립적인 가상환경 
> python3.7에서는 다음과 같이 별도의 virtualenv 를 설치하지 않고 가상환경을 만들수 있다.
~~~sh
python3 -m venv /path/to/new/virtual/environment
~~~
> 실행예
~~~sh
[agent@host ~]$ python3 -m venv venv3
[agent@host ~]$ source ./venv3/bin/activate
(venv3) [agent@host ~]$
~~~
> virtualenv를 이용해서 python3의 환경을 만들수 있다.
~~~sh
virtualenv -p python3 venv
~~~



