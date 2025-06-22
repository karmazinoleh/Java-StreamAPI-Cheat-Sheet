# Java StreamAPI Cheat Sheet

### Content
**1. [Elements of StreamAPI](#elements-of-streamapi):**
- [forEach()](#foreach)
- [map()](#-map)
- [filter()](#-filter)
- [limit(n)](#-limitn)
- [skip()](#-skipn)
- [flatMap()](#-flatmap)
- [allMatch()](#-allmatch)
- [anyMatch()](#-anymatch)
- [noneMatch()](#-nonematch)
- [findFirst()](#%EF%B8%8F-findfirst)
- [findAny()](#-findany)
- [collect()](#-collect)
- [count()](#-count)
- [min/max(Comparator)](#%EF%B8%8F%EF%B8%8F-minmaxcomparator)
- [reduce()](#-reduce())
- [distinct()](#1%EF%B8%8F⃣-distinct)
- [sorted()](#EF%B8%8F-sorted)
  
**2. [Typical Patterns](#typical-patterns)**\
**3. [3-decision Rule](#3-decision-rule)**

## 🔁 Elements of StreamAPI
### forEach()
*Used for:*\
Go through the elements\
*Example:*\
```list.stream().forEach(System.out::println);```

### 🔂 map()
*Used for:*\
Convert elements\
*Example:*\
```list.stream().map(String::toUpperCase)```

### 🔍 filter()
*Used for:*\
Filter items\
*Example:*\
```list.stream().filter(s -> s.length() > 3)```

### ⬇️ limit(n)
*Used for:*\
Take the first N elements\
*Example:*\
```list.stream().limit(5)```

### 🛂 skip(n)
*Used for:*\
Skip the first N elements\
*Example:*\
```list.stream().skip(5)```

### 🧵 flatMap()
*Used for:*\
Expand nested lists\
*Example:*\
```listOfLists.stream().flatMap(List::stream)```

### ✅ allMatch()
*Used for:*\
Do all the elements satisfy the condition?\
*Example:*\
```stream.allMatch(x -> x > 0)```

### ❓ anyMatch()
*Used for:*\
Does at least one element satisfy the condition?\
*Example:*\
```stream.anyMatch(x -> x == 0)```

### ❌ noneMatch()
*Used for:*\
None of the elements satisfy the condition?\
*Example:*\
```stream.noneMatch(x -> x < 0)```

### ▶️ findFirst()
*Used for:*\
Return the first element\
*Example:*\
```stream.findFirst().orElse(null)```

### 🔙 findAny()
*Used for:*\
Return any item\
*Example:*\
```stream.findAny().orElse(null)```

### 📦 collect()
*Used for:*\
Add to the collection\
*Example:*
- To List
```stream.collect(Collectors.toList())```
- Grouping
```collect(Collectors.groupingBy(Person::getAge))```
- To Map
```collect(Collectors.toMap(User::getId, User::getName))```
- Count avarage
```collect(Collectors.averagingInt(User::getAge))```
- Sum
```collect(Collectors.summarizingInt(User::getAge))```
- Joining
```collect(Collectors.joining(", "))```

### 📊 count()
*Used for:*\
Calculate the amount\
*Example:*\
```stream.count()```

### ⬇️⬆️ min/max(Comparator)
*Used for:*\
Min/Max\
*Example:*\
```stream.max(Comparator.comparing(x -> x))```

### ➕ reduce()
*Used for:*\
Customizable reduction\
*Example:*\
```stream.reduce(0, Integer::sum)```\
```stream.reduce((a, b) -> a + b)```

### 1️⃣ distinct()
*Used for:*\
Unique values\
*Example:*\
```stream().distinct().count()```

### ↕️ sorted()
*Used for:*\
Sort\
*Example:
- ```stream.sorted()```
- Sort by field
```stream.sorted(Comparator.comparing(Person::getAge))```



## Typical Patterns
### Filter and Transform
```
List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```
### Count amount for elements
```
long count = list.stream().filter(x -> x > 10).count();
```
### Group by field
```
Map<Integer, List<Person>> peopleByAge =
    people.stream().collect(Collectors.groupingBy(Person::getAge));
```
### Search by condition
```
Optional<Person> found = people.stream()
    .filter(p -> p.getAge() > 30)
    .findAny(); // or findFirst()
```
### Search by condition
```
Optional<Person> found = people.stream()
    .filter(p -> p.getAge() > 30)
    .findAny(); // or findFirst()
    // .orElse(new Person("Unknown", 31));
```
### Sorting by field
```
List<Person> sorted = people.stream()
    .sorted(Comparator.comparing(Person::getAge))
    .collect(Collectors.toList());
```
### List to Map without collisions
```
Map<Integer, String> idToName = people.stream()
    .collect(Collectors.toMap(
    Person::getId,
    Person::getName,
    (existing, replacement) -> existing // merge-function
));
```
### flatMap for expanding nested lists
```
List<String> allTags = articles.stream()
    .flatMap(article -> article.getTags().stream())
    .distinct()
    .collect(Collectors.toList());
```

## 3-decision Rule
> A simple hint to help you understand which elements to use.
1. **What do I want to do with each element?**
   *[map()](#map), [filter()](#filter), [flatMap()](#flatMap)...?*
2. **What do I want to do with the collection as a whole?**
   *collect, reduce, count, min, max...?*
3. **What result do I need?**
   *List, Set, Map, Optional, String*...?
