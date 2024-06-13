row => tuple, entity\
column => attribute\
cell => field

# Normalization

https://www.geeksforgeeks.org/types-of-normal-forms-in-dbms/ \
https://en.wikipedia.org/wiki/Database_normalization \
https://www.javatpoint.com/dbms-normalization

__Unnormalized form (UNF):__

__First Normal Form (1NF):__\
Each field/cell contains a single/atomic value. A field/cell must not contain a set of values or a nested record.

__Second Normal Form (2NF):__\
No partial dependence. When a column completely depends on PK.\
Partial dependence. When a column depends on one part of a composite key, but not on the whole key.

__Third Normal Form (3NF):__\
No transitive dependence. When a column depends more on another column rather than PK.

Enchanced 3NF | Boyce-Codd Normal Form (BCNF). 

__Fourth normal form (4NF):__\
No multi-valued dependency.

__Fifth normal form (5NF):__\
No join dependency.

__Sixth normal form (6NF):__\
Is not used in real systems.