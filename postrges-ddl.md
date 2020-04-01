# postrges DDL

### column

```text
-- column rename
alter table {table} rename {old column} to {new column}

-- column data type
alter table {table} alter column {column} type {data type}

-- default value create
alter table {table} alter column {column} set default {value}

-- default value drop
alter table {table} alter column {column} drop default

-- not null 
alter table {table} alter column {column} set not null
alter table {table} alter column {column} drop not null

-- column drop
alter table {table} drop column {column}
```

