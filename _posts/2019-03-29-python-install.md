## python source로 설치하기 
> 기본적으로 아직까지는 Linux를 설치하면 python 버전이 2.x 이기 때문에 
> 만일 python3.x 를 사용하고자 한다면 별도로 설치를 해주어야 한다.

* source compile을 위해 root 권한으로 다음을 실행해 준다.
~~~sh
# yum -y groupinstall development
# yum -y install zlib-devel
~~~

* python download
~~~sh
# wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tar.xz
# tar xJfv Python-3.7.3.tar.xz
# cd Python-3.7.3
# ./configure
# make
# make install
~~~

> 만일 make install 설치중 <b>ImportError: No module named '_ctypes'</b> 오류가 난다면 다음을 실행한다.
~~~sh
# yum install libffi-devel
~~~
> 설치된 위치를 확인한다.
~~~sh
# which python3
~~~
> python3 을 실행한다.
~~~sh
$ python3
Python 3.7.3 (default, Mar 29 2019, 10:26:59)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-36)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
$
~~~

