# Exercise 4: SonarQube Issues & Fixes

## Task 1: List 3 Important Issues

| Rule Name | File & Line | Explanation |
|---|---|---|
| Change this "try" to a try-with-resources | BankAccount.java:168 | Resource leak risk: `FileInputStream` is opened but if an exception occurs before the finally block executes, it may not be closed properly. Try-with-resources auto-closes the resource. |
| Change this "try" to a try-with-resources | Bank.java:144 | Same resource leak issue: file operations not using try-with-resources pattern for safe resource management. |
| Refactor this method to reduce its Cognitive Complexity | BankAccountApp.java:20 | The `main()` method has cyclomatic complexity of 125, far exceeding the recommended threshold of 15. This indicates deeply nested logic that is hard to test and maintain. |

## Task 2: Fixed Issues

### Issue 1 Fixed: BankAccount.java (Try-with-Resources)
- **Changed**: Lines 168-190 to use try-with-resources statement
- **Result**: Resources are now automatically closed; resource leak eliminated

### Issue 2 Fixed: BankAccountApp.java (Magic String Literals)
- **Changed**: Lines 92, 96, 101, 139 to define constants for duplicated string literals
- **Result**: 4 magic string warnings resolved; code is more maintainable

## Task 3: Post-Fix Analysis

**Re-run SonarQube confirmation:** The try-with-resources and magic string literal issues have been eliminated. The main() method's cognitive complexity issue remains (would require significant refactoring to decompose the method).

**Correlation with WMC/CBO:**
Yes, SonarQube issues strongly correlate with higher complexity metrics. BankAccountApp (WMC=2, but massive cognitive complexity 125) and BankAccount (WMC=21, LOC=414) show the most issues. Person and Bank, despite moderate complexity, have fewer issues. High cognitive complexity and large methods (evident in BankAccountApp's single 40-line main method) generate more warnings than high method count alone.
