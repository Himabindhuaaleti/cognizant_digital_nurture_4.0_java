


# Week 1: Design Patterns Hands-On




# Exercise 1: Implementing the Singleton Pattern

## Scenario:
You need to ensure that a logging utility class in your application has only one instance throughout the application lifecycle to ensure consistent logging.

## Steps:
1. Create a New Java Project: Create a new Java project named SingletonPatternExample.
2. Define a Singleton Class: Create a class named Logger that has a private static instance of itself. Ensure the constructor of Logger is private. Provide a public static method to get the instance of the Logger class.
3. Implement the Singleton Pattern: Write code to ensure that the Logger class follows the Singleton design pattern.
4. Test the Singleton Implementation: Create a test class to verify that only one instance of Logger is created and used across the application.

## Code:

### `Logger.java`
```java
package SingletonPatternExample;

public class Logger {
    private static Logger instance;

    private Logger() {
        // private constructor to prevent instantiation
    }

    public static Logger getInstance() {
        if (instance == null) {
            instance = new Logger();
        }
        return instance;
    }

    public void log(String message) {
        System.out.println("Log: " + message);
    }
}
```

### `TestSingleton.java`
```java
package SingletonPatternExample;

public class TestSingleton {
    public static void main(String[] args) {
        Logger logger1 = Logger.getInstance();
        Logger logger2 = Logger.getInstance();

        System.out.println("Are logger1 and logger2 the same instance? " + (logger1 == logger2));

        logger1.log("This is the first log message.");
        logger2.log("This is the second log message.");
    }
}
```

## Output:
```
Are logger1 and logger2 the same instance? true
Log: This is the first log message.
Log: This is the second log message.
```




# Exercise 2: Implementing the Factory Method Pattern

## Scenario:
You are developing a document management system that needs to create different types of documents (e.g., Word, PDF, Excel). Use the Factory Method Pattern to achieve this.

## Steps:
1. Create a New Java Project: Create a new Java project named FactoryMethodPatternExample.
2. Define Document Classes: Create interfaces or abstract classes for different document types such as WordDocument, PdfDocument, and ExcelDocument.
3. Create Concrete Document Classes: Implement concrete classes for each document type that implements or extends the above interfaces or abstract classes.
4. Implement the Factory Method: Create an abstract class DocumentFactory with a method createDocument(). Create concrete factory classes for each document type that extends DocumentFactory and implements the createDocument() method.
5. Test the Factory Method Implementation: Create a test class to demonstrate the creation of different document types using the factory method.

## Code:

### `Document.java`
```java
package FactoryMethodPatternExample;

public interface Document {
    void open();
    void save();
    void close();
}
```

### `WordDocument.java`
```java
package FactoryMethodPatternExample;

public class WordDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening Word Document.");
    }

    @Override
    public void save() {
        System.out.println("Saving Word Document.");
    }

    @Override
    public void close() {
        System.out.println("Closing Word Document.");
    }
}
```

### `PdfDocument.java`
```java
package FactoryMethodPatternExample;

public class PdfDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening PDF Document.");
    }

    @Override
    public void save() {
        System.out.println("Saving PDF Document.");
    }

    @Override
    public void close() {
        System.out.println("Closing PDF Document.");
    }
}
```

### `ExcelDocument.java`
```java
package FactoryMethodPatternExample;

public class ExcelDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening Excel Document.");
    }

    @Override
    public void save() {
        System.out.println("Saving Excel Document.");
    }

    @Override
    public void close() {
        System.out.println("Closing Excel Document.");
    }
}
```

### `DocumentFactory.java`
```java
package FactoryMethodPatternExample;

public abstract class DocumentFactory {
    public abstract Document createDocument();
}
```

### `WordDocumentFactory.java`
```java
package FactoryMethodPatternExample;

public class WordDocumentFactory extends DocumentFactory {
    @Override
    public Document createDocument() {
        return new WordDocument();
    }
}
```

### `PdfDocumentFactory.java`
```java
package FactoryMethodPatternExample;

public class PdfDocumentFactory extends DocumentFactory {
    @Override
    public Document createDocument() {
        return new PdfDocument();
    }
}
```

