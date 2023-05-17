# Development Principles

This is not "Rules". This is "Principles". Rules can be changed. Principles will not be changed. You must follow these principles.

## You need to think about:

### DRY.
* 
* Means “Don't Repeat Yourself”. You never write same/similar code on the different place. Never do copy & paste. When you want to do Copy & Paste,  make new function to handle shared work.

### Flexibility & Extendability.
* 
* Your shared function is not okay enough just for current requirement. You have to imagine the future and design it to support future extension.

### KISS. Keep it simple, stupid.
* 
* You need to write your code as simple as possible.
* It doesn't mean that you can just write simplest stupid code which missing many thing. You need to think more and more and more and more and more and more to shape up your code to reduce.
* It doesn't mean reduce white space. You need to format the code to follow the existing coding convention.

### Less inline comments
* 
* It doesn't mean that you don't have to write inline code. It means that write a good code which doesn't need inline comment.
* Good code doesn't need comments because good code itself is really descriptive. if naming (Variable names, class, method names … ) are enough descriptive, other people can easily catch the meaning of the process without any comments.

## Naming

* You MUST use descriptive terms. never use “user1” or “tab2” like ambiguous naming.
* You MUST not use "abbreviated form”. E.G. never use “Cat” for “category”.
* You must be careful about plural form and singular form. Single data must be stored in variables which have singular form name such as “user”, “category". Multiple data( such as array of same data ) must be stored in variables which have plural form name such as “users”, “categories”.
* Never use “list”/“data" or “info” and similar postfix . If you want to use “UserList”, it must be “Users”. “UserInfo” must be “user”. “list”/“data" or “info” have no meanings.


## Find a solution

* Never ask for support to others without careful consideration. Don't bother others. You must think as much as you can and did everything you can and state hypotheses as much as you can.
* NEVER choose the most easiest solution. choose the best solution which fits best to the situation.
* NEVER choose the first solution you found on Google. It is not always best solution. You must continue googling until you find best solution.
* You always need try to think better way. Doubt your way of coding always and try to think what is the better way.
* Always think( Or Find ) at least 3 ways when you face a problem/issue and choose the best way ( not easiest way ).
* Never choose a solution which is good enough, choose the best solution.


## Using third-party Library

* Be aware of the license of the library. Never use GPL, LGPL licensed libraries in the client apps and you many know why you cannot use them.
* You can use MIT / Apache license only
* Learn about common licenses.


## Copy & Paste

* Never Do Copy & Paste
    * If you want to do that, it's a chance to refactor your code to share same function/method.
* If you still want to bring some code from others.


## Support & Question

* If you need my support when you have a problem, you must give me 3 or more your hypotheses you've already tried and what you knew from the trial.


## Coding Principles

* Define coding standard and follow it.
* All classes, modules, functions methods, property have their own responsibilities.
    * Never write 2 or more different task in one methods/functions.
    * Never implement 2 or more different entities in one class
* Never write long methods/functions/classes. If it becomes long, it's timing to divide to 2 or more classes/functions.
    * One Method/Function must be shorter than 20 lines.
    * One Class/File must be shorter than 100 lines
