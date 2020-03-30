---
description: 'download : https://www.postgresql.org/download/'
---

# postgesql install

## CentOS Install

```text
$ yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
$ yum install postgresql11
$ yum install postgresql11-server
$ /usr/pgsql-11/bin/postgresql-11-setup initdb
$ systemctl enable postgresql-11
$ systemctl start postgresql-11
```

#### 설정파

```text
$ ls -al /usr/pgsql-11/share/pg_hba.conf
$ vi /var/lib/pgsql/11/data/pg_hba.conf
```

#### Restart

```text
$ sudo systemctl restart postgresql-11
```

#### postgres password 변경

```text
$ sudo -u postgres psql
$ alter user postgres with encrypted password 'password';
```

#### 사용자 

```text
$ createuser jira --interactive

Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n

$ createuser confluence --interactive
$ createuser bamboo --interactive
$ createuser bitbucket --interactive
```

or

```text
CREATE USER confluence WITH ENCRYPTED PASSWORD 'secret123';
```

#### Database 

```text
$ sudo -i -u postgres

$ createdb jiradb -O jira --encoding='utf-8' --locale=en_US.utf8 --template=template0
$ createdb confluencedb -O confluence --encoding='utf-8' --locale=en_US.utf8 --template=template0
$ createdb bamboodb -O bamboo --encoding='utf-8' --locale=en_US.utf8 --template=template0
$ createdb bitbucketdb -O bitbucket --encoding='utf-8' --locale=en_US.utf8 --template=template0
```

or 

```text
$ sudo -i -u postgres psql

postgres=# CREATE DATABASE jiradb OWNER jira ENCODING 'utf-8';
postgres=# CREATE DATABASE confluencedb OWNER confluence ENCODING 'utf-8';
postgres=# CREATE DATABASE bamboodb OWNER bamboo ENCODING 'utf-8';
postgres=# CREATE DATABASE bitbucketdb OWNER bitbucket ENCODING 'utf-8';
```

#### Connect 

```text
$ psql -U confluence -d confluencedb  -W -h localhost
```

> * -U : username
> * -d : database name
> * -W : password 사용
> * -h: 연결할 호스트. 제외할 경우 "peer authentication failed" 에러 발생 가능

