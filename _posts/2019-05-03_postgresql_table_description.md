---
layout: post
title: postgresql table and column description 
date: 2019-05-03 11:00:00 +0900
categories: postgresql
---

## PostgreSQL 의 테이블과 컬럼을 조회하는 쿼리
* pd.objsubid = 0 이면 table 만 조회
* pd.objsubid > 0 이면 column 만 조회

~~~ sql
SELECT psu.relname    AS table_nm
     , pa.attname     AS column_nm
     , pd.description AS desc 
     , pd.objsubid
  from pg_catalog.pg_stat_user_tables   psu
       left outer join pg_catalog.pg_description pd on psu.relid = pd.objoid
       left outer join pg_catalog.pg_attribute   pa on (pd.objoid = pa.attrelid and pd.objsubid = pa.attnum)
 WHERE 1=1
   AND pd.objsubid = 0   -- table only
--   AND pd.objsubid > 0   -- column only
   AND psu.schemaname  = {schema name}
   AND psu.relname = {table name}
ORDER BY psu.relname, pd.objsubid
;   
~~~

