```mermaid
flowchart TD
    A[Table A] -->|All A + matches in B| B[Table B]
    A -.->|Unmatched rows| N[NULLs from B]
```

# LEFT JOIN — Simple Template

## 1. Purpose
Return all rows from A and matching rows from B; unmatched B rows become NULL.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Join table B  
- Third Part: Join condition  
- Fourth Part: Final SELECT  

## 3. Template
```sql
SELECT
    A.<column_list_from_A>,         
    B.<column_list_from_B>
FROM <table_1> A                    
LEFT JOIN <table_2> B               
    ON A.<join_key_1> = B.<join_key_2>;
```
