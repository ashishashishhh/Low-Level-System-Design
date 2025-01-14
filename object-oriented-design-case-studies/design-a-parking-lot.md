<h1 align="center">Design a Parking Lot</h1>
<h3 align="center">Let's make an object-oriented design for a multi-floor Parking Lot</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagram](#activity-diagram)
* [Code](#code)

A parking lot or car park is a dedicated cleared area that is intended for parking vehicles. In most countries where cars are a major mode of transportation, parking lots are a feature of every city and suburban area. Shopping malls, sports stadiums, megachurches, and similar venues often feature parking lots over large areas.

<p align="center">
    <img src="/media-files/parking-lot.png" alt="Parking Lot">
    <br />
    Parking Lot
</p>

### System Requirements

We will focus on the following set of requirements while designing the parking lot:

1. The parking lot should have multiple floors where customers can park their cars.
2. The parking lot should have multiple entry and exit points.
3. Customers can collect a parking ticket from the entry points and can pay the parking fee at the exit points on their way out.
4. Customers can pay the tickets at the automated exit panel or to the parking attendant.
5. Customers can pay via both cash and credit cards.
6. Customers should also be able to pay the parking fee at the customer’s info portal on each floor. If the customer has paid at the info portal, they don’t have to pay at the exit.
7. The system should not allow more vehicles than the maximum capacity of the parking lot. If the parking is full, the system should be able to show a message at the entrance panel and on the parking display board on the ground floor.
8. Each parking floor will have many parking spots. The system should support multiple types of parking spots such as Compact, Large, Handicapped, Motorcycle, etc.
9. The Parking lot should have some parking spots specified for electric cars. These spots should have an electric panel through which customers can pay and charge their vehicles.
10. The system should support parking for different types of vehicles like car, truck, van, motorcycle, etc.
11. Each parking floor should have a display board showing any free parking spot for each spot type.
12. The system should support a per-hour parking fee model. For example, customers have to pay $4 for the first hour, $3.5 for the second and third hours, and $2.5 for all the remaining hours.

### Use Case Diagram

Here are the main Actors in our system:

* **Admin:** Mainly responsible for adding and modifying parking floors, parking spots, entrance, and exit panels, adding/removing parking attendants, etc.
* **Customer:** All customers can get a parking ticket and pay for it.
* **Parking Attendant:** Parking attendants can do all the activities on the customer’s behalf, and can take cash for ticket payment.
* **System:** To display messages on different info panels, as well as assigning and removing a vehicle from a parking spot.

Here are the top use cases for Parking Lot:

* **Add/Remove/Edit parking floor:** To add, remove or modify a parking floor from the system. Each floor can have its own display board to show free parking spots.
* **Add/Remove/Edit parking spot:** To add, remove or modify a parking spot on a parking floor.
* **Add/Remove a parking attendant:** To add or remove a parking attendant from the system.
* **Take ticket:** To provide customers with a new parking ticket when entering the parking lot.
* **Scan ticket:** To scan a ticket to find out the total charge.
* **Credit card payment:** To pay the ticket fee with credit card.
* **Cash payment:** To pay the parking ticket through cash.
* **Add/Modify parking rate:** To allow admin to add or modify the hourly parking rate.

Here is the use case diagram of our Parking Lot:

<p align="center">
    <img src="/media-files/parking-use-case-diagram.svg" alt="Parking Lot Use Case Diagram">
    <br />
    Use Case Diagram for Parking Lot
</p>

### Class Diagram

Here are the main classes of our Parking Lot System:

* **ParkingLot:** The central part of the organization for which this software has been designed. It has attributes like ‘Name’ to distinguish it from any other parking lots and ‘Address’ to define its location.
* **ParkingFloor:** The parking lot will have many parking floors.
* **ParkingSpot:** Each parking floor will have many parking spots. Our system will support different parking spots 1) Handicapped, 2) Compact, 3) Large, 4) Motorcycle, and 5) Electric.
* **Account:** We will have two types of accounts in the system: one for an Admin, and the other for a parking attendant.
* **Parking ticket:** This class will encapsulate a parking ticket. Customers will take a ticket when they enter the parking lot.
* **Vehicle:** Vehicles will be parked in the parking spots. Our system will support different types of vehicles 1) Car, 2) Truck, 3) Electric, 4) Van and 5) Motorcycle.
* **EntrancePanel and ExitPanel:** EntrancePanel will print tickets, and ExitPanel will facilitate payment of the ticket fee.
* **Payment:** This class will be responsible for making payments. The system will support credit card and cash transactions.
* **ParkingRate:** This class will keep track of the hourly parking rates. It will specify a dollar amount for each hour. For example, for a two hour parking ticket, this class will define the cost for the first and the second hour.
* **ParkingDisplayBoard:** Each parking floor will have a display board to show available parking spots for each spot type. This class will be responsible for displaying the latest availability of free parking spots to the customers.
* **ParkingAttendantPortal:** This class will encapsulate all the operations that an attendant can perform, like scanning tickets and processing payments.
* **CustomerInfoPortal:** This class will encapsulate the info portal that customers use to pay for the parking ticket. Once paid, the info portal will update the ticket to keep track of the payment.
* **ElectricPanel:** Customers will use the electric panels to pay and charge their electric vehicles.