### `ExcelDocumentFactory.java`
```java
package FactoryMethodPatternExample;

public class ExcelDocumentFactory extends DocumentFactory {
    @Override
    public Document createDocument() {
        return new ExcelDocument();
    }
}
```

### `TestFactoryMethod.java`
```java
package FactoryMethodPatternExample;

public class TestFactoryMethod {
    public static void main(String[] args) {
        DocumentFactory wordFactory = new WordDocumentFactory();
        Document wordDoc = wordFactory.createDocument();
        wordDoc.open();
        wordDoc.save();
        wordDoc.close();

        System.out.println("\n");

        DocumentFactory pdfFactory = new PdfDocumentFactory();
        Document pdfDoc = pdfFactory.createDocument();
        pdfDoc.open();
        pdfDoc.save();
        pdfDoc.close();

        System.out.println("\n");

        DocumentFactory excelFactory = new ExcelDocumentFactory();
        Document excelDoc = excelFactory.createDocument();
        excelDoc.open();
        excelDoc.save();
        excelDoc.close();
    }
}
```

## Output:
```
Opening Word Document.
Saving Word Document.
Closing Word Document.

Opening PDF Document.
Saving PDF Document.
Closing PDF Document.

Opening Excel Document.
Saving Excel Document.
Closing Excel Document.
```




# Exercise 3: Implementing the Builder Pattern

## Scenario:
You are developing a system to create complex objects such as a Computer with multiple optional parts. Use the Builder Pattern to manage the construction process.

## Steps:
1. Create a New Java Project: Create a new Java project named BuilderPatternExample.
2. Define a Product Class: Create a class Computer with attributes like CPU, RAM, Storage, etc.
3. Implement the Builder Class: Create a static nested Builder class inside Computer with methods to set each attribute. Provide a build() method in the Builder class that returns an instance of Computer.
4. Implement the Builder Pattern: Ensure that the Computer class has a private constructor that takes the Builder as a parameter.
5. Test the Builder Implementation: Create a test class to demonstrate the creation of different configurations of Computer using the Builder pattern.

## Code:

### `Computer.java`
```java
package BuilderPatternExample;

public class Computer {
    private String CPU;
    private String RAM;
    private String Storage;
    private boolean hasGraphicsCard;
    private boolean hasWifi;

    private Computer(Builder builder) {
        this.CPU = builder.CPU;
        this.RAM = builder.RAM;
        this.Storage = builder.Storage;
        this.hasGraphicsCard = builder.hasGraphicsCard;
        this.hasWifi = builder.hasWifi;
    }

    public static class Builder {
        private String CPU;
        private String RAM;
        private String Storage;
        private boolean hasGraphicsCard = false;
        private boolean hasWifi = false;

        public Builder(String CPU, String RAM, String Storage) {
            this.CPU = CPU;
            this.RAM = RAM;
            this.Storage = Storage;
        }

        public Builder setGraphicsCard(boolean hasGraphicsCard) {
            this.hasGraphicsCard = hasGraphicsCard;
            return this;
        }

        public Builder setWifi(boolean hasWifi) {
            this.hasWifi = hasWifi;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }
    }

    @Override
    public String toString() {
        return "Computer [CPU=" + CPU + ", RAM=" + RAM + ", Storage=" + Storage + ", GraphicsCard=" + hasGraphicsCard + ", Wifi=" + hasWifi + "]";
    }
}
```

### `TestBuilder.java`
```java
package BuilderPatternExample;

public class TestBuilder {
    public static void main(String[] args) {
        Computer gamingPC = new Computer.Builder("Intel i9", "32GB", "1TB SSD")
                                .setGraphicsCard(true)
                                .setWifi(true)
                                .build();
        System.out.println(gamingPC);

        Computer officePC = new Computer.Builder("Intel i5", "8GB", "256GB SSD")
                                .setWifi(true)
                                .build();
        System.out.println(officePC);

        Computer basicPC = new Computer.Builder("AMD Ryzen 3", "4GB", "500GB HDD")
                                .build();
        System.out.println(basicPC);
    }
}
```

