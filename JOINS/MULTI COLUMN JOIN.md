```mermaid
flowchart TD
    A[Table A] -->|Multiple keys| B[Table B]
```

# MULTI COLUMN JOIN — Simple Template

## 1. Purpose
Join tables using more than one column.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Join table B  
- Third Part: Multiple join conditions  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>,
    B.<column_list_from_B>
FROM <table_1> A
JOIN <table_2> B
    ON A.<key1> = B.<key1>
   AND A.<key2> = B.<key2>;
```
