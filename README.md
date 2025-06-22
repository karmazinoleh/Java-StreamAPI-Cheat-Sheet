### Java StreamAPI Cheat Sheet

## Content
1. [Elements of StreamAPI](#elements-of-streamapi)
2. [Typical Patterns](#typical-patterns)
3. [3-decision Rule](#3-decision-rule)

## Elements of StreamAPI
# forEach()
*Used for:*
> Go through the elements 🔁
*Example:*
```list.stream().forEach(System.out::println);```

# map()
*Used for:*
> Convert elements 📦
*Example:*
```list.stream().map(String::toUpperCase)```

# filter()
*Used for:*
> Filter items 🔍
*Example:*
```list.stream().filter(s -> s.length() > 3)```

# limit(n)
*Used for:*
> Take the first N elements ⬇️
*Example:*
```list.stream().limit(5)```

# skip(n)
*Used for:*
> Skip the first N elements 🛂
*Example:*
```list.stream().skip(5)```

# flatMap()
*Used for:*
> Expand nested lists 🧵
*Example:*
```listOfLists.stream().flatMap(List::stream)```

# allMatch()
*Used for:*
> Do all the elements satisfy the condition? ✅
*Example:*
```stream.allMatch(x -> x > 0)```

# anyMatch()
*Used for:*
> Does at least one element satisfy the condition? ❓
*Example:*
```stream.anyMatch(x -> x == 0)```

# noneMatch()
*Used for:*
> None of the elements satisfy the condition? ❌ 
*Example:*
```stream.noneMatch(x -> x < 0)```

# findFirst()
*Used for:*
> Return the first element ▶️
*Example:*
```stream.findFirst().orElse(null)```

# findAny()
*Used for:*
> Return any item 🔙
*Example:*
```stream.findAny().orElse(null)```

# collect()
*Used for:*
> Add to the collection 📦
*Example:*
```stream.collect(Collectors.toList())```

# count()
*Used for:*
> Calculate the amount 📊
*Example:*
```stream.count()```

# min/max(Comparator)
*Used for:*
> Min/Max ⬇️⬆️
*Example:*
```stream.max(Comparator.comparing(x -> x))```

# reduce()
*Used for:*
> Customizable reduction ➕
*Example:*
```stream.reduce(0, Integer::sum)```
```stream.reduce((a, b) -> a + b);```

## Typical Patterns
# Search for an object by condition

## 3-decision Rule
> A simple hint to help you understand which elements to use.
1. **What do I want to do with each element?**
   *[map()](#map), [filter()](#filter), [flatMap()](#flatMap)...?*
2. **What do I want to do with the collection as a whole?**
   *collect, reduce, count, min, max...?*
3. **What result do I need?**
   *List, Set, Map, Optional, String*...?