## Output:
```
Computer [CPU=Intel i9, RAM=32GB, Storage=1TB SSD, GraphicsCard=true, Wifi=true]
Computer [CPU=Intel i5, RAM=8GB, Storage=256GB SSD, GraphicsCard=false, Wifi=true]
Computer [CPU=AMD Ryzen 3, RAM=4GB, Storage=500GB HDD, GraphicsCard=false, Wifi=false]
```




# Exercise 4: Implementing the Adapter Pattern

## Scenario:
You are developing a payment processing system that needs to integrate with multiple third-party payment gateways with different interfaces. Use the Adapter Pattern to achieve this.

## Steps:
1. Create a New Java Project: Create a new Java project named AdapterPatternExample.
2. Define Target Interface: Create an interface PaymentProcessor with methods like processPayment().
3. Implement Adaptee Classes: Create classes for different payment gateways with their own methods.
4. Implement the Adapter Class: Create an adapter class for each payment gateway that implements PaymentProcessor and translates the calls to the gateway-specific methods.
5. Test the Adapter Implementation: Create a test class to demonstrate the use of different payment gateways through the adapter.

## Code:

### `PaymentProcessor.java`
```java
package AdapterPatternExample;

public interface PaymentProcessor {
    void processPayment(double amount);
}
```

### `PayPalGateway.java`
```java
package AdapterPatternExample;

public class PayPalGateway {
    public void makePayment(double amount) {
        System.out.println("Processing payment of $" + amount + " through PayPal.");
    }
}
```

### `StripeGateway.java`
```java
package AdapterPatternExample;

public class StripeGateway {
    public void charge(double amount) {
        System.out.println("Charging $" + amount + " through Stripe.");
    }
}
```

### `PayPalAdapter.java`
```java
package AdapterPatternExample;

public class PayPalAdapter implements PaymentProcessor {
    private PayPalGateway payPalGateway;

    public PayPalAdapter(PayPalGateway payPalGateway) {
        this.payPalGateway = payPalGateway;
    }

    @Override
    public void processPayment(double amount) {
        payPalGateway.makePayment(amount);
    }
}
```

### `StripeAdapter.java`
```java
package AdapterPatternExample;

public class StripeAdapter implements PaymentProcessor {
    private StripeGateway stripeGateway;

    public StripeAdapter(StripeGateway stripeGateway) {
        this.stripeGateway = stripeGateway;
    }

    @Override
    public void processPayment(double amount) {
        stripeGateway.charge(amount);
    }
}
```

### `TestAdapter.java`
```java
package AdapterPatternExample;

public class TestAdapter {
    public static void main(String[] args) {
        PayPalGateway payPalGateway = new PayPalGateway();
        PaymentProcessor payPalAdapter = new PayPalAdapter(payPalGateway);
        payPalAdapter.processPayment(100.00);

        StripeGateway stripeGateway = new StripeGateway();
        PaymentProcessor stripeAdapter = new StripeAdapter(stripeGateway);
        stripeAdapter.processPayment(250.50);
    }
}
```

## Output:
```
Processing payment of $100.0 through PayPal.
Charging $250.5 through Stripe.
```




# Exercise 5: Implementing the Decorator Pattern

## Scenario:
You are developing a notification system where notifications can be sent via multiple channels (e.g., Email, SMS). Use the Decorator Pattern to add functionalities dynamically.

## Steps:
1. Create a New Java Project: Create a new Java project named DecoratorPatternExample.
2. Define Component Interface: Create an interface Notifier with a method send().
3. Implement Concrete Component: Create a class EmailNotifier that implements Notifier.
4. Implement Decorator Classes: Create abstract decorator class NotifierDecorator that implements Notifier and holds a reference to a Notifier object. Create concrete decorator classes like SMSNotifierDecorator, SlackNotifierDecorator that extend NotifierDecorator.
5. Test the Decorator Implementation: Create a test class to demonstrate sending notifications via multiple channels using decorators.

## Code:

### `Notifier.java`
```java
package DecoratorPatternExample;

public interface Notifier {
    void send(String message);
}
```

### `EmailNotifier.java`
```java
package DecoratorPatternExample;

public class EmailNotifier implements Notifier {
    @Override
    public void send(String message) {
        System.out.println("Sending Email with message: " + message);
    }
}
```

