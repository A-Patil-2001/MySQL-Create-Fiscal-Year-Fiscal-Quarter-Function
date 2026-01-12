# MySQL-Create-Fiscal-Year-Fiscal-Quarter-Function
In this project, **MySQL user-defined functions** are built to transform **calendar dates** into **Fiscal Years** and **Fiscal Quarters** for financial and business analytics.

## **Why Do We Use This?**
Businesses do not analyze performance based on the **January–December calendar year**.
Instead, financial reporting follows a **Fiscal Year (September-August)** and **Fiscal Quarters (Q1, Q2, Q3, Q4)** because this aligns with budgeting, taxation, and strategic planning.

To simplify this, we can create MySQL functions that return fiscal year and fiscal quarter directly from any date.

## Function 1: Fiscal_Year()
Go to functions tab and right click → create function and write this code:

### Code

```
````markdown CREATE FUNCTION ````markdown`get_fiscal_year`(
		calendar_date DATE 
) RETURNS int
    DETERMINISTIC
BEGIN
	DECLARE fiscal_year INT;
    SET fiscal_year = YEAR(DATE_ADD(calendar_date, INTERVAL 4 MONTH));
RETURN fiscal_year;
END
```
