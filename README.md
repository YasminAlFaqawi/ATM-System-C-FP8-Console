# ATM System (C++)

A console-based Automated Teller Machine (ATM) simulation developed in **C++20**. The application allows a client to log in using an account number and PIN, perform basic banking transactions, and view their current account balance. Client records are stored in a text file and updated when transactions are confirmed.

> **Project type:** Educational C++ console application  
> **Development environment:** Visual Studio / Microsoft C++ (MSVC)  
> **Language standard:** C++20

## Overview

The ATM System simulates a simple banking workflow through a text-based interface. After successful authentication, the client can choose from several banking operations. The application reads client records from `Clients.txt`, works with the selected client's information, and writes updated records back to the file after a confirmed transaction.

## Features

- **Client authentication:** Validates the account number and PIN against the records stored in `Clients.txt`.
- **Quick withdrawal:** Offers predefined withdrawal amounts (20, 50, 100, 200, 400, 600, 800, and 1000).
- **Normal withdrawal:** Allows the client to enter a custom withdrawal amount, subject to the application's multiple-of-five rule.
- **Deposit:** Accepts a positive deposit amount.
- **Balance inquiry:** Displays the logged-in client's current balance.
- **Transaction confirmation:** Requests confirmation before processing a deposit or withdrawal.
- **Data persistence:** Saves client balance changes to `Clients.txt` so they remain available after the program closes.
- **Logout:** Returns the user to the login screen.

## Technologies and Concepts

- C++20
- Standard Template Library (STL)
- `struct` for representing client records
- `enum` for identifying main-menu options
- `vector` for storing client records in memory
- File handling with `fstream`, `ifstream`-style input, and output streams
- String processing with `find`, `substr`, and `erase`
- Functions and `switch` statements for organizing program operations

## Project Structure

```text
ATM-System/
├── ATMSystem.slnx
├── Clients.txt                 # Local client data file (do not publish real credentials)
├── README.md
├── LICENSE.txt
└── ATMSystem/
    ├── ATMSystem.cpp           # Application source code
    └── ATMSystem.vcxproj       # Visual Studio project configuration
```

The Visual Studio project is configured to copy `Clients.txt` to the build output directory. The application expects this file to be available in its working directory when it runs.

## Getting Started

### Requirements

- Windows
- Visual Studio with the Microsoft C++ build tools and C++20 support

### Build and run

1. Clone or download the repository.
2. Make sure a valid `Clients.txt` file is available in the application's working directory.
3. Open `ATMSystem.slnx` in Visual Studio. If your Visual Studio version does not support the solution format, open `ATMSystem/ATMSystem.vcxproj` directly.
4. Select a configuration such as **Debug** and a platform such as **x64**.
5. Build the project, then run it with **Ctrl + F5** or **Start Without Debugging**.

## Client Data File

The application uses `Clients.txt` as a simple text-based data store. Each line represents one client and contains five fields separated by the delimiter `#//#`:

```text
AccountNumber#//#PinCode#//#Name#//#Phone#//#AccountBalance
```

For example, a fictional record can be written as:

```text
A300#//#0000#//#Sample Client#//#0000000000#//#2500.00
```

Keep the field order and delimiter unchanged when adding test records. The program reads the file at login and updates it after a confirmed transaction.


## Application Workflow

1. The application displays the login screen.
2. The client enters an account number and PIN.
3. The program loads the client records and checks whether both values match a record.
4. After successful login, the main menu is displayed.
5. The client selects a transaction or requests the current balance.
6. For deposits and withdrawals, the application asks for confirmation and updates the client data file when the transaction is accepted.
7. The client can return to the main menu or log out.

## Main Menu

| Option | Operation | Description |
|---|---|---|
| 1 | Quick Withdraw | Select one of the predefined withdrawal amounts. |
| 2 | Normal Withdraw | Enter a custom amount that is a multiple of five. |
| 3 | Deposit | Add a positive amount to the account balance. |
| 4 | Check Balance | Display the current account balance. |
| 5 | Logout | Return to the login screen. |

## Implementation Notes

- `sClient` represents a client and contains the account number, PIN, name, phone number, and account balance.
- `SplitString` separates a data-file line into fields using the configured delimiter.
- `ConvertLinetoRecord` converts a text line into an `sClient` record.
- `ConvertRecordToLine` converts a client record back into the text-file format.
- `LoadCleintsDataFromFile` loads client records into a `vector`.
- `SaveCleintsDataToFile` writes the client records back to the data file.
- `FindClientByAccountNumberAndPinCode` checks the login credentials.
- The transaction and menu functions handle the application's user interactions and operations.

## Current Scope and Limitations

This project is a learning-oriented console simulation. It does not connect to a real bank, process real payments, or provide production-grade account security. Data is stored in a plain text file, PINs are not hashed or encrypted, and the application uses Windows-specific console commands such as `system("cls")` and `system("pause>0")`.

The project can be extended with stronger input validation, safer credential storage, clearer transaction-result handling, a transaction history, and a more robust data-storage solution. In the current implementation, the calling functions adjust `CurrentClient.AccountBalance` even if the user declines the confirmation prompt. This can make the displayed in-memory balance differ from the value saved in `Clients.txt`; transaction success or cancellation should be returned explicitly and used before changing the current client balance.

## License

This project is distributed under the license included in [`LICENSE.txt`](LICENSE.txt).
