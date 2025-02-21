# Sorting Techniques in Java

This README provides a detailed explanation of various sorting techniques in Java for different data structures and scenarios. It includes examples, explanations, and practical applications.

---

## Table of Contents

- [Sorting Arrays](#sorting-arrays)
  - [Ascending Order](#ascending-order)
  - [Descending Order](#descending-order)
- [Sorting Lists](#sorting-lists)
  - [Sorting a List of Integers](#sorting-a-list-of-integers)
  - [Sorting a List of Custom Objects](#sorting-a-list-of-custom-objects)
- [Sorting Maps](#sorting-maps)
  - [Sort a Map by Keys](#sort-a-map-by-keys)
  - [Sort a Map by Values](#sort-a-map-by-values)
- [Sorting Scenarios](#sorting-scenarios)
  - [Sort an Array Based on Another Array](#sort-an-array-based-on-another-array)
  - [Sort an Index Array Based on Values](#sort-an-index-array-based-on-values)

---

## Sorting Arrays

### Ascending Order
```java
import java.util.Arrays;

public class AscendingSort {
    public static void main(String[] args) {
        int[] array = {5, 2, 8, 1, 3};
        Arrays.sort(array);
        System.out.println("Sorted array in ascending order: " + Arrays.toString(array));
    }
}
```

### Descending Order
```java
import java.util.Arrays;
import java.util.Collections;

public class DescendingSort {
    public static void main(String[] args) {
        Integer[] array = {5, 2, 8, 1, 3};
        Arrays.sort(array, Collections.reverseOrder());
        System.out.println("Sorted array in descending order: " + Arrays.toString(array));
    }
}
```

---

## Sorting Lists

### Sorting a List of Integers
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class SortList {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(5);
        list.add(2);
        list.add(8);
        list.add(1);
        list.add(3);

        Collections.sort(list);
        System.out.println("Sorted list in ascending order: " + list);

        Collections.sort(list, Collections.reverseOrder());
        System.out.println("Sorted list in descending order: " + list);
    }
}
```

### Sorting a List of Custom Objects
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class SortCustomObjects {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 20));
        students.add(new Student("Charlie", 21));

        // Sort by age
        students.sort(Comparator.comparingInt(s -> s.age));
        System.out.println("Sorted by age: " + students);

        // Sort by name
        students.sort(Comparator.comparing(s -> s.name));
        System.out.println("Sorted by name: " + students);
    }
}
```

---

## Sorting Maps

### Sort a Map by Keys
```java
import java.util.Map;
import java.util.TreeMap;

public class SortMapByKeys {
    public static void main(String[] args) {
        Map<String, Integer> map = Map.of("Banana", 2, "Apple", 3, "Cherry", 1);

        // Sort by keys using TreeMap
        Map<String, Integer> sortedMap = new TreeMap<>(map);
        System.out.println("Map sorted by keys: " + sortedMap);
    }
}
```

### Sort a Map by Values
```java
import java.util.*;

public class SortMapByValues {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Banana", 2);
        map.put("Apple", 3);
        map.put("Cherry", 1);

        // Sort by values
        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());
        entries.sort(Map.Entry.comparingByValue());

        // LinkedHashMap to maintain order
        Map<String, Integer> sortedMap = new LinkedHashMap<>();
        for (Map.Entry<String, Integer> entry : entries) {
            sortedMap.put(entry.getKey(), entry.getValue());
        }

        System.out.println("Map sorted by values: " + sortedMap);
    }
}
```

### Sort map by values descending order
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Banana", 2);
        map.put("Apple", 3);
        map.put("Cherry", 1);

        // Sort by values in descending order
        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());
        entries.sort(Map.Entry.comparingByValue(Comparator.reverseOrder()));

        // LinkedHashMap to maintain order
        Map<String, Integer> sortedMap = new LinkedHashMap<>();
        for (Map.Entry<String, Integer> entry : entries) {
            sortedMap.put(entry.getKey(), entry.getValue());
        }

        System.out.println("Map sorted by values in descending order: " + sortedMap);
    }
}
```

---

## Sorting Scenarios

### Sort an Array Based on Another Array
```java
import java.util.Arrays;

public class SortArrayBasedOnAnother {
    public static void main(String[] args) {
        int[] array1 = {5, 8, 1, 3, 7};
        int[] array2 = {2, 0, 4};

        // Sort array2 based on values in array1
        Integer[] indices = Arrays.stream(array2).boxed().toArray(Integer[]::new);
        Arrays.sort(indices, (a, b) -> Integer.compare(array1[a], array1[b]));

        // Print the sorted array2
        int[] sortedArray2 = Arrays.stream(indices).mapToInt(i -> array2[i]).toArray();
        System.out.println("Sorted array2: " + Arrays.toString(sortedArray2));
    }
}
```

### Sort an Index Array Based on Values
```java
import java.util.Arrays;

public class SortIndexArray {
    public static void main(String[] args) {
        int[] array1 = {7, 8, 5, 4, 3, 1};
        int[] indexArray = {0, 1};

        // Create a helper array of pairs (index, value)
        int[][] pairs = new int[indexArray.length][2];
        for (int i = 0; i < indexArray.length; i++) {
            pairs[i][0] = indexArray[i]; // Index
            pairs[i][1] = array1[indexArray[i]]; // Value at index
        }

        // Sort pairs based on values (descending order)
        Arrays.sort(pairs, (a, b) -> Integer.compare(b[1], a[1]));

        // Extract sorted indices back to indexArray
        for (int i = 0; i < pairs.length; i++) {
            indexArray[i] = pairs[i][0];
        }

        // Print the sorted index array
        System.out.println("Sorted index array: " + Arrays.toString(indexArray));

        // Print the corresponding values from array1 in descending order
        System.out.println("Values in sorted order: " + Arrays.toString(
            Arrays.stream(indexArray).map(i -> array1[i]).toArray()
        ));
    }
}
```

---

## Contributing
Feel free to submit pull requests or open issues to add more sorting techniques or use cases.

---

## License
This project is licensed under the MIT License.
