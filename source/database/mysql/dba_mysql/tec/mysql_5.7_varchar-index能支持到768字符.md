# MySQL 5.7.12 开始

> https://dev.mysql.com/doc/refman/5.7/en/create-index.html

## 测试结果

```sql
create table  booboo_db1.t20211018 (id int primary key, a varchar(5000));
alter table booboo_db1.t20211018 add index idx_a768 (a(768));
0 row(s) affected Records: 0  Duplicates: 0  Warnings: 0

alter table booboo_db1.t20211018 add index idx_a769 (a(769));
0 row(s) affected, 1 warning(s): 1071 Specified key was too long; max key length is 3072 bytes Records: 0  Duplicates: 0  Warnings: 1
```

## 官方说明

#### Column Prefix Key Parts

For string columns, indexes can be created that use only the leading part of column values, using `*`col_name`*(*`length`*)` syntax to specify an index prefix length:

- Prefixes can be specified for [`CHAR`](https://dev.mysql.com/doc/refman/5.7/en/char.html), [`VARCHAR`](https://dev.mysql.com/doc/refman/5.7/en/char.html), [`BINARY`](https://dev.mysql.com/doc/refman/5.7/en/binary-varbinary.html), and [`VARBINARY`](https://dev.mysql.com/doc/refman/5.7/en/binary-varbinary.html) key parts.

- Prefixes _must_ be specified for [`BLOB`](https://dev.mysql.com/doc/refman/5.7/en/blob.html) and [`TEXT`](https://dev.mysql.com/doc/refman/5.7/en/blob.html) key parts. Additionally, [`BLOB`](https://dev.mysql.com/doc/refman/5.7/en/blob.html) and [`TEXT`](https://dev.mysql.com/doc/refman/5.7/en/blob.html) columns can be indexed only for `InnoDB`, `MyISAM`, and `BLACKHOLE` tables.

- Prefix _limits_ are measured in bytes. However, prefix _lengths_ for index specifications in [`CREATE TABLE`](https://dev.mysql.com/doc/refman/5.7/en/create-table.html), [`ALTER TABLE`](https://dev.mysql.com/doc/refman/5.7/en/alter-table.html), and [`CREATE INDEX`](https://dev.mysql.com/doc/refman/5.7/en/create-index.html) statements are interpreted as number of characters for nonbinary string types ([`CHAR`](https://dev.mysql.com/doc/refman/5.7/en/char.html), [`VARCHAR`](https://dev.mysql.com/doc/refman/5.7/en/char.html), [`TEXT`](https://dev.mysql.com/doc/refman/5.7/en/blob.html)) and number of bytes for binary string types ([`BINARY`](https://dev.mysql.com/doc/refman/5.7/en/binary-varbinary.html), [`VARBINARY`](https://dev.mysql.com/doc/refman/5.7/en/binary-varbinary.html), [`BLOB`](https://dev.mysql.com/doc/refman/5.7/en/blob.html)). Take this into account when specifying a prefix length for a nonbinary string column that uses a multibyte character set.

  Prefix support and lengths of prefixes (where supported) are storage engine dependent. For example, a prefix can be up to 767 bytes long for [`InnoDB`](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html) tables or 3072 bytes if the [`innodb_large_prefix`](https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#sysvar_innodb_large_prefix) option is enabled. For [`MyISAM`](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html) tables, the prefix length limit is 1000 bytes. The [`NDB`](https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster.html) storage engine does not support prefixes (see [Section 21.2.7.6, “Unsupported or Missing Features in NDB Cluster”](https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster-limitations-unsupported.html)).

As of MySQL 5.7.17, if a specified index prefix exceeds the maximum column data type size, [`CREATE INDEX`](https://dev.mysql.com/doc/refman/5.7/en/create-index.html) handles the index as follows:

- For a nonunique index, either an error occurs (if strict SQL mode is enabled), or the index length is reduced to lie within the maximum column data type size and a warning is produced (if strict SQL mode is not enabled).
- For a unique index, an error occurs regardless of SQL mode because reducing the index length might enable insertion of nonunique entries that do not meet the specified uniqueness requirement.

The statement shown here creates an index using the first 10 characters of the `name` column (assuming that `name` has a nonbinary string type):

```sql
CREATE INDEX part_of_name ON customer (name(10));
```

If names in the column usually differ in the first 10 characters, lookups performed using this index should not be much slower than using an index created from the entire `name` column. Also, using column prefixes for indexes can make the index file much smaller, which could save a lot of disk space and might also speed up [`INSERT`](https://dev.mysql.com/doc/refman/5.7/en/insert.html) operations.
