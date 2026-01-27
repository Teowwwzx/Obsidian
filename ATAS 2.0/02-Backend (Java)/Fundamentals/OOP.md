# Four Pillars:
## 1. Encapsulation
use **Private** to hide method inside a class.
- ### Private
	- A access modifier and main tool for **Encapsulation.**

## 2. Inheritance
Use **extends** to pass traits from parent to child.
- ### extend
	- Build relationship with the class only or method also?

| Without extend                                                                            | With extend |
| ----------------------------------------------------------------------------------------- | ----------- |
| Both class are independent, we can't inherit the method and used @override from the class |             |

## 3. Polymorphism
One interface, many different forms (like a universal remote).

## 4. Abstraction
Hide complex details and only show the "buttons" you need.


---

# Keywords:
## Static Method
This method belongs to the Class, not an object instance.
No need use the new keyword.
Example: `Math.sqrt()` is a static method

## **Abstract**
Use **Abstract** when want to force a group of different things to follow the same "rule" or "button" even if they work differently inside.

**An E-commerce Shipping System** with shipping providers: **FedEx, DHL and UPS.**
- **The Abstract Class (`ShippingProvider`):** You create an abstract class that defines a method `calculateRate()` . You don't write the code for it yet because FedEx calculates rates by weight, while DH: calculates by distance.
- **The Situation:** By making it **Abstract** to ensure if a new developer adds "China Post" tomorrow, the code **will not run** unless they implement `calculateRate`. It acts as a safety contract.
- **The Benefit:** Main "checkout" code doesn't need to know which company is being used; it just calls `.calculateRate()` on any shipping object.

## `.this`
In Java, we use `this` instead of `self`.
It refers to **current object.**
It help the code know you mean the "class variable", not a "local parameter."

**Updating a Profile**
- **The Situation:** Having a class variable called `bio`. A user submits a forms with a new `bio`.
- **The Code:** `this.bio = bio;`
- **Why it happens:** `this.bio` is the "permanent" data saved in the **Object**
	- `bio` is the "temporary" data coming from the User's Request.
	- `this` tells Java: "Take the new text and save it into this specific object's private memory."

## **void** 
Mean Empty, No return value
- Execute a method without return anything
	- exp: System.out.println("Nothing to return")
- A method required a return value after execution
	- exp: int will return a number.

## **@Override**
A best practice to avoid create a new method while inherited from a parent class
- Without @override
	- Ide will recognize as a new method which run the method correctly but losing what?
- With @override
	- Ide will report bug immediately and tell: "No pya() method in parent class"


---

## Why Java requires "new Object()"?
Java is a **class-based language.** Think of a **Class** as a blueprint and an **Object** as the actual house built from that blueprint.
- **Memory Management:** The `new` keyword tell Java to set aside a specific spot in the computer's memory for that unique instance.
- **Encapsulation:** By creating an object, you are creating a **safe** where that specific object's data (like a user's balance) is kept private and separate from other objects.
- **Identity:** If two "User" objects, they might have same blueprint, but `new` ensures they have different date (User A is not User B)

## What kind of Language is Python?
Python is a **high-level, interpreted, and dynamically typed** language.
- **Interpreted:** Unlike Java which compiled into bytecode and run by the JVM, Python code executed line-by-line by the Python Interpreter.
- **Dynamically Typed:** Don't need declare variable types (like `int` or `string`). Python figures out the type at runtime.
- **Everything is an Object:** In Python, even a simple number or a function is an object.

## How Python Handles Memory Management?
Python uses two main systems to manage memory: **Reference Counting** and **Garbage Collection**
- **Reference Counting:** Every object in Python keeps track of how many other things are "pointing" to it.
	- As soon as the count hits zero (meaning nothing is using it), Python immediately frees that memory.
- **Garbage Collection (GC):** Python has a built-in "cleaner" that looks for "circular references" (where Object A points to B, and B points to A, but your program is not using these two Object). This GC finds these and deletes them.
- **Memory Efficiency:** Python objects are considered "heavy" because they carry a lot of metadata (extra info about the object).

### 3. The 1k Users Scenario: Java vs. Python
If your system handles 1,000 users at the same time:

**Java's Background:** Yes, Java will run **1,000 instances** of the `User` object on the [[Heap memory]].
- Java uses a [[Thread Pool]]. Each "Request" (user) is usually handled by a thread, and that thread creates the objects it needs (like an [[Entity]] or [[DTO]]).

**Python's Background:** Python would also create 1,000 objects. However, Python objects (especially [[ORM]] objects like [[SQLAlchemy]]) are "live" and connected to the database, making them very "heavy" in memory.
- Because Python's memory management for 1,000 heavy objects can be expensive, developers often use **[[Serialization]]** to turn those objects into simple strings or dictionaries to save space.


### 4.1 `@Entity`
- Like **SQLAlchemy** in Python.
- `UserEnrity` is a live object carries hidden state like `_sa_instance_state` to keep track of database changes, so it's heavy.

```
// This represents the actual table in your Database
@Entity 
public class UserEntity { 
	private Long id;
	private String username;
	private String email;
	private String passwordHash; // ❌ SENSITIVE: Should never leave the server
	
	// Getters and Setters... 
}
```

### 4.2 DTO and the Constructor
- Like **Pydantic**.
-  `public UserResponseDTO(String username, String email)`, this is called a **Constructor**.
-  `this` keyword to save them into the object's **private** variables.
- constructor creates a **new** instance in memory every time a user profile is requested unlike static method.
```
// This is the "Clean" version for the User/API 
public class UserResponseDTO { 
	private String username;
	private String email; // Notice: NO passwordHash here. The "box" is safe.

	public UserResponseDTO(String username, String email) { 
		this.username = username;
		this.email = email; 
	} 
}
```


### 4.3 Service Layer & `@Autowired`
Java uses [[Dependency Injection]] (the `@Autowired` part).
- **What is `@Autowired`?** * In FastAPI, you might manually create a database session or pass it as a dependency.
    
    - In Java, `@Autowired` tells Spring: _"I need the tool called UserRepository to do my job. Please find it and plug it in for me automatically"_. It is like having a tool belt that is automatically filled when you start working.

- **Why need a `UserRepository` object?** * The Service handles **Logic** (e.g., "Is this user banned?"), but it doesn't know how to talk to the database.
    
    - The `UserRepository` is the **Repository** layer; it is the specific "Librarian" who knows exactly how to find the data in the stacks.

**The `getUserProfile` Method:** * `public UserResponseDTO getUserProfile(Long id)` is a method **inside** the `UserService` file.

- It **returns** a `UserResponseDTO` object.
    
- **The Logic:** It asks the Repository for a "Heavy" Entity, extracts the safe parts, puts them into a "Clean" DTO, and hands it back to the Controller.

```
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public UserResponseDTO getUserProfile(Long id) {
        // 1. Get the "Heavy" Entity from Database
        UserEntity user = userRepository.findById(id); 

        // 2. "Move" data to the Clean DTO (The Decoupling Step)
        // We only take what we need. The password stays in the Entity.
        UserResponseDTO cleanBox = new UserResponseDTO(
            user.getUsername(), 
            user.getEmail()
        );

        return cleanBox; // Send the clean box to the Controller
    }
}
```






---

## Spring Cloud
A set of tools for building **Microservices.**
It helps different small programs talk to each other safely.
It handles thing like configurations and service discovery in big systems.

---

## Data Structure

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


