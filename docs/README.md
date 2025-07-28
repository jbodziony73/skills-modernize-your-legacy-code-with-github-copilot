# COBOL Account Management System Documentation

This document provides detailed information about the COBOL-based Account Management System, including the purpose of each file, key functions, and business rules for student account management.

## System Overview

The Account Management System is a COBOL-based application designed to handle basic banking operations for student accounts. The system provides functionality for viewing account balances, crediting accounts, and debiting accounts with appropriate validation and error handling.

## File Structure and Components

### 1. `main.cob` - Main Program Controller

**Program ID:** `MainProgram`

**Purpose:**
The main entry point of the Account Management System that provides a menu-driven interface for users to interact with account operations.

**Key Functions:**

- Displays a user-friendly menu with available operations
- Handles user input validation
- Controls program flow through menu selection
- Manages the main application loop

**Menu Options:**

1. View Balance - Displays current account balance
2. Credit Account - Adds funds to the account
3. Debit Account - Withdraws funds from the account (with validation)
4. Exit - Terminates the program

**Business Rules:**

- Invalid menu selections (not 1-4) display an error message
- The program continues to display the menu until the user selects option 4 (Exit)
- All account operations are delegated to the `Operations` program

### 2. `operations.cob` - Business Logic Handler

**Program ID:** `Operations`

**Purpose:**
Handles the core business logic for all account operations including balance inquiries, credits, and debits.

**Key Functions:**

- **Balance Inquiry (`TOTAL`)**: Retrieves and displays current account balance
- **Credit Operation (`CREDIT`)**: Adds funds to the account
- **Debit Operation (`DEBIT`)**: Withdraws funds with insufficient funds validation

**Business Rules:**

- **Credit Operations:**
  - Accepts any positive amount for credit
  - Updates the account balance immediately
  - Displays the new balance after successful credit

- **Debit Operations:**
  - Validates sufficient funds before processing withdrawal
  - Prevents overdrafts by checking if balance >= debit amount
  - Displays "Insufficient funds" message when balance is inadequate
  - Only processes debit if sufficient funds are available

- **Balance Display:**
  - Shows current balance formatted with decimal precision
  - Retrieves balance data through the `DataProgram` interface

**Data Validation:**

- Amounts are stored with 6 digits before decimal and 2 digits after (9(6)V99)
- Maximum transaction amount: $9999.99
- Initial account balance: $1000.00

### 3. `data.cob` - Data Management Layer

**Program ID:** `DataProgram`

**Purpose:**
Manages data persistence and provides a centralized interface for reading and writing account balance information.

**Key Functions:**

- **Read Operation (`READ`)**: Retrieves the current stored balance
- **Write Operation (`WRITE`)**: Updates the stored balance with new value

**Data Storage:**

- Maintains account balance in working storage
- Balance format: 6 digits before decimal, 2 digits after (PIC 9(6)V99)
- Default initial balance: $1000.00

**Business Rules:**

- Acts as a simple in-memory data store
- Provides atomic read and write operations
- Maintains data consistency across operations
- Balance persists only during program execution (no file I/O)

## System Architecture

```text
┌─────────────────┐
│   main.cob      │ ← User Interface Layer
│  (MainProgram)  │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│ operations.cob  │ ← Business Logic Layer
│  (Operations)   │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│   data.cob      │ ← Data Access Layer
│ (DataProgram)   │
└─────────────────┘
```

## Student Account Management Features

### Account Balance Management

- Real-time balance tracking
- Immediate balance updates after transactions
- Balance validation for withdrawal operations

### Transaction Processing

- **Credit Transactions**: No upper limit validation (accepts any positive amount)
- **Debit Transactions**: Strict validation to prevent overdrafts
- **Balance Inquiries**: Instant access to current balance

### Error Handling

- Invalid menu selection handling
- Insufficient funds validation
- User-friendly error messages

## Technical Specifications

### Data Types and Limits

- Account Balance: Maximum $999,999.99
- Transaction Amounts: Maximum $999,999.99
- Precision: 2 decimal places for all monetary values

### Program Flow

1. User starts `MainProgram`
2. Menu is displayed with operation choices
3. User selection triggers appropriate `Operations` call
4. `Operations` program calls `DataProgram` for data access
5. Results are displayed to user
6. Process repeats until user exits

## Usage Examples

### Viewing Balance

```text
User selects option 1 → Calls Operations with 'TOTAL' → Displays current balance
```

### Crediting Account

```text
User selects option 2 → Prompts for amount → Adds to balance → Displays new balance
```

### Debiting Account

```text
User selects option 3 → Prompts for amount → Validates funds → 
Either processes debit or shows insufficient funds error
```

## Security and Validation

- **Overdraft Protection**: Prevents account balance from going below zero
- **Input Validation**: Validates numeric input for transaction amounts
- **Menu Validation**: Handles invalid menu selections gracefully

## Future Enhancement Opportunities

- File-based persistence for balance storage
- Multiple account support
- Transaction history logging
- Account authentication
- Interest calculation features
- Transfer between accounts functionality
