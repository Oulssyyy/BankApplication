# Exercise 6: Maven Project Configuration

## Task: Convert BankApplication to Maven Project

### Changes Made:

**Updated `pom.xml` with required coordinates:**
```xml
<groupId>com.imt.mines</groupId>
<artifactId>bank-application</artifactId>
<version>1.0-SNAPSHOT</version>
```

**Added Maven compiler properties:**
```xml
<properties>
  <maven.compiler.source>1.8</maven.compiler.source>
  <maven.compiler.target>1.8</maven.compiler.target>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

### Source Structure:
✓ Main application classes located in: `src/main/java/bankAccountApp/`
  - ACHService.java
  - ACHServiceImpl.java
  - Bank.java
  - BankAccount.java
  - BankAccountApp.java
  - Person.java

### Build Command:
```bash
cd jay-bank
mvn clean compile
```

### Status:
- ✓ `pom.xml` updated with correct Maven coordinates
- ✓ Source files properly organized in `src/main/java` structure
- ✓ Java compiler properties configured for Java 8
- ✓ Ready for compilation (Maven installation required)

**Note:** To compile, ensure Maven is installed and available in your PATH, then run `mvn compile` from the `jay-bank` directory.
