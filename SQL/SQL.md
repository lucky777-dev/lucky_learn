# SQL

# CREATE (create table)

```sql
CREATE TABLE test (
    tId char(7) NOT NULL CONSTRAINT idPK PRIMARY KEY,
    tName varchar(14) NOT NULL,
    tAge int DEFAULT 18 NOT NULL,
    tWeight decimal(4, 1) NULL,
    CONSTRAINT tAgeC CHECK(tAge > 16 AND tAge < 140),
    CONSTRAINT tWeightC CHECK(tWeight BETWEEN 20 AND 300)
    );
```

> - **`char(7)`**<br>
7 characters (no more no less).
> - **`varchar(14)`**<br>
Maximum 14 characters.
> - **`decimal(4, 1)`**<br>
Decimal number with 4 digits and only one after coma.<br>
*(From `0.0` to `999.9` in this case)*<br>
This has `NULL` parameter, so `tWeight` is **optional**.
> - **`DEFAULT`**<br>
This will set the default value on creation of an attribute.


# DROP (delete table)

```sql
DROP TABLE test;
```

> - **`DROP TABLE`**<br>
This request will delete the table.