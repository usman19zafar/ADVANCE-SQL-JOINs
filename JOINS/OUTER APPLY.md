```mermaid
flowchart TD
    A[Table A] -->|Optional row-by-row| B[Derived Table]
```

# OUTER APPLY — Simple Template

## 1. Purpose
Apply a subquery to each row of A, returning NULLs when no match exists.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Lateral subquery B  
- Third Part: Condition inside subquery  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>,
    B.<column_list_from_B>
FROM <table_1> A
OUTER APPLY (
    SELECT <column_list_from_B>
    FROM <table_2>
    WHERE <conditions_using_A>
) B;
```
