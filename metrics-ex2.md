# Exercise 2: Cyclomatic Complexity on a Key Method

## Chosen Method: `withdrawMoney(double withdrawAmount)`

**Cyclomatic Complexity:** 5 (from ckjm_ext.jar output)

## Method Code with Decision Points Marked:

```java
public boolean withdrawMoney(double withdrawAmount) {
    // Decision point 1: withdrawAmount >= 0
    // Decision point 2: balance >= withdrawAmount
    // Decision point 3: withdrawAmount < withdrawLimit
    // Decision point 4: withdrawAmount + amountWithdrawn <= withdrawLimit
    if (withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount < withdrawLimit
            && withdrawAmount + amountWithdrawn <= withdrawLimit) {
        balance = balance - withdrawAmount;
        success = true;
        amountWithdrawn += withdrawAmount;
    } else {
        success = false;
    }
    return success;
}
```

## Refactoring Proposal

The `withdrawMoney` method has high complexity due to multiple validation checks combined in a single compound boolean expression. To reduce complexity, I would extract the validation logic into a helper method named `isWithdrawalValid(double withdrawAmount)` that performs all the checks and returns a boolean result. This would separate the validation logic from the business logic of updating the balance, making the code more readable and testable. Additionally, individual validation helper methods like `hasAvailableBalance(double amount)` and `isWithinDailyLimit(double amount)` could further decompose the complex condition, reducing cyclomatic complexity of each method to 2 or less.

## Bonus: Refactoring Implementation

### Refactored Code:

```java
public boolean withdrawMoney(double withdrawAmount) {
    if (isWithdrawalValid(withdrawAmount)) {
        balance = balance - withdrawAmount;
        success = true;
        amountWithdrawn += withdrawAmount;
    } else {
        success = false;
    }
    return success;
}

private boolean isWithdrawalValid(double withdrawAmount) {
    return withdrawAmount >= 0 
        && balance >= withdrawAmount 
        && withdrawAmount < withdrawLimit
        && withdrawAmount + amountWithdrawn <= withdrawLimit;
}
```

**Expected Cyclomatic Complexity after refactoring:**
- `withdrawMoney`: 2 (one if-else decision)
- `isWithdrawalValid`: 5 (four && conditions + method entry)
- **Total WMC reduction:** The individual method complexity is lower, improving maintainability and testability.