<p align="center">
    <img src="/media-files/parking-class-diagram.png" alt="Parking Lot Class Diagram">
    <br />
    Class Diagram for Parking Lot
</p>

<p align="center">
    <img src="/media-files/parking-uml.svg" alt="Parking Lot UML">
    <br />
    UML for Parking Lot
</p>

### Activity Diagram

**Customer paying for parking ticket:** Any customer can perform this activity. Here are the set of steps:

<p align="center">
    <img src="/media-files/parking-ticket.svg" alt="Parking Ticket Activity Diagram">
    <br />
    Activity Diagram for Parking Lot Parking Ticket
</p>

### Code

Following is the skeleton code for our parking lot system:

**Enums and Constants:** Here are the required enums, data types, and constants:

import java.util.*;

enum VehicleType {
    CAR, TRUCK, ELECTRIC, VAN, MOTORBIKE
}

enum ParkingSpotType {
    HANDICAPPED, COMPACT, LARGE, MOTORBIKE, ELECTRIC
}

enum AccountStatus {
    ACTIVE, BLOCKED, BANNED, COMPROMISED, ARCHIVED, UNKNOWN
}

enum ParkingTicketStatus {
    ACTIVE, PAID, LOST
}

class Address {
    private String streetAddress;
    private String city;
    private String state;
    private String zipCode;
    private String country;

    public Address(String street, String city, String state, String zipCode, String country) {
        this.streetAddress = street;
        this.city = city;
        this.state = state;
        this.zipCode = zipCode;
        this.country = country;
    }
}

class Person {
    private String name;
    private Address address;
    private String email;
    private String phone;

    public Person(String name, Address address, String email, String phone) {
        this.name = name;
        this.address = address;
        this.email = email;
        this.phone = phone;
    }
}

class Account {
    private String userName;
    private String password;
    private Person person;
    private AccountStatus status;

    public Account(String userName, String password, Person person, AccountStatus status) {
        this.userName = userName;
        this.password = password;
        this.person = person;
        this.status = status;
    }

    public void resetPassword() {
        // Reset password logic
    }
}

class Admin extends Account {
    public Admin(String userName, String password, Person person, AccountStatus status) {
        super(userName, password, person, status);
    }

    public void addParkingFloor(String floor) {
        // Logic to add parking floor
    }

    public void addParkingSpot(String floorName, String spot) {
        // Logic to add parking spot
    }

    public void addParkingDisplayBoard(String floorName, String displayBoard) {
        // Logic to add parking display board
    }

    public void addCustomerInfoPanel(String floorName, String infoPanel) {
        // Logic to add customer info panel
    }

    public void addEntrancePanel(String entrancePanel) {
        // Logic to add entrance panel
    }

    public void addExitPanel(String exitPanel) {
        // Logic to add exit panel
    }
}

class ParkingAttendant extends Account {
    public ParkingAttendant(String userName, String password, Person person, AccountStatus status) {
        super(userName, password, person, status);
    }

    public void processTicket(String ticketNumber) {
        // Logic to process ticket
    }
}

