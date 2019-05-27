# SOLID Object Oriented Programming Principles

Help write readable, maintainable, easy to upgrade/modify code

## S -  Single responsibility

- A class/function should do one and only one job
- easy to testing, reading, maintain 
- Example: 

```java
// bad
class Developer {
	name;
	age;
	
	coding(); // violet
	testing(); // violet
	managing(); // violet
	
}
```
```java
// Good
abstract class Employee {
    name;
	age;
}

class Developer extend Employee {
	coding();
}

class Tester extend Employee {
	testing();
}

class Manger extend Employee {
	managing();
}

// => In the above example the Employee maintains the Employee info. 
// => Developer do coding, tester only do testing and manger only do managing
```

## O - Open for Extension/Closed for Modification
- Software entities should be Open for extension, but closed for modification.
- That mean when we add new one feature we do not need to modify the source code. 
- Example: 
```java
// bad 
abstract class Employee {
    name;
	age;
}

class Developer extend Employee {
	coding();
}

class Manger extend Employee {
	managingDeveloper(Developer developer); 
}

// => when we add new one staff then we need to add more task for manager
class Tester extend Employee {
	testing();
}

class Manger extend Employee {
	managingDeveloper(Developer developer); // violet
	managingTester(Tester tester); // violet
}

```
```java
// good
class Manger extend Employee {
	managing(Employee Employee); // ok
}
// => when we add new one staff then we don't need to add more task for manager
```

## L - Liskov Substitution

- A child class must be able to completely substitute and act-in for it’s base(parent) class
- Example: 

```java
// Let say only manager or director can see the employee salary
// bad
abstract class Employee {
    name;
    age;
    abstract viewOtherMemberSalary();
}

class Developer extend Employee {
	coding();
	viewOtherMemberSalary(); // Developer role cannot viewOtherMemberSalary
}

class Manger extend Employee {
	managingDeveloper(Developer developer);
	viewOtherMemberSalary(); // ok
} 

```
```java
// good
abstract class Employee {
    name;
    age;
}

abstract class ManagementTeam extend Employee {
	abstract viewOtherMemberSalary();
}

class Developer extend Employee {
	coding();
}

class Manger extend ManagementTeam {
	managingDeveloper(Developer developer);
	viewOtherMemberSalary(); // ok
}

class Director extend ManagementTeam {
	viewOtherMemberSalary(); // ok
}
```
## I - Interface Segregation
- A client should never be forced to implement a function that it does not require. Instead of having bloated interfaces, segregate them based on roles.
- Implement class only have implement what it needs don't forced. should separate by roles
- Example:
```java
// bad
interface Employee {
	reporting();
	coding();
	testing();
	manage()
}

class Developer implement Employee {
	coding() { i can code };
	reporting(){ i can report };
	testing(){}; // violet
	manage(){}; // violet
}
```

```java
// good
interface Employee {
	reporting();
}

interface CodeAble {
	coding();
}


interface TestAble {
	testing();
}

interface MangeAble {
	manage();
}


class Developer implement CodeAble, Employee {
	coding() { i can code }; // ok
	reporting(){ i can report }; //ok
}
```
## D - Dependency Inversion
- Entities must depend on abstractions instead of concretions. Instead of using direct references from a high-level module to a low-level module, use abstractions.
- Example:
```java
// bad 
class ApplePhone {
	call();
	message();
}


class PhoneUser() {
	ApplePhone phone;
	
	PhoneUser(ApplePhone phone) {
		this.phone = phone;
	}
	
	call() {
		this.phone.call()
	}
}

// -> when we want to use other type of phone like SamsungPhone we need to modify the PhoneUser again or update ApplePhone
```
```java
// good
interface SmartPhone {
	call();
	message();
}

class ApplePhone implement SmartPhone {
	call();
	message();
}

class SamsungPhone implement SmartPhone {
	call();
	message();
}


class PhoneUser() {
	SmartPhone phone;
	
	PhoneUser(SmartPhone phone) {
		this.phone = phone;
	}
	
	call() {
		this.phone.call()
	}
}

```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