### `NotifierDecorator.java`
```java
package DecoratorPatternExample;

public abstract class NotifierDecorator implements Notifier {
    protected Notifier wrappedNotifier;

    public NotifierDecorator(Notifier wrappedNotifier) {
        this.wrappedNotifier = wrappedNotifier;
    }

    @Override
    public void send(String message) {
        wrappedNotifier.send(message);
    }
}
```

### `SMSNotifierDecorator.java`
```java
package DecoratorPatternExample;

public class SMSNotifierDecorator extends NotifierDecorator {
    public SMSNotifierDecorator(Notifier wrappedNotifier) {
        super(wrappedNotifier);
    }

    @Override
    public void send(String message) {
        super.send(message);
        System.out.println("Sending SMS with message: " + message);
    }
}
```

### `SlackNotifierDecorator.java`
```java
package DecoratorPatternExample;

public class SlackNotifierDecorator extends NotifierDecorator {
    public SlackNotifierDecorator(Notifier wrappedNotifier) {
        super(wrappedNotifier);
    }

    @Override
    public void send(String message) {
        super.send(message);
        System.out.println("Sending Slack message with message: " + message);
    }
}
```

### `TestDecorator.java`
```java
package DecoratorPatternExample;

public class TestDecorator {
    public static void main(String[] args) {
        Notifier emailNotifier = new EmailNotifier();
        emailNotifier.send("Hello from Email!");

        System.out.println("\n");

        Notifier smsAndEmailNotifier = new SMSNotifierDecorator(new EmailNotifier());
        smsAndEmailNotifier.send("Hello from SMS and Email!");

        System.out.println("\n");

        Notifier allChannelNotifier = new SlackNotifierDecorator(new SMSNotifierDecorator(new EmailNotifier()));
        allChannelNotifier.send("Hello from all channels!");
    }
}
```

## Output:
```
Sending Email with message: Hello from Email!

Sending Email with message: Hello from SMS and Email!
Sending SMS with message: Hello from SMS and Email!

Sending Email with message: Hello from all channels!
Sending SMS with message: Hello from all channels!
Sending Slack message with message: Hello from all channels!
```




# Exercise 6: Implementing the Proxy Pattern

## Scenario:
You are developing an image viewer application that loads images from a remote server. Use the Proxy Pattern to add lazy initialization and caching.

## Steps:
1. Create a New Java Project: Create a new Java project named ProxyPatternExample.
2. Define Subject Interface: Create an interface Image with a method display().
3. Implement Real Subject Class: Create a class RealImage that implements Image and loads an image from a remote server.
4. Implement Proxy Class: Create a class ProxyImage that implements Image and holds a reference to RealImage. Implement lazy initialization and caching in ProxyImage.
5. Test the Proxy Implementation: Create a test class to demonstrate the use of ProxyImage to load and display images.

## Code:

### `Image.java`
```java
package ProxyPatternExample;

public interface Image {
    void display();
}
```

### `RealImage.java`
```java
package ProxyPatternExample;

public class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromRemoteServer(fileName);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + fileName);
    }

    private void loadFromRemoteServer(String fileName) {
        System.out.println("Loading " + fileName + " from remote server...");
    }
}
```

### `ProxyImage.java`
```java
package ProxyPatternExample;

public class ProxyImage implements Image {
    private String fileName;
    private RealImage realImage;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}
```

### `TestProxy.java`
```java
package ProxyPatternExample;

public class TestProxy {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("photo1.jpg");
        Image image2 = new ProxyImage("photo2.jpg");

        System.out.println("First call to image1:");
        image1.display(); // Loads and displays

        System.out.println("\nSecond call to image1:");
        image1.display(); // Displays from cache

        System.out.println("\nFirst call to image2:");
        image2.display(); // Loads and displays
    }
}
```

## Output:
```
First call to image1:
Loading photo1.jpg from remote server...
Displaying photo1.jpg

Second call to image1:
Displaying photo1.jpg

First call to image2:
Loading photo2.jpg from remote server...
Displaying photo2.jpg
```




# Exercise 7: Implementing the Observer Pattern

## Scenario:
You are developing a stock market monitoring application where multiple clients need to be notified whenever stock prices change. Use the Observer Pattern to achieve this.

