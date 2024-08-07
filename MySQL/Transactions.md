# Autocommit. When each statement is run as transaction

https://www.youtube.com/watch?v=GOQVlrQohtM \
https://dev.mysql.com/doc/refman/8.0/en/innodb-autocommit-commit-rollback.html

<img width="653" alt="01" src="https://github.com/VIK2395/Databases/assets/50545334/760b95c3-5f4d-4258-ac77-d7a150247482">

```mysql
# Global scope
SET @@GLOBAL.autocommit = 0;
# Session scope
SET @@SESSION.autocommit = 0;
# Next transaction only
SET @@autocommit = 0;

# Global scope
SELECT @@GLOBAL.autocommit = 0;
# Session scope
SELECT @@SESSION.autocommit = 0;
# Next transaction only
SELECT @@autocommit = 0;
```

# Locks and isolation levels
https://retool.com/blog/isolation-levels-and-locking-in-relational-databases

https://www.youtube.com/watch?v=S3XbZzqPS3g&list=PLd5sTGXltJ-l9PKT2Bynhg0Ou2uESOJiH&index=17 \
https://www.youtube.com/watch?v=ER8oKX5myE0

__Read Phenomena:__

https://en.wikipedia.org/wiki/Isolation_(database_systems) \
https://learn.microsoft.com/en-us/sql/odbc/reference/develop-app/transaction-isolation-levels?view=sql-server-ver16

- Dirty Reads;
- Non Repeatable read;
- Phantom Read;

__Isolation levels:__

![image](https://github.com/VIK2395/Databases/assets/50545334/24a03409-3204-4f67-8f5a-0369c2ed4262)
SQL standard defines four isolation levels that prevents the phenomena above:
- Read Uncommitted;
- Read Committed;
- Repeatable Read;
- Serializable;

https://www.baeldung.com/sql/mysql-lock-wait-timeout-error#isolation-level
![image](https://github.com/VIK2395/Databases/assets/50545334/3a73dc0e-984e-4d7e-97bd-046dd7e0305b)

In the following table, an "X" marks each phenomenon that can occur.
![image](https://github.com/VIK2395/Databases/assets/50545334/4e16acaf-fa3f-4d59-ae25-e550e702ee8a)

![image](https://github.com/VIK2395/Databases/assets/50545334/a3dd5b36-0859-43a6-85df-0b192854aac6)

https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/

An isolation level represents a particular locking strategy employed in the database system to improve data consistency. The higher the isolation level, the more complex the locking strategy behind it. Type of locks used described below. \
https://docs.actian.com/zen/v14/index.html#page/adonet/isolation.htm

```mysql
# Global scope
SET GLOBAL TRANSACTION ISOLATION LEVEL <READ UNCOMMITED | READ COMMITED | REPEATABLE READ | SERIALIZABLE>;
# Session scope
SET SESSION TRANSACTION ISOLATION LEVEL <READ UNCOMMITED | READ COMMITED | REPEATABLE READ | SERIALIZABLE>;
# Next transaction only
SET SESSION TRANSACTION ISOLATION LEVEL <READ UNCOMMITED | READ COMMITED | REPEATABLE READ | SERIALIZABLE>;

# Global scope
SELECT @@GLOBAL.transaction_isolation;
# Session scope
SELECT @@SESSION.transaction_isolation;
# Next transaction only
SELECT @@transaction_isolation;
```

__Lock modes(types):__
- Shared lock (S);
- Exclusive lock (X);
- Intention shared lock (IS);
- Intention exclusive lock (IX);\
.\
.\
.

https://dev.mysql.com/doc/refman/8.4/en/innodb-locking.html \
https://mariadb.com/kb/en/innodb-lock-modes/

Shared lock -> Prevents others from updating the data. Shared lock is also called read lock. It allows simultaneous read by multiple transactions (this is why it is called Shared). When read lock is held, then not write can occur. Write will await until read lock is released. Read lock can be owned/acquired by multiple transactions at a time(further reinforces the calling Shared).

Exclusive lock -> Prevents others from reading and updating the data. Also called write lock. Read and write will await until the write lock is released. Write lock can be owned/acquired by only one transaction at a time(this is why it is called Exclusive).

Intensive locks -> more granularity locks that allow coexistence of table locks and __row locks__

![image](https://github.com/VIK2395/Databases/assets/50545334/5f1d69c5-ece5-4f61-8954-78605598902a)
![image](https://github.com/VIK2395/Databases/assets/50545334/53094fe4-117a-4cf9-864e-a853d26e8fac)

https://www.geeksforgeeks.org/levels-of-locking-in-dbms/ \
https://www.sqlpassion.at/archive/2016/05/16/why-do-we-need-intent-locks-in-sql-server/ \
https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html \
https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-model.html

# About dead locks
https://www.youtube.com/watch?v=y5h3mI9OvOI (30:50)

When dead lock happens, the both transactions get rollback (NOT TRUE => CHECKED).\
When dead lock happens, only the transaction that got dead lock gets rollback. The other continues.

# LOCK WAIT TIMEOUT
https://dev.mysql.com/doc/refman/8.4/en/innodb-parameters.html#sysvar_innodb_lock_wait_timeout
https://www.baeldung.com/sql/mysql-lock-wait-timeout-error#testing-scenarios

```mysql
# Global scope, in seconds
SET @@GLOBAL.innodb_lock_wait_timeout = 10;
# Session scope
SET @@SESSION.innodb_lock_wait_timeout = 10;
# Next transaction only
SET @@innodb_lock_wait_timeout = 10;

# Global scope
SELECT @@GLOBAL.innodb_lock_wait_timeout;
# Session scope
SELECT @@SESSION.innodb_lock_wait_timeout;
# Next transaction only
SELECT @@innodb_lock_wait_timeout;
```

__Two phase commit:__\
https://en.wikipedia.org/wiki/ACID \
https://www.geeksforgeeks.org/two-phase-locking-protocol/
