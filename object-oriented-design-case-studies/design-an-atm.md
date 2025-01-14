<h1 align="center">Design an ATM</h1>
<h3 align="center">Let's design an ATM.</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [How ATM works?](#how-atm-works)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagrams](#activity-diagrams)
* [Sequence Diagram](#sequence-diagram)
* [Code](#code)

An automated teller machine (ATM) is an electronic telecommunications instrument that provides the clients of a financial institution with access to financial transactions in a public space without the need for a cashier or bank teller. ATMs are necessary as not all the bank branches are open every day of the week, and some customers may not be in a position to visit a bank each time they want to withdraw or deposit money.

<p align="center">
    <img src="/media-files/atm.png" alt="ATM">
    <br />
    ATM
</p>

### System Requirements

The main components of the ATM that will affect interactions between the ATM and its users are:

1. **Card reader:** to read the users’ ATM cards.
2. **Keypad:** to enter information into the ATM e.g. PIN. cards.
3. **Screen:** to display messages to the users.
4. **Cash dispenser:** for dispensing cash.
5. **Deposit slot:** For users to deposit cash or checks.
6. **Printer:** for printing receipts.
7. **Communication/Network Infrastructure:** it is assumed that the ATM has a communication infrastructure to communicate with the bank upon any transaction or activity.

The user can have two types of accounts: 1) Checking, and 2) Savings, and should be able to perform the following five transactions on the ATM:

1. **Balance inquiry:** To see the amount of funds in each account.
2. **Deposit cash:** To deposit cash.
3. **Deposit check:** To deposit checks.
4. **Withdraw cash:** To withdraw money from their checking account.
5. **Transfer funds:** To transfer funds to another account.

### How ATM works?

The ATM will be managed by an operator, who operates the ATM and refills it with cash and receipts. The ATM will serve one customer at a time and should not shut down while serving. To begin a transaction in the ATM, the user should insert their ATM card, which will contain their account information. Then, the user should enter their Personal Identification Number (PIN) for authentication. The ATM will send the user’s information to the bank for authentication; without authentication, the user cannot perform any transaction/service.

The user’s ATM card will be kept in the ATM until the user ends a session. For example, the user can end a session at any time by pressing the cancel button, and the ATM Card will be ejected. The ATM will maintain an internal log of transactions that contains information about hardware failures; this log will be used by the ATM operator to resolve any issues.

1. Identify the system user through their PIN.
2. In the case of depositing checks, the amount of the check will not be added instantly to the user account; it is subject to manual verification and bank approval.
3. It is assumed that the bank manager will have access to the ATM’s system information stored in the bank database.
4. It is assumed that user deposits will not be added to their account immediately because it will be subject to verification by the bank.
5. It is assumed the ATM card is the main player when it comes to security; users will authenticate themselves with their debit card and security pin.

### Use Case Diagram

Here are the actors of the ATM system and their use cases:

**Operator:** The operator will be responsible for the following operations:

1. Turning the ATM ON/OFF using the designated Key-Switch.
2. Refilling the ATM with cash.
3. Refilling the ATM’s printer with receipts.
4. Refilling the ATM’s printer with INK.
5. Take out deposited cash and checks.

**Customer:** The ATM customer can perform the following operations:

1. Balance inquiry: the user can view his/her account balance.
2. Cash withdrawal: the user can withdraw a certain amount of cash.
3. Deposit funds: the user can deposit cash or checks.
4. Transfer funds: the user can transfer funds to other accounts.

**Bank Manager:** The Bank Manager can perform the following operations:

1. Generate a report to check total deposits.
2. Generate a report to check total withdrawals.
3. Print total deposits/withdrawal reports.
4. Checks the remaining cash in the ATM.

Here is the use case diagram of our ATM system:

<p align="center">
    <img src="/media-files/atm-use-case-diagram.svg" alt="ATM Use Case Diagram">
    <br />
    Use Case Diagram for ATM
</p>

### Class Diagram

Here are the main classes of the ATM System:

* **ATM:** The main part of the system for which this software has been designed. It has attributes like ‘atmID’ to distinguish it from other available ATMs, and ‘location’ which defines the physical address of the ATM.
* **CardReader:** To encapsulate the ATM’s card reader used for user authentication.
* **CashDispenser:** To encapsulate the ATM component which will dispense cash.
* **Keypad:** The user will use the ATM’s keypad to enter their PIN or amounts.
* **Screen:** Users will be shown all messages on the screen and they will select different transactions by touching the screen.
* **Printer:** To print receipts.
* **DepositSlot:** User can deposit checks or cash through the deposit slot.
* **Bank:** To encapsulate the bank which ownns the ATM. The bank will hold all the account information and the ATM will communicate with the bank to perform customer transactions.
* **Account:** We’ll have two types of accounts in the system: 1)Checking and 2)Saving.
* **Customer:** This class will encapsulate the ATM’s customer. It will have the customer’s basic information like name, email, etc.
* **Card:** Encapsulating the ATM card that the customer will use to authenticate themselves. Each customer can have one card.
* **Transaction:** Encapsulating all transactions that the customer can perform on the ATM, like BalanceInquiry, Deposit, Withdraw, etc.

