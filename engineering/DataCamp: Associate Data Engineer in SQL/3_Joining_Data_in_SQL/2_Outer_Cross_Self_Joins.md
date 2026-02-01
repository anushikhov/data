## Outer Joins, Cross Joins and Self Joins  

**LEFT JOIN will return all records in the left table, and those records in the right table that match on the joining field provided.**    
  

| id            | left\_val     |
| ------------- |:-------------:|
| 1             | L1            |
| 2             | L2            |
| 3             | L3            |  
| 4             | L4            |  

   left table                                   right table
| id | left\_val |                          | id | right\_val |
|----------------|                          |:---------------:| 
| 1  | L1        |                          | 1  | R1         |
| 2  | L2        |                          | 4  | R2         |
| 3  | L3        |                          | 5  | R3         |
| 4  | L4        |                          | 6  | R4         |
  


