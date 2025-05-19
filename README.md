# Oops
import java.util.Scanner;

class Book {
    private int bookID;
    private String title;
    private String author;
    private boolean isAvailable;

    public Book(int bookID, String title, String author, boolean isAvailable) {
        this.bookID = bookID;
        this.title = title;
        this.author = author;
        this.isAvailable = isAvailable;
    }

    public int getBookID() {
        return bookID;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public boolean isAvailable() {
        return isAvailable;
    }
    public void setAvailable(boolean available) {
        isAvailable = available;
    }

    public void displayInfo() {
        System.out.println("ID: " + bookID + ", Title: " + title + ", Author: " + author + ", Available: " + isAvailable);
    }
}

class Library {
    private Book[] books;
    private int count;

    public Library() {
        books = new Book[5];
        count = 0;
    }

    public void addBook(Book book) {
        if (count < books.length) {
            books[count] = book;
            count++;
            System.out.println("Book added successfully.");
        } else {
            System.out.println("Library is full!");
        }
    }

    public void replaceBook(int bookID, String newTitle, String newAuthor) {
        for (int i = 0; i < count; i++) {
            if (books[i].getBookID() == bookID) {
                books[i].setTitle(newTitle);
                books[i].setAuthor(newAuthor);
                System.out.println("Book updated successfully.");
                return;
            }
        }
        System.out.println("Book ID not found.");
    }

    public Book searchBook(int bookID) {
        for (int i = 0; i < count; i++) {
            if (books[i].getBookID() == bookID) {
                return books[i];
            }
        }
        return null;
    }

    public void displayBooks() {
        if (count == 0) {
            System.out.println("Library is empty.");
            return;
        }
        for (int i = 0; i < count; i++) {
            books[i].displayInfo();
        }
    }
}

public class BookManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();
        int choice;

        do {
            System.out.println("\n=== Library Management ===");
            System.out.println("1. Add Book");
            System.out.println("2. Replace Book");
            System.out.println("3. Search Book by ID");
            System.out.println("4. Display All Books");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Book ID: ");
                    int id = scanner.nextInt();
                    scanner.nextLine(); // consume leftover newline
                    System.out.print("Enter Title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter Author: ");
                    String author = scanner.nextLine();
                    System.out.print("Is Available (true/false): ");
                    boolean available = scanner.nextBoolean();
                    library.addBook(new Book(id, title, author, available));
                    break;

                case 2:
                    System.out.print("Enter Book ID to replace: ");
                    int replaceID = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter new Title: ");
                    String newTitle = scanner.nextLine();
                    System.out.print("Enter new Author: ");
                    String newAuthor = scanner.nextLine();
                    library.replaceBook(replaceID, newTitle, newAuthor);
                    break;

                case 3:
                    System.out.print("Enter Book ID to search: ");
                    int searchID = scanner.nextInt();
                    Book found = library.searchBook(searchID);
                    if (found != null) {
                        found.displayInfo();
                    } else {
                        System.out.println("Book not found.");
                    }
                    break;

                case 4:
                    library.displayBooks();
                    break;

                case 5:
                    System.out.println("Exiting. Goodbye!");
                    break;

                default:
                    System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
2.Create Interface Taxable with members sales Tax-7% and income Tax-10.5% create abstract method calc Tax().



import java.util.Scanner;

// Step 1: Create Interface
interface Taxable {
    double salesTax = 0.07;   // 7% sales tax
    double incomeTax = 0.105; // 10.5% income tax
    
    void calcTax();           // abstract method
}

// Step 2a: Create Employee class
class Employee implements Taxable {
    int empId;
    String name;
    double salary; // monthly salary

    Employee(int empId, String name, double salary) {
        this.empId = empId;
        this.name = name;
        this.salary = salary;
    }

    @Override
    public void calcTax() {
        double yearlySalary = salary * 12;
        double tax = yearlySalary * incomeTax;
        System.out.println("Income Tax for " + name + " (Yearly Salary): " + tax);
    }
}

// Step 2b: Create Product class
class Product implements Taxable {
    int pid;
    double price;
    int quantity;

    Product(int pid, double price, int quantity) {
        this.pid = pid;
        this.price = price;
        this.quantity = quantity;
    }

    @Override
    public void calcTax() {
        double tax = price * salesTax;
        System.out.println("Sales Tax for product ID " + pid + " (per unit): " + tax);
    }
}

// Step 2c: Create DriverMain class
public class DriverMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Employee details
        System.out.print("Enter Employee ID: ");
        int empId = sc.nextInt();
        sc.nextLine(); // consume newline
        System.out.print("Enter Employee Name: ");
        String name = sc.nextLine();
        System.out.print("Enter Monthly Salary: ");
        double salary = sc.nextDouble();

        Employee emp = new Employee(empId, name, salary);
        emp.calcTax();

        // Product details
        System.out.print("\nEnter Product ID: ");
        int pid = sc.nextInt();
        System.out.print("Enter Product Price: ");
        double price = sc.nextDouble();
        System.out.print("Enter Product Quantity: ");
        int quantity = sc.nextInt();

        Product prod = new Product(pid, price, quantity);
        prod.calcTax();

        sc.close();
    }
}import java.util.Scanner;

class Book {
    private int bookID;
    private String title;
    private String author;
    private boolean isAvailable;

