# Chapter 02
```
Name things well
```
## Meaningful Names
- i must always choose good names which are easy to understand
- name must answer those 3 questions `why, what, how`
- if name need commment to be clarified then that name is not meaningful


## Avoid Disinformation
- don't use appreviations like famous appreviations like `hp` for `hypothesis`
- use `accountList` as variable name only if that variable is a list but it is not preferred
- if you have array of accounts use `accounts` rather than `accountList` 
- never to name variables to only satisfy the compiler, if variable already exists name it variable2, that is meaningless 
- don't use words that are simillar in very small ways like `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`
- Use Pronounceable Names: use names that you can read to can talk about them with team during meetings


## searchable names
- i must choose names which are easy to use as search parameters
- notice the problem if i choose variable name to be `e` and i try to search for it on project, bad senario 


## avoid encoding
- never to use encoding variable names
- it is not logic to ask programmer to learn encoding language to can understand variable names


## Hungarian Notation (HN)
- in that we name variables by name + type
- ex: phoneString rather than phoneNumber
- that way cause problems:
  - if i make updates to my project and change that phone number to be object not stirng that name is meaningless, now i had to change variable name which will take a lot of time
  - in modern programming it is preffered to name variables by there job and never to think about type of variable



## Naming

### interfaces and implementations
- we don't need to name variable like that `IShape` or `ShapeImp` it is better to name them `Shape`

### class name
- must be a noun not verb

### method name
- must start with verb
- use set and get for accessors and mutators

### pick one word per concept
- get, fetch, and retrieve give the same meaning
- use same name to get values, use same verb for simillar functions
  - ex: if i want to get all data and data with id name two functions like that 
     - getAllData() and getDataById
   - not to name them: getAllData() and retreiveDataById


## don't pun
- never to use same verb for two diffrent functions
- ex: say you want to add two numbers then you will use method add
  - now you want to add element to list, will i use method add too?
  - of course no i should here use another verb like insert or append becasue veb add has been used for diffrent perpose in that code

## use solution domain names
- remember that the one who read code after you will be a programmer
- so use names that are common used for you both 
- like names in cs 

## use problem domain names
- if i can't name veriables with variables famous for developers
- i must name them using solution domain names
- so if the next developer can't understand what i mean with those variables, he will ask domain expert what those mean


## add meaningfull context
- there are few words which are meaningful in context
- if the word is not meaningful then add prefix to add
- ex: status in class Address is meaningful (`status`)
    - if i use that status outside class to refere to status of address it will be meaningless so i must use prefic address before it (`addrStatus`)
- break big function into smaller functions each with meaningfull meaning to make code more clean and easy to understand and abstraction

## Don’t Add Gratuitous Context
- shorter names are more better than longer names
- add no more context to the name rather than is neccessary
- longer and very specific names are bad sometimes because i may want to use same method in another place and that name will not be helpful for me 
- ex: if i make method to create email for admin i call it `makeAdminEmail` after that i find that i have to make email for client, both structure is the same, not name `makeAdminEmail` is meaningless for user and if i make another function with the same structure it will be duplication so it was much better to name that method `makeEmail`

## final words
- Naming is a descriptive skill that requires both proficiency and a shared cultural understanding among developers.
- There's often a fear of renaming elements in code due to potential objections from other developers. However, it's important not to let this fear hinder improvements.
- we don't share that fair
- in fact other developers will be very gratuful when i rename things to meaningfull names
- if you try to rename things in your code use tools to make it more easy