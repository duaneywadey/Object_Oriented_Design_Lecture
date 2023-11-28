# Object Oriented Design Sample Codes

## Encapsulation

```java
// Student class
class Student {
    private String name; // Encapsulated private attribute
    private int age; // Encapsulated private attribute

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Encapsulated getter for name attribute
    public String getName() {
        return name;
    }

    // Encapsulated setter for name attribute
    public void setName(String name) {
        this.name = name;
    }

    // Encapsulated getter for age attribute
    public int getAge() {
        return age;
    }

    // Encapsulated setter for age attribute
    public void setAge(int age) {
        this.age = age;
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

// Main class to demonstrate the student management system
class StudentManagementSystem {
    public static void main(String[] args) {
        // Create a Student instance
        Student student = new Student("Jane Smith", 20);
        student.displayInfo();  // Output: Name: Jane Smith, Age: 20

        // Update student's name and age using setters
        student.setName("John Doe");
        student.setAge(25);
        student.displayInfo();  // Output: Name: John Doe, Age: 25

        // Access student's name and age using getters
        System.out.println("Student Name: " + student.getName());  // Output: Student Name: John Doe
        System.out.println("Student Age: " + student.getAge());  // Output: Student Age: 25
    }
}

```

## Inheritance 

```java
import java.util.ArrayList; // import the ArrayList class

// Person class
class Person {
    protected String name;
    protected int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void info() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

// Student class inheriting from Person
class Student extends Person {
    private String studentId;
    private ArrayList<String> courses;

    public Student(String name, int age, String studentId) {
        super(name, age);
        this.studentId = studentId;
        this.courses = new ArrayList<>();
    }

    public void enroll(String course) {
        courses.add(course);
    }

    public void displayCourses() {
        System.out.println("Enrolled courses:");
        for (String course : courses) {
            System.out.println(course);
        }
        System.out.println();
    }
}

// Main class to demonstrate the student management system
class StudentManagementSystem {
    public static void main(String[] args) {
        
        // Create a Person instance
        Person person = new Person("John Doe", 25);
        person.info();  // Output: Name: John Doe, Age: 25

        // Create a Student instance
        Student student = new Student("Jane Smith", 20, "S12345");
        student.info();  // Output: Name: Jane Smith, Age: 20
        student.enroll("Math");  // Enroll the student in a course
        student.enroll("Science");
        student.displayCourses();  // Output: Enrolled courses: Math, Science
    }
}
```

## Polymorphism
```java
import java.util.ArrayList; // import the ArrayList class

// Person class
class Person {
    protected String name;
    protected int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void info() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

// Student class inheriting from Person
class Student extends Person {
    private String studentId;
    private ArrayList<String> courses;

    public Student(String name, int age, String studentId) {
        super(name, age);
        this.studentId = studentId;
        this.courses = new ArrayList<>();
    }
    
    public void enroll(String course) {
        courses.add(course);
    }
    
    public void displayCourses() {
        System.out.println("Enrolled courses:");
        for (String course : courses) {
            System.out.println(course);
        }
        System.out.println();
    }

    @Override
    public void info() {
        super.info();
        System.out.println("Student ID: " + studentId);
    }
}

// Teacher class inheriting from Person
class Teacher extends Person {
    private String teacherId;
    private ArrayList<String> classesTaught;

    public Teacher(String name, int age, String teacherId) {
        super(name, age);
        this.teacherId = teacherId;
        this.classesTaught = new ArrayList<>();
    }

    public void addClass(String classes) {
        classesTaught.add(classes);
    }
    
    public void displayClasses() {
        System.out.println("Classes Handled:");
        for (String classes : classesTaught) {
            System.out.println(classes);
        }
        System.out.println();
    }

    @Override
    public void info() {
        System.out.println();
        super.info();
        System.out.println("Teacher ID: " + teacherId);
    }
}

// Main class to demonstrate the student management system
class StudentManagementSystem {
    public static void main(String[] args) {
        
        // Create a Student instance
        Student student = new Student("Jane Smith", 20, "S12345");
        student.info();  // Output: Name: Jane Smith, Age: 20
        student.enroll("Math");  // Enroll the student in a course
        student.enroll("Science");
        student.displayCourses();  // Output: Enrolled courses: Math, Science
        
        // Create a Teacher instance
        Teacher teacher = new Teacher("Melinda Cruz", 44, "A25266");
        teacher.info(); 
        teacher.addClass("UCOS 2-1");  
        teacher.addClass("UCOS 2-2");
        teacher.displayClasses();
        
    }
}

```

