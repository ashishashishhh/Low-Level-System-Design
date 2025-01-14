<h1 align="center">Design a Car Rental System</h1>
<h3 align="center">Let's design a Car Rental System</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagrams](#activity-diagrams)
* [Code](#code)

A Car Rental System is a software built to handle the renting of automobiles for a short period of time, generally ranging from a few hours to a few weeks. A car rental system often has numerous local branches (to allow its user to return a vehicle to a different location), and primarily located near airports or busy city areas.

<p align="center">
    <img src="/media-files/car-rent.png" alt="Car Rental System">
    <br />
    Car Rental System
</p>

### System Requirements

We will focus on the following set of requirements while designing our Car Rental System:

1. The system will support the renting of different automobiles like cars, trucks, SUVs, vans, and motorcycles.
2. Each vehicle should be added with a unique barcode and other details, including a parking stall number which helps to locate the vehicle.
3. The system should be able to retrieve information like which member took a particular vehicle or what vehicles have been rented out by a specific member.
4. The system should collect a late-fee for vehicles returned after the due date.
5. Members should be able to search the vehicle inventory and reserve any available vehicle.
6. The system should be able to send notifications whenever the reservation is approaching the pick-up date, as well as when the vehicle is nearing the due date or has not been returned within the due date.
7. The system will be able to read barcodes from vehicles.
8. Members should be able to cancel their reservations.
9. The system should maintain a vehicle log to track all events related to the vehicles.
10. Members can add rental insurance to their reservation.
11. Members can rent additional equipment, like navigation, child seat, ski rack, etc.
12. Members can add additional services to their reservation, such as roadside assistance, additional driver, wifi, etc.

### Use Case Diagram

We have four main Actors in our system:

* **Receptionist:** Mainly responsible for adding and modifying vehicles and workers. Receptionists can also reserve vehicles.
* **Member:** All members can search the catalog, as well as reserve, pick-up, and return a vehicle.
* **System:** Mainly responsible for sending notifications about overdue vehicles, canceled reservation, etc.
* **Worker:** Mainly responsible for taking care of a returned vehicle and updating the vehicle log.

Here are the top use cases of the Car Rental System:

* **Add/Remove/Edit vehicle:** To add, remove or modify a vehicle.
* **Search catalog:** To search for vehicles by type and availability.
* **Register new account/Cancel membership:** To add a new member or cancel an existing membership.
* **Reserve vehicle:** To reserve a vehicle.
* **Check-out vehicle:** To rent a vehicle.
* **Return a vehicle:** To return a vehicle which was checked-out to a member.
* **Add equipment:** To add an equipment to a reservation like navigation, child seat, etc.
* **Update car log:** To add or update a car log entry, such as refueling, cleaning, damage, etc.

Here is the use case diagram of our Car Rental System:

<p align="center">
    <img src="/media-files/car-rent-use-case-diagram.svg" alt="Car Rental System Use Case Diagram">
    <br />
    Use Case Diagram for Car Rental System
</p>

### Class Diagram

Here are the main classes of our Car Rental System:

* **CarRentalSystem:** The main part of the organization for which this software has been designed.
* **CarRentalLocation:** The car rental system will have multiple locations, each location will have attributes like ‘Name’ to distinguish it from any other locations and ‘Address’ which defines the address of the rental location.
* **Vehicle:** The basic building block of the system. Every vehicle will have a barcode, license plate number, passenger capacity, model, make, mileage, etc. Vehicles can be of multiple types, like car, truck, SUV, etc.
* **Account:** Mainly, we will have two types of accounts in the system, one will be a general member and the other will be a receptionist. Another account can be of the worker taking care of the returned vehicle.
* **VehicleReservation:** This class will be responsible for managing reservations for a vehicle.
* **Notification:** Will take care of sending notifications to members.
* **VehicleLog:** To keep track of all the events related to a vehicle.
* **RentalInsurance:** Stores details about the various rental insurances that members can add to their reservation.
* **Equipment:** Stores details about the various types of equipment that members can add to their reservation.
* **Service:** Stores details about the various types of service that members can add to their reservation, such as additional drivers, roadside assistance, etc.
* **Bill:** Contains different bill-items for every charge for the reservation.

<p align="center">
    <img src="/media-files/car-rent-class-diagram.png" alt="Car Rental System Class Diagram">
    <br />
    Class Diagram for Car Rental System
</p>

<p align="center">
    <img src="/media-files/car-rent-uml.svg" alt="Car Rental System UML">
    <br />
    UML for Car Rental System
</p>

### Activity Diagrams

**Pick up a vehicle:** Any member can perform this activity. Here are the steps to pick up a vehicle:

<p align="center">
    <img src="/media-files/car-rent-pick-up-activity-diagram.svg" alt="Car Rental System Pick Up Activity Diagram">
    <br />
    Activity Diagram for Car Rental System Pick Up
</p>

**Return a vehicle:** Any worker can perform this activity. While returning a vehicle, the system must collect a late fee from the member if the return date is after the due date. Here are the steps for returning a vehicle:

<p align="center">
    <img src="/media-files/car-rent-return-activity-diagram.svg" alt="Car Rental System Return Activity Diagram">
    <br />
    Activity Diagram for Car Rental System Return
</p>

### Code

Here is the high-level definition for the classes described above.


import java.util.*;

enum VehicleType {
    CAR, TRUCK, SUV, VAN, MOTORCYCLE
}

enum Equipment {
    NAVIGATION, CHILD_SEAT, SKI_RACK
}

enum Service {
    ROADSIDE_ASSISTANCE, ADDITIONAL_DRIVER, WIFI
}

class Vehicle {
    private VehicleType type;
    private int barcode;
    private int parkingSlot;
    private Date rentDate;
    private Date dueDate;

    public Vehicle(VehicleType type) {
        this.type = type;
        this.barcode = new Random().nextInt(90000) + 10000;
        this.parkingSlot = new Random().nextInt(900) + 100;
        this.rentDate = null;
        this.dueDate = null;
    }

    public void clearBooking() {
        this.rentDate = null;
        this.dueDate = null;
    }

    // Getters and setters
    public VehicleType getType() {
        return type;
    }

    public int getBarcode() {
        return barcode;
    }

    public Date getRentDate() {
        return rentDate;
    }

    public void setRentDate(Date rentDate) {
        this.rentDate = rentDate;
    }

    public Date getDueDate() {
        return dueDate;
    }

    public void setDueDate(Date dueDate) {
        this.dueDate = dueDate;
    }
}

class Member {
    private String name;
    private String id;
    private boolean isInsured;
    private List<Equipment> equipments;
    private List<Service> services;
    private Vehicle rentedVehicle;
    private Vehicle bookedVehicle;

    public Member(String name, String id) {
        this.name = name;
        this.id = id;
        this.isInsured = false;
        this.equipments = new ArrayList<>();
        this.services = new ArrayList<>();
        this.rentedVehicle = null;
        this.bookedVehicle = null;
    }

    // Getters and setters
    public Vehicle getRentedVehicle() {
        return rentedVehicle;
    }

    public void setRentedVehicle(Vehicle rentedVehicle) {
        this.rentedVehicle = rentedVehicle;
    }

    public Vehicle getBookedVehicle() {
        return bookedVehicle;
    }

    public void setBookedVehicle(Vehicle bookedVehicle) {
        this.bookedVehicle = bookedVehicle;
    }
}

class RentingSystem {
    private Map<String, Member> members;
    private List<Vehicle> availableVehicles;
    private Map<Integer, Vehicle> bookedVehicles;
    private Map<Integer, Vehicle> rentedVehicles;

    public RentingSystem() {
        this.members = new HashMap<>();
        this.availableVehicles = new ArrayList<>();
        this.bookedVehicles = new HashMap<>();
        this.rentedVehicles = new HashMap<>();
    }

    public void registerMember(String name, String id) {
        Member member = new Member(name, id);
        members.put(id, member);
    }

    public void addVehicle(VehicleType type) {
        Vehicle vehicle = new Vehicle(type);
        availableVehicles.add(vehicle);
    }

    public List<Vehicle> searchVehicle(VehicleType type) {
        List<Vehicle> results = new ArrayList<>();
        for (Vehicle vehicle : availableVehicles) {
            if (vehicle.getType() == type) {
                results.add(vehicle);
            }
        }
        return results;
    }

    public String reserveVehicle(Vehicle vehicle, Date bookingDate) {
        if (!availableVehicles.remove(vehicle)) {
            return "Vehicle not available";
        }
        bookedVehicles.put(vehicle.getBarcode(), vehicle);
        vehicle.setRentDate(bookingDate);
        return "Booked successfully";
    }

    public String rentVehicle(Vehicle vehicle, int days) {
        if (!bookedVehicles.containsKey(vehicle.getBarcode())) {
            return "Vehicle not booked";
        }
        bookedVehicles.remove(vehicle.getBarcode());
        rentedVehicles.put(vehicle.getBarcode(), vehicle);
        vehicle.setRentDate(new Date());
        Calendar calendar = Calendar.getInstance();
        calendar.setTime(vehicle.getRentDate());
        calendar.add(Calendar.DAY_OF_YEAR, days);
        vehicle.setDueDate(calendar.getTime());
        return "Rented successfully";
    }

    public String returnVehicle(Member member) {
        Vehicle vehicle = member.getRentedVehicle();
        if (vehicle == null) {
            return "No vehicle rented";
        }
        if (new Date().after(vehicle.getDueDate())) {
            return "Late fee applicable";
        }
        rentedVehicles.remove(vehicle.getBarcode());
        vehicle.clearBooking();
        availableVehicles.add(vehicle);
        return "Vehicle returned successfully";
    }

    public String cancelReservation(Member member) {
        Vehicle vehicle = member.getBookedVehicle();
        if (vehicle == null) {
            return "Vehicle not booked";
        }
        if (!bookedVehicles.containsKey(vehicle.getBarcode())) {
            return "Cannot find booking";
        }
        bookedVehicles.remove(vehicle.getBarcode());
        availableVehicles.add(vehicle);
        return "Reservation canceled successfully";
    }
}