## Steps:
1. Create a New Java Project: Create a new Java project named ObserverPatternExample.
2. Define Subject Interface: Create an interface Stock with methods to register, deregister, and notify observers.
3. Implement Concrete Subject: Create a class StockMarket that implements Stock and maintains a list of observers.
4. Define Observer Interface: Create an interface Observer with a method update().
5. Implement Concrete Observers: Create classes MobileApp, WebApp that implement Observer.
6. Test the Observer Implementation: Create a test class to demonstrate the registration and notification of observers.

## Code:

### `Stock.java`
```java
package ObserverPatternExample;

public interface Stock {
    void registerObserver(Observer o);
    void deregisterObserver(Observer o);
    void notifyObservers();
}
```

### `StockMarket.java`
```java
package ObserverPatternExample;

import java.util.ArrayList;
import java.util.List;

public class StockMarket implements Stock {
    private List<Observer> observers;
    private double stockPrice;

    public StockMarket() {
        observers = new ArrayList<>();
    }

    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }

    @Override
    public void deregisterObserver(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(stockPrice);
        }
    }

    public void setStockPrice(double stockPrice) {
        this.stockPrice = stockPrice;
        notifyObservers();
    }
}
```

### `Observer.java`
```java
package ObserverPatternExample;

public interface Observer {
    void update(double stockPrice);
}
```

### `MobileApp.java`
```java
package ObserverPatternExample;

public class MobileApp implements Observer {
    private String appName;

    public MobileApp(String appName) {
        this.appName = appName;
    }

    @Override
    public void update(double stockPrice) {
        System.out.println(appName + ": Stock price updated to " + stockPrice);
    }
}
```

### `WebApp.java`
```java
package ObserverPatternExample;

public class WebApp implements Observer {
    private String appName;

    public WebApp(String appName) {
        this.appName = appName;
    }

    @Override
    public void update(double stockPrice) {
        System.out.println(appName + ": Stock price updated to " + stockPrice);
    }
}
```

### `TestObserver.java`
```java
package ObserverPatternExample;

public class TestObserver {
    public static void main(String[] args) {
        StockMarket stockMarket = new StockMarket();

        MobileApp mobileApp1 = new MobileApp("MobileApp1");
        WebApp webApp1 = new WebApp("WebApp1");
        MobileApp mobileApp2 = new MobileApp("MobileApp2");

        stockMarket.registerObserver(mobileApp1);
        stockMarket.registerObserver(webApp1);
        stockMarket.registerObserver(mobileApp2);

        System.out.println("Setting stock price to 100.50");
        stockMarket.setStockPrice(100.50);

        System.out.println("\nDeregistering WebApp1");
        stockMarket.deregisterObserver(webApp1);

        System.out.println("\nSetting stock price to 101.75");
        stockMarket.setStockPrice(101.75);
    }
}
```

## Output:
```
Setting stock price to 100.50
MobileApp1: Stock price updated to 100.5
WebApp1: Stock price updated to 100.5
MobileApp2: Stock price updated to 100.5

Deregistering WebApp1

Setting stock price to 101.75
MobileApp1: Stock price updated to 101.75
MobileApp2: Stock price updated to 101.75
```




# Exercise 8: Implementing the Strategy Pattern

## Scenario:
You are developing a payment system where different payment methods (e.g., Credit Card, PayPal) can be selected at runtime. Use the Strategy Pattern to achieve this.

## Steps:
1. Create a New Java Project: Create a new Java project named StrategyPatternExample.
2. Define Strategy Interface: Create an interface PaymentStrategy with a method pay().
3. Implement Concrete Strategies: Create classes CreditCardPayment, PayPalPayment that implement PaymentStrategy.
4. Implement Context Class: Create a class PaymentContext that holds a reference to PaymentStrategy and a method to execute the strategy.
5. Test the Strategy Implementation: Create a test class to demonstrate selecting and using different payment strategies.

## Code:

### `PaymentStrategy.java`
```java
package StrategyPatternExample;

public interface PaymentStrategy {
    void pay(double amount);
}
```

