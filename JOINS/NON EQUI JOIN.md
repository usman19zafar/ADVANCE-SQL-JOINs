```mermaid
flowchart TD
    A[Table A] -->|Range or inequality| B[Table B]
```

# NON EQUI JOIN — Simple Template

## 1. Purpose
Join tables using non‑equality conditions (>, <, BETWEEN).

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Join table B  
- Third Part: Non‑equality condition  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>,
    B.<column_list_from_B>
FROM <table_1> A
JOIN <table_2> B
    ON A.<value> BETWEEN B.<min_value> AND B.<max_value>;
```
