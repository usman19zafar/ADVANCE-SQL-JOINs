# Window Functions + JOIN — Simple Template

## Diagram
```mermaid
B[Table B - Windowed]
B[Table B Windowed]
B[Table B: Windowed]
B["Table B (Windowed)"]   <-- also valid because quotes protect it

```

1. Purpose
Join two tables where one side uses window functions to compute analytical metrics before joining.

2. Four-Part Flow
First Part: Main table A

Second Part: Windowed table B

Third Part: Join condition

Fourth Part: Final SELECT

WITH Bx AS (                                      -- Second Part
    SELECT
        B.<join_key>,
        B.<column_list_from_B>,
        ROW_NUMBER() OVER (                       -- Window Function
            PARTITION BY B.<partition_key>
            ORDER BY B.<sort_key> DESC
        ) AS rn
    FROM <table_2> B
)
SELECT
    A.<column_list_from_A>,                       -- Fourth Part
    Bx.<column_list_from_B>,
    Bx.rn
FROM <table_1> A                                   -- First Part
INNER JOIN Bx                                      -- Second Part (windowed table)
    ON A.<join_key> = Bx.<join_key>;               -- Third Part
