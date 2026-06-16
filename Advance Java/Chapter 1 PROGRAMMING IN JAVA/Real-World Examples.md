
### Example 1: Student Grades

```java
public class GradeTracker {
    public static void main(String[] args) {
        String[] students = {"Alice", "Bob", "Charlie", "Diana"};
        int[] grades = {85, 92, 78, 96};
        
        // Calculate average
        int sum = 0;
        for (int grade : grades) {
            sum += grade;
        }
        double average = (double) sum / grades.length;
        
        // Find highest score
        int highest = grades[0];
        int highestIndex = 0;
        for (int i = 1; i < grades.length; i++) {
            if (grades[i] > highest) {
                highest = grades[i];
                highestIndex = i;
            }
        }
        
        System.out.println("Class average: " + average);
        System.out.println("Highest score: " + highest + 
                         " (" + students[highestIndex] + ")");
    }
}
```

### Example 2: Reverse Array

```java
public class ReverseArray {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        
        System.out.println("Original: " + Arrays.toString(arr));
        
        // Reverse in place
        for (int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - 1 - i];
            arr[arr.length - 1 - i] = temp;
        }
        
        System.out.println("Reversed: " + Arrays.toString(arr));
    }
}
```

### Example 3: Remove Duplicates (basic)

```java
public class RemoveDuplicates {
    public static void main(String[] args) {
        int[] arr = {1, 2, 2, 3, 4, 4, 5};
        
        // Simpler approach: use a boolean array to track seen numbers
        boolean[] seen = new boolean[100];  // Assume numbers 0-99
        
        System.out.print("Unique values: ");
        for (int num : arr) {
            if (!seen[num]) {
                System.out.print(num + " ");
                seen[num] = true;
            }
        }
    }
}
```

---
