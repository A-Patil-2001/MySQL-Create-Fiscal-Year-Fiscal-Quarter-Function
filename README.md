# MySQL-Create-Fiscal-Year-Fiscal-Quarter-Function
In this project, **MySQL user-defined functions** are built to transform **calendar dates** into **Fiscal Years** and **Fiscal Quarters** for financial and business analytics.

## **Why Do We Use This?**
Businesses do not analyze performance based on the **January–December calendar year**.
Instead, financial reporting follows a **Fiscal Year (September-August)** and **Fiscal Quarters (Q1, Q2, Q3, Q4)** because this aligns with budgeting, taxation, and strategic planning.

To simplify this, we can create MySQL functions that return fiscal year and fiscal quarter directly from any date.

## Function 1: Fiscal_Year()
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

- **Logic:** Shifts the given date forward by 4 months.

- **Example:** 2020-09-01 (Sep 1, 2020) → shifted to 2021-01-01.
- **Output:** Returns the year of the shifted date, which represents the Fiscal Year.
-- If fiscal year starts in September, then:
--- Sept 2020 → Fiscal Year 2021
--- March 2021 → Fiscal Year 2021
