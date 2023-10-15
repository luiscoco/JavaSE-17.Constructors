# JavaSE-Constructors

In Java, a constructor is a special type of method that is used to initialize objects. 

It is called when an object of a class is created. Constructors have the same name as the class and do not have a return type.

Here's a simple example:

```java
public class Car {
    // Instance variables
    String brand;
    String model;
    int year;

    // Constructor with parameters
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Another constructor without parameters (default constructor)
    public Car() {
        // Default values
        this.brand = "Unknown";
        this.model = "Unknown";
        this.year = 0;
    }

    // Other methods can go here

    public static void main(String[] args) {
        // Creating objects using constructors
        Car myCar = new Car("Toyota", "Camry", 2020);
        Car defaultCar = new Car(); // This will use the default constructor

        // Accessing object properties
        System.out.println("My car: " + myCar.brand + " " + myCar.model + " " + myCar.year);
        System.out.println("Default car: " + defaultCar.brand + " " + defaultCar.model + " " + defaultCar.year);
    }
}
```

In this example, the Car class has two constructors. The first constructor (public Car(String brand, String model, int year)) takes parameters and initializes the brand, model, and year properties of the object. The second constructor (public Car()) is a default constructor without parameters, and it initializes the properties with default values.

When you create a Car object using new Car("Toyota", "Camry", 2020), it calls the first constructor to initialize the object with the specified values. If you create a Car object without passing any values (new Car()), it calls the default constructor, setting default values.

Constructors are essential for ensuring that objects are properly initialized when they are created.

# Advance Constructors features

Let's delve into more advanced features of constructors in Java:

## 1. Constructor Overloading:
You can define multiple constructors for a class with different parameter lists. This is known as constructor overloading.

```java
public class Car {
    String brand;
    String model;
    int year;

    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Default constructor
    public Car() {
        this("Unknown", "Unknown", 0); // Calling the parameterized constructor
    }

    // Constructor with only brand and model
    public Car(String brand, String model) {
        this(brand, model, 0); // Calling the parameterized constructor with default year
    }
}
```

Here, we have three constructors. The first is the parameterized constructor, the second is a default constructor that calls the parameterized constructor with default values, and the third is a constructor that takes only brand and model, calling the parameterized constructor with a default year.

## 2. Chaining Constructors (this()):
You can use this() to invoke one constructor from another in the same class. This is known as constructor chaining.

```java
public class Car {
    String brand;
    String model;
    int year;

    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Default constructor chaining to the parameterized constructor
    public Car() {
        this("Unknown", "Unknown", 0);
    }
}
```

## 3. Static Constructors (not exactly):
While Java doesn't support static constructors, you can use a static block to achieve similar functionality. A static block is executed only once when the class is loaded.

```java
public class Car {
    static {
        // Static block
        System.out.println("Class Car is loaded.");
    }

    // Rest of the class
}
```

## 4. Copy Constructors:
A copy constructor creates a new object by copying the state of an existing object.

```java
public class Car {
    String brand;
    String model;
    int year;

    // Copy constructor
    public Car(Car otherCar) {
        this.brand = otherCar.brand;
        this.model = otherCar.model;
        this.year = otherCar.year;
    }
}
```

Now you can create a new Car by copying an existing one:

```java
Car car1 = new Car("Toyota", "Camry", 2020);
Car car2 = new Car(car1); // Using the copy constructor
```

These are some advanced features and patterns related to constructors in Java. They provide flexibility and help in creating more versatile and convenient classes.

## 5. "Constructors" in inheritance

In Java, constructors play a crucial role in initializing objects. When it comes to inheritance, constructors are also inherited, but there are some important things to understand.

Let's say you have a superclass called Vehicle:

```java
public class Vehicle {
    private String brand;

    public Vehicle(String brand) {
        this.brand = brand;
    }

    public void start() {
        System.out.println("Vehicle is starting.");
    }
}
```

Now, you want to create a subclass called Car that extends Vehicle:

```java
public class Car extends Vehicle {
    private int numberOfDoors;

    public Car(String brand, int numberOfDoors) {
        // Call the constructor of the superclass (Vehicle)
        super(brand);
        
        // Initialize the subclass-specific variable
        this.numberOfDoors = numberOfDoors;
    }

    public void drive() {
        System.out.println("Car is driving.");
    }
}
```

Vehicle class: It has a constructor that takes a brand parameter and initializes the brand field.

Car class: It extends Vehicle. In its constructor, it first calls the constructor of the superclass (super(brand)), ensuring that the brand is initialized in the Vehicle part of the object. 
Then, it initializes its own field, numberOfDoors.

Now, when you create a Car object, you need to provide values for both brand and numberOfDoors:

```java
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car("Toyota", 4);
        myCar.start(); // This method is inherited from Vehicle
        myCar.drive(); // This is a method specific to Car
    }
}
```

This example demonstrates how constructors in the superclass and subclass work together during the creation of objects in an inheritance hierarchy. The super(brand) call in the Car constructor ensures that the initialization code in the Vehicle constructor is executed before the Car constructor continues with its own initialization.
