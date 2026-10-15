# Object-Oriented Programming in Java: Lab 11 and Mini-Project

| | |
|---|---|
| **Name** | Tadiwanashe Mundingi |
| **Reg number** | H250549X |
| **Manual** | Object-Oriented Programming in Java: University Lab Manual |
| **Lab** | Lab 11: Design Patterns and the Mini-Project |
| **Mini-project** | Library Management System |

## Contents

```
lab11/          Program 11.1 (Singleton and Factory), Program 11.2 (Strategy and Observer), expected output files
mini-project/   Library Management System: src/, run.sh, class_diagram.png, report.docx / report.md, sample runs
```

Requirement: JDK 17 or later (`java -version`).

---

## Part 1: Lab 11, Design Patterns

### What the code does

**Program 11.1, `SingletonFactoryDemo.java`**
- *Singleton*: `AppConfig` has a private constructor and one static instance, so every call to `getInstance()` returns the same object. The program prints `Same instance? true`.
- *Factory*: `NotificationFactory.create("email" | "sms")` returns a `Notification` (`EmailNotification` or `SmsNotification`) without the caller naming the concrete class. An unknown type throws `IllegalArgumentException`.

**Program 11.2, `StrategyObserverDemo.java`**
- *Strategy*: `Checkout` holds a `DiscountStrategy` that can be swapped at run time with `setStrategy`. The demo changes from no discount (200.0) to a 10% student discount (180.0) using lambdas.
- *Observer*: `GradeBook` keeps a list of `GradeListener`s and notifies all of them when a grade is published. One listener prints to a student portal and another prints an advisor alert when the mark is below 50.

### Implementation and how to run

```
cd lab11
javac *.java
java SingletonFactoryDemo
java StrategyObserverDemo
```

The output matches the manual's expected output (`expected_output_11.1.txt` and `expected_output_11.2.txt`).

---

## Part 2: Mini-Project, Library Management System

### What the code does

A console program for running a small library. Users can add books and DVDs, register members, borrow and return items, list overdue loans, and search by title. Each member can hold at most 3 loans. Data is saved to CSV files when the program exits and reloaded when it starts, so nothing is lost between runs.

### Implementation

| File | Role |
|---|---|
| `LibraryItem` (abstract) | id, title and availability. Declares `loanPeriodDays()`. Implements `Borrowable`. |
| `Book`, `Dvd` | Subclasses. Book has a 21-day loan and a DVD has a 7-day loan (polymorphism). |
| `Borrowable` (interface) | `borrow(Member)` and `giveBack()` |
| `Member` | id, name and current loans. Maximum of 3 (`MAX_LOANS`). |
| `Loan` | Links a member and an item, with a borrow date, due date and `isOverdue(date)` |
| `ItemNotAvailableException`, `MemberLimitExceededException` | Custom checked exceptions |
| `Library` | Core service with `Map<String, LibraryItem>` and `Map<String, Member>`. Borrow, return, stream-based `searchByTitle` and `listOverdue`, CSV `save` and `load`. |
| `Csv` | Helper to read and write CSV lines safely (handles commas in titles) |
| `Main` | Menu: add item, register member, borrow, return, list overdue, search, list all, save and exit |
| `LibraryTests` | 30 automatic checks (validation, rules, exceptions, overdue, search, save/reload) |

OOP concepts used: encapsulation (private fields and validation), inheritance, abstraction, polymorphism, an interface, custom exceptions, collections (`Map`, `List`), streams and lambdas, and file I/O with `java.nio.file`.

### How to run

```
cd mini-project
./run.sh
```

`run.sh` compiles the code, runs the 30 tests, then starts the menu. To run the steps yourself:

```
javac -d out src/*.java
java -cp out LibraryTests
java -cp out Main data
```

Data is stored in the `data/` folder (`items.csv`, `members.csv`, `loans.csv`). `sample_run_1.txt` and `sample_run_2.txt` show two separate runs where a loan made in the first is still there in the second.

The report is `mini-project/report.docx` and the class diagram is `mini-project/class_diagram.png`.
