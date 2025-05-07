# Java Streams

## Overview
Java Streams provide a modern, functional-style way to process sequences of data. They enable operations like filtering, mapping, reducing, and collecting without modifying the underlying data source.

Streams are not data structures but **pipelines** of operations.

---

## Stream Characteristics
- **Lazy evaluation:** Operations are only executed when a terminal operation is called.
- **Parallelizable:** Can be easily parallelized for performance.
- **Immutable source:** Streams do not change the original data.

---

## Creating Streams
```java
import java.util.*;
import java.util.stream.*;

// From a collection
List<String> list = Arrays.asList("apple", "banana", "cherry");
Stream<String> stream = list.stream();

// From an array
Stream<Integer> arrayStream = Arrays.stream(new Integer[]{1, 2, 3});

// Using Stream.of()
Stream<String> directStream = Stream.of("A", "B", "C");

// Infinite stream (limit required)
Stream<Double> randoms = Stream.generate(Math::random).limit(5);
```

---

## Stream Operations

### Intermediate Operations (lazy)
- `.filter()` → filters elements
- `.map()` → transforms each element
- `.distinct()` → removes duplicates
- `.sorted()` → sorts elements
- `.peek()` → performs an action (for debugging)
- `.limit()`, `.skip()` → limit or skip elements

### Terminal Operations (trigger execution)
- `.forEach()` → performs an action on each element
- `.collect()` → gathers results into a collection or string
- `.reduce()` → reduces elements to a single result
- `.count()` → counts elements
- `.anyMatch()`, `.allMatch()`, `.noneMatch()` → match predicates
- `.findFirst()`, `.findAny()` → find elements

---

## Examples

### Filter and print
```java
list.stream()
    .filter(s -> s.startsWith("a"))
    .forEach(System.out::println);
```

### Map and collect
```java
List<Integer> lengths = list.stream()
    .map(String::length)
    .collect(Collectors.toList());
```

### Reduce
```java
int sum = Arrays.asList(1, 2, 3, 4)
    .stream()
    .reduce(0, Integer::sum);
```

### Parallel Stream
```java
list.parallelStream()
    .forEach(System.out::println);
```

---

## Collectors
- `Collectors.toList()` → collect to list
- `Collectors.toSet()` → collect to set
- `Collectors.joining(", ")` → join elements into string
- `Collectors.groupingBy()` → group by classifier
- `Collectors.partitioningBy()` → partition by predicate

Example:
```java
Map<Integer, List<String>> grouped = list.stream()
    .collect(Collectors.groupingBy(String::length));
```

---

## Best Practices
- Avoid modifying source inside streams (no side effects).
- Use parallel streams only when necessary.
- Keep stream operations simple and readable.
- Remember: streams can only be used once.

---

## Summary
| Feature                | Description                                    |
|------------------------|------------------------------------------------|
| **Stream Source**      | Collection, array, generator                  |
| **Intermediate Ops**   | filter, map, sorted, distinct, peek, limit    |
| **Terminal Ops**       | forEach, collect, reduce, count, match, find  |
| **Parallel Streams**   | For performance with multi-core processors    |
| **Collectors**         | toList, toSet, joining, groupingBy, partitioningBy |

Let me know if you want additional examples, diagrams, or practice tasks!
