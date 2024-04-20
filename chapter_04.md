# chapter 04
```text
comments are failure
```
- comments are always failure, we should always try to express ourselves in code, avoid using comments
- the more older comments is and the further away from the thing it descripe, the more its just plain wrong
- bad comments are evail because programmers whill not maintan them
- the energy used to maintain bad comments should be used to maintain code, we don't need comments in forst place
- inaccurate comments worse than no comments
- `truth can only be found in one place: the code`
  - the code can truly tell you what it does
  - it is the only source of accurate information
  - comments are sometimes necessary but we will pay alot of energy to minimize them

## comments don't make make up for bad code
- one of the common motivation for writing comments is bad code
- when you write bad code, you will comment it and try to write another code
- you shouldn't comment thet code, you should rewrite it
- when you write bad code, you try to express it using comments, rather than spending time writing comments to express bad code, spend that time to clean it.

## explain yourself in code
- instead of writing comments to express part of code, make function say the same as comment say 
- notice the difference:
```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && 
 (employee.age > 65)) 

if (employee.isEligibleForFullBenefits())
```

## good comments
```text
the only good comment is the comment that you have no way to write it
```

### legal comments
- sometimes, we are forced to to write legal comments
- ex: copyright, authorship
- as possible refer to licence or external documentation rather than putting all standards in code

### informative comments
- sometimes comments are useful
- notice that example
```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile(
 "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
- but it might be cleaner if i pass special class that convert the formats of date and time

### explanation of intent
- sometimes comments are useful when it explain the intent of hard idea of code

### clarification 
- sometimes comments are useful when it clarify the part of code or variable or function name
- it is better to name that variable or function with name easy to understand
- but if that name is from library or if you haven't access to alter it then a helpful clarifying comment is useful

### warning consequences
- sometimes i want to warn about the consequences of bad code
- i write comment to warn other programmers from using that function because it take long time for ex

### TODO comments
- they are jobs that programmer should do but for some reason can't do at the moment
- it is written like that
```php
//TODO: task that should be done
```
- usage of TODO comments:
  1. reminder to delete deprecated feature
  2. plea for someone else to look at problem
  3. request for someone else to think of better name
  4. reminder to make change that is dependent on a planned event
- IDEs have new feature that locate all TODO comments, to not be lost 
- always scan those comments TODOs and try to eliminate them as soon as possible
- [TODO link in php storm](https://www.jetbrains.com/help/phpstorm/using-todo.html#add_pattern_filter_todo)

### amplification
- comment can be used to amplify the importance of part of code that others may think it is inconsequential

### Javadocs in Public APIs

## Bad Comments
```text
most comments fall here
```
### Mumbling
- if you decide to write comment spend more time to think of that comment and try to not use it.

### redundant comments
- add nothing do the code, code is easier to understand 

### Misleading comments
- comment is not accurate describing the function
- it say wrong thing about that function 
- notice that example comment say that it will throw exception if this.closed is true, but code throw exception when it is false 
````php
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis) 
    throws Exception
{
if(!closed)
{
    wait(timeoutMillis);
    if(!closed)
        throw new Exception("MockResponseSender could not be closed");
}
}
````
### Mandated Comments
- comments have no benefits
- they add nothing to understanding the code
- like javadocs

### journal comments
- add comments to tell when i go something in module
- it like comments now days
- they used it long ago, but now version control replace it
- they are something like that:
```php
/*
* Changes (from 11-Oct-2001)
 * --------------------------
 * 11-Oct-2001 : Re-organised the class and moved it to new package 
 * com.jrefinery.date (DG);
 * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate 
 * class (DG);
 * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate 
 * class is gone (DG); Changed getPreviousDayOfWeek(), 
 * getFollowingDayOfWeek() and getNearestDayOfWeek() to correct 
 * bugs (DG);
 * 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
 * 29-May-2002 : Moved the month constants into a separate interface 
 * (MonthConstants) (DG);
 * 27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
 * 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
 * 13-Mar-2003 : Implemented Serializable (DG);
 * 29-May-2003 : Fixed bug in addMonths method (DG);
 * 04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
 * 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
 */
```
### Noise comments 
- add no thing to code, like that
```php
/**
 * Returns the day of the month.
 *
 * @return the day of the month.
 */
public int getDayOfMonth() {
 return dayOfMonth;
}
```
### scary noise
- comments used in javadocs
- add nothing to code, like that
```php
/** The name. */
private String name;
/** The version. */
private String version;
/** The licenceName. */
private String licenceName;
/** The version. */
private String info;
```
### Don’t Use a Comment When You Can Use a Function or a Variable
- always try to replace comments that express part of code with good named functions or variables
- you can add comments as hint during making function, but after finishing it you must remove all of them

### Position Markers
- like that:
```php
// Actions //////////////////////////
```
- sometimes they are useful to be used but I should always try to reduce their usage
- use them only when they have benefit
- if you use them a lot, they will be ignored while reading code

### closing brace comments
- often i have to use them because the function is too long, instead of using them try to shorten your code

### Attributions and Bylines
- add comment to tell me who wrote that code, but version control like github solved it
```php
/* Added by Rick */
```

### Commented-Out Code
- never to comment code 
- other programmers will think that that code is too important to delete 
- you may be afraid about deleting code because you will need it in the future
- never to be afraid delete it and you can find it in github

### HTML Comments
- never to add html comment
- they will be very hard to read
- we add comments for more clarification
```php
/**
 * Task to run fit tests. 
 * This task runs fitnesse tests and publishes the results.
 * <p/>
 * <pre>
 * Usage:
 * &lt;taskdef name=&quot;execute-fitnesse-tests&quot; 
 * classname=&quot;fitnesse.ant.ExecuteFitnesseTestsTask&quot; 
 * classpathref=&quot;classpath&quot; /&gt;
 * OR
 * &lt;taskdef classpathref=&quot;classpath&quot; 
 * resource=&quot;tasks.properties&quot; /&gt;
 * <p/>
 * &lt;execute-fitnesse-tests 
 * suitepage=&quot;FitNesse.SuiteAcceptanceTests&quot; 
 * fitnesseport=&quot;8082&quot; 
 * resultsdir=&quot;${results.dir}&quot; 
 * resultshtmlpage=&quot;fit-results.html&quot; 
 * classpathref=&quot;classpath&quot; /&gt;
 * </pre>
 */
```
### Nonlocal Information
- if you have to put comment then make it describe the function 
- don't offer system wide information, like port number
```php
/**
 * Port on which fitnesse would run. Defaults to <b>8082</b>.
 *
 * @param fitnessePort
 */
public void setFitnessePort(int fitnessePort)
{
this.fitnessePort = fitnessePort;
}
```
### Too Much Information
- don't add any historical discussion or irrelevant description details into your comment
### Inobvious Connection
- comment must add some information to clarify the function
- never to add comment that can't be understand like function 
- it is like when i can't understand think and ask someone else who can't understand too, so now we need third one to explain.
### function headers
- i add that description to describe what function does
- that might happen because function it is too long
- short function doesn't need description
- like short function with good naming and never to use description
### Javadocs in Nonpublic Code
- adding javadocs to nonpublic code is not useful

