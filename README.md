* SOLID OOP(Object Oriented Programming) principles: -> help write readable, maintainable, easy to upgrade/modify code
==
- S: Single responsibility
-> A class/function should do one and only one job
-> easy to testing, reading, maintain  
Ex: 
``
// bad
Developer {
	name;
	age;
	
	coding();
	testing();
	managing();
	
}

// Good
abstract Employee {
    name;
	age;
}

Developer extend Employee {
	coding();
}

Tester extend Employee {
	testing();
}

Manger extend Employee {
	managing();
}

-> In the above example the Employee maintains the Employee info. 
Developer do coding, tester only do testing and manger only do managing
``
==

O: Open for Extension/Closed for Modification: -> Software entities should be Open for extension, but closed for modification.
-> That mean when we add new one feature we do not need to modify the source code. 
Ex:
// bad 
abstract Employee {
    name;
	age;
}

Developer extend Employee {
	coding();
}

Manger extend Employee {
	managingDeveloper(Developer developer);
}

-> when we add new one staff then we need to add more task for manager
Tester extend Employee {
	testing();
}

Manger extend Employee {
	managingDeveloper(Developer developer);
	managingTester(Tester tester);
}

// good
Manger extend Employee {
	managing(Employee Employee);
}
-> when we add new one staff then we don't need to add more task for manager
==
L: Liskov Substitution -> A child class must be able to completely substitute and act-in for it’s base(parent) class 
(1 lop con phai co kha nang thay the hoan toan và hanh dong cho lop cha cua no)(thua ke 100% tu cha cua no)
Ex: Let say only manager or director can see the employee salary
// bad

abstract Employee {
    name;
	age;
	abstract viewOtherMemberSalary();
}

Developer extend Employee {
	coding();
	viewOtherMemberSalary(); // Developer role cannot viewOtherMemberSalary
}

Manger extend Employee {
	managingDeveloper(Developer developer);
	viewOtherMemberSalary(); // ok
}

// good
abstract Employee {
    name;
	age;
}

abstract ManagementTeam extend Employee {
	abstract viewOtherMemberSalary();
}

Developer extend Employee {
	coding();
}

Manger extend ManagementTeam {
	managingDeveloper(Developer developer);
	viewOtherMemberSalary(); // ok
}

Director extend ManagementTeam {
	viewOtherMemberSalary(); // ok
}
==
I: Interface Segregation // Phan chia giao dien
-> A client should never be forced to implement a function that it does not require. Instead of having bloated interfaces, segregate them based on roles.
-> Implement class only have implement what it needs don't forced. should separate by roles
Ex:
// bad
interface Employee {
	reporting();
	coding();
	testing();
	manage()
}

Developer implement Employee {
	coding() { i can code };
	reporting(){ i can report };
	testing(){}; // violet
	manage(){}; // violet
}

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


Developer implement CodeAble, Employee {
	coding() { i can code };
	reporting(){ i can report };
}
==
D: Dependency Inversion - Dao nguoc phu thuoc
-> Entities must depend on abstractions instead of concretions. Instead of using direct references from a high-level module to a low-level module, use abstractions.
-> phu thuoc vao abstractions ko phai class
Ex: 
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

-> when we want to use other type of phone like SamsungPhone we need to modify the PhoneUser again or update ApplePhone

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











