<h1 align="center">Design a Library Management System</h1>
<h3 align="center">Let's design a Library Management System</h3>

**We'll cover the following:**

- [System Requirements](#system-requirements)
- [Use Case Diagram](#use-case-diagram)
- [Class Diagram](#class-diagram)
- [Activity Diagrams](#activity-diagrams)
- [Code](#code)

A Library Management System is a software built to handle the primary housekeeping functions of a library. Libraries rely on library management systems to manage asset collections as well as relationships with their members. Library management systems help libraries keep track of the books and their checkouts, as well as members’ subscriptions and profiles.

Library management systems also involve maintaining the database for entering new books and recording books that have been borrowed with their respective due dates.

<p align="center">
    <img src="/media-files/library-system.png" alt="Library Management System">
    <br />
    Library Management System
</p>

### System Requirements

<p align="center">
    <b>
        <i>
            Always clarify requirements at the beginning of the interview. Be sure to ask questions to find the exact scope of the system that the interviewer has in mind.
        </i>
    </b>
</p>

We will focus on the following set of requirements while designing the Library Management System:

1. Any library member should be able to search books by their title, author, subject category as well by the publication date.
2. Each book will have a unique identification number and other details including a rack number which will help to physically locate the book.
3. There could be more than one copy of a book, and library members should be able to check-out and reserve any copy. We will call each copy of a book, a book item.
4. The system should be able to retrieve information like who took a particular book or what are the books checked-out by a specific library member.
5. There should be a maximum limit (5) on how many books a member can check-out.
6. There should be a maximum limit (10) on how many days a member can keep a book.
7. The system should be able to collect fines for books returned after the due date.
8. Members should be able to reserve books that are not currently available.
9. The system should be able to send notifications whenever the reserved books become available, as well as when the book is not returned within the due date.
10. Each book and member card will have a unique barcode. The system will be able to read barcodes from books and members’ library cards.

### Use Case Diagram

We have three main actors in our system:

- **Librarian:** Mainly responsible for adding and modifying books, book items, and users. The Librarian can also issue, reserve, and return book items.
- **Member:** All members can search the catalog, as well as check-out, reserve, renew, and return a book.
- **System:** Mainly responsible for sending notifications for overdue books, canceled reservations, etc.

Here are the top use cases of the Library Management System:

- **Add/Remove/Edit book:** To add, remove or modify a book or book item.
- **Search catalog:** To search books by title, author, subject or publication date.
- **Register new account/cancel membership:** To add a new member or cancel the membership of an existing member.
- **Check-out book:** To borrow a book from the library.
- **Reserve book:** To reserve a book which is not currently available.
- **Renew a book:** To reborrow an already checked-out book.
- **Return a book:** To return a book to the library which was issued to a member.

Here is the use case diagram of our Library Management System:

<p align="center">
    <img src="/media-files/lib-use-case-diagram.png" alt="Library Use Case Diagram">
    <br />
    Use Case Diagram for Library Management System
</p>

### Class Diagram

Here are the main classes of our Library Management System:

- **Library:** The central part of the organization for which this software has been designed. It has attributes like ‘Name’ to distinguish it from any other libraries and ‘Address’ to describe its location.
- **Book:** The basic building block of the system. Every book will have ISBN, Title, Subject, Publishers, etc.
- **BookItem:** Any book can have multiple copies, each copy will be considered a book item in our system. Each book item will have a unique barcode.
- **Account:** We will have two types of accounts in the system, one will be a general member, and the other will be a librarian.
- **LibraryCard:** Each library user will be issued a library card, which will be used to identify users while issuing or returning books.
- **BookReservation:** Responsible for managing reservations against book items.
- **BookLending:** Manage the checking-out of book items.
- **Catalog:** Catalogs contain list of books sorted on certain criteria. Our system will support searching through four catalogs: Title, Author, Subject, and Publish-date.
- **Fine:** This class will be responsible for calculating and collecting fines from library members.
- **Author:** This class will encapsulate a book author.
- **Rack:** Books will be placed on racks. Each rack will be identified by a rack number and will have a location identifier to describe the physical location of the rack in the library.
- **Notification:** This class will take care of sending notifications to library members.

<p align="center">
    <img src="/media-files/image.png" alt="Library Class Diagram">
    <br />
    Class Diagram for Library Management System
</p>

<p align="center">
    <img src="/media-files/lib-uml.svg" alt="Library UML">
    <br />
    UML for Library Management System
</p>

### Activity Diagrams

**Check-out a book:** Any library member or librarian can perform this activity. Here are the set of steps to check-out a book:

<p align="center">
    <img src="/media-files/lib-check-out-book.svg" alt="Check-out Book Activity Diagram">
    <br />
    Activity Diagram for Library Management System Check-out Book
</p>

**Return a book:** Any library member or librarian can perform this activity. The system will collect fines from members if they return books after the due date. Here are the steps for returning a book:

<p align="center">
    <img src="/media-files/lib-return-book.png" alt="Return Book Activity Diagram">
    <br />
    Activity Diagram for Library Management System Return Book
</p>

**Renew a book:** While renewing (re-issuing) a book, the system will check for fines and see if any other member has not reserved the same book, in that case the book item cannot be renewed. Here are the different steps for renewing a book:

<p align="center">
    <img src="/media-files/lib-renew-book.svg" alt="Renew Book Activity Diagram">
    <br />
    Activity Diagram for Library Management System Renew Book
</p>

### Code

Here is the code for the use cases mentioned above: 1) Check-out a book, 2) Return a book, and 3) Renew a book.

Note: This code only focuses on the design part of the use cases. Since you are not required to write a fully executable code in an interview, you can assume parts of the code to interact with the database, payment system, etc.

**Enums and Constants:** Here are the required enums, data types, and constants:

**Code Snippet:**

```python
from abc import ABC
from enum import Enum


class BookFormat(Enum):
    HARDCOVER, PAPERBACK, AUDIO_BOOK, EBOOK, NEWSPAPER, MAGAZINE, JOURNAL = 1, 2, 3, 4, 5, 6, 7


class BookStatus(Enum):
    AVAILABLE, RESERVED, LOANED, LOST = 1, 2, 3, 4


class ReservationStatus(Enum):
    WAITING, PENDING, CANCELED, NONE = 1, 2, 3, 4


class AccountStatus(Enum):
    ACTIVE, CLOSED, CANCELED, BLACKLISTED, NONE = 1, 2, 3, 4, 5


class Address:
    def __init__(self, street, city, state, zip_code, country):
        self.__street_address = street
        self.__city = city
        self.__state = state
        self.__zip_code = zip_code
        self.__country = country


class Person(ABC):
    def __init__(self, name, address, email, phone):
        self.__name = name
        self.__address = address
        self.__email = email
        self.__phone = phone


class Constants:
    def __init__(self):
          self.MAX_BOOKS_ISSUED_TO_A_USER = 5
          self.MAX_LENDING_DAYS = 10


```

**Account, Member, and Librarian:** These classes represent various people that interact with our system:

**Code Snippet:**

```python
# For simplicity, we are not defining getter and setter functions. The reader can
# assume that all class attributes are private and accessed through their respective
# public getter methods and modified only through their public methods function.


from abc import ABC
from datetime import datetime

from .constants import *
from .models import *


class Account(ABC):
    def __init__(self, id, password, person, status=AccountStatus.Active):
        self.__id = id
        self.__password = password
        self.__status = status
        self.__person = person

    def reset_password(self):
        None


class Librarian(Account):
    def __init__(self, id, password, person, status=AccountStatus.Active):
        super().__init__(id, password, person, status)

    def add_book_item(self, book_item):
        None

    def block_member(self, member):
        None

    def un_block_member(self, member):
        None


class Member(Account):
    def __init__(self, id, password, person, status=AccountStatus.Active):
        super().__init__(id, password, person, status)
        self.__date_of_membership = datetime.date.today()
        self.__total_books_checkedout = 0

    def get_total_books_checkedout(self):
        return self.__total_books_checkedout

    def reserve_book_item(self, book_item):
        None

    def increment_total_books_checkedout(self):
        None

    def renew_book_item(self, book_item):
        None

    def checkout_book_item(self, book_item):
        if self.get_total_books_checked_out() >= Constants.MAX_BOOKS_ISSUED_TO_A_USER:
            print("The user has already checked-out maximum number of books")
            return False
        book_reservation = BookReservation.fetch_reservation_details(book_item.get_barcode())
        if book_reservation != None and book_reservation.get_member_id() != self.get_id():
            # book item has a pending reservation from another user
            print("self book is reserved by another member")
            return False
        elif book_reservation != None:
            # book item has a pending reservation from the give member, update it
            book_reservation.update_status(ReservationStatus.COMPLETED)

        if not book_item.checkout(self.get_id()):
            return False

        self.increment_total_books_checkedout()
        return True

    def check_for_fine(self, book_item_barcode):
        book_lending = BookLending.fetch_lending_details(book_item_barcode)
        due_date = book_lending.get_due_date()
        today = datetime.date.today()
        # check if the book has been returned within the due date
        if today > due_date:
            diff = today - due_date
            diff_days = diff.days
            Fine.collect_fine(self.get_member_id(), diff_days)

    def return_book_item(self, book_item):
        self.check_for_fine(book_item.get_barcode())
        book_reservation = BookReservation.fetch_reservation_details(book_item.get_barcode())
        if book_reservation != None:
            # book item has a pending reservation
            book_item.update_book_item_status(BookStatus.RESERVED)
            book_reservation.send_book_available_notification()
            book_item.update_book_item_status(BookStatus.AVAILABLE)

    def renew_book_item(self, book_item):
        self.check_for_fine(book_item.get_barcode())
        book_reservation = BookReservation.fetch_reservation_details(
        book_item.get_barcode())
        # check if self book item has a pending reservation from another member
        if book_reservation != None and book_reservation.get_member_id() != self.get_member_id():
            print("self book is reserved by another member")
            self.decrement_total_books_checkedout()
            book_item.update_book_item_state(BookStatus.RESERVED)
            book_reservation.send_book_available_notification()
            return False
        elif book_reservation != None:
            # book item has a pending reservation from self member
            book_reservation.update_status(ReservationStatus.COMPLETED)

        BookLending.lend_book(book_item.get_bar_code(), self.get_member_id())
        book_item.update_due_date(datetime.datetime.now().AddDays(Constants.MAX_LENDING_DAYS))
        return True


```

**BookReservation, BookLending, and Fine:** These classes represent a book reservation, lending, and fine collection, respectively.

**Code Snippet:**

This is my first take on the famous "Design a Library Management System". Feel free to provide feedback on what's wrong / how this can be improved.


Requirements
Books have the following information:


Unique id
Title
Author
Publication Date
There can be multiple copies of the same book (book items). Each book item has a unique barcode.


There can be 2 types of users:


Librarians - Can add and remove books, book items and users, search the catalog (by title, author or publication date). Can also checkout, renew and return books.
General members - can search the catalog (by title, author or publication date), as well as check-out, renew, and return a book.
Each user has a unique barcode and a name.


Also, we have the following limitations:


A member can checkout at most 3 books
A member can keep a book at most 20 days.
The system should be able to calculate the fine for the users who return the books after the expected deadline.
My Solution:
We have the following classes/interfaces:


A BookDetails class representing the details for a given book (id, title, author, etc). This is NOT a book item, just a class describing book details. Notice that it is immutable (once created, cannot be modified) so it can be used as a key for Maps:


public class BookDetails {
	private String id;
	private String authorName;
	private LocalDateTime publicationDate;

	public BookDetails(String id, String authorName, LocalDateTime publicationDate) {
		this.id = id;
		this.authorName = authorName;
		this.publicationDate = publicationDate;
	}

	public String getId() {
		return id;
	}

	public String getAuthorName() {
		return authorName;
	}

	public LocalDateTime getPublicationDate() {
		return publicationDate;
	}

}
A BookItem class representing a single instance of a given book. We use aggregation here to get the book details. In addition to the book details, we are also adding a barcode property that is unique to each BookItem:


public class BookItem {
	public BookItem(String bookItemId, BookDetails bookDetails) {
		this.bookItemId = bookItemId;
		this.bookDetails = bookDetails;
	}

	private String bookItemId;

	private BookDetails bookDetails;

	public String getBookItemId() {
		return bookItemId;
	}

	public BookDetails getBookDetails() {
		return bookDetails;
	}
}
A UserType enum representing user types.


public enum UserType {
	LIBRARIAN, MEMBER
}
A User class representing the library users. Some solutions suggest creating multiple classes for different types of users (not sure what we are achieving by doing that):


public class User {
	public User(String barcode, String name, UserType userType) {
		this.barcode = barcode;
		this.name = name;
		this.userType = userType;
	}

	private String barcode;
	private String name;
	private UserType userType;

	public String getBarcode() {
		return barcode;
	}

	public UserType getUserType() {
		return userType;
	}

	public String getName() {
		return name;
	}
}
Now, let's look at the main class - the Library class that exposes all the necessary actions:


public class Library {

	private User currentUser;
	private UserRepository userRepository;
	private BookCatalog bookCatalog;
	private LendingService lendingService;

	private void ensureLoggedInUser() {
		Objects.requireNonNull(this.currentUser, "There should be a logged in user");
	}

	private void ensureLibrarianAccess() throws RestrictedAccessException {
		ensureLoggedInUser();
		if (currentUser.getUserType() != UserType.LIBRARIAN) {
			throw new RestrictedAccessException();
		}
	}

	public void loginUser(String barcode) {
		User user = userRepository.getUserByBarCode(barcode);

		Objects.requireNonNull(user, "Wrong barcode");

		this.currentUser = user;
	}

	public void createUser(User newUser) throws RestrictedAccessException {
		ensureLibrarianAccess();

		userRepository.addUser(newUser);
	}

	public void removeUser(String barcode) throws RestrictedAccessException {
		ensureLibrarianAccess();

		User user = userRepository.getUserByBarCode(barcode);

		Objects.requireNonNull(user, "No user found");

		userRepository.removeUser(barcode);
	}

	public void addBookItem(BookItem bookItem) throws RestrictedAccessException {
		ensureLibrarianAccess();

		bookCatalog.addBookItem(bookItem);
	}

	public void removeBookItem(String bookItemID) throws RestrictedAccessException  {
		ensureLibrarianAccess();

		bookCatalog.removeBookItem(bookItemID);
	}

	public List<BookDetails> searchByTitle(String title) {
		ensureLoggedInUser();

		return bookCatalog.searchByTitle(title);
	}

	public List<BookDetails> searchByAuthor(String name) {
		ensureLoggedInUser();

		return bookCatalog.searchByAuthor(name);
	}

	public List<BookDetails> searchByPublicationDate(LocalDateTime publicationDate) {
		ensureLoggedInUser();

		return bookCatalog.searchByPublicationDate(publicationDate);
	}

	public List<BookItem> getCheckoutBooks() {
		ensureLoggedInUser();

		return lendingService.getCheckedOutBooks(currentUser);
	}

	public List<User> getLendingUsers(String bookID) throws RestrictedAccessException {
		ensureLibrarianAccess();

		return lendingService.getLendingUsers(bookID);
	}

	public int getOverdueFines() {
		ensureLoggedInUser();
		return lendingService.getOverdueFineAmount(currentUser);
	}

	public BookItem checkout(String bookID) {
		ensureLoggedInUser();

		return lendingService.checkout(currentUser, bookID);
	}

	public boolean renew(BookItem item) {
		ensureLoggedInUser();

		return lendingService.renew(currentUser, item);
	}

	public boolean returnBookItem(BookItem item) {
		ensureLoggedInUser();

		return lendingService.returnBook(currentUser, item);
	}

	public Library(
		UserRepository userRepository,
		BookCatalog bookCatalog,
		LendingService lendingService
	) {
		this.userRepository = userRepository;
		this.bookCatalog = bookCatalog;
		this.lendingService = lendingService;
	}
}
A couple of important notes about this class:


Throught constructor injection we get a UserRepository (a repository handling user persistence), a BookCatalog (allowing us to search/add/remove books and book items) and a LendingService (responsible for actions like checkout, renew, return and find calculation). UserRepository , BookCatalog and LendingService are all interfaces exposing appropriate actions (they will be discussed later). This makes unit testing easier and results in a loosely coupled code. The Library class uses these services to perform all the necessary actions. This seems to be a neat way to organize the responsibilities (if you feel that this can be further improved, please, let me know).
Since we have to make access checks, we have to introduce the notion of the currently logged in user (it is saved in the currentUser field). Also, we have a couple of access check related methods (ensureLoggedInUser, ensureLibrarianAccess) that are throwing exceptions if certain invariants are violated. As a potential improvement, we could create an AccessCheckService that does this.
The rest of the code is fairly simple. For each action, we ensure that the current user can perform it (otherwise, an exception is thrown) and then the action is performed through the services.
Now, let's look at the service interfaces:


Fairly simple user persistence abstraction. I haven't provided a concrete implementation, can be done by having a Map from barcode to user instance:


public interface UserRepository {
	User getUserByBarCode(String barCode);
	void addUser(User user);
	void removeUser(String barCode);
}
The BookCatalog interface - represents a book catalog. For brevity, I have not have provided an implementation for this either but its easy to code a Map based implementation:


public interface BookCatalog {
	void addBookItem(BookItem bookItem);
	void removeBookItem(String bookItemID);
	List<BookDetails> searchByTitle(String title);
	List<BookDetails> searchByAuthor(String name);
	List<BookDetails> searchByPublicationDate(LocalDateTime publicationDate);
}
A LendingService interface - performs the lending related tasks:


public interface LendingService {
	List<BookItem> getCheckedOutBooks(User user);
	List<User> getLendingUsers(String bookID);
	int getOverdueFineAmount(User user);
	BookItem checkout(User user, String bookID);
	boolean renew(User user, BookItem bookItem);
	boolean returnBook(User user, BookItem bookItem);
}