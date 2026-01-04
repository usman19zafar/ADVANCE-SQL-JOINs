```mermaid
flowchart TD
    A[Table A] -->|Not in B| B[Table B]
```

# ANTI JOIN (NOT EXISTS) — Simple Template

## 1. Purpose
Return rows from A where NO matching rows exist in B.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Subquery table B  
- Third Part: NOT EXISTS condition  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>
FROM <table_1> A
WHERE NOT EXISTS (
    SELECT 1
    FROM <table_2> B
    WHERE A.<join_key_1> = B.<join_key_2>
);
```
