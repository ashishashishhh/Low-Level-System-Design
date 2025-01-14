<h1 align="center">Design a Restaurant Management System</h1>
<h3 align="center">Let's design a Restaurant Management System</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagrams](#activity-diagrams)
* [Code](#code)

A Restaurant Management System is a software built to handle all restaurant activities in an easy and safe manner. This System will give the Restaurant management power and flexibility to manage the entire system from a single portal. The system allows the manager to keep track of available tables in the system as well as the reservation of tables and bill generation.

<p align="center">
    <img src="/media-files/restaurant-management-system.png" alt="Restaurant Management System">
    <br />
    Restaurant Management System
</p>

### System Requirements

We will focus on the following set of requirements while designing the Restaurant Management System:

1. The restaurant will have different branches.
2. Each restaurant branch will have a menu.
3. The menu will have different menu sections, containing different menu items.
4. The waiter should be able to create an order for a table and add meals for each seat.
5. Each meal can have multiple meal items. Each meal item corresponds to a menu item.
6. The system should be able to retrieve information about tables currently available to seat walk-in customers.
7. The system should support the reservation of tables.
8. The receptionist should be able to search for available tables by date/time and reserve a table.
9. The system should allow customers to cancel their reservation.
10. The system should be able to send notifications whenever the reservation time is approaching.
11. The customers should be able to pay their bills through credit card, check or cash.
12. Each restaurant branch can have multiple seating arrangements of tables.

### Use Case Diagram

Here are the main Actors in our system:

**Receptionist:** Mainly responsible for adding and modifying tables and their layout, and creating and canceling table reservations.
**Waiter:** To take/modify orders.
**Manager:** Mainly responsible for adding new workers and modifying the menu.
**Chef:** To view and work on an order.
**Cashier:** To generate checks and process payments.
**System:** Mainly responsible for sending notifications about table reservations, cancellations, etc.

Here are the top use cases of the Restaurant Management System:

* **Add/Modify tables:** To add, remove, or modify a table in the system.
* **Search tables:** To search for available tables for reservation.
* **Place order:** Add a new order in the system for a table.
* **Update order:** Modify an already placed order, which can include adding/modifying meals or meal items.
* **Create a reservation:** To create a table reservation for a certain date/time for an available table.
* **Cancel reservation:** To cancel an existing reservation.
* **Check-in:** To let the guest check in for their reservation.
* **Make payment:** Pay the check for the food.

Here is the use case diagram of our Restaurant Management System:

<p align="center">
    <img src="/media-files/rms-use-case-diagram.svg" alt="Restaurant Management System Use Case Diagram">
    <br />
    Use Case Diagram for Restaurant Management System
</p>

### Class Diagram

Here is the description of the different classes of our Restaurant Management System:

* **Restaurant:** This class represents a restaurant. Each restaurant has registered employees. The employees are part of the restaurant because if the restaurant becomes inactive, all its employees will automatically be deactivated.
* **Branch:** Any restaurants can have multiple branches. Each branch will have its own set of employees and menus.
* **Menu:** All branches will have their own menu.
* **MenuSection and MenuItem:** A menu has zero or more menu sections. Each menu section consists of zero or more menu items.
* **Table and TableSeat:** The basic building block of the system. Every table will have a unique identifier, maximum sitting capacity, etc. Each table will have multiple seats.
* **Order:** This class encapsulates the order placed by a customer.
* **Meal:** Each order will consist of separate meals for each table seat.
* **Meal Item:** Each Meal will consist of one or more meal items corresponding to a menu item.
* **Account:** We’ll have different types of accounts in the system, one will be a receptionist to search and reserve tables and the other, the waiter will place orders in the system.
* **Notification:** Will take care of sending notifications to customers.
* **Bill:** Contains different bill-items for every meal item.

<p align="center">
    <img src="/media-files/rms-class-diagram.png" alt="Restaurant Management System Class Diagram">
    <br />
    Class Diagram for Restaurant Management System
</p>

<p align="center">
    <img src="/media-files/rms-uml.svg" alt="Restaurant Management System UML">
    <br />
    UML for Restaurant Management System
</p>

### Activity Diagrams

**Place order:** Any waiter can perform this activity. Here are the steps to place an order:

<p align="center">
    <img src="/media-files/rms-place-order-activity-diagram.svg" alt="Restaurant Management System Place Order">
    <br />
    Activity Diagram for Restaurant Management System Place Order
</p>

**Make a reservation:** Any receptionist can perform this activity. Here are the steps to make a reservation:

<p align="center">
    <img src="/media-files/rms-make-reservation-activity-diagram.svg" alt="Restaurant Management System Make Reservation">
    <br />
    Activity Diagram for Restaurant Management System Make Reservation
</p>

**Cancel a reservation:** Any receptionist can perform this activity. Here are the steps to cancel a reservation:

<p align="center">
    <img src="/media-files/rms-cancel-reservation-activity-diagram.svg" alt="Restaurant Management System Cancel Reservation">
    <br />
    Activity Diagram for Restaurant Management System Cancel Reservation
</p>

### Code

Here is the high-level definition for the classes described above.


// Enums representing various statuses in the restaurant management system

public enum ReservationStatus {
    REQUESTED, PENDING, CONFIRMED, CHECKED_IN, CANCELED, ABANDONED
}

public enum SeatType {
    REGULAR, KID, ACCESSIBLE, OTHER
}

public enum OrderStatus {
    RECEIVED, PREPARING, COMPLETED, CANCELED, NONE
}

public enum TableStatus {
    FREE, RESERVED, OCCUPIED, MAINTENANCE, OTHER
}

public enum AccountStatus {
    ACTIVE, CLOSED, CANCELED, BLACKLISTED, BLOCKED
}

public enum PaymentStatus {
    UNPAID, PENDING, COMPLETED, FAILED, DECLINED, CANCELLED, ABANDONED, SETTLING, SETTLED, REFUNDED
}

// Supporting Address class
public class Address {
    private String streetAddress;
    private String city;
    private String state;
    private String zipCode;
    private String country;

    // Constructors, getters, and setters are omitted for brevity
}

// Abstract class for Person, common attributes for all types of people involved
public abstract class Person {
    private String name;
    private String email;
    private String phone;

    // Constructor and methods omitted for brevity
}

// Abstract Employee class extending Person
public abstract class Employee extends Person {
    private int employeeID;
    private Date dateJoined;
    private Account account;

    // Constructor and methods omitted for brevity
}

// Concrete Receptionist class
public class Receptionist extends Employee {
    public boolean createReservation(Reservation reservation) {
        System.out.println("Reservation created successfully.");
        return true;
    }

    public List<Customer> searchCustomer(String name) {
        // Search logic
        return new ArrayList<>();
    }
}

// Concrete Manager class
public class Manager extends Employee {
    public boolean addEmployee(Employee employee) {
        System.out.println("Employee added successfully.");
        return true;
    }

    public boolean modifyMenu(Menu menu) {
        System.out.println("Menu modified successfully.");
        return true;
    }
}

// Chef class for processing orders
public class Chef extends Employee {
    public boolean takeOrder(Order order) {
        System.out.println("Chef received order: " + order.getOrderID());
        return true;
    }
}

// Cashier class for processing payments
public class Cashier extends Employee {
    public boolean generateCheck(Order order) {
        System.out.println("Check generated for order: " + order.getOrderID());
        return true;
    }

    public boolean processPayment(Check check) {
        System.out.println("Payment processed for check: " + check.getCheckID());
        return true;
    }
}

// Notification system using the Observer Pattern
interface Observer {
    void update(String message);
}

class Customer implements Observer {
    private String name;
    private Account account;

    public Customer(String name, Account account) {
        this.name = name;
        this.account = account;
    }

    @Override
    public void update(String message) {
        System.out.println("Notification for customer " + name + ": " + message);
    }
}

// SystemNotifier to send notifications to customers
class SystemNotifier {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

// Table-related classes
public class Table {
    private int tableID;
    private TableStatus status;
    private int maxCapacity;
    private List<TableSeat> seats;

    public boolean isTableFree() {
        return status == TableStatus.FREE;
    }

    public boolean addReservation(Reservation reservation) {
        this.status = TableStatus.RESERVED;
        System.out.println("Table reserved.");
        return true;
    }

    public static List<Table> search(int capacity, Date startTime) {
        // Search for tables based on capacity and availability
        return new ArrayList<>();
    }
}

public class TableSeat {
    private int seatNumber;
    private SeatType type;

    public boolean updateSeatType(SeatType type) {
        this.type = type;
        return true;
    }
}

// Reservation class
public class Reservation {
    private int reservationID;
    private Date reservationTime;
    private int peopleCount;
    private ReservationStatus status;
    private Table table;
    private Customer customer;
    private List<Notification> notifications;

    public boolean updatePeopleCount(int count) {
        this.peopleCount = count;
        System.out.println("People count updated.");
        return true;
    }
}

// Menu-related classes
public class MenuItem {
    private int menuItemID;
    private String title;
    private String description;
    private double price;

    public boolean updatePrice(double price) {
        this.price = price;
        System.out.println("Menu item price updated.");
        return true;
    }
}

public class MenuSection {
    private int sectionID;
    private String title;
    private List<MenuItem> menuItems;

    public boolean addMenuItem(MenuItem menuItem) {
        menuItems.add(menuItem);
        return true;
    }
}

public class Menu {
    private int menuID;
    private String title;
    private List<MenuSection> menuSections;

    public boolean addMenuSection(MenuSection section) {
        menuSections.add(section);
        return true;
    }
}

// Order-related classes
public class MealItem {
    private int mealItemID;
    private int quantity;
    private MenuItem menuItem;

    public boolean updateQuantity(int quantity) {
        this.quantity = quantity;
        return true;
    }
}

public class Meal {
    private int mealID;
    private TableSeat seat;
    private List<MealItem> mealItems;

    public boolean addMealItem(MealItem item) {
        mealItems.add(item);
        return true;
    }
}

public class Order {
    private int orderID;
    private OrderStatus status;
    private Date creationTime;
    private Meal[] meals;
    private Table table;
    private Check check;
    private Waiter waiter;
    private Chef chef;

    public int getOrderID() {
        return orderID;
    }

    public OrderStatus getStatus() {
        return status;
    }

    public void setStatus(OrderStatus status) {
        this.status = status;
        System.out.println("Order status updated to: " + status);
    }

    public boolean addMeal(Meal meal) {
        System.out.println("Meal added to order.");
        return true;
    }

    public boolean removeMeal(Meal meal) {
        System.out.println("Meal removed from order.");
        return true;
    }
}

// Check class for processing payments
public class Check {
    private int checkID;
    private PaymentStatus status;
    private double amount;

    public int getCheckID() {
        return checkID;
    }

    public boolean processPayment() {
        System.out.println("Payment processed for check: " + checkID);
        return true;
    }
}

// Command Pattern for creating orders
interface Command {
    void execute();
}

class CreateOrderCommand implements Command {
    private Order order;

    public CreateOrderCommand(Order order) {
        this.order = order;
    }

    @Override
    public void execute() {
        System.out.println("Order created with ID: " + order.getOrderID());
    }
}

// Example Main class demonstrating the usage of Observer, Command, and other patterns
public class Main {
    public static void main(String[] args) {
        // Create SystemNotifier and customers
        SystemNotifier notifier = new SystemNotifier();
        Customer alice = new Customer("Alice", new Account());
        Customer bob = new Customer("Bob", new Account());
        notifier.addObserver(alice);
        notifier.addObserver(bob);

        // Notify customers about table reservation
        notifier.notifyObservers("Table reservation confirmed!");

        // Create an order using the Command pattern
        Order order = new Order();
        order.setStatus(OrderStatus.RECEIVED);
        Command createOrder = new CreateOrderCommand(order);
        createOrder.execute();

        // Process a payment using Cashier
        Cashier cashier = new Cashier();
        Check check = new Check();
        cashier.processPayment(check);
    }
}

