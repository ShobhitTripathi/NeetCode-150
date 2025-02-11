# Sorting Techniques in Java

This document provides a comprehensive guide to various sorting techniques in Java, covering different data structures and scenarios.

## 1. Sorting Lists

### Ascending Order
```java
List<Integer> list = Arrays.asList(5, 2, 8, 1);
Collections.sort(list); // Ascending
```

### Descending Order
```java
list.sort(Comparator.reverseOrder()); // Descending
```

---

## 2. Sorting Arrays

### Ascending Order
```java
int[] arr = {5, 2, 8, 1};
Arrays.sort(arr);
```

### Custom Comparator
```java
Integer[] arr = {5, 2, 8, 1};
Arrays.sort(arr, Comparator.reverseOrder());
```

---

## 3. Sorting Maps by Keys

### Using TreeMap
```java
Map<String, Integer> map = new HashMap<>();
map.put("B", 2);
map.put("A", 3);
map.put("C", 1);
Map<String, Integer> sortedMap = new TreeMap<>(map);
```

---

## 4. Sorting Maps by Values

### Using Streams
```java
Map<String, Integer> map = new HashMap<>();
map.put("B", 2);
map.put("A", 3);
map.put("C", 1);

List<Map.Entry<String, Integer>> list = new ArrayList<>(map.entrySet());
list.sort(Map.Entry.comparingByValue());

Map<String, Integer> sortedByValue = new LinkedHashMap<>();
for (Map.Entry<String, Integer> entry : list) {
    sortedByValue.put(entry.getKey(), entry.getValue());
}
```

---

## 5. Sorting a Custom Object List

### Custom Comparator Example
```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

List<Person> people = Arrays.asList(new Person("Alice", 30), new Person("Bob", 25));
people.sort(Comparator.comparingInt(person -> person.age));
```

---

## 6. Sorting Sets

### Using TreeSet
```java
Set<Integer> set = new TreeSet<>(Arrays.asList(5, 2, 8, 1));
```

---

## 7. Sorting Multilevel Structures

### Sort Based on Multiple Criteria
```java
people.sort(Comparator.comparing(Person::getName).thenComparing(Person::getAge));
```

---

## 8. Parallel Sorting

### For Large Datasets
```java
int[] largeArray = {5, 2, 8, 1};
Arrays.parallelSort(largeArray);
```

---

## 9. Sorting Streams

### Example
```java
List<String> strings = Arrays.asList("Banana", "Apple", "Cherry");
List<String> sortedStrings = strings.stream().sorted().collect(Collectors.toList());
```

---

## 10. Sorting a Map with Streams

### Example
```java
Map<String, Integer> map = Map.of("A", 3, "B", 1, "C", 2);
Map<String, Integer> sortedMap = map.entrySet()
    .stream()
    .sorted(Map.Entry.comparingByValue())
    .collect(Collectors.toMap(
        Map.Entry::getKey,
        Map.Entry::getValue,
        (e1, e2) -> e1,
        LinkedHashMap::new
    ));
```

---

### Additional Notes
- Choose the appropriate sorting method depending on the data structure and requirements.
- For custom objects, always ensure proper implementation of comparators.
