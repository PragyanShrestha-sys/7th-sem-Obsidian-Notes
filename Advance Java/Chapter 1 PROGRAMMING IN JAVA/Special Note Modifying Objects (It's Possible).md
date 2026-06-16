
While you can't change the **reference**, you CAN modify the **object's properties**:

```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}

Person[] people = {new Person("Alice"), new Person("Bob")};

// ✅ This works - modifies the object, not the reference
for (Person p : people) {
    p.name = p.name.toUpperCase();  // Changes the actual object
}
// Now names are "ALICE", "BOB"

// ❌ This doesn't work - trying to change the reference
for (Person p : people) {
    p = new Person("New");  // Only changes local variable
}
```
