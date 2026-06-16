Here's a **simple introduction** to reading and writing objects in Java (Serialization).

---

## What is Serialization?

**Serialization** = Saving an object to a file (converting object to bytes)

**Deserialization** = Reading an object from a file (converting bytes back to object)

```
Object in memory → Serialize → File on disk
File on disk → Deserialize → Object in memory
```

---

## The Magic Words

| Keyword | What it does |
|---------|--------------|
| `implements Serializable` | Marks a class as "save-able" |
| `ObjectOutputStream` | Writes objects to file |
| `ObjectInputStream` | Reads objects from file |

---

## Simplest Example

```java
import java.io.*;

// Step 1: Make your class Serializable
class Person implements Serializable {
    String name;
    int age;
}

public class SimpleSerialization {
    public static void main(String[] args) {
        
        // Step 2: Create an object
        Person p = new Person();
        p.name = "Alice";
        p.age = 25;
        
        // Step 3: Save object to file (SERIALIZE)
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream("person.dat"))) {
            
            out.writeObject(p);
            System.out.println("Object saved!");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Step 4: Read object from file (DESERIALIZE)
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream("person.dat"))) {
            
            Person savedPerson = (Person) in.readObject();
            System.out.println("Name: " + savedPerson.name);
            System.out.println("Age: " + savedPerson.age);
            
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Object saved!
Name: Alice
Age: 25
```

---

## Complete Example: Game Save System

```java
import java.io.*;

// Make your class serializable
class Player implements Serializable {
    String name;
    int level;
    int score;
    
    public Player(String name, int level, int score) {
        this.name = name;
        this.level = level;
        this.score = score;
    }
    
    void display() {
        System.out.println("Player: " + name);
        System.out.println("Level: " + level);
        System.out.println("Score: " + score);
    }
}

public class GameSave {
    
    // Save game
    public static void saveGame(Player p, String filename) {
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream(filename))) {
            
            out.writeObject(p);
            System.out.println("Game saved!");
            
        } catch (IOException e) {
            System.out.println("Save failed: " + e.getMessage());
        }
    }
    
    // Load game
    public static Player loadGame(String filename) {
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream(filename))) {
            
            Player p = (Player) in.readObject();
            System.out.println("Game loaded!");
            return p;
            
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Load failed: " + e.getMessage());
            return null;
        }
    }
    
    public static void main(String[] args) {
        
        // Create player
        Player player = new Player("Hero", 5, 1250);
        
        System.out.println("=== BEFORE SAVE ===");
        player.display();
        
        // Save to file
        saveGame(player, "savegame.dat");
        
        // Modify original
        player.level = 99;
        player.score = 99999;
        
        System.out.println("\n=== MODIFIED (not saved) ===");
        player.display();
        
        // Load from file (restores original state)
        Player loaded = loadGame("savegame.dat");
        
        System.out.println("\n=== AFTER LOAD ===");
        loaded.display();
    }
}
```

**Output:**
```
=== BEFORE SAVE ===
Player: Hero
Level: 5
Score: 1250
Game saved!

=== MODIFIED (not saved) ===
Player: Hero
Level: 99
Score: 99999

Game loaded!

=== AFTER LOAD ===
Player: Hero
Level: 5
Score: 1250
```

---

## The `transient` Keyword

**`transient`** = Don't save this field (skip it)

```java
class User implements Serializable {
    String username;
    transient String password;  // Won't be saved to file
    
    User(String username, String password) {
        this.username = username;
        this.password = password;
    }
}

// When you save and load:
// - username is saved and restored
// - password is NOT saved (will be null after loading)
```

**Why use `transient`?**
- Passwords (security)
- Fields that can be recalculated
- Temporary data
- Large fields you don't need to save

---

## Multiple Objects in One File

```java
import java.io.*;
import java.util.*;

class Student implements Serializable {
    String name;
    int id;
    
    Student(String name, int id) {
        this.name = name;
        this.id = id;
    }
    
    void display() {
        System.out.println(id + ": " + name);
    }
}

public class MultipleObjects {
    public static void main(String[] args) {
        
        // Create list of objects
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 1));
        students.add(new Student("Bob", 2));
        students.add(new Student("Charlie", 3));
        
        // Save entire list
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream("students.dat"))) {
            
            out.writeObject(students);
            System.out.println("All students saved!");
            
        } catch (IOException e) {
            System.out.println("Save error: " + e.getMessage());
        }
        
        // Load entire list
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream("students.dat"))) {
            
            ArrayList<Student> loaded = (ArrayList<Student>) in.readObject();
            
            System.out.println("\nLoaded students:");
            for (Student s : loaded) {
                s.display();
            }
            
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Load error: " + e.getMessage());
        }
    }
}
```

---

## Quick Reference

```java
// SAVING an object
try (ObjectOutputStream out = new ObjectOutputStream(
        new FileOutputStream("file.dat"))) {
    out.writeObject(myObject);
}

// LOADING an object
try (ObjectInputStream in = new ObjectInputStream(
        new FileInputStream("file.dat"))) {
    MyObject obj = (MyObject) in.readObject();
}

// Class must implement Serializable
class MyObject implements Serializable {
    // fields
}
```

---

## Common Mistakes

```java
// ❌ ERROR: Class doesn't implement Serializable
class Person {  // Missing "implements Serializable"
    String name;
}

// ✅ CORRECT
class Person implements Serializable {
    String name;
}

// ❌ ERROR: Trying to save non-serializable object
ObjectOutputStream out = new ObjectOutputStream(...);
out.writeObject(new Scanner(System.in));  // Scanner not serializable!

// ✅ OK: Only save your own objects that implement Serializable
```

---

## When to Use Object I/O

| Use Case | Example |
|----------|---------|
| **Game saves** | Save player progress |
| **User preferences** | Save settings |
| **Application state** | Save what user was doing |
| **Cache data** | Save计算结果 for later |
| **Configuration** | Save object-based config |

---

## The Golden Rule

> **To save an object to a file: (1) Make class `implements Serializable`, (2) Use `ObjectOutputStream.writeObject()`. To load it back: use `ObjectInputStream.readObject()`.**

**Memory trick:**
```
Serializable = "I am save-able"
ObjectOutputStream = "Out goes the object" (save)
ObjectInputStream = "In comes the object" (load)
transient = "Don't save this field"
```

Would you like me to explain **version control with `serialVersionUID`** or **custom serialization** next?