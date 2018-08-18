# MySQL Transaction Isolation Levels

Describe and test the transaction isolation levels in MySQL InnoDB.

### Three Read Phenomena

- Dirty Read
- Non-Repeatable Read
- Phantom Read

### Four Isolation Levels

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable

### Isolation Levels vs Read Phenomena

|                    | Dirty reads | Non-repeatable reads | Phantoms    |
| ------------------ | ----------- | -------------------- | ----------- |
| `Read Uncommitted` | may occur   | may occur            | may occur   |
| `Read Committed`   | don't occur | may occur            | may occur   |
| `Repeatable Read`  | don't occur | don't occur          | may occur   |
| `Serializable`     | don't occur | don't occur          | don't occur |

### Try it yourself

```sql
create table users (
    id int primary key,
    name varchar(100)
);

insert into users(id, name) values(1, 'alice');
insert into users(id, name) values(2, 'billy');
insert into users(id, name) values(3, 'chris');
```

1. `Dirty Reads` occur in `Read Uncommitted` level.

![Dirty-Reads-occur-in-Read-Uncommitted-level](1-Dirty-Reads-occur-in-Read-Uncommitted-level.jpg?raw=true)

2. `Dirty Reads` don't occur in `Read Committed` level.

![Dirty-Reads-dont-occur-in-Read-Committed-level](2-Dirty-Reads-dont-occur-in-Read-Committed-level.jpg?raw=true)

3. `Non-Repeatable Reads` occur in `Read Committed` level.

![Non-Repeatable-Reads-occur-in-Read-Committed-level](3-Non-Repeatable-Reads-occur-in-Read-Committed-level.jpg?raw=true)

4. `Non-Repeatable Reads` don't occur in `Repeatable Read` level.

![Non-Repeatable-Reads-dont-occur-in-Repeatable-Read-level](4-Non-Repeatable-Reads-dont-occur-in-Repeatable-Read-level.jpg?raw=true)

5. `Phantom Reads` don't occur in `Repeatable Read` level if `SELECT` only.

![Phantom-Reads-dont-occur-in-Repeatable-Read-level-if-SELECT-only](5-Phantom-Reads-dont-occur-in-Repeatable-Read-level-if-SELECT-only.jpg?raw=true)

> It is more restrictive in `Repeatable Read` level of MySQL than SQL Standard, but it doesn't means MySQL prevents `Phantom Reads` entirely in `Repeatable Read` level. See the following Part 6.

6. `Phantom Reads` occur in `Repeatable Read` level after `UPDATE`.

![Phantom-Reads-occur-in-Repeatable-Read-level-after-UPDATE](6-Phantom-Reads-occur-in-Repeatable-Read-level-after-UPDATE.jpg?raw=true)

7. `Phantom Reads` don't occur in `Serializable` level.

![Phantom-Reads-dont-occur-in-Serializable-level-1](7-Phantom-Reads-dont-occur-in-Serializable-level-1.jpg?raw=true)

![Phantom-Reads-dont-occur-in-Serializable-level-2](7-Phantom-Reads-dont-occur-in-Serializable-level-2.jpg?raw=true)


### References
- [Isolation - Wikipedia](https://en.wikipedia.org/wiki/Isolation_(database_systems))