abstract class ParkingSpot {
    private String number;
    private boolean isFree;
    private Object vehicle; // Placeholder for vehicle object
    private ParkingSpotType parkingSpotType;

    public ParkingSpot(String number, ParkingSpotType parkingSpotType) {
        this.number = number;
        this.isFree = true;
        this.vehicle = null;
        this.parkingSpotType = parkingSpotType;
    }

    public boolean isFree() {
        return isFree;
    }

    public void assignVehicle(Object vehicle) {
        this.vehicle = vehicle;
        this.isFree = false;
    }

    public void removeVehicle() {
        this.vehicle = null;
        this.isFree = true;
    }

    public String getNumber() {
        return number;
    }

    public ParkingSpotType getParkingSpotType() {
        return parkingSpotType;
    }
}

class HandicappedSpot extends ParkingSpot {
    public HandicappedSpot(String number) {
        super(number, ParkingSpotType.HANDICAPPED);
    }
}

class CompactSpot extends ParkingSpot {
    public CompactSpot(String number) {
        super(number, ParkingSpotType.COMPACT);
    }
}

class LargeSpot extends ParkingSpot {
    public LargeSpot(String number) {
        super(number, ParkingSpotType.LARGE);
    }
}

class MotorbikeSpot extends ParkingSpot {
    public MotorbikeSpot(String number) {
        super(number, ParkingSpotType.MOTORBIKE);
    }
}

class ElectricSpot extends ParkingSpot {
    public ElectricSpot(String number) {
        super(number, ParkingSpotType.ELECTRIC);
    }
}

class ParkingFloor {
    private String name;
    private Map<String, ParkingSpot> handicappedSpots = new HashMap<>();
    private Map<String, ParkingSpot> compactSpots = new HashMap<>();
    private Map<String, ParkingSpot> largeSpots = new HashMap<>();
    private Map<String, ParkingSpot> motorbikeSpots = new HashMap<>();
    private Map<String, ParkingSpot> electricSpots = new HashMap<>();
    private ParkingDisplayBoard displayBoard;

    public ParkingFloor(String name) {
        this.name = name;
        this.displayBoard = new ParkingDisplayBoard();
    }

    public void addParkingSpot(ParkingSpot spot) {
        switch (spot.getParkingSpotType()) {
            case HANDICAPPED:
                handicappedSpots.put(spot.getNumber(), spot);
                break;
            case COMPACT:
                compactSpots.put(spot.getNumber(), spot);
                break;
            case LARGE:
                largeSpots.put(spot.getNumber(), spot);
                break;
            case MOTORBIKE:
                motorbikeSpots.put(spot.getNumber(), spot);
                break;
            case ELECTRIC:
                electricSpots.put(spot.getNumber(), spot);
                break;
            default:
                System.out.println("Invalid parking spot type!");
        }
    }

    // Add other methods like assignVehicleToSpot, freeSpot, updateDisplayBoard
}

class ParkingDisplayBoard {
    private String id;
    private ParkingSpot handicappedFreeSpot;
    private ParkingSpot compactFreeSpot;
    private ParkingSpot largeFreeSpot;
    private ParkingSpot motorbikeFreeSpot;
    private ParkingSpot electricFreeSpot;

    public void showEmptySpotNumber() {
        System.out.println("Handicapped Free Spot: " + (handicappedFreeSpot != null ? handicappedFreeSpot.getNumber() : "Full"));
        System.out.println("Compact Free Spot: " + (compactFreeSpot != null ? compactFreeSpot.getNumber() : "Full"));
        System.out.println("Large Free Spot: " + (largeFreeSpot != null ? largeFreeSpot.getNumber() : "Full"));
        System.out.println("Motorbike Free Spot: " + (motorbikeFreeSpot != null ? motorbikeFreeSpot.getNumber() : "Full"));
        System.out.println("Electric Free Spot: " + (electricFreeSpot != null ? electricFreeSpot.getNumber() : "Full"));
    }

    // Add getters and setters for each spot type
}

// Singleton for ParkingLot
class ParkingLot {
    private static ParkingLot instance;

    private ParkingLot() {
    }

    public static synchronized ParkingLot getInstance() {
        if (instance == null) {
            instance = new ParkingLot();
        }
        return instance;
    }

    // Implement other ParkingLot methods
}

