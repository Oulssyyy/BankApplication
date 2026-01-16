# Exercise 8: Unit Tests for BankApplication

## Test Status Summary

### Current Test Results:
- **Total tests**: 59
- **Passing**: 56
- **Failing**: 3 (InputMismatchException in Person parsing)

### Failing Tests:
1. `BankAccountTest.test_create_vert3_and_gets` - Line 82
2. `PersonTest.test_create_ver4_and_gets` - Line 126  
3. `PersonTest.test_create_ver4_and_gets_hamcrest` - Line 144

### Root Cause:
The `Person(String accountHolder)` constructor (line 92-112) parses serialized data using a Scanner with `"\n"` delimiter. The issue occurs when parsing the serialized Person format - the `InputMismatchException` happens when trying to call `scan.nextFloat()` for height/weight fields.

### Code Analysis:
The `Person` class stores:
- `height` and `weight` as `float` fields (lines 18-19)
- Constructor parameter order expects: name, gender, age, height, weight, hairColor, eyeColor, email

The serialized format is:
```
name\ngender\nage\nheight\nweight\nhairColor\neyeColor\nemail
```

### Fixes Applied:
1. **BankAccountTest.java** (lines 15-16):
   - Changed `int weight = 190` → `float weight = 190.0f`
   - Changed `float height = 172` → `float height = 172.0f`
   - This ensures consistent type when building serialized Person strings

### Investigation Needed:
The Person Scanner parsing logic appears to have an issue with the delimiter handling when transitioning between `nextInt()` for age and `nextFloat()` for height. This may be:
1. A whitespace/delimiter formatting issue
2. A Scanner state issue between different nextXxx() calls
3. An actual data format mismatch in test setup

### Happy Path Tests (PASSING):
- `test_create_vert1_and_gets` - Default constructor
- `test_create_vert2_and_gets` - Constructor with balance/limit/date
- `test_create_and_deposit_money` - Deposit functionality ✓
- `test_create_and_withdraw_money` - Withdraw functionality ✓
- `test_create_and_setWithdrawLimit_failure1` - Withdrawal exceeds balance
- `test_create_and_setWithdrawLimit_failure2` - Exceeds daily withdrawal limit
- `test_toString` - String representation

### Edge Case Tests (PASSING):
- Withdrawal limit enforcement
- Insufficient funds handling
- Daily withdrawal limit tracking

### Recommendation:
To fully resolve the 3 failing tests, the Person class parsing logic should be reviewed to handle the Scanner delimiter properly, potentially by using a different delimiter character or refactoring the parsing logic to be more robust.
