# COBOL Account Management System Test Plan

This test plan covers all business logic implemented in the current COBOL application. It is designed to validate the system with business stakeholders and will serve as a foundation for future unit and integration tests in the Node.js transformation.

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status (Pass/Fail) | Comments |
|--------------|----------------------|----------------|------------|-----------------|--------------|--------------------|----------|
| TC01 | View initial account balance | Application is started; no transactions performed | 1. Start app<br>2. Select 'View Balance' | Balance displayed as $1000.00 |  |  |  |
| TC02 | Credit account with valid amount | Application is started | 1. Start app<br>2. Select 'Credit Account'<br>3. Enter 100 | Balance increases by 100; new balance $1100.00 |  |  |  |
| TC03 | Debit account with valid amount (sufficient funds) | Account balance >= debit amount | 1. Start app<br>2. Select 'Debit Account'<br>3. Enter 150 | Balance decreases by 150; new balance $850.00 |  |  |  |
| TC04 | Debit account with insufficient funds | Account balance < debit amount | 1. Start app<br>2. Select 'Debit Account'<br>3. Enter amount greater than balance | Error message: "Insufficient funds for this debit."; balance unchanged |  |  |  |
| TC05 | Credit account with zero amount | Application is started | 1. Start app<br>2. Select 'Credit Account'<br>3. Enter 0 | Balance unchanged; new balance $1000.00 |  |  |  |
| TC06 | Debit account with zero amount | Application is started | 1. Start app<br>2. Select 'Debit Account'<br>3. Enter 0 | Balance unchanged; new balance $1000.00 |  |  |  |
| TC07 | Credit account with maximum allowed amount | Application is started | 1. Start app<br>2. Select 'Credit Account'<br>3. Enter 999999.99 | Balance increases by 999999.99; new balance $1000999.99 |  |  |  |
| TC08 | Debit account with maximum allowed amount (sufficient funds) | Account balance >= 999999.99 | 1. Start app<br>2. Select 'Debit Account'<br>3. Enter 999999.99 | Balance decreases by 999999.99; new balance $0.01 |  |  |  |
| TC09 | Invalid menu selection | Application is started | 1. Start app<br>2. Enter invalid menu option (e.g., 5 or letter) | Error message: "Invalid choice, please select 1-4." |  |  |  |
| TC10 | Exit application | Application is started | 1. Start app<br>2. Select 'Exit' | Application terminates with exit message |  |  |  |
| TC11 | Multiple sequential credits and debits | Application is started | 1. Start app<br>2. Perform several credits and debits in sequence | Balance updates correctly after each transaction |  |  |  |
| TC12 | Data consistency after transactions | Application is started | 1. Start app<br>2. Perform credit and debit<br>3. View balance | Balance reflects all previous transactions accurately |  |  |  |
| TC13 | Menu loop continues until exit | Application is started | 1. Start app<br>2. Perform any operation<br>3. Repeat until 'Exit' selected | Menu reappears after each operation until exit |  |  |  |
