<h1 align="center">Design a Hotel Management System</h1>
<h3 align="center">Let's design a Hotel Management System</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagrams](#activity-diagrams)
* [Code](#code)

A Hotel Management System is a software built to handle all online hotel activities easily and safely. This System will give the hotel management power and flexibility to manage the entire system from a single online portal. The system allows the manager to keep track of all the available rooms in the system as well as to book rooms and generate bills.

<p align="center">
    <img src="/media-files/hotel-management-system.png" alt="Hotel Management System">
    <br />
    Hotel Management System
</p>

### System Requirements

We’ll focus on the following set of requirements while designing the Hotel Management System:

1. The system should support the booking of different room types like standard, deluxe, family suite, etc.
2. Guests should be able to search the room inventory and book any available room.
3. The system should be able to retrieve information, such as who booked a particular room, or what rooms were booked by a specific customer.
4. The system should allow customers to cancel their booking - and provide them with a full refund if the cancelation occurs before 24 hours of the check-in date.
5. The system should be able to send notifications whenever the booking is nearing the check-in or check-out date.
6. The system should maintain a room housekeeping log to keep track of all housekeeping tasks.
7. Any customer should be able to add room services and food items.
8. Customers can ask for different amenities.
9. The customers should be able to pay their bills through credit card, check or cash.

### Use Case Diagram

Here are the main Actors in our system:

* **Guest:** All guests can search the available rooms, as well as make a booking.
* **Receptionist:** Mainly responsible for adding and modifying rooms, creating room bookings, check-in, and check-out customers.
* **System:** Mainly responsible for sending notifications for room booking, cancellation, etc.
* **Manager:** Mainly responsible for adding new workers.
* **Housekeeper:** To add/modify housekeeping record of rooms.
* **Server:** To add/modify room service record of rooms.

Here are the top use cases of the Hotel Management System:

* **Add/Remove/Edit room:** To add, remove, or modify a room in the system.
* **Search room:** To search for rooms by type and availability.
* **Register or cancel an account:** To add a new member or cancel the membership of an existing member.
* **Book room:** To book a room.
* **Check-in:** To let the guest check-in for their booking.
* **Check-out:** To track the end of the booking and the return of the room keys.
* **Add room charge:** To add a room service charge to the customer’s bill.
* **Update housekeeping log:** To add or update the housekeeping entry of a room.

Here is the use case diagram of our Hotel Management System:

<p align="center">
    <img src="/media-files/hms-use-case-diagram.svg" alt="Hotel Management System Use Case Diagram">
    <br />
    Use Case Diagram for Hotel Management System
</p>

### Class Diagram

Here are the main classes of our Hotel Management System:

* **Hotel and HotelLocation:** Our system will support multiple locations of a hotel.
* **Room:** The basic building block of the system. Every room will be uniquely identified by the room number. Each Room will have attributes like Room Style, Booking Price, etc.
* **Account:** We will have different types of accounts in the system: one will be a guest to search and book rooms, another will be a receptionist. Housekeeping will keep track of the housekeeping records of a room, and a Server will handle room service.
* **RoomBooking:** This class will be responsible for managing bookings for a room.
* **Notification:** Will take care of sending notifications to guests.
* **RoomHouseKeeping:** To keep track of all housekeeping records for rooms.
* **RoomCharge:** Encapsulates the details about different types of room services that guests have requested.
* **Invoice:** Contains different invoice-items for every charge against the room.
* **RoomKey:** Each room can be assigned an electronic key card. Keys will have a barcode and will be uniquely identified by a key-ID.

<p align="center">
    <img src="/media-files/hms-class-diagram.png" alt="Hotel Management System Class Diagram">
    <br />
    Class Diagram for Hotel Management System
</p>

<p align="center">
    <img src="/media-files/hms-uml.svg" alt="Hotel Management System UML">
    <br />
    UML for Hotel Management System
</p>

### Activity Diagrams

**Make a room booking:** Any guest or receptionist can perform this activity. Here are the set of steps to book a room:

<p align="center">
    <img src="/media-files/hms-room-booking-activity-diagram.svg" alt="Hotel Management System Room Booking">
    <br />
    Activity Diagram for Hotel Management System Room Booking
</p>

**Check in:** Guest will check in for their booking. The Receptionist can also perform this activity. Here are the steps:

<p align="center">
    <img src="/media-files/hms-check-in-activity-diagram.svg" alt="Hotel Management System Check in">
    <br />
    Activity Diagram for Hotel Management System Check in
</p>

**Cancel a booking:** Guest can cancel their booking. Receptionist can perform this activity. Here are the different steps of this activity:

<p align="center">
    <img src="/media-files/hms-cancel-booking-activity-diagram.svg" alt="Hotel Management System Cancel Booking">
    <br />
    Activity Diagram for Hotel Management System Cancel Booking
</p>

### Code

Here is the high-level definition for the classes described above.

public enum RoomStyle {
  STANDARD, DELUXE, FAMILY_SUITE, BUSINESS_SUITE
}

public enum RoomStatus {
  AVAILABLE, RESERVED, OCCUPIED, NOT_AVAILABLE, BEING_SERVICED, OTHER
}

public enum BookingStatus {
  REQUESTED, PENDING, CONFIRMED, CHECKED_IN, CHECKED_OUT, CANCELLED, ABANDONED
}

public enum AccountStatus {
  ACTIVE, CLOSED, CANCELED, BLACKLISTED, BLOCKED
}

public enum AccountType {
  MEMBER, GUEST, MANAGER, RECEPTIONIST
}

public enum PaymentStatus {
  UNPAID, PENDING, COMPLETED, FILLED, DECLINED, CANCELLED, ABANDONED, SETTLING, SETTLED, REFUNDED
}

// Observer Pattern for notifications
interface Observer {
    void update(String message);
}

class Guest implements Observer {
    private String name;
    private int totalRoomsCheckedIn;

    public List<RoomBooking> getBookings() {
        // return booking details
    }

    @Override
    public void update(String message) {
        System.out.println("Notification for Guest: " + name + ": " + message);
    }
}

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

// Factory Method Pattern for creating rooms and room services
abstract class RoomFactory {
    public abstract Room createRoom(RoomStyle style, String roomNumber, double price, boolean isSmoking);
}

class DeluxeRoomFactory extends RoomFactory {
    @Override
    public Room createRoom(RoomStyle style, String roomNumber, double price, boolean isSmoking) {
        return new Room(roomNumber, style, price, isSmoking);
    }
}

class FamilySuiteRoomFactory extends RoomFactory {
    @Override
    public Room createRoom(RoomStyle style, String roomNumber, double price, boolean isSmoking) {
        return new Room(roomNumber, style, price, isSmoking);
    }
}

// Strategy Pattern for searching rooms
interface SearchStrategy {
    List<Room> searchRooms(List<Room> rooms, RoomStyle style, Date startDate, int duration);
}

class RoomStyleSearchStrategy implements SearchStrategy {
    @Override
    public List<Room> searchRooms(List<Room> rooms, RoomStyle style, Date startDate, int duration) {
        List<Room> result = new ArrayList<>();
        for (Room room : rooms) {
            if (room.getStyle() == style && room.isRoomAvailable()) {
                result.add(room);
            }
        }
        return result;
    }
}

class RoomAvailabilitySearchStrategy implements SearchStrategy {
    @Override
    public List<Room> searchRooms(List<Room> rooms, RoomStyle style, Date startDate, int duration) {
        List<Room> result = new ArrayList<>();
        for (Room room : rooms) {
            if (room.isRoomAvailable() && room.getStyle() == style) {
                result.add(room);
            }
        }
        return result;
    }
}

// Command Pattern for handling room bookings and services
interface Command {
    void execute();
}

class BookRoomCommand implements Command {
    private RoomBooking booking;

    public BookRoomCommand(RoomBooking booking) {
        this.booking = booking;
    }

    @Override
    public void execute() {
        System.out.println("Booking room for reservation: " + booking.getReservationNumber());
        booking.setStatus(BookingStatus.CONFIRMED);
    }
}

class CancelBookingCommand implements Command {
    private RoomBooking booking;

    public CancelBookingCommand(RoomBooking booking) {
        this.booking = booking;
    }

    @Override
    public void execute() {
        System.out.println("Cancelling booking for reservation: " + booking.getReservationNumber());
        booking.setStatus(BookingStatus.CANCELLED);
    }
}

// Template Method Pattern for Housekeeping and Room Service
abstract class RoomServiceTemplate {
    public final void executeService(Room room) {
        checkServiceAvailability();
        performService(room);
        addServiceCharge(room);
    }

    protected abstract void checkServiceAvailability();
    protected abstract void performService(Room room);
    protected abstract void addServiceCharge(Room room);
}

class HousekeepingService extends RoomServiceTemplate {
    @Override
    protected void checkServiceAvailability() {
        System.out.println("Checking availability for housekeeping service.");
    }

    @Override
    protected void performService(Room room) {
        System.out.println("Performing housekeeping for room: " + room.getRoomNumber());
    }

    @Override
    protected void addServiceCharge(Room room) {
        System.out.println("Adding housekeeping charge to room: " + room.getRoomNumber());
    }
}

class FoodService extends RoomServiceTemplate {
    @Override
    protected void checkServiceAvailability() {
        System.out.println("Checking availability for food service.");
    }

    @Override
    protected void performService(Room room) {
        System.out.println("Serving food to room: " + room.getRoomNumber());
    }

    @Override
    protected void addServiceCharge(Room room) {
        System.out.println("Adding food service charge to room: " + room.getRoomNumber());
    }
}

// Supporting Classes
public class Room {
    private String roomNumber;
    private RoomStyle style;
    private RoomStatus status;
    private double bookingPrice;
    private boolean isSmoking;

    public Room(String roomNumber, RoomStyle style, double bookingPrice, boolean isSmoking) {
        this.roomNumber = roomNumber;
        this.style = style;
        this.bookingPrice = bookingPrice;
        this.isSmoking = isSmoking;
        this.status = RoomStatus.AVAILABLE;
    }

    public String getRoomNumber() {
        return roomNumber;
    }

    public RoomStyle getStyle() {
        return style;
    }

    public RoomStatus getStatus() {
        return status;
    }

    public boolean isRoomAvailable() {
        return status == RoomStatus.AVAILABLE;
    }

    public void checkIn() {
        status = RoomStatus.OCCUPIED;
    }

    public void checkOut() {
        status = RoomStatus.AVAILABLE;
    }
}

public class RoomBooking {
    private String reservationNumber;
    private Date startDate;
    private int durationInDays;
    private BookingStatus status;
    private Date checkin;
    private Date checkout;
    private Room room;

    public RoomBooking(String reservationNumber, Room room, Date startDate, int durationInDays) {
        this.reservationNumber = reservationNumber;
        this.room = room;
        this.startDate = startDate;
        this.durationInDays = durationInDays;
        this.status = BookingStatus.PENDING;
    }

    public String getReservationNumber() {
        return reservationNumber;
    }

    public void setStatus(BookingStatus status) {
        this.status = status;
    }
}

// Main class for testing
public class Main {
    public static void main(String[] args) {
        // Create rooms using Factory Pattern
        RoomFactory deluxeFactory = new DeluxeRoomFactory();
        Room room1 = deluxeFactory.createRoom(RoomStyle.DELUXE, "101", 200.0, false);

        // Create room booking
        RoomBooking booking1 = new RoomBooking("R123", room1, new Date(), 3);

        // Create commands for booking and canceling
        Command bookRoom = new BookRoomCommand(booking1);
        Command cancelBooking = new CancelBookingCommand(booking1);

        // Execute commands
        bookRoom.execute();
        cancelBooking.execute();

        // Execute room service using Template Method Pattern
        RoomServiceTemplate housekeeping = new HousekeepingService();
        housekeeping.executeService(room1);

        // System notification (Observer Pattern)
        SystemNotifier notifier = new SystemNotifier();
        Guest guest = new Guest(); // Observer
        notifier.addObserver(guest);
        notifier.notifyObservers("Your room booking is confirmed.");
    }
}

