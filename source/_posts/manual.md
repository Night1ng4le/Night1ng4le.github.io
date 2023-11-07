---
title: Manual Java & C++
categories: [API]
tags: [Java, C++, coding]
---

一个备忘手册（无视我）

<!--more-->

### Java

**HashMap**

```java
import java.util.HashMap; // import the HashMap class

HashMap<Key_type, Value_type> obj = new HashMap<Key_type, Value_type>(); // Create HashMap

obj.put(key, value); // Add Item

obj.get(key); // Access item, return its value

obj.remove(key); // Remove item

obj.clear(); // Remove all items

obj.size(); // Return size of hashtable

// Print keys
for (String i : obj.keySet()) {
  System.out.println(i);
}

// Print values
for (String i : obj.values()) {
  System.out.println(i);
}

// Print keys and values
for (String i : obj.keySet()) {
  System.out.println("key: " + i + " value: " + obj.get(i));
}
```

**HashSet**

```java

```

### C++

**vector**

```c++
// c++11
template < class T, class Alloc = allocator<T> > class vector; // generic template

T // value_type

Alloc // allocator_type

value_type& // reference

const value_type& //const reference

value_type* // pointer


vector<int> vec(size); //initialization

// return empty vector
return {}; // c++ 11
return vector<type>();

vec.push_back() //add new element after the last element
```

**map**

```c++
template < class Key,                                     // map::key_type
           class T,                                       // map::mapped_type
           class Compare = less<Key>,                     // map::key_compare
           class Alloc = allocator<pair<const Key,T> >    // map::allocator_type
           > class map;

map<key_type, value_type> map; // Definition

map.empty() // Test whether container is empty

map.size() // Return container size

map.insert() // Insert elements

map.erase() // Erase elements

map.find(key) // Return value 
```