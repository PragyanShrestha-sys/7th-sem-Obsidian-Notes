## Complete Example

### IDL (Calculator.idl) - THE CONTRACT
```idl
interface Calculator {
    long add(long a, long b);
};
```

### Java Implementation (Different from C++)
```java
public class CalculatorImpl extends CalculatorPOA {
    public int add(int a, int b) {
        // Java-specific code
        System.out.println("Java adding: " + a + " + " + b);
        return a + b;
    }
}
```

### C++ Implementation (Different from Java)
```cpp
class CalculatorImpl : public CalculatorPOA {
public:
    CORBA::Long add(CORBA::Long a, CORBA::Long b) {
        // C++-specific code
        cout << "C++ adding: " << a << " + " << b << endl;
        return a + b;
    }
};
```