## Abstraction 

```java
abstract class TuitionDiscount {
    public abstract double getDiscount(int given_amount);
}

class PartialScholarship extends TuitionDiscount {
    public double getDiscount(int given_amount) {
        double discount = given_amount * 0.20;
        double final_amt = given_amount - discount;
        return final_amt;
    }
}

class AcademicScholarship extends TuitionDiscount {
    public double getDiscount(int given_amount) {
        double discount = given_amount * 0.50;
        double final_amt = given_amount - discount;
        return final_amt;
    }
}

class PremiumScholarship extends TuitionDiscount {
    public double getDiscount(int given_amount) {
        double discount = given_amount * 0.75;
        double final_amt = given_amount - discount;
        return final_amt;
    }
}

class Main {
    public static void main(String[] args) {
        TuitionDiscount partial = new PartialScholarship();
        TuitionDiscount academic = new AcademicScholarship();
        System.out.println(partial.getDiscount(5000));
    }
}

```

## Abstraction (REFACTORED)
```java
abstract class TuitionDiscount {
    protected double discountPercentage;

    public TuitionDiscount(double discountPercentage) {
        this.discountPercentage = discountPercentage;
    }

    public double getDiscount(int givenAmount) {
        double discount = givenAmount * discountPercentage;
        double finalAmount = givenAmount - discount;
        return finalAmount;
    }
}

class PartialScholarship extends TuitionDiscount {
    public PartialScholarship() {
        super(0.20);
    }
}

class AcademicScholarship extends TuitionDiscount {
    public AcademicScholarship() {
        super(0.50);
    }
}

class PremiumScholarship extends TuitionDiscount {
    public PremiumScholarship() {
        super(0.75);
    }
}

class Main {
    public static void main(String[] args) {
        TuitionDiscount partial = new PartialScholarship();
        TuitionDiscount academic = new AcademicScholarship();
        System.out.println(partial.getDiscount(5000));
    }
}

```

## Encapsulation (Bank System Example)

```java
class BankAccount {
    private String accountNumber;
    private double balance;

    public BankAccount(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }

    public void deposit(double amount) {
        // Encapsulated method
        balance += amount;
    }

    public void withdraw(double amount) {
        // Encapsulated method
        if (balance >= amount) {
            balance -= amount;
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    public String getAcctNo() {
        return accountNumber;
    }

    public double getBalance() {
        // Encapsulated method
        return balance;
    }
}

class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("12345678", 1000);
        account.deposit(1000);
        account.withdraw(300);
        System.out.println("Account number: " + account.getAcctNo());
        System.out.println("Current balance: " + account.getBalance());
    }
}

```

## Inheritance (Bank System Example)

```java
// BankAccount class (Superclass)

class BankAccount {
    private String accountNumber;
    private double balance;

    public BankAccount(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    public double getBalance() {
        return balance;
    }

}

// SavingsAccount class (Subclass)

class SavingsAccount extends BankAccount {
    private double interestRate;

    // Include annual interest rate
    public SavingsAccount(String accountNumber, double balance, double interestRate) {
        super(accountNumber, balance); // Inheriting attributes 
        this.interestRate = interestRate;
    }

    public double getAnnualInterest() {
        return getBalance() * (interestRate / 100); // Inheriting getBalance() method
    }

    public double getMonthlyInterestRate() {
        return interestRate / 12;
    }

    public double getMonthlyInterest() {
        return getBalance() * (getMonthlyInterestRate() / 100);
    }

}


class MainClass {
    public static void main(String[] args) {
    
    // Creating an instance of SavingsAccount
    SavingsAccount savingsAccount = new SavingsAccount("1234567890", 1000, 3);
    savingsAccount.deposit(25000); 
    savingsAccount.withdraw(2000); 

    // Yearly Interest
    System.out.println("Balance from savings account: " + savingsAccount.getBalance()); 
    System.out.println("Annual interest from savings account: " + savingsAccount.getAnnualInterest()); 

    // Monthly Interest
    System.out.println("Balance from savings account: " + savingsAccount.getBalance()); 
    System.out.println("Monthly interest from savings account: " + savingsAccount.getMonthlyInterest()); 
    
    }
}

```