# SQL

- ## DDL (Data Definition Language)

  - `CREATE`
    - [x] [CREATE DATABASE](#create-database)
    - [ ] CREATE FUNCTION
    - [ ] CREATE INDEX
    - [ ] CREATE PROCEDURE
    - [x] [CREATE TRIGGER](#create-trigger)
    - [x] [CREATE VIEW](#create-view)
    - [x] [CREATE TABLE](#create-table)
  - `RENAME`
    - [x] [RENAME TABLE](#rename-table)
  - `ALTER`

    - [ ] ALTER DATABASE
    - [ ] ALTER FUNCTION
    - [ ] ALTER PROCEDURE
    - [x] [ALTER TABLE](#alter-table)
      - [x] ADD
      - [x] MODIFY
      - [x] DROP
      - [x] RENAME
    - [x] [ALTER VIEW](#alter-view)

  - `DROP`
    - [x] [DROP DATABASE](#drop-database)
    - [ ] DROP FUNCTION
    - [ ] DROP INDEX
    - [ ] DROP PROCEDURE
    - [x] [DROP TABLE](#drop-table)
    - [x] [DROP TRIGGER](#drop-trigger)
    - [x] [DROP VIEW](#drop-view)

- ## DML (Data Manipulation Language)

  Option For **SELECT** after syntax `FROM tbl_name`

  - [x] SELECT

    - [x] [LIMIT](#limit)
    - [ ] [GROUP BY](#group-by)
    - [ ] HAVING
    - [ ] GROUP_CONCAT
    - [ ] JSON_OBJECT
    - [x] [WHERE](#where)
      - [x] AND
      - [x] OR
      - [x] LIKE
      - [ ] BETWEEN
      - [ ] IN
      - [ ] NOT
      - [ ] EXIST

  - [x] [INSERT](#insert)

    - [x] syntax
    - [x] multiple syntax

  - [x] [UPDATE](#update)
  - [x] [DELETE](#delete)
    - [x] WHERE
    - [x] LIMIT
    - [x] EXIST

- ## DCL (Data Control Language)

  - [x] [Create Account](#create-account)
  - GRANT
    - [ ] GRANT SELECT
    - [ ] GRANT UPDATE
    - [ ] GRANT INSERT
    - [ ] GRANT DELETE
  - REVOKE
    - [ ] REVOKE SELECT
    - [ ] REVOKE DELETE
    - [ ] REVOKE INSERT
    - [ ] REVOKE UPDATE

---

## CREATE

- ### CREATE DATABASE

  ```sql
  CREATE DATABASE namedb
  ```

- ### CREATE TRIGGER

  ```sql
  CREATE TRIGGER trigger_name
  [BEFORE | AFTER]
  [INSERT | UPDATE | DELETE]
  ON table_name FOR EACH ROW
  BEGIN
    statement
  END
  ```

  - `trigger_name` merupakan nama dari `TRIGGER` yang akan dibuat
  - `BEFORE / AFTER` menentukan kapan program akan di eksekusi
  - `INSERT / UPDATE / DELETE` menjalankan event di dalam `TRIGGER`
  - `table_name` merupakan dimana table `TRIGGER` berada
  - `statement` sekumpulan perintah ketika event dilakukan
  - `BEGIN / END` jika terdapat perintah `TRIGGER`
  - `OLD` Data yang telah diproses `NEW` Data yang belum diproses

- ### CREATE VIEW

  ```sql
  CREATE VIEW view_name AS
    SELECT columns
      FROM tables
    [WHERE conditions]
  ```

  - `OR REPLACE`
    Optional. If you do not specify this clause and the VIEW already exists, the CREATE VIEW statement will return an error.
  - `view_name`
    The name of the VIEW that you wish to create in MariaDB.
  - `WHERE conditions`
    Optional. The conditions that must be met for the records to be included in the VIEW.

- ### CREATE TABLE

  ```sql
  CREATE TABLE tbl_name (
      create_definition,...
    )
  ```

## RENAME

- ### RENAME TABLE

  ```sql
  RENAME TABLE tbl_name
    TO new_tbl_name
      [, tbl_name2 TO new_tbl_name2] ...
  ```

## ALTER

- ### ALTER TABLE

  - ADD

    ```sql
    ALTER TABLE table_name
      ADD new_column_name column_definition
        [ FIRST | AFTER column_name ]
    ```

  - MODIFY

    ```sql
    ALTER TABLE table_name
      MODIFY column_name column_definition
        [ FIRST | AFTER column_name ]
    ```

  - DROP

    ```sql
    ALTER TABLE table_name
      DROP COLUMN column_name
    ```

  - RENAME

    ```sql
    ALTER TABLE table_name
      CHANGE COLUMN old_name new_name
        column_definition
        [ FIRST | AFTER column_name ]
    ```

- ### ALTER VIEW

  You can modify the definition of a VIEW in MariaDB without dropping it by using the ALTER VIEW statement.

  ```sql
  ALTER VIEW view_name AS
    SELECT columns
      FROM table
        WHERE conditions;
  ```

## DROP

- ### DROP DATABASE

  ```sql
  DROP DATABASE db_name
  ```

- ### DROP TABLE

  ```sql
  DROP TABLE tbl_name
  ```

- ### DROP TRIGGER

  ```sql
  DROP TRIGGER trigger_name
  ```

- ### DROP VIEW

  ```sql
  DROP VIEW view_name
  ```

---

## SELECT

- ### Syntax

  ```sql
  SELECT expressions
  FROM tables
  [WHERE conditions];
  ```

- ### Full Syntax

  _make sure [ ] is option_

  ```sql
  SELECT [ ALL | DISTINCT ]
  expressions
  FROM tables
  [WHERE conditions [AND | OR | LIKE | BETWEEN | IN | NOT]]
  [GROUP BY expressions]
  [HAVING condition]
  [ORDER BY expression [ ASC | DESC ]]
  [LIMIT [offset_value] number_rows | LIMIT number_rows OFFSET offset_value]
  [PROCEDURE procedure_name]
  [INTO [ OUTFILE 'file_name' options
         | DUMPFILE 'file_name'
         | @variable1, @variable2, ... @variable_n ]
  [FOR UPDATE | LOCK IN SHARE MODE];
  ```

- ### WHERE

  ```sql
  SELECT expression FROM tables WHERE conditions;
  ```

  **example**

  ```sql
  SELECT *
  FROM sites
  WHERE site_name = 'kevinaltaf.com';
  ```

- ### AND

  `make sure syntax AND must different table!`

  ```sql
  SELECT *
  FROM sites
  WHERE site_name = 'kevinaltaf.com';
  AND site_id <= 10;
  ```

- ### OR

  - Syntax

    ```sql
    WHERE condition1
    OR condition2
    ...
    OR condition_n;
    ```

  - Example

    ```sql
    SELECT *
    FROM sites
    WHERE site_name = 'CheckYourMath.com'
    OR site_id = 2;
    ```

- ### LIKE

  [More Information About LIKE](https://www.techonthenet.com/mariadb/like.php)

  - Syntax

    ```sql
    expression LIKE pattern [ ESCAPE 'escape_character' ]
    ```

    - `expression`
      A character expression such as a column or field.
    - `pattern`
      A character expression that contains pattern matching. The patterns that you can choose from are:
    - `espace_character`
      Optional. It allows you to test for literal instances of a wildcard character such as % or \_. If you do not provide the escape_character, MariaDB assumes that "\" is the escape_character.

  - Example

    ```sql
    SELECT site_name
    FROM sites
    WHERE site_name LIKE 'Tech%';
    ```

- ### BETWEEN

  ```sql
  SELECT expression FROM tbl_name
    WHERE column
      BETWEEN condition AND condition;
  ```

  - Example

    ```sql
    SELECT * FROM Items
      WHERE total
        BETWEEN 2 AND 5;
    ```

    > 2 and 5 it's range between 2, 3, 4, 5 will show

- ### IN

  ```sql
  SELECT expression FROM tbl_name
    WHERE column
      IN (condition1, condition2, ...);
  ```

  - example

    ```sql
    SELECT * FROM Items
      WHERE `id item`
        IN (1, 2);
    ```

    > will show row `id item` 1 and 2

- ### NOT

  ```sql
  SELECT expression FROM tbl_name
    WHERE NOT condition
  ```

  or

  ```sql
  SELECT expression FROM tbl_name
    WHERE column
      NOT condition;
  ```

  - example

    ```sql
    SELECT * FROM Items
      WHERE `id item`
        NOT IN (1, 2);
    ```

    > will `not` show row `id item` 1 and 2

    or

    ```sql
    SELECT * FROM Items
      WHERE `id item`
        IS NOT NULL
    ```

    > will not show `id item` which null

- ### EXIST

  - example

    ```sql
    SELECT COUNT(*) FROM sites
    WHERE EXISTS
      ( SELECT *
        FROM pages
        WHERE pages.site_id = sites.site_id
        AND site_id <= 45 );
    ```

- ### LIMIT

  > nb: you can use this for `Many DML`

  ```sql
  SELECT expression FROM tbl_name
    LIMIT condition
  ```

  example

  ```sql
  SELECT ProdukID FROM produk LIMIT 3
  ```

- ### GROUP BY

  ```sql
  SELECT expression FROM tbl_name
    GROUP BY condition
  ```

  example

  ```sql
  SELECT ProdukID
  ```

- ### HAVING

- ### GROUP CONCAT

  ```sql
  SELECT
    GROUP_CONCAT(
      DISTINCT expression
      ORDER BY expression
      SEPARATOR symbol
    ) FROM tbl_name;
  ```

- ### INSERT

  - syntax

    ```sql
    INSERT INTO table
    (column1, column2, ... )
    VALUES
    (expression1, expression2, ... ),
    (expression1, expression2, ... ),
    ...;
    ```

  - multiple syntax

    ```sql
    INSERT INTO table
    (column1, column2, ... )
    SELECT expression1, expression2, ...
    FROM source_table
    [WHERE conditions];
    ```

  - example multiple syntax

    ```sql
    INSERT INTO contacts
    (contact_id, contact_name)
    SELECT site_id, site_name
    FROM sites
    WHERE site_name = 'kevinaltaf.com';
    ```

- ## UPDATE

  - syntax

    ```sql
    UPDATE table1
    SET column1 = (SELECT expression1
                   FROM table2
                   WHERE conditions)
    [WHERE conditions];
    ```

  - complite syntax

    ```sql
    UPDATE table
    SET column1 = expression1,
        column2 = expression2,
        ...
    [WHERE conditions]
    [ORDER BY expression [ ASC | DESC ]]
    [LIMIT number_rows];
    ```

  - example

    ```sql
    UPDATE sites
    SET site_name = 'kevinaltaf.com'
    WHERE id_site = 1;
    ```

- ## DELETE

  - syntax

    ```sql
    DELETE FROM table
    [WHERE conditions]
    [ORDER BY expression [ ASC | DESC ]]
    [LIMIT number_rows];
    ```

  - example

    ```sql
    DELETE FROM sites
    WHERE id_sites = 1;
    ```

  - multiple syntax example

    ```sql
    DELETE FROM sites
    WHERE site_name = 'kevinaltaf.com'
    AND site_id >= 65;
    ```

  - `EXIST`

    ```sql
    DELETE FROM sites
    WHERE EXISTS
      ( SELECT *
        FROM pages
        WHERE pages.site_id = sites.site_id
        AND site_id <= 45 );
    ```

- ### CREATE ACCOUNT

  ```sql
  CREATE USER 'newuser'@'10.8.0.5' IDENTIFIED BY 'user_password';
  ```

  To create a user that can connect from any host, use the '%' wildcard as a host part:

  ```sql
  CREATE USER 'newuser'@'%' IDENTIFIED BY 'user_password';
  ```

  <https://linuxize.com/post/how-to-create-mysql-user-accounts-and-grant-privileges/>