    public Book(int bookID, String title, String author, boolean isAvailable) {
        this.bookID = bookID;
        this.title = title;
        this.author = author;
        this.isAvailable = isAvailable;
    }

    public int getBookID() {
        return bookID;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public boolean isAvailable() {
        return isAvailable;
    }
    public void setAvailable(boolean available) {
        isAvailable = available;
    }

    public void displayInfo() {
        System.out.println("ID: " + bookID + ", Title: " + title + ", Author: " + author + ", Available: " + isAvailable);
    }
}

class Library {
    private Book[] books;
    private int count;

    public Library() {
        books = new Book[5];
        count = 0;
    }

    public void addBook(Book book) {
        if (count < books.length) {
            books[count] = book;
            count++;
            System.out.println("Book added successfully.");
        } else {
            System.out.println("Library is full!");
        }
    }

    public void replaceBook(int bookID, String newTitle, String newAuthor) {
        for (int i = 0; i < count; i++) {
            if (books[i].getBookID() == bookID) {
                books[i].setTitle(newTitle);
                books[i].setAuthor(newAuthor);
                System.out.println("Book updated successfully.");
                return;
            }
        }
        System.out.println("Book ID not found.");
    }

    public Book searchBook(int bookID) {
        for (int i = 0; i < count; i++) {
            if (books[i].getBookID() == bookID) {
                return books[i];
            }
        }
        return null;
    }

    public void displayBooks() {
        if (count == 0) {
            System.out.println("Library is empty.");
            return;
        }
        for (int i = 0; i < count; i++) {
            books[i].displayInfo();
        }
    }
}

public class BookManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();
        int choice;

        do {
            System.out.println("\n=== Library Management ===");
            System.out.println("1. Add Book");
            System.out.println("2. Replace Book");
            System.out.println("3. Search Book by ID");
            System.out.println("4. Display All Books");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Book ID: ");
                    int id = scanner.nextInt();
                    scanner.nextLine(); // consume leftover newline
                    System.out.print("Enter Title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter Author: ");
                    String author = scanner.nextLine();
                    System.out.print("Is Available (true/false): ");
                    boolean available = scanner.nextBoolean();
                    library.addBook(new Book(id, title, author, available));
                    break;

                case 2:
                    System.out.print("Enter Book ID to replace: ");
                    int replaceID = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter new Title: ");
                    String newTitle = scanner.nextLine();
                    System.out.print("Enter new Author: ");
                    String newAuthor = scanner.nextLine();
                    library.replaceBook(replaceID, newTitle, newAuthor);
                    break;

                case 3:
                    System.out.print("Enter Book ID to search: ");
                    int searchID = scanner.nextInt();
                    Book found = library.searchBook(searchID);
                    if (found != null) {
                        found.displayInfo();
                    } else {
                        System.out.println("Book not found.");
                    }
                    break;

                case 4:
                    library.displayBooks();
                    break;

                case 5:
                    System.out.println("Exiting. Goodbye!");
                    break;

                default:
                    System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
2.Create Interface Taxable with members sales Tax-7% and income Tax-10.5% create abstract method calc Tax().

a. Create class Employee(empId,name, salary) and implement Taxable to calculate income Tax on yearly salary.

b. Create class Product(pid.price,quantity) and implement Taxable to calculate sales Tax on unit price of product.

c. Create class for main method(Say DriverMain), accept employee information and a product information from user and print income tax and sales tax respectively

import java.util.Scanner;

// Step 1: Create Interface
interface Taxable {
    double salesTax = 0.07;   // 7% sales tax
    double incomeTax = 0.105; // 10.5% income tax
    
    void calcTax();           // abstract method
}

// Step 2a: Create Employee class
class Employee implements Taxable {
    int empId;
    String name;
    double salary; // monthly salary

    Employee(int empId, String name, double salary) {
        this.empId = empId;
        this.name = name;
        this.salary = salary;
    }

    @Override
    public void calcTax() {
        double yearlySalary = salary * 12;
        double tax = yearlySalary * incomeTax;
        System.out.println("Income Tax for " + name + " (Yearly Salary): " + tax);
    }
}

// Step 2b: Create Product class
class Product implements Taxable {
    int pid;
    double price;
    int quantity;

    Product(int pid, double price, int quantity) {
        this.pid = pid;
        this.price = price;
        this.quantity = quantity;
    }

    @Override
    public void calcTax() {
        double tax = price * salesTax;
        System.out.println("Sales Tax for product ID " + pid + " (per unit): " + tax);
    }
}

// Step 2c: Create DriverMain class
public class DriverMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Employee details
        System.out.print("Enter Employee ID: ");
        int empId = sc.nextInt();
        sc.nextLine(); // consume newline
        System.out.print("Enter Employee Name: ");
        String name = sc.nextLine();
        System.out.print("Enter Monthly Salary: ");
        double salary = sc.nextDouble();

        Employee emp = new Employee(empId, name, salary);
        emp.calcTax();

        // Product details
        System.out.print("\nEnter Product ID: ");
        int pid = sc.nextInt();
        System.out.print("Enter Product Price: ");
        double price = sc.nextDouble();
        System.out.print("Enter Product Quantity: ");
        int quantity = sc.nextInt();

        Product prod = new Product(pid, price, quantity);
        prod.calcTax();

        sc.close();
    }
}
