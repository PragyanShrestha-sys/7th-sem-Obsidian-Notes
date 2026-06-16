
| Feature | Array | ArrayList |
|---------|-------|-----------|
| **Size** | Fixed | Dynamic (grows/shrinks) |
| **Syntax** | `int[] arr` | `ArrayList<Integer> list` |
| **Add elements** | `arr[i] = value` | `list.add(value)` |
| **Remove elements** | Can't (without creating new array) | `list.remove(index)` |
| **Primitives** | ✅ Yes | ❌ No (need wrapper classes) |
| **Performance** | Faster | Slightly slower |
| **Length/Size** | `arr.length` (property) | `list.size()` (method) |

```java
// Array
int[] arr = new int[5];
arr[0] = 10;

// ArrayList
ArrayList<Integer> list = new ArrayList<>();
list.add(10);  // Automatically grows
```
