# JSON #

script for updating table element with procedure
```sql
DELIMITER $$
DROP PROCEDURE IF EXISTS updateNumericValues$$
CREATE PROCEDURE updateNumericValues()
BEGIN
    DECLARE count INT DEFAULT 0;
    WHILE count < 6 DO
            SET @idealCapacity = CONCAT('$.keywords[',count,'].idealCapacity');

            UPDATE StatementOfWorkLocal.statements_of_work set your_business = JSON_SET(your_business, @idealCapacity, CAST(JSON_EXTRACT(your_business, @idealCapacity) AS CHAR))
                WHERE CONCAT('', JSON_EXTRACT(your_business, @idealCapacity) * 1) != JSON_EXTRACT(your_business, @idealCapacity);

            SET count = count + 1;
        END WHILE;
END$$
DELIMITER ;

call updateNumericValues();
```

script for updating table element
```sql
UPDATE statement_of_work_snapshots
set your_business = JSON_REPLACE(your_business,
                                 '$.keywords[0].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[0].currentCapacity')) AS CHAR),
                                 '$.keywords[1].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[1].currentCapacity')) AS CHAR),
                                 '$.keywords[2].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[2].currentCapacity')) AS CHAR),
                                 '$.keywords[3].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[3].currentCapacity')) AS CHAR),
                                 '$.keywords[4].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[4].currentCapacity')) AS CHAR),
                                 '$.keywords[5].currentCapacity', CAST(JSON_UNQUOTE(JSON_EXTRACT(your_business, '$.keywords[5].currentCapacity')) AS CHAR));
```