<p align="center">
    <img src="/media-files/atm-class-diagram.png" alt="ATM Class Diagram">
    <br />
    Class Diagram for ATM
</p>

<p align="center">
    <img src="/media-files/atm-uml.svg" alt="ATM UML">
    <br />
    UML for ATM
</p>

### Activity Diagrams

**Customer authentication:** Following is the activity diagram for a customer authenticating themselves to perform an ATM transaction:

<p align="center">
    <img src="/media-files/atm-cus-auth-activity-diagram.svg" alt="ATM Customer Authentication Activity Diagram">
    <br />
    Activity Diagram for ATM Customer Authentication
</p>

**Cash withdraw:** Following is the activity diagram for a user withdrawing cash:

<p align="center">
    <img src="/media-files/atm-withdraw-activity-diagram.svg" alt="ATM Cash Withdraw Activity Diagram">
    <br />
    Activity Diagram for ATM Cash Withdraw
</p>

**Deposit check:** Following is the activity diagram for the customer depositing a check:

<p align="center">
    <img src="/media-files/atm-deposit-activity-diagram.svg" alt="ATM Deposit Check Activity Diagram">
    <br />
    Activity Diagram for ATM Deposit Check
</p>

**Fund transfer:** Following is the activity diagram for a user transferring funds to another account:

<p align="center">
    <img src="/media-files/atm-transfer-activity-diagram.png" alt="ATM Fund Transfer Activity Diagram">
    <br />
    Activity Diagram for ATM Fund Transfer
</p>

### Sequence Diagram

Here is the sequence diagram for balance inquiry transaction:

<p align="center">
    <img src="/media-files/atm-sequence-diagram.svg" alt="ATM Sequence Diagram">
    <br />
    Sequence Diagram for ATM
</p>

### Code

Here is the skeleton code for the classes defined above:

**Enums and Constants:** Here are the required enums, data types, and constants:

import java.util.Scanner;

// Context class representing the ATM
class ATM {
    private ATMState currentState;
    private int balance;

    public ATM(int initialBalance) {
        currentState = new IdleState(this);
        balance = initialBalance;
    }

    public void setCurrentState(ATMState state) {
        currentState = state;
    }

    public int getBalance() {
        return balance;
    }

    public void setBalance(int balance) {
        this.balance = balance;
    }

    public void insertCard() {
        currentState.insertCard();
    }

    public void ejectCard() {
        currentState.ejectCard();
    }

    public void enterPIN() {
        currentState.enterPIN();
    }

    public void withdraw(int amount) {
        currentState.withdraw(amount);
    }
}

// State interface
interface ATMState {
    void insertCard();

    void ejectCard();

    void enterPIN();

    void withdraw(int amount);
}

// Concrete state representing the idle state
class IdleState implements ATMState {
    private ATM atm;

    public IdleState(ATM atm) {
        this.atm = atm;
    }

    @Override
    public void insertCard() {
        System.out.println("Card inserted");
        atm.setCurrentState(new CardInsertedState(atm));
    }

    @Override
    public void ejectCard() {
        System.out.println("No card to eject");
    }

    @Override
    public void enterPIN() {
        System.out.println("Please insert a card first");
    }

    @Override
    public void withdraw(int amount) {
        System.out.println("Please insert a card and enter PIN first");
    }
}

// Concrete state representing the card inserted state
class CardInsertedState implements ATMState {
    private ATM atm;

    public CardInsertedState(ATM atm) {
        this.atm = atm;
    }

    @Override
    public void insertCard() {
        System.out.println("Card is already inserted");
    }

    @Override
    public void ejectCard() {
        System.out.println("Card ejected");
        atm.setCurrentState(new IdleState(atm));
    }

    @Override
    public void enterPIN() {
        System.out.println("PIN entered");
        atm.setCurrentState(new PINEnteredState(atm));
    }

    @Override
    public void withdraw(int amount) {
        System.out.println("Please enter PIN first");
    }
}

// Concrete state representing the PIN entered state
class PINEnteredState implements ATMState {
    private ATM atm;

    public PINEnteredState(ATM atm) {
        this.atm = atm;
    }

    @Override
    public void insertCard() {
        System.out.println("Card is already inserted");
    }

    @Override
    public void ejectCard() {
        System.out.println("Card ejected");
        atm.setCurrentState(new IdleState(atm));
    }

    @Override
    public void enterPIN() {
        System.out.println("PIN is already entered");
    }

    @Override
    public void withdraw(int amount) {
        if (amount > atm.getBalance()) {
            System.out.println("Insufficient funds");
        } else {
            atm.setBalance(atm.getBalance() - amount);
            System.out.println("Withdrawal successful. Remaining balance: " + atm.getBalance());
            atm.setCurrentState(new IdleState(atm));
        }
    }
}

// Main class to run the ATM
public class Main {
    public static void main(String[] args) {
        // Initialize the ATM with an initial balance
        ATM atm = new ATM(1000);

        // Simulate ATM interactions
        atm.insertCard();
        atm.enterPIN();
        atm.withdraw(500);
        atm.ejectCard();
    }
}