# MySQL Create Fiscal Year Fiscal Quarters User Define Functions
In this project, **MySQL user-defined functions** are built to transform **calendar dates** into **Fiscal Years** and **Fiscal Quarters** for financial and business analytics.

## **Why Do We Use This?**
Businesses do not analyze performance based on the **January–December calendar year**.
Instead, financial reporting follows a **Fiscal Year (September-August)** and **Fiscal Quarters (Q1, Q2, Q3, Q4)** because this aligns with budgeting, taxation, and strategic planning.

To simplify this, we can create MySQL functions that return fiscal year and fiscal quarter directly from any date.

## User Define Function 1: Fiscal_Year()
Go to functions tab and right click → create function and write this code:

### Code
```sql
CREATE FUNCTION `get_fiscal_year`(
		calendar_date DATE 
) RETURNS int
    DETERMINISTIC
BEGIN
	DECLARE fiscal_year INT;
    SET fiscal_year = YEAR(DATE_ADD(calendar_date, INTERVAL 4 MONTH));
RETURN fiscal_year;
END
```

### Result
```sql
CREATE DEFINER=`abhishek`@`localhost` FUNCTION `get_fiscal_year`(
		calendar_date DATE 
) RETURNS int
    DETERMINISTIC
BEGIN
	DECLARE fiscal_year INT;
    SET fiscal_year = YEAR(DATE_ADD(calendar_date, INTERVAL 4 MONTH));
RETURN fiscal_year;
END
```

### Explanation
- **Input:** calendar date.
- **Logic:** Increase the given date forward by 4 months.
- **Example:** 2020-09-01 (Sep 1, 2020) → shifted to 2021-01-01.
- **Output:** Returns the year of the Increased date, which represents the Fiscal Year.
- **Example:** If fiscal year starts in September, then:
  - Sept 2020 → Fiscal Year 2021
  - March 2021 → Fiscal Year 2021

 ## User Define Function 2: Quarters()
 ### Code
```sql
CREATE FUNCTION `get_fiscal_quarter`(
		calendar_date DATE
) RETURNS char(2) 
    DETERMINISTIC
BEGIN
	DECLARE M TINYINT;
    DECLARE QTR CHAR(2);
    SET M = MONTH(calendar_date);
		CASE
			WHEN M IN (9,10,11) THEN SET QTR = "Q1";
            WHEN M IN (12,1,2) THEN SET QTR = "Q2";
            WHEN M IN (3,4,5) THEN SET QTR = "Q3";
            WHEN M IN (6,7,8) THEN SET QTR = "Q4";
		END CASE;
RETURN QTR;
END
```

### Result
```sql
CREATE DEFINER=`abhishek`@`localhost` FUNCTION `get_fiscal_quarter`(
		calendar_date DATE
) RETURNS char(2) CHARSET utf8mb4
    DETERMINISTIC
BEGIN
	DECLARE M TINYINT;
    DECLARE QTR CHAR(2);
    SET M = MONTH(calendar_date);
		CASE
			WHEN M IN (9,10,11) THEN SET QTR = "Q1";
            WHEN M IN (12,1,2) THEN SET QTR = "Q2";
            WHEN M IN (3,4,5) THEN SET QTR = "Q3";
            WHEN M IN (6,7,8) THEN SET QTR = "Q4";
		END CASE;
RETURN QTR;
END
```
### Explanation
- **Input:** calendar date.
- **Logic:** Extracts the month number (M) and assigns it to the correct Fiscal Quarter.
  - Sept–Nov → Q1
  - Dec–Feb → Q2
  - Mar–May → Q3
  - Jun–Aug → Q4
- **Output:** Returns Q1, Q2, Q3, or Q4.

### Examples
```sql
SELECT 
	"2020-09-01" as date,
    get_fiscal_year("2020-09-01") as fiscal_year,
    get_fiscal_quarter("2020-09-01")as fiscal_quarter;
```
#### Output:
date       | fiscal_year | fiscal_quarter
2020-09-01 | 2021        |	Q1
