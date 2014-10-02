# MySQL Index

## [MySQL uses indexes for these operations](http://dev.mysql.com/doc/refman/5.5/en/mysql-indexes.html)
- To find the rows matching a **WHERE** clause quickly. (to operators such as =, >, ≦, BETWEEN, IN, and so on, in a WHERE clause)
- To eliminate rows from consideration. If there is a choice between multiple indexes, MySQL normally uses the index that finds the smallest number of rows (the most selective index).
- To retrieve rows from other tables when performing joins.
- To find the MIN() or MAX() value for a specific indexed column key_col.
- To sort or group a table if the sorting or grouping is done on a leftmost prefix of a usable key (for example, ORDER BY key_part1, key_part2). If all key parts are followed by DESC, the key is read in reverse order.

## [Multi-column index](http://dev.mysql.com/doc/refman/5.5/en/multiple-column-indexes.html)
- if you have a three-column index on (col1, col2, col3), you have indexed search capabilities on (col1), (col1, col2), and (col1, col2, col3).
Suppose that a table has the following specification:
```sql
CREATE TABLE test (
    id         INT NOT NULL,
    last_name  CHAR(30) NOT NULL,
    first_name CHAR(30) NOT NULL,
    PRIMARY KEY (id),
    INDEX name (last_name,first_name)
);
```

The name index is used for lookups in the following queries:
```sql
SELECT * FROM test WHERE last_name='Widenius';

SELECT * FROM test
  WHERE last_name='Widenius' AND first_name='Michael';

SELECT * FROM test
  WHERE last_name='Widenius'
  AND (first_name='Michael' OR first_name='Monty');

SELECT * FROM test
  WHERE last_name='Widenius'
  AND first_name >='M' AND first_name < 'N';
```

However, the name index is **NOT** used for lookups in the following queries:
```sql
SELECT * FROM test WHERE first_name='Michael';

SELECT * FROM test
  WHERE last_name='Widenius' OR first_name='Michael';
```
