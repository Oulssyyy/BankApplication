# Exercise 5: Java Report GitHub Actions Workflow

## Workflow Created: `.github/workflows/java-report.yml`

This GitHub Actions workflow performs the following tasks:

### Steps:

1. **Checkout Code**
   - Uses `actions/checkout@v3` to fetch the repository

2. **Check for Committed `.class` Files**
   - Scans for any `*.class` files outside of `target/` and `.git/` directories
   - **Fails the workflow** if any `.class` files are found (enforcing best practice)
   - Prints results to console

3. **Validate Java Files Exist**
   - Counts total `.java` files in the repository
   - **Fails the workflow** if count is zero (no Java files found)

4. **Generate Java File Report**
   - Outputs to `java-file-report.txt`:
     - Total count of `.java` files
     - Total lines of code across all files
     - Per-file breakdown sorted by line count (descending):
       - File path and line count for each `.java` file

5. **Upload Artifact**
   - Uses `actions/upload-artifact@v3` to upload `java-file-report.txt`
   - Artifact name: `java-file-report`
   - Retention: 30 days

### Triggers:
- Runs on push to `main`, `master`, or `develop` branches
- Runs on pull requests to `main`, `master`, or `develop` branches

### Sample Output:
The report will contain a format like:
```
====================
JAVA FILE REPORT
====================

Total Java Files: 7
Total Lines of Code: 2547

====================
PER-FILE BREAKDOWN
====================
jay-bank/src/main/java/bankAccountApp/BankAccountApp.java -- 225 lines
jay-bank/src/main/java/bankAccountApp/BankAccount.java -- 198 lines
jay-bank/src/main/java/bankAccountApp/Bank.java -- 310 lines
...
```
