## Features of Object-Oriented Programming (OOP)

### 4 Main Pillars of OOP

| Feature | Description | Example |
|---------|-------------|---------|
| **Encapsulation** | Bundling data and methods together, hiding internal details | Private variables, public getters/setters |
| **Inheritance** | Creating new classes from existing ones | Child class extends Parent class |
| **Polymorphism** | Same method name, different behaviors | Method overloading, overriding |
| **Abstraction** | Hiding complex implementation, showing only essentials | Abstract classes, interfaces |

### Additional Features
- **Classes & Objects**: Blueprint and instances
- **Modularity**: Breaking code into reusable pieces
- **Code Reusability**: DRY principle
- **Data Hiding**: Using access modifiers (private, protected)

---

## Shortest Version

```java
class Distance {
    private int ft;
    private float in;
    
    Distance(int f, float i) { ft = f; in = i; if(in>=12){ft+=in/12; in%=12;} }
    
    Distance add(Distance d) { return new Distance(ft+d.ft, in+d.in); }
    
    int compare(Distance d) {
        float t = ft*12+in, o = d.ft*12+d.in;
        return t > o ? 1 : t < o ? -1 : 0;
    }
    
    void display() { System.out.println(ft + "ft " + in + "in"); }
}

public class Main {
    public static void main(String[] args) {
        Distance d1 = new Distance(5, 8.5f);
        Distance d2 = new Distance(3, 10f);
        d1.display();
        d2.display();
        d1.add(d2).display();
        System.out.println(d1.compare(d2));
    }
}
```

---

## Key OOP Features in This Code

| OOP Feature | How It's Used |
|-------------|---------------|
| **Encapsulation** | `feet` and `inches` are `private` |
| **Abstraction** | `normalize()` is private, hidden from user |
| **Constructor** | `Distance(int, float)` creates objects |
| **Method Overloading** | Default + Parameterized constructors |
| **Object Passing** | `add(Distance d)` receives object |
| **Returning Objects** | `add()` returns a new Distance object |
| **Data Hiding** | Private fields, public methods |

---
