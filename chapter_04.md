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
- the only good comment is the comment that you have no way to write it
## legal comments
- 