### `CreditCardPayment.java`
```java
package StrategyPatternExample;

public class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    private String name;

    public CreditCardPayment(String cardNumber, String name) {
        this.cardNumber = cardNumber;
        this.name = name;
    }

    @Override
    public void pay(double amount) {
        System.out.println(amount + " paid with credit card: " + cardNumber);
    }
}
```

### `PayPalPayment.java`
```java
package StrategyPatternExample;

public class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(double amount) {
        System.out.println(amount + " paid using PayPal account: " + email);
    }
}
```

### `PaymentContext.java`
```java
package StrategyPatternExample;

public class PaymentContext {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void executePayment(double amount) {
        paymentStrategy.pay(amount);
    }
}
```

### `TestStrategy.java`
```java
package StrategyPatternExample;

public class TestStrategy {
    public static void main(String[] args) {
        PaymentContext context = new PaymentContext();

        // Pay with Credit Card
        CreditCardPayment creditCardPayment = new CreditCardPayment("1234-5678-9012-3456", "John Doe");
        context.setPaymentStrategy(creditCardPayment);
        context.executePayment(150.75);

        // Pay with PayPal
        PayPalPayment payPalPayment = new PayPalPayment("john.doe@example.com");
        context.setPaymentStrategy(payPalPayment);
        context.executePayment(75.20);
    }
}
```

## Output:
```
150.75 paid with credit card: 1234-5678-9012-3456
75.2 paid using PayPal account: john.doe@example.com
```




# Exercise 9: Implementing the Command Pattern

## Scenario:
You are developing a home automation system where commands can be issued to turn devices on or off. Use the Command Pattern to achieve this.

## Steps:
1. Create a New Java Project: Create a new Java project named CommandPatternExample.
2. Define Command Interface: Create an interface Command with a method execute().
3. Implement Concrete Commands: Create classes LightOnCommand, LightOffCommand that implement Command.
4. Implement Invoker Class: Create a class RemoteControl that holds a reference to a Command and a method to execute the command.
5. Implement Receiver Class: Create a class Light with methods to turn on and off.
6. Test the Command Implementation: Create a test class to demonstrate issuing commands using the RemoteControl.

## Code:

### `Command.java`
```java
package CommandPatternExample;

public interface Command {
    void execute();
}
```

### `Light.java`
```java
package CommandPatternExample;

public class Light {
    public void turnOn() {
        System.out.println("Light is ON");
    }

    public void turnOff() {
        System.out.println("Light is OFF");
    }
}
```

### `LightOnCommand.java`
```java
package CommandPatternExample;

public class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}
```

### `LightOffCommand.java`
```java
package CommandPatternExample;

public class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }
}
```

### `RemoteControl.java`
```java
package CommandPatternExample;

public class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}
```

### `TestCommand.java`
```java
package CommandPatternExample;

public class TestCommand {
    public static void main(String[] args) {
        Light livingRoomLight = new Light();

        LightOnCommand lightOn = new LightOnCommand(livingRoomLight);
        LightOffCommand lightOff = new LightOffCommand(livingRoomLight);

        RemoteControl remote = new RemoteControl();

        remote.setCommand(lightOn);
        remote.pressButton();

        remote.setCommand(lightOff);
        remote.pressButton();
    }
}
```

## Output:
```
Light is ON
Light is OFF
```




# Exercise 10: Implementing the MVC Pattern

## Scenario:
You are developing a simple web application for managing student records using the MVC pattern.

## Steps:
1. Create a New Java Project: Create a new Java project named MVCPatternExample.
2. Define Model Class: Create a class Student with attributes like name, id, and grade.
3. Define View Class: Create a class StudentView with a method displayStudentDetails().
4. Define Controller Class: Create a class StudentController that handles the communication between the model and the view.
5. Test the MVC Implementation: Create a main class to demonstrate creating a Student, updating its details using StudentController, and displaying them using StudentView.

## Code:

### `Student.java`
```java
package MVCPatternExample;

public class Student {
    private String name;
    private String id;
    private String grade;

    public Student(String name, String id, String grade) {
        this.name = name;
        this.id = id;
        this.grade = grade;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getGrade() {
        return grade;
    }

    public void setGrade(String grade) {
        this.grade = grade;
    }
}
```

