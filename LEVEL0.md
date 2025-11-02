# Level 0 Exam 05 - Complete Reference Guide

## Table of Contents
1. [VECT2 - Complete Implementation Guide](#vect2---complete-implementation-guide)
2. [BIGINT - Complete Implementation Guide](#bigint---complete-implementation-guide)
3. [POLYSET - Complete Breakdown](#polyset---complete-breakdown)
4. [Difficulty Legend](#difficulty-legend)
5. [Implementation Priority Order](#implementation-priority-order)
6. [Time Estimates](#time-estimates)

---

## **VECT2 - Complete Implementation Guide**

| **Operator** | **Signature** | **What It Does** | **Difficulty** | **Implementation Notes** |
|--------------|---------------|------------------|----------------|--------------------------|
| **Constructors & Basic** |
| Default constructor | `vect2()` | Creates (0, 0) | ⭐ Easy | `x = 0; y = 0;` |
| Parameterized constructor | `vect2(int x, int y)` | Creates (x, y) | ⭐ Easy | `this->x = x; this->y = y;` |
| Copy constructor | `vect2(const vect2& other)` | Copies another vect2 | ⭐ Easy | `*this = other;` |
| Assignment | `vect2& operator=(const vect2& other)` | Assigns one to another | ⭐ Easy | Check self-assignment, copy x and y |
| Destructor | `~vect2()` | Cleanup | ⭐ Easy | Nothing to do (no dynamic memory) |
| **Array Access** |
| Subscript (const) | `int operator[](int index) const` | Read component (0=x, 1=y) | ⭐ Easy | Return x if index==0, else y |
| Subscript (non-const) | `int& operator[](int index)` | Modify component | ⭐ Easy | Return reference to x or y |
| **Binary Arithmetic** |
| Addition | `vect2 operator+(const vect2& other) const` | Component-wise addition | ⭐ Easy | Return new vect2(x+other.x, y+other.y) |
| Subtraction | `vect2 operator-(const vect2& other) const` | Component-wise subtraction | ⭐ Easy | Return new vect2(x-other.x, y-other.y) |
| Multiplication (vector) | `vect2 operator*(const vect2& other) const` | Component-wise multiplication | ⭐ Easy | Return new vect2(x*other.x, y*other.y) |
| Multiplication (scalar) | `vect2 operator*(int scalar) const` | Scale vector by number | ⭐ Easy | Return new vect2(x*scalar, y*scalar) |
| **Compound Assignment** |
| Add-assign | `vect2& operator+=(const vect2& other)` | Add and modify self | ⭐ Easy | `x += other.x; y += other.y; return *this;` |
| Subtract-assign | `vect2& operator-=(const vect2& other)` | Subtract and modify self | ⭐ Easy | `x -= other.x; y -= other.y; return *this;` |
| Multiply-assign (vector) | `vect2& operator*=(const vect2& other)` | Multiply and modify self | ⭐ Easy | `x *= other.x; y *= other.y; return *this;` |
| Multiply-assign (scalar) | `vect2& operator*=(int scalar)` | Scale and modify self | ⭐ Easy | `x *= scalar; y *= scalar; return *this;` |
| **Unary Operators** |
| Unary minus | `vect2 operator-() const` | Negate both components | ⭐ Easy | Return vect2(-x, -y) |
| **Increment/Decrement** |
| Pre-increment | `vect2& operator++()` | ++both, return new value | ⭐⭐ Medium | `++x; ++y; return *this;` |
| Post-increment | `vect2 operator++(int)` | Save old, ++both, return old | ⭐⭐ Medium | Save copy, call pre-inc, return copy |
| Pre-decrement | `vect2& operator--()` | --both, return new value | ⭐⭐ Medium | `--x; --y; return *this;` |
| Post-decrement | `vect2 operator--(int)` | Save old, --both, return old | ⭐⭐ Medium | Save copy, call pre-dec, return copy |
| **Comparison** |
| Equality | `bool operator==(const vect2& other) const` | Check if both components equal | ⭐ Easy | `return x==other.x && y==other.y;` |
| Inequality | `bool operator!=(const vect2& other) const` | Check if different | ⭐ Easy | `return !(*this == other);` |
| **Non-Member Functions** |
| Reversed scalar multiply | `vect2 operator*(int scalar, const vect2& v)` | Scale: int * vect2 | ⭐ Easy | `return v * scalar;` (reuse member version) |
| Stream output | `std::ostream& operator<<(std::ostream& os, const vect2& v)` | Print as {x, y} | ⭐ Easy | `os << "{" << v[0] << ", " << v[1] << "}";` |

**Total for vect2: 26 functions** (24 member + 2 non-member)

---

## **BIGINT - Complete Implementation Guide**

| **Operator** | **Signature** | **What It Does** | **Difficulty** | **Implementation Notes** |
|--------------|---------------|------------------|----------------|--------------------------|
| **Constructors & Basic** |
| Default constructor | `bigint()` | Creates "0" | ⭐ Easy | `str = "0";` |
| Int constructor | `bigint(unsigned int num)` | Convert int to string | ⭐⭐ Medium | Use stringstream to convert |
| Copy constructor | `bigint(const bigint& other)` | Copy string | ⭐ Easy | `*this = other;` |
| Assignment | `bigint& operator=(const bigint& other)` | Assign string | ⭐ Easy | Check self-assignment, copy str |
| Getter | `std::string getStr() const` | Return string representation | ⭐ Easy | `return str;` |
| **Addition** |
| Addition | `bigint operator+(const bigint& other) const` | Add two big numbers | ⭐⭐⭐ Hard | Digit-by-digit addition with carry |
| Add-assign | `bigint& operator+=(const bigint& other)` | Add and modify self | ⭐ Easy | `*this = *this + other; return *this;` |
| **Increment** |
| Pre-increment | `bigint& operator++()` | Add 1, return new value | ⭐ Easy | `*this = *this + bigint(1); return *this;` |
| Post-increment | `bigint operator++(int)` | Save old, add 1, return old | ⭐⭐ Medium | Save copy, call pre-inc, return copy |
| **Left Shift (×10^n)** |
| Left shift (int) | `bigint operator<<(unsigned int n) const` | Multiply by 10^n (append zeros) | ⭐⭐ Medium | Insert n zeros at end of string |
| Left shift (bigint) | `bigint operator<<(const bigint& other) const` | Shift by bigint amount | ⭐⭐ Medium | Convert bigint to uint, call int version |
| Left shift-assign (int) | `bigint& operator<<=(unsigned int n)` | Shift and modify self | ⭐ Easy | `*this = *this << n; return *this;` |
| Left shift-assign (bigint) | `bigint& operator<<=(const bigint& other)` | Shift by bigint and modify | ⭐ Easy | `*this = *this << other; return *this;` |
| **Right Shift (÷10^n)** |
| Right shift (int) | `bigint operator>>(unsigned int n) const` | Divide by 10^n (remove digits) | ⭐⭐ Medium | Erase last n digits from string |
| Right shift (bigint) | `bigint operator>>(const bigint& other) const` | Shift by bigint amount | ⭐⭐ Medium | Convert bigint to uint, call int version |
| Right shift-assign (int) | `bigint& operator>>=(unsigned int n)` | Shift and modify self | ⭐ Easy | `*this = *this >> n; return *this;` |
| Right shift-assign (bigint) | `bigint& operator>>=(const bigint& other)` | Shift by bigint and modify | ⭐ Easy | `*this = *this >> other; return *this;` |
| **Comparison** |
| Equality | `bool operator==(const bigint& other) const` | Check if equal | ⭐ Easy | `return str == other.str;` |
| Inequality | `bool operator!=(const bigint& other) const` | Check if different | ⭐ Easy | `return !(*this == other);` |
| Less than | `bool operator<(const bigint& other) const` | Check if smaller | ⭐⭐⭐ Hard | Compare length first, then lexicographic |
| Greater than | `bool operator>(const bigint& other) const` | Check if larger | ⭐⭐ Medium | `return !(*this < other \|\| *this == other);` |
| Less or equal | `bool operator<=(const bigint& other) const` | Check if smaller/equal | ⭐ Easy | `return *this < other \|\| *this == other;` |
| Greater or equal | `bool operator>=(const bigint& other) const` | Check if larger/equal | ⭐ Easy | `return *this > other \|\| *this == other;` |
| **Non-Member Functions** |
| Stream output | `std::ostream& operator<<(std::ostream& os, const bigint& obj)` | Print number | ⭐ Easy | `os << obj.getStr();` |
| **Helper Functions** |
| String reversal | `std::string reverse(const std::string& s)` | Reverse a string | ⭐ Easy | Loop backwards, build new string |
| String to uint | `unsigned int stringToUInt(const std::string& s)` | Convert string to uint | ⭐ Easy | Use stringstream |
| Addition helper | `std::string addition(const bigint& a, const bigint& b)` | Digit-by-digit addition | ⭐⭐⭐ Hard | Core addition algorithm with carry |

**Total for bigint: 26 functions** (23 member + 3 non-member/helper)

---

## **POLYSET - Complete Breakdown**

### **Understanding the Exercise**

#### **What You're Given:**

You receive 4 base classes:

1. **`bag`** - Abstract interface (pure virtual functions)
   - Can insert elements
   - Can print all elements
   - Can clear all elements
   - **Allows duplicates** (like a multiset)

2. **`searchable_bag`** - Abstract interface extending bag
   - Adds search capability: `has(int value)`
   - Still abstract (pure virtual function)

3. **`array_bag`** - Concrete implementation of bag
   - Uses dynamic array (`int* data`, `int size`)
   - Implements insert, print, clear
   - **Already fully implemented and working**

4. **`tree_bag`** - Concrete implementation of bag
   - Uses binary search tree (`node* tree`)
   - Implements insert, print, clear
   - **Already fully implemented and working**

#### **What You Must Implement:**

You need to create **6 files** total:

**Part 1: Searchable Implementations (4 files)**
1. `searchable_array_bag.hpp` + `searchable_array_bag.cpp`
2. `searchable_tree_bag.hpp` + `searchable_tree_bag.cpp`

**Part 2: Set Wrapper (2 files)**
3. `set.hpp` + `set.cpp`

---

### **The Diamond Problem & Virtual Inheritance**

```
         bag (abstract)
         /          \
        /            \
   array_bag      searchable_bag (abstract)
        \            /
         \          /
    searchable_array_bag
```

This is a **diamond inheritance** pattern. Without `virtual` inheritance, `searchable_array_bag` would have **TWO copies** of `bag`!

**Solution:** Both `array_bag` and `searchable_bag` use `virtual public bag`

```cpp
class array_bag : virtual public bag { ... };
class searchable_bag : virtual public bag { ... };
```

This ensures only **ONE** `bag` base class exists in `searchable_array_bag`.

---

### **Part 1: Searchable Classes**

#### **searchable_array_bag**

| **Function** | **Signature** | **What It Does** | **Difficulty** | **Implementation** |
|--------------|---------------|------------------|----------------|--------------------|
| Default constructor | `searchable_array_bag()` | Initialize empty | ⭐ Easy | Call parent constructors (implicit) |
| Copy constructor | `searchable_array_bag(const searchable_array_bag& src)` | Deep copy | ⭐⭐ Medium | Call `array_bag(src)` in initializer list |
| Assignment | `searchable_array_bag& operator=(const searchable_array_bag& src)` | Copy assign | ⭐⭐ Medium | Check self-assignment, call `array_bag::operator=` |
| Has function | `bool has(int value) const` | Search for value | ⭐⭐ Medium | Linear search through `data` array |
| Destructor | `~searchable_array_bag()` | Cleanup | ⭐ Easy | Nothing needed (parent handles it) |

**Key Challenge:** Accessing protected members `data` and `size` from `array_bag`

```cpp
bool searchable_array_bag::has(int value) const {
    for (int i = 0; i < size; i++) {  // size is from array_bag
        if (data[i] == value)         // data is from array_bag
            return true;
    }
    return false;
}
```

---

#### **searchable_tree_bag**

| **Function** | **Signature** | **What It Does** | **Difficulty** | **Implementation** |
|--------------|---------------|------------------|----------------|--------------------|
| Default constructor | `searchable_tree_bag()` | Initialize empty | ⭐ Easy | Call parent constructors (implicit) |
| Copy constructor | `searchable_tree_bag(const searchable_tree_bag& src)` | Deep copy tree | ⭐⭐ Medium | Call `tree_bag(src)` in initializer list |
| Assignment | `searchable_tree_bag& operator=(const searchable_tree_bag& src)` | Copy assign | ⭐⭐ Medium | Check self-assignment, call `tree_bag::operator=` |
| Has function | `bool has(int value) const` | Search BST | ⭐⭐⭐ Hard | Recursive BST search |
| Helper search | `bool search(node* n, int value) const` | Recursive search helper | ⭐⭐⭐ Hard | Navigate BST: left if <, right if >, found if == |
| Destructor | `~searchable_tree_bag()` | Cleanup | ⭐ Easy | Nothing needed (parent handles it) |

**Key Challenge:** Implementing recursive BST search

```cpp
// Private helper function
bool searchable_tree_bag::search(node* current, int value) const {
    if (current == nullptr)
        return false;                          // Not found
    
    if (current->value == value)
        return true;                           // Found!
    
    if (value < current->value)
        return search(current->l, value);      // Search left subtree
    else
        return search(current->r, value);      // Search right subtree
}

// Public interface
bool searchable_tree_bag::has(int value) const {
    return search(tree, value);  // tree is from tree_bag
}
```

---

### **Part 2: Set Wrapper**

#### **The Concept:**

A **set** is like a **bag**, but **NO DUPLICATES** allowed!

You wrap a `searchable_bag` and check before inserting.

---

#### **set Class**

| **Function** | **Signature** | **What It Does** | **Difficulty** | **Implementation** |
|--------------|---------------|------------------|----------------|--------------------|
| Constructor | `set(searchable_bag& sb)` | Wrap a searchable_bag | ⭐⭐ Medium | Store reference, initialize in initializer list |
| Has function | `bool has(int value) const` | Check if exists | ⭐ Easy | Delegate to `bag.has(value)` |
| Insert single | `void insert(int value)` | Insert if not exists | ⭐⭐ Medium | Check `has()` first, then insert |
| Insert array | `void insert(int* arr, int count)` | Insert multiple | ⭐⭐ Medium | Loop and call single insert |
| Print | `void print() const` | Print all elements | ⭐ Easy | Delegate to `bag.print()` |
| Clear | `void clear()` | Remove all | ⭐ Easy | Delegate to `bag.clear()` |
| Get bag | `const searchable_bag& get_bag()` | Return wrapped bag | ⭐ Easy | `return bag;` |
| Destructor | `~set()` | Cleanup | ⭐ Easy | Nothing needed (reference, not owned) |
| Copy constructor | `set(const set&) = delete` | Prevent copying | ⭐ Easy | Use `= delete` |
| Assignment | `set& operator=(const set&) = delete` | Prevent assignment | ⭐ Easy | Use `= delete` |
| Default constructor | `set() = delete` | Prevent default construction | ⭐ Easy | Use `= delete` |

---

### **Key Challenge: Reference Member Variable**

**The Critical Part:**

```cpp
class set {
private:
    searchable_bag& bag;  // REFERENCE! Not a pointer, not a copy
    
public:
    set(searchable_bag& sb) : bag(sb) { }  // MUST use initializer list!
    // Cannot do: bag = sb; in constructor body (references can't be reassigned)
};
```

**Why References?**
- The set doesn't OWN the bag, it just USES it
- Changes to set affect the original bag
- No memory management needed

---

### **Why Delete Copy/Assignment?**

```cpp
set(const set&) = delete;              // No copy constructor
set& operator=(const set&) = delete;    // No assignment
set() = delete;                         // No default constructor
```

**Reasons:**
1. Reference members can't be reseated (changed to refer to different objects)
2. No default constructor because a set MUST wrap something
3. Copying is problematic with reference members

---

### **Complete Implementation Difficulty Table**

#### **searchable_array_bag.hpp & .cpp**

| **Component** | **Difficulty** | **Time** | **Key Point** |
|---------------|----------------|----------|---------------|
| Header guards & includes | ⭐ Easy | 1 min | `#pragma once`, include both parents |
| Class declaration | ⭐⭐ Medium | 2 min | Multiple inheritance syntax |
| Constructors | ⭐ Easy | 3 min | Can be empty bodies |
| Copy constructor | ⭐⭐ Medium | 5 min | Call parent in initializer list |
| Assignment operator | ⭐⭐ Medium | 5 min | Call `array_bag::operator=` |
| `has()` function | ⭐⭐ Medium | 7 min | Linear search through array |
| Destructor | ⭐ Easy | 1 min | Empty body |
| **Total** | | **~25 min** | |

---

#### **searchable_tree_bag.hpp & .cpp**

| **Component** | **Difficulty** | **Time** | **Key Point** |
|---------------|----------------|----------|---------------|
| Header guards & includes | ⭐ Easy | 1 min | `#pragma once`, include both parents |
| Class declaration | ⭐⭐ Medium | 2 min | Multiple inheritance, private helper |
| Constructors | ⭐ Easy | 3 min | Can be empty bodies |
| Copy constructor | ⭐⭐ Medium | 5 min | Call parent in initializer list |
| Assignment operator | ⭐⭐ Medium | 5 min | Call `tree_bag::operator=` |
| Private `search()` helper | ⭐⭐⭐ Hard | 10 min | Recursive BST navigation |
| Public `has()` function | ⭐ Easy | 2 min | Just call helper |
| Destructor | ⭐ Easy | 1 min | Empty body |
| **Total** | | **~30 min** | |

---

#### **set.hpp & .cpp**

| **Component** | **Difficulty** | **Time** | **Key Point** |
|---------------|----------------|----------|---------------|
| Header guards & includes | ⭐ Easy | 1 min | Include searchable_bag |
| Reference member | ⭐⭐⭐ Hard | 2 min | Understanding reference semantics |
| Deleted functions | ⭐⭐ Medium | 3 min | `= delete` syntax |
| Constructor | ⭐⭐⭐ Hard | 5 min | **MUST use initializer list** |
| `has()` | ⭐ Easy | 2 min | Delegate to bag |
| `insert(int)` | ⭐⭐ Medium | 5 min | Check then insert logic |
| `insert(int*, int)` | ⭐⭐ Medium | 5 min | Loop calling single insert |
| `print()` | ⭐ Easy | 1 min | Delegate to bag |
| `clear()` | ⭐ Easy | 1 min | Delegate to bag |
| `get_bag()` | ⭐ Easy | 2 min | Return const reference |
| Destructor | ⭐ Easy | 1 min | Empty body |
| **Total** | | **~30 min** | |

---

### **Common Pitfalls & How to Avoid Them**

#### **Pitfall 1: Forgetting Virtual Inheritance**

❌ **Wrong:**
```cpp
class searchable_array_bag : public array_bag, public searchable_bag { };
```

✅ **Correct:**
```cpp
class searchable_array_bag : public array_bag, public searchable_bag { };
// Note: array_bag and searchable_bag already use "virtual public bag"
```

---

#### **Pitfall 2: Not Using Initializer List for References**

❌ **Wrong:**
```cpp
set::set(searchable_bag& sb) {
    bag = sb;  // ERROR! Can't assign to reference!
}
```

✅ **Correct:**
```cpp
set::set(searchable_bag& sb) : bag(sb) {
    // Reference initialized in initializer list
}
```

---

#### **Pitfall 3: Accessing Protected Members Incorrectly**

❌ **Wrong:**
```cpp
bool searchable_array_bag::has(int value) const {
    return this->array_bag::data[0];  // Overly complex
}
```

✅ **Correct:**
```cpp
bool searchable_array_bag::has(int value) const {
    // Protected members are directly accessible
    for (int i = 0; i < size; i++) {
        if (data[i] == value)
            return true;
    }
    return false;
}
```

---

#### **Pitfall 4: Wrong BST Search Logic**

❌ **Wrong:**
```cpp
bool search(node* n, int value) const {
    if (n->value == value) return true;  // Crashes if n is nullptr!
    return search(n->l, value) || search(n->r, value);  // Searches BOTH sides!
}
```

✅ **Correct:**
```cpp
bool search(node* n, int value) const {
    if (n == nullptr) return false;      // Check nullptr FIRST
    if (n->value == value) return true;
    if (value < n->value)
        return search(n->l, value);      // Only search ONE side
    else
        return search(n->r, value);
}
```

---

#### **Pitfall 5: Forgetting to Check Before Insert in Set**

❌ **Wrong:**
```cpp
void set::insert(int value) {
    bag.insert(value);  // Allows duplicates!
}
```

✅ **Correct:**
```cpp
void set::insert(int value) {
    if (!has(value))     // Check first!
        bag.insert(value);
}
```

---

## **Difficulty Legend**

| **Symbol** | **Difficulty** | **Time Estimate** | **Characteristics** |
|------------|----------------|-------------------|---------------------|
| ⭐ | **Easy** | 1-5 minutes | Straightforward, direct implementation |
| ⭐⭐ | **Medium** | 5-15 minutes | Requires understanding of pre/post or conversion logic |
| ⭐⭐⭐ | **Hard** | 15-30 minutes | Complex algorithm (addition with carry, comparison logic, recursion) |

---

## **Implementation Priority Order**

### **For VECT2:**
1. ⭐ Constructors, destructor, assignment
2. ⭐ Array access operators
3. ⭐ Binary arithmetic (+, -, *)
4. ⭐ Compound assignment (+=, -=, *=)
5. ⭐ Unary minus
6. ⭐⭐ Increment/decrement operators
7. ⭐ Comparison operators
8. ⭐ Non-member functions (<<, scalar *)

### **For BIGINT:**
1. ⭐ Constructors, assignment, getter
2. ⭐⭐⭐ **Addition helper function** (most critical!)
3. ⭐⭐⭐ Addition operator (uses helper)
4. ⭐ Add-assign
5. ⭐ Pre/post increment
6. ⭐⭐ Left shift operators
7. ⭐⭐ Right shift operators
8. ⭐⭐⭐ Less than operator
9. ⭐ Other comparison operators
10. ⭐ Stream output

### **For POLYSET:**
1. **Start with searchable_array_bag** (easier, no recursion)
2. **Then searchable_tree_bag** (harder, needs recursion)
3. **Finally set** (needs understanding of references)

This way you build confidence before tackling the hardest parts!

---

## **Time Estimates**

### **Individual Exercise Estimates:**

| **Exercise** | **Easy Functions** | **Medium Functions** | **Hard Functions** | **Total Time** |
|--------------|-------------------|---------------------|-------------------|----------------|
| **vect2** | ~20 functions × 3 min | ~6 functions × 10 min | 0 | **~2 hours** |
| **bigint** | ~16 functions × 3 min | ~6 functions × 10 min | ~3 functions × 20 min | **~3 hours** |
| **polyset** | Multiple components | Multiple components | Multiple components | **~1.5 hours** |

### **POLYSET Detailed Breakdown:**

| **Component** | **Time** | **Difficulty** |
|---------------|----------|----------------|
| searchable_array_bag | 25 min | ⭐⭐ Medium |
| searchable_tree_bag | 30 min | ⭐⭐⭐ Hard |
| set | 30 min | ⭐⭐⭐ Hard |
| **Total** | **~85 min** | **1.5 hours** |

---

## **Key Implementation Challenges**

### **VECT2 Challenges:**
| **Challenge** | **Solution** |
|---------------|--------------|
| Pre vs post increment | Post saves copy first, then increments |
| Const vs non-const `[]` | Non-const returns reference (`int&`) |
| Reversed scalar multiply | Non-member function: `int * vect2` |

### **BIGINT Challenges:**
| **Challenge** | **Solution** |
|---------------|--------------|
| Addition with carry | Reverse strings, add digit-by-digit, handle carry |
| String manipulation | Use insert/erase for shifts |
| Comparison | Compare length first, then lexicographic |
| Converting bigint to int | Use stringstream or atoi |
| Avoiding leading zeros | Right shift should set "0" if result empty |

### **POLYSET Challenges:**

#### **Conceptual Challenges:**
1. **Virtual inheritance** - Understanding diamond problem
2. **Multiple inheritance** - Inheriting from two classes
3. **Reference members** - Can't be reassigned, must use initializer list
4. **Recursive BST search** - Tree navigation logic
5. **Abstract classes** - Pure virtual functions must be implemented

#### **Syntax Challenges:**
1. Calling parent constructors in initializer list
2. Calling parent assignment operators explicitly
3. Using `= delete` for deleted functions
4. Initializing reference members
5. Accessing protected members from parent classes

---

## **Quick Reference: Operator Overloading Patterns**

| **Operator Type** | **Return Type** | **Const?** | **Returns** | **Member/Non-member** |
|-------------------|-----------------|------------|-------------|----------------------|
| `+`, `-`, `*` (binary) | `T` | Yes | New object | Member |
| `+=`, `-=`, `*=` | `T&` | No | `*this` | Member |
| `++x` (pre) | `T&` | No | `*this` | Member |
| `x++` (post) | `T` | No | Old value | Member (int param) |
| `[]` (read) | `int` | Yes | Value | Member |
| `[]` (write) | `int&` | No | Reference | Member |
| `==`, `!=`, `<`, etc. | `bool` | Yes | Boolean | Member |
| `-x` (unary) | `T` | Yes | New object | Member |
| `<<` (stream) | `ostream&` | N/A | Stream | **Non-member** |
| `int * T` | `T` | N/A | New object | **Non-member** |

---

## **Exam Strategy**

1. **Read all three exercises first** - Understand what's required
2. **Start with vect2** - Build confidence with easier operators
3. **Move to polyset's searchable_array_bag** - Get familiar with inheritance
4. **Tackle bigint addition** - The hardest single algorithm
5. **Complete remaining functions** - Use patterns you've established
6. **Test with provided mains** - Ensure everything compiles and runs

**Remember:** Start with easy functions in each exercise to build momentum before tackling the hard ones!
