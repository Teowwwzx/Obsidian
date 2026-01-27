# Four Pillars
## 1. Encapsulation
use **Private** to hide method inside a class.
### Private
A access modifier and main tool for **Encapsulation.**

## 2. Inheritance
## 3. Polymorphism
## 4. Abstraction


# Keywords
## Static Method
This method belongs to the Class, not an object instance.
No need use the new keyword.
Example: `Math.sqrt()` is a static method

**Abstract**


**Void** 
Mean Empty, No return value
- Execute a method without return anything
	- exp: System.out.println("Nothing to return")
- A method required a return value after execution
	- exp: int will return a number.

**@Override**
A best practice to avoid create a new method while inherited from a parent class
- Without @override
	- Ide will recognize as a new method which run the method correctly but losing what?
- With @override
	- Ide will report bug immediately and tell: "No pya() method in parent class"

**Extend**
Build relationship with the class only or method also?
- Without Extend
	- Both class are independent, we can't inherit the method and used @override from the class
- With Extend



Why Java always need to create object like
- new Obejct = object
and this required more steps like called.self?

Spring Cloud


String
- Why need stringbuilder?
Int
- Any important notes?
Set
- Pro: To avoid duplicated data inside a set.
- noDuplicatedSet = {"a", "b"}
BigDecimal
- Pros: To avoid floating points issues like float
HashDictionary
- Key-pair value and the performance O(1)
- Cons: More memory, no order when retrieved
LinkedHashDictionary
- Pros: Store with timestamp
- Cons: Used more memory than HashDictionary
CoccurentHashDictionary
- Pros: Can modify the same Dictionary at the same time
- Cons: More complex architecture