### `StudentView.java`
```java
package MVCPatternExample;

public class StudentView {
    public void displayStudentDetails(String studentName, String studentId, String studentGrade) {
        System.out.println("Student Details:");
        System.out.println("Name: " + studentName);
        System.out.println("ID: " + studentId);
        System.out.println("Grade: " + studentGrade);
    }
}
```

### `StudentController.java`
```java
package MVCPatternExample;

public class StudentController {
    private Student model;
    private StudentView view;

    public StudentController(Student model, StudentView view) {
        this.model = model;
        this.view = view;
    }

    public String getStudentName() {
        return model.getName();
    }

    public void setStudentName(String name) {
        model.setName(name);
    }

    public String getStudentId() {
        return model.getId();
    }

    public void setId(String id) {
        model.setId(id);
    }

    public String getStudentGrade() {
        return model.getGrade();
    }

    public void setGrade(String grade) {
        model.setGrade(grade);
    }

    public void updateView() {
        view.displayStudentDetails(model.getName(), model.getId(), model.getGrade());
    }
}
```

### `TestMVC.java`
```java
package MVCPatternExample;

public class TestMVC {
    public static void main(String[] args) {
        // Create a Student model
        Student model = new Student("John Doe", "12345", "A");

        // Create a StudentView
        StudentView view = new StudentView();

        // Create a StudentController
        StudentController controller = new StudentController(model, view);

        // Display initial student details
        System.out.println("Initial Details:");
        controller.updateView();

        // Update student details
        controller.setStudentName("Jane Smith");
        controller.setStudentGrade("B");

        // Display updated student details
        System.out.println("\nUpdated Details:");
        controller.updateView();
    }
}
```

## Output:
```
Initial Details:
Student Details:
Name: John Doe
ID: 12345
Grade: A

Updated Details:
Student Details:
Name: Jane Smith
ID: 12345
Grade: B
```




# Exercise 11: Implementing Dependency Injection

## Scenario:
You are developing a customer management application where the service class depends on a repository class. Use Dependency Injection to manage these dependencies.

## Steps:
1. Create a New Java Project: Create a new Java project named DependencyInjectionExample.
2. Define Repository Interface: Create an interface CustomerRepository with methods like findCustomerById().
3. Implement Concrete Repository: Create a class CustomerRepositoryImpl that implements CustomerRepository.
4. Define Service Class: Create a class CustomerService that depends on CustomerRepository.
5. Implement Dependency Injection: Use constructor injection to inject CustomerRepository into CustomerService.
6. Test the Dependency Injection Implementation: Create a main class to demonstrate creating a CustomerService with CustomerRepositoryImpl and using it to find a customer.

## Code:

### `CustomerRepository.java`
```java
package DependencyInjectionExample;

public interface CustomerRepository {
    String findCustomerById(String id);
}
```

### `CustomerRepositoryImpl.java`
```java
package DependencyInjectionExample;

public class CustomerRepositoryImpl implements CustomerRepository {
    @Override
    public String findCustomerById(String id) {
        // In a real application, this would fetch data from a database
        if (id.equals("123")) {
            return "John Doe";
        } else {
            return "Customer not found";
        }
    }
}
```

### `CustomerService.java`
```java
package DependencyInjectionExample;

public class CustomerService {
    private CustomerRepository customerRepository;

    // Constructor Injection
    public CustomerService(CustomerRepository customerRepository) {
        this.customerRepository = customerRepository;
    }

    public String getCustomerName(String id) {
        return customerRepository.findCustomerById(id);
    }
}
```

### `TestDI.java`
```java
package DependencyInjectionExample;

public class TestDI {
    public static void main(String[] args) {
        // Create a concrete implementation of the repository
        CustomerRepository customerRepository = new CustomerRepositoryImpl();

        // Inject the repository into the service via constructor
        CustomerService customerService = new CustomerService(customerRepository);

        // Use the service to find a customer
        System.out.println("Customer with ID 123: " + customerService.getCustomerName("123"));
        System.out.println("Customer with ID 456: " + customerService.getCustomerName("456"));
    }
}
```

## Output:
```
Customer with ID 123: John Doe
Customer with ID 456: Customer not found
```


