# chapter 06 (Objects and Data Structures)
```text
some times i have to make my variables private
i don't want any other classes to depend on it 
i want to leave it freedom to change data type and implementation 
```

## Abstraction
- it is preferred to hide details of the function and give it name that express its usage
```php
// bad example
public interface Vehicle {
 double getFuelTankCapacityInGallons();
 double getGallonsOfGasoline();
}

// good example
public interface Vehicle {
 double getPercentFuelRemaining();
}
```

## Data/Object Anti-Symmetry
```text
here my goal is to open and modify only one place if i want to add new type or functionality
modify or add only one class (only one file, only one function)
```
### object & OO code
- object hide data and expose functions
- it is better when i have to add new data type rather than new function 
- ex: if i want to add new shape diamond
```php
public class Square implements Shape {
 private Point topLeft;
 private double side;
 public double area() {
 return side*side;
 }
}
public class Rectangle implements Shape {
 private Point topLeft;
 private double height;
 private double width;
 public double area() {
 return height * width;
 }
}
public class Circle implements Shape {
 private Point center;
 private double radius;
 public final double PI = 3.141592653589793;
 public double area() {
 return PI * radius * radius;
 }
}
```

### data structure and procedure code
- data structure expose data and have no meaningful functions 
- it is better when i have to add new function rather than new type
- like add function parameter, it will be added only to Geometry class
```php
public class Square {
 public Point topLeft;
 public double side;
}
public class Rectangle {
 public Point topLeft;
 public double height;
 public double width;
}
public class Circle {
 public Point center;
 public double radius;
}
public class Geometry {
 public final double PI = 3.141592653589793;
 public double area(Object shape) throws NoSuchShapeException 
 {
 if (shape instanceof Square) {
 Square s = (Square)shape;
 return s.side * s.side;
 }
 else if (shape instanceof Rectangle) {
 Rectangle r = (Rectangle)shape;
 return r.height * r.width;
 }
 else if (shape instanceof Circle) {
 Circle c = (Circle)shape;
 return PI * c.radius * c.radius;
 }
 throw new NoSuchShapeException();
 }
}
```
### imagine the bad scenario if i opposite the two above examples
- if i want to add new shape 'diamond' and i use data structure and procedure code:
  - i will create new class Diamond extends shape
  - i will add the implementation of calculating area to Geometry class
  - change 2 files
- if i want to add parameter function and i use object and OO code
  - i will add that function to every class, add it to circle, square, rectangle
  - change 3 files

## The Law of Demeter
- the innards shouldn't know about the innards of the object it manipulates
- if i have method f and class c, method should call object of:
  1. class c
  2. object created by f
  3. object passed as an argument to f
  4. object held instance variable of c
- function must call to friends not to strangers
```php
// that code violates the Law of Demeter
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```
- why violate?
   - function call object created by another function
### Train Wrecks
```php
// bad example
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

// good example
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

### hybrid
- i sometimes have to make hybrid structure, that is half object and half data structure
- that hybrid is the most bad thing
- avoid creating it
- that make it hard to add new function or add new data type 

## Hiding Structure
- 
## Data Transfer Objects
- quintessential form of data structure is a class with public variables and no functions
- this quintessential form is called (DTO) data transfer object
- that is very useful in web application, transfer raw data in database into object in application

### active record
- DTO with navigational methods like save and find
- unfortunately some developers trait data structure as they were objects by putting methods in them,
it is bad because it is a hybrid class
- to treat that i must create new object that contains the business rules and hide the internal structure

