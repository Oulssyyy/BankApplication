| Class | WMC | LCO | Short description of responsibility |
|---|---|---|---|
| Bank | 14 | 393 | Manages a collection of bank accounts, provides operations to add, find, delete accounts, calculate statistics (average, min, max balance), and save/load account data |
| BankAccount | 20 | 405 | Represents a single bank account with balance, withdraw limit, account holder, and provides deposit/withdraw operations |
| Person | 23 | 294 | Represents a person with basic personal attributes (name, gender, age, physical characteristics, contact info). Provides encapsulation through getters/setters with validation for gender and age. Supports multiple initialization methods and string serialization. |
| BankAccountApp | 2 | 447 | Main application class that provides the command-line interface for interacting with the banking system |

## Do you feel its size roughly matches its responsibility?

**Bank**: The size (393 LOC) seems reasonable for its WMC of 14. It handles multiple responsibilities including account management and statistics, which justifies the moderate complexity and size.

**BankAccount**: With WMC=20 and 405 LOC, this class may be slightly over-complicated for representing a single account. The high complexity suggests it might be handling too many concerns beyond basic account operations.

**Person**: This class shows a concerning mismatch - WMC=23 (highest complexity) with only 294 LOC. This suggests many small methods, likely excessive getters/setters for simple attributes. The responsibility description confirms over-engineering with "multiple initialization methods" for what should be a simple data class.

**BankAccountApp**: This is the most problematic - WMC=2 with 447 LOC indicates very few, very large methods. This suggests procedural code concentrated in one or two massive methods rather than proper decomposition, which is a significant code smell for a UI/CLI application.
