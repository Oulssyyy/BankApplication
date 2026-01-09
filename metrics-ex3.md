| Class | LOC | WMC | CBO | LCOM | Quick notes |
|---|---|---|---|---|---|
| Bank | 393 | 14 | 5 | 0 | Higher coupling (CBO 5) but cohesive (LCOM 0); moderate size and complexity |
| BankAccount | 414 | 21 | 4 | 46 | Large, fairly complex for a single account; cohesion is slipping (LCOM 46) |
| Person | 294 | 23 | 4 | 79 | Highest complexity and low cohesion for a simple data holder; likely overloaded with validation/constructors |

**Which class has the highest WMC?** Person (WMC 23).

**Which class has the highest CBO?** Bank (CBO 5).

**Looking at WMC + CBO + LCOM together: which one class would you worry about most for future maintenance, and why?** Person — it has the highest WMC and very high LCOM despite being a simple domain object, implying too many responsibilities and poor cohesion that will make changes risky.
