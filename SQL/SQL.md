- [SQL](#sql)
  * [Languages](#languages)
- [DML](#dml)
  * [Structure](#structure)
  * [SELECT](#select)
    + [DISTINCT](#distinct)
  * [WHERE](#where)
    + [IN](#in)
    + [BETWEEN](#between)
    + [LIKE](#like)
    + [null](#null)
  * [Agregates](#agregates)
    + [COUNT(...)](#count--)
    + [SUM(...)](#sum--)
    + [AVG(...)](#avg--)
    + [MAX(...)](#max--)
    + [MIN(...)](#min--)
- [DDL](#ddl)
  * [CREATE](#create)
- [DROP (delete table)](#drop--delete-table-)

---

# SQL

## Languages

> `SQL: `Structured Query Language<br>
`DML: `Data Manipulation Language *`(INSERT/SELECT/UPDATE/DELETE)`*<br>
`DDL: `Data Definition Language *`(create/delete tables or columns)`*<br>
`DCL: `Data Control Language *`(tables access permissions)`*

# DML

Data Manipulation Language

## Structure

```sql
SELECT [DISCTINCT] {expressions} [AS nickname]
 FROM [tables] [AS nickname]
    [WHERE condition]
    [GROUP BY {attributes}]
    [HAVING condition]
    [ORDER BY {attributes} [ASC/DESC]];
           or {column_nbr} [ASC/DESC]];
```

## SELECT

`Selection in a data base.`

```sql
SELECT id, lastname
 FROM customer;
```
> The result will be a list with all customer IDs and names.

```sql
SELECT *
 FROM my_table;
```
> The result will be a list with all lines of the table.*my_table*

### DISTINCT

`No duplicates.`

```sql
SELECT DISTINCT city AS city
 FROM customer;
```
> The result will be a list with all the cities of the customers, but <u>without duplicates</u>.<br>
So even if more than one customer lives in `Brussels`, we will see it only once in our resulting list.<br>
The column `customer_city` of the resulting list will be named `city`.

## WHERE

`Condition.`

```sql
SELECT lastname, city, code
 FROM customer
    WHERE city == 'Brussels' AND code != 1070;
```
> The result will be a list with the name, city and code of all customers who live in `Brussels`, but **not** in the town with the postal code `1000`.

### IN

```sql
SELECT lastname, city
 FROM customer
    WHERE city in ('Brussels', 'Liege', 'Antwerp');
```
> The result will be a list with the name and the city of all customers who live in `Brussels`, `Liege` or `Antwerp`.

### BETWEEN

```sql
SELECT lastname, age
 FROM customer
    WHERE age BETWEEN 18 AND 25;
```
> The result will be a list with the name of the customers from `18` to `25` years old.

### LIKE

```sql
SELECT lastname, cat
 FROM customer
    WHERE lastname LIKE '%x%' AND cat LIKE 'B_';
    /*
    Equivalence in Linux:
        %x%  =>  *x*
        B_   =>   B?
```
> The result will be a list with the name and the category of all customers with a `e` in their name and with a category of two letters, starting with a `B`.
>> Examples for lastname:
>>  - `somethingxelse` *ok*<br>
>>  - `xs` *ok*<br>
>>  - `testxxx` *ok*<br>
>>  - `x` *ok*<br>
>>  - `blbl` *not ok!*
>
>> Examples for cat:
>>  - `BA` *ok*<br>
>>  - `B2` *ok*<br>
>>  - `BAA` *not ok!*<br>
>>  - `2A` *not ok!*<br>

```sql
SELECT product_name AS Product, 0.21*price AS Taxe
 FROM product;
    /*
    price = price of the product
    taxe = 21% of the price
    */
```
> The result will be a list with the `name` and the `Taxe` of all products.

### null

```sql
SELECT *
 FROM customer
    WHERE city IS null AND code IS NOT null;
      /*
      city == null -> NOT GOOD
      code != null -> NOT GOOD
      */
```
> `null` can't be compared to anything, not even with itself.<br>
We need to use the word `IS` instead of `=`.

## Agregates

### COUNT(...)

`Line counting.`

```sql
SELECT COUNT(lastname)
 FROM customer;
```
> The result will be a list with the `count` of lines where lastname is `non-null`.

```sql
SELECT COUNT(DISTINCT city)
 FROM customer;
```
> The result will be a list with the `count` of lines where city is `non-null`, but <u>without counting twice the same city</u>.

### SUM(...)

`Sum of values.`

```sql
SELECT SUM(price)
 FROM product;
```
> The result will be a line with the `sum` of the price of all products in the table.<br>
If we have 3 products at 5€, the result will be 15.

### AVG(...)

`Average of values.`

```sql
SELECT AVG(price)
 FROM product;
```
> The result will be a line with the `average price` of all products in the table.<br>
If we have 1 product at 10€, 1 at 15€ and one at 20€, the result will be 15.

### MAX(...)

`Maximum value.`

```sql
SELECT MAX(price)
 FROM product;
```
> The result will be a line with the `maximum price` of all products in the table.<br>
If we have 1 product at 10€, 1 at 15€ and one at 20€, the result will be 20.

### MIN(...)

`Minimum value.`

```sql
SELECT MIN(price)
 FROM product;
```
> The result will be a line with the `minimum price` of all products in the table.<br>
If we have 1 product at 10€, 1 at 15€ and one at 20€, the result will be 10.





# DDL

Data Definition Language

## CREATE

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