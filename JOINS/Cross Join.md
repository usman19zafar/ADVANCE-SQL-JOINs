```mermaid
flowchart TD
    A[Table A] --- B[Table B]
```

# CROSS JOIN — Simple Template

## 1. Purpose
Return the Cartesian product of both tables.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Join table B  
- Third Part: (No condition)  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>,         
    B.<column_list_from_B>
FROM <table_1> A                    
CROSS JOIN <table_2> B;
```
