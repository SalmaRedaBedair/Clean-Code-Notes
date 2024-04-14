# Chapter 03
```text
We always use functions, let's learn how to write good function
```
## small
- the first rule of function that they should be small
- the second rule of function that they should be smaller than that
- function should be be hardly ever 20 lines long
### how should function be small
- every function should be 2-4 lines long
- each should tell you a story
- each led you to next in compelling order

## blocks and indecating
- blocks within if statements, else statements, while statements should be one line long
- probably that line should be function call
- that not only keep function small but also documentary value because those functions name discripe what the function do 
- number of indent level (if statements) in function should not be greater than one or two 

## do only one thing
```text
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.
THEY SHOULD DO IT ONLY
```
### one level of abstraction
- function should have only one level of abstraction
- to know if function have only one level of abstraction or not it should be expressed with `To paragraph`
- like that 
```text
TO RenderPageWithSetupsAndTeardowns, we check to see whether the page is a test page
and if so, we include the setups and teardowns. In either case we render the page in
HTML
```

## one level of abstraction
- there is 3 levels of abstraction (high, intermediate, low)
- function should be only of one level of those three levels 
- mixing levels is always confustion, readers may not be able to tell wheather that particular expression is an essential or a detail

### Reading code from top to bottom: the step down rule
- we should read function as To paragraph, each of which should describe that level of abstraction and refering subsequent TO paragraphs at the next level down
```text
To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns.
To include the setups, we include the suite setup if this is a suite, then we include the
regular setup.
To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page
and add an include statement with the path of that page.
To search the parent. . .
```
- notice that above paragraph every To paragraph descripe some thing in the above paragraph
- above paragraph is high level of abstraction, next level is lower and lower ...
- _By following this approach, code becomes easier to understand because it mirrors the way humans naturally process information: starting with high-level concepts and progressively diving deeper into the details. This makes it easier for developers to follow the logic and flow of the code, enhancing readability and maintainability_.
- it is too difficult for programmer to follow those rules, but learing that rules is very important, try to follow them, by practice you will be able to follow all of those rules
## switch statements

## use descriptive names
- it is too important to choose descriptive names for functions
- the smaller function is, the easier it is to choose descriptive names
- don't be afraid to make long name for functions, long name is better than short useless name

## function arguments
- ideal number of arguments in function is zero
- then 1, then close by 2
- 3 should be avoided but is possible
- more than 3 require very special cases, they should be avoided
### reading code
- pass arguments make reading code more hard because it adds new detail that is not important for me now 
### testing
- passes arguments make it harder
- Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly
- no argumnets => trivial
- one argument => not too hard
- two arguments => a bit more challenging
- more than two arguments => toooooooooooooooooo hard

### when to pass one argument to funciton (monadic functions)
- there are two reasons to pass one argument to funciton
  - you want to ask a question about that argument
    ```php
    public function isActive($is_active)
    ```
  - you want to make operation on that argument
    ```php
    // like remove spaces as an example
    public function removeSpaces($textField);
    ```
### flag arguments
- it is a bad practice to pass boolen argument to function 
- it violates the rule that every function should do only one thig
- in that case that function will to diffrent things when true and false

### two function arguments (dyadic function)
- always try to convert it to monadic function
- use it when i have Cartesian points
- when i want to check if give value like expected
  - when do it be careful to name function with name make it easy for you to except which argument should be passed first
    ```php
    public function CheckInputEqualsExpected($input, $expected)

    // i think it is useless new ides tell me the order of the arguments
    ```
### three arguments (triads)
- functions that take three arguments are harder to understand than dyads
- you should think carefully before creating them

### argument objects
- when function need more than two or three arguments, map some of those arguments to a class 
```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

### argument list (...args)
- function have variable number of arguments
```java
String.format("%s worked %.2f hours.", name, hours);
```
- that function must be monadic, dyadic or triadic only 
- it will be a mistake to give them more than 3 arguments
```java
void monad(Integer... args);
void dyad(String name, Integer... args);
void triad(String name, int count, Integer... args);
```

## verbs and keywords
- i must choose good name for function and its arguments and be careful of the order of those arguments
- in case of monadic function and its argument must form a very nice verb/noun pair
```java
write(name)
// but that is better 
writeField(name) 
```
- in case of dyadic 
```java
assertEquals(expected, actual)
// might be better written as 
assertExpectedEqualsActual(expected, actual)
```
## have no side effects
- when i make function but it does another hidden thing too, that is called temporal coupling
- like itialize session 
```java
public class UserValidator {
    private Cryptographer cryptographer;
    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
        if ("Valid Password".equals(phrase)) {
            Session.initialize();
            return true;
            }
        }
        return false;
    }
}
```
- when you have temporal coupling it should be clear in the name of the function `checkPasswordAndInitializeSession`

## command query seperation
- function chould either do something or answer something, but not both.
```java
public boolean set(String attribute, String value);
// set value and return true if successfully save
```
```java
if (set("username", "unclebob"))
```
- there is a confusion
  - is it check if the attribute set successfully
  - or if the attribute username is equal to unclebob
- so that is more better to seperate the function the set the value form the fucntion that check
```java
public void set(String attribute, String value);
public boolean ifExists(String attribute, String value);
```
## prefere exceptions to return error codes
- returning error code using if statement lead me to deeply nested structure
- if i use exceptions instead of returning error code, returning error process can be seperated from happy code path 
```java
try {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}
catch (Exception e) {
    logger.log(e.getMessage());
}
```
### try/catch extraction
- it is better to extract try catch body into seperated function, like that: 
```java
public void delete(Page page) {
 try {
    deletePageAndAllReferences(page);
 }
 catch (Exception e) {
    logError(e);
 }
 }
 private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
 }
 private void logError(Exception e) {
    logger.log(e.getMessage());
 }
```
- that seperation make code easy to understand and modify

### error handling is one thing 
- try/catch/finally should be the only code inside function
- try should be first thing in function
- catch/finally should be last thing in function

## don't repeat yourself

## structured programming
- dijekstra said that, every function and every block inside function should have only one entry and only one exit
- following that rule mean that there should be only one return inside function
- no break or continue inside loop
- never to use goto
- all of that rules will be avoided if you try to make your function small

## how do i write a function like this
- at first i write long function with long list of arguments and many nested loops, then i try to refactor it and apply all the rules we have discussed inside that chapter

## conclusion
- Master programmers think of systems as stories to be told rather than programs to be written.
