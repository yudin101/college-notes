# BIT153 Object Oriented Programming — 3-Evening Survival Guide

Built from: syllabus + model question + real papers 2078, 2079, 2080, 2081, 2082 (6 papers total).

## Index (click to jump)

- [0. Read this first (the blunt version)](#s0)
- [1. Frequency table (what repeats)](#s1)
- [2. TypeScript → C++ cheat sheet](#s2)
- [3. Topics ranked easiest → hardest](#s3)
    - [1. Features of OOP (EASIEST, pure theory)](#t1)
    - [2. Default arguments & inline functions](#t2)
    - [3. Static members](#t3)
    - [4. `this` pointer](#t4)
    - [5. Exception handling (6/6 papers, EASY for you)](#t5)
    - [6. Function templates & class templates](#t6)
    - [7. Constructors & destructors (6/6 papers, GUARANTEED)](#t7)
    - [8. Friend function & friend class](#t8)
    - [9. Objects as function arguments & returning objects](#t9)
    - [10. Polymorphism cluster (MOST REPEATED: 9 questions)](#t10)
    - [11. File handling (6/6 papers, GUARANTEED, but mostly memorization)](#t11)
    - [12. Inheritance (7 questions)](#t12)
    - [13. Ambiguity & virtual base class](#t13)
    - [14. Operator overloading (HARDEST SYNTAX, 6 questions)](#t14)
    - [15. Type conversion (basic ↔ class ↔ class)](#t15)
- [4. Quick hits (10-minute skim, all easy, mostly 1 appearance)](#s4)
- [5. Skip list](#s5)
- [6. Study plan](#s6)
- [7. Exam-writing tips](#s7)

---

<a id="s0"></a>

## 0. Read this first (the blunt version)

- **Theory paper = 60 marks, pass = 24.** Section A: 2 of 3 questions × 10 marks. Section B: 8 of 9 questions × 5 marks. You can only drop **one** Section B question per paper, so you cannot skip whole chapters. Your leverage is in choosing which Section A questions to attempt.
- **Pass strategy:** Aim for ~35, not 24. Get all easy Section B questions (≈25 marks), plus one solid Section A (≈7-8) and a partial second.
- **The syllabus also has Lab (20) and Internal (20) with their own pass marks (8 + 8).** This guide covers only the 60-mark theory paper. Check separately that you're covered on the rest.
- **You must hand-write C++ on paper.** Reading this is not enough. Writing each program from memory once is the difference between passing and failing. Syntax errors on paper cost marks.
- **TypeScript helps with concepts, not syntax.** Classes, inheritance, generics, try/catch, abstract classes: you already understand these. Operator overloading, friend, destructors, pointers, virtual base classes, file objects: **no TS equivalent, pure memorization.**

---

<a id="s1"></a>

## 1. Frequency table (what repeats)

| Topic | Papers it appeared in (of 6) | Total questions | Verdict |
|---|---|---|---|
| **Polymorphism / virtual / abstract vs concrete / early vs late binding / pure virtual** | 6/6 | **9** | **Most repeated. Must know.** |
| **Inheritance** (types, access, ctor/dtor order, Employee→Typist) | 6/6 | **7** | Must know |
| **Constructors / destructors** | 6/6 | 6 | **Guaranteed every year** |
| **Exception handling** | 6/6 | 6 | **Guaranteed every year** |
| **File handling** | 6/6 | 6 | **Guaranteed every year** |
| **Operator overloading** | 5/6 | 6 | Must know (hardest syntax) |
| Type conversion (basic ↔ class) | 4/6 | 4 | Should know |
| Function/class templates | 4/6 | 4 | Should know |
| Friend function / friend class | 4/6 | 4 | Should know |
| Default arguments / inline functions | 4/6 | 4 | Easy marks |
| Ambiguity / virtual base class | 4/6 | 4 | Should know |
| `this` pointer | 3/6 | 3 | Easy marks |
| Features of OOP (theory) | 3/6 | 3 | Easy marks |
| Objects as args / returning objects | 3/6 | 4 | Medium |
| Static members | 2/6 | 2 | Easy marks |
| Namespace, `setw`/`setprecision` | 2/6 | 2 | Quick skim |
| Structure vs class | 2/6 | 2 | Quick skim |
| `new`/`delete`, call by value vs reference, overloading vs overriding, aggregation vs inheritance | 1/6 each | 1 each | Skim only |
| Time class with `const`, Quadratic class | 1/6 each | 1 each | **Skip** |

Note: the "model question" mirrors 2078 closely, so it weights less than a real paper. Real-papers-only conclusions are the same.

**Guaranteed every year: constructors, exception handling, file handling, polymorphism, inheritance.** If you only learn five things, learn those.

---

<a id="s2"></a>

## 2. TypeScript → C++ cheat sheet

| TypeScript | C++ |
|---|---|
| `console.log(x)` | `cout << x << endl;` |
| `prompt()` / read input | `cin >> x;` |
| `import ...` | `#include <iostream>` + `using namespace std;` |
| `class A { private x: number }` | `class A { private: int x; };` ← **semicolon after `}`** |
| `new A()` (always heap, GC'd) | `A a;` (stack, auto-destroyed) or `A* p = new A(); ... delete p;` |
| `a.method()` | `a.method()` for objects, `p->method()` for pointers |
| `this.x` | `this->x` (`this` is a **pointer**) |
| `class B extends A` | `class B : public A` |
| `super(x)` | `B(int x) : A(x) { }` (initializer list) |
| methods are always dynamic | must write `virtual` to get polymorphism |
| `abstract class` | class with a pure virtual function: `virtual void f() = 0;` |
| `function f<T>(a: T)` | `template <typename T> void f(T a)` |
| `try / catch (e) / throw` | same keywords, but you can throw any type (`int`, `const char*`) |
| `constructor() {}` | function with the class's name, no return type |
| no destructors | `~ClassName() { }` runs when object dies |
| `fs.readFileSync` | `ifstream fin("file.txt");` |
| `string` | `#include <string>` then `string` |

Minimum program skeleton (memorize):

```cpp
#include <iostream>
using namespace std;

int main() {
    // code
    return 0;
}
```

---

<a id="s3"></a>

## 3. Topics ranked easiest → hardest

For each: **where it appeared**, what to write, and code. Answer format for 5 marks: 1-line definition → 3-4 key points → short program → output. For 10 marks: longer definition, more points, fuller program.

---

<a id="t1"></a>

### 1. Features of OOP (EASIEST, pure theory)
**Appeared:** 2078 Q2, 2079 Q9, 2081 Q4 (also "OOP vs POP" in 2078 Q2)

Write these 8 with 1-2 lines each:
1. **Object**: instance of a class; has data + behaviour.
2. **Class**: blueprint/template for objects.
3. **Data abstraction**: show essential features, hide implementation.
4. **Encapsulation**: wrapping data and functions together in a class; data hiding via `private`.
5. **Inheritance**: new class acquires properties of existing class → reusability.
6. **Polymorphism**: one name, many forms (overloading = compile time, virtual functions = run time).
7. **Dynamic binding**: function call resolved at run time (via virtual functions).
8. **Message passing**: objects communicate by calling each other's member functions.

**POP vs OOP table (write this if asked):**

| Procedure-oriented | Object-oriented |
|---|---|
| Focus on functions/procedures | Focus on objects/data |
| Top-down | Bottom-up |
| Data is global, little security | Data hidden (encapsulation) |
| No inheritance | Inheritance supported |
| Hard to reuse | Reusable |
| e.g. C, Pascal | e.g. C++, Java |

---

<a id="t2"></a>

### 2. Default arguments & inline functions
**Appeared:** Model Q4, 2079 Q5, 2081 Q9, 2082 Q4

**Default argument:** a value given in the function declaration that is used when the caller omits that argument. Rules: defaults go **right to left**; specify in the declaration (prototype) only.

```cpp
#include <iostream>
using namespace std;

int add(int a, int b = 10, int c = 0) {
    return a + b + c;
}

inline int square(int x) { return x * x; }

int main() {
    cout << add(5) << endl;          // 15  (b=10, c=0)
    cout << add(5, 20) << endl;      // 25
    cout << add(5, 20, 30) << endl;  // 55
    cout << square(4) << endl;       // 16
    return 0;
}
```

**Inline function:** `inline` asks the compiler to paste the function body at the call site instead of doing a normal call.
- **Advantages:** removes function-call overhead (faster for small functions), type-safe unlike macros.
- **Disadvantages:** increases executable size (code bloat), useless/ignored for large functions or loops/recursion, compiler may ignore the request, harder to debug.

---

<a id="t3"></a>

### 3. Static members
**Appeared:** 2079 Q6, 2080 Q12

- **Static data member:** one copy shared by **all** objects. Must be defined outside the class. Initialized to 0 by default.
- **Static member function:** can only access static members; called with `ClassName::func()`; has no `this` pointer.

```cpp
#include <iostream>
using namespace std;

class Counter {
    static int count;          // declaration
public:
    Counter() { count++; }
    static int getCount() { return count; }
};
int Counter::count = 0;        // definition outside class (don't forget)

int main() {
    Counter a, b, c;
    cout << "Objects created: " << Counter::getCount() << endl;  // 3
    return 0;
}
```

---

<a id="t4"></a>

### 4. `this` pointer
**Appeared:** Model Q5, 2080 Q8, 2082 Q5

`this` is a hidden pointer available inside every non-static member function that points to the object that called the function.

**Uses:** (1) resolve name conflict between parameter and member variable, (2) return the current object (`return *this;`) for chaining, (3) pass the current object's address elsewhere.

```cpp
#include <iostream>
using namespace std;

class Box {
    int length;
public:
    Box& setLength(int length) {
        this->length = length;   // left = member, right = parameter
        return *this;            // enables chaining
    }
    void show() { cout << "Length = " << length << endl; }
};

int main() {
    Box b;
    b.setLength(10).show();
    return 0;
}
```
Without `this->`, `length = length;` just assigns the parameter to itself and the member never changes. That's the 2080 Q8 answer.

---

<a id="t5"></a>

### 5. Exception handling (6/6 papers, EASY for you)
**Appeared:** every paper. Variants: "divide by zero" (2082), "array index out of range" (Model), "why handle exceptions" (2081), "why does the program terminate" (2079), "types" (2080).

Your TS `try/catch/throw` knowledge transfers directly.

**Definition:** Exception = runtime error (divide by zero, bad index, file not found). Exception handling = mechanism to detect and respond to it without crashing.

**Mechanism:** `try` (code that may fail) → `throw` (signals the error) → `catch` (handles it).

**Why the program terminates:** if an exception is thrown and **no matching catch exists**, C++ calls `terminate()`, which aborts the program.

**Why we need it:** separates error handling from normal logic, program doesn't crash, errors can be propagated to a caller that knows how to handle them.

**Types (2080 Q5):** *synchronous* (array out of bounds, divide by zero, which C++ handles) and *asynchronous* (keyboard interrupt, hardware failure, which C++ exception handling does not handle).

**Division by zero:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cout << "Enter two numbers: ";
    cin >> a >> b;
    try {
        if (b == 0)
            throw "Division by zero!";
        cout << "Result = " << a / b << endl;
    }
    catch (const char* msg) {
        cout << "Error: " << msg << endl;
    }
    return 0;
}
```

**Array index out of range:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int idx;
    cout << "Enter index: ";
    cin >> idx;
    try {
        if (idx < 0 || idx >= 5)
            throw idx;
        cout << "Value = " << arr[idx] << endl;
    }
    catch (int i) {
        cout << "Index " << i << " is out of range" << endl;
    }
    return 0;
}
```

**Multiple catch + catch-all:**
```cpp
try {
    // ...
    throw 3.5;
}
catch (int e)    { cout << "int caught"; }
catch (double e) { cout << "double caught"; }
catch (...)      { cout << "anything else"; }   // catches all
```

---

<a id="t6"></a>

### 6. Function templates & class templates
**Appeared:** Model Q11, 2079 Q1, 2080 Q10, 2082 Q8

Equivalent to TypeScript generics. **Why needed:** write one function that works for any data type; avoids duplicating code for int/float/double; type-safe (unlike macros).

**Swap (2082 Q8):**
```cpp
#include <iostream>
using namespace std;

template <typename T>
void swapValues(T &a, T &b) {
    T temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 5, y = 10;
    swapValues(x, y);
    cout << x << " " << y << endl;      // 10 5

    float p = 1.5, q = 2.5;
    swapValues(p, q);
    cout << p << " " << q << endl;      // 2.5 1.5
    return 0;
}
```

**Greater of two numbers (2080 Q10), ints and floats:**
```cpp
template <class T>
T greater(T a, T b) { return (a > b) ? a : b; }
```
> Name it `maxOf` in real code. `greater` collides with `std::greater` when `using namespace std;` is on. In the exam, either is fine, but `maxOf` avoids compile errors if you test it.

```cpp
template <class T>
T maxOf(T a, T b) { return (a > b) ? a : b; }

int main() {
    cout << maxOf(3, 7) << endl;        // 7
    cout << maxOf(2.5f, 1.5f) << endl;  // 2.5
    return 0;
}
```

**Class template (the "1 mark" definition in 2080 Q10):** a class blueprint that takes a type as a parameter.
```cpp
template <class T>
class Pair {
    T a, b;
public:
    Pair(T x, T y) : a(x), b(y) {}
    T getMax() { return (a > b) ? a : b; }
};
// usage: Pair<int> p(3, 7);  cout << p.getMax();
```

---

<a id="t7"></a>

### 7. Constructors & destructors (6/6 papers, GUARANTEED)
**Appeared:** Model Q1/Q6, 2078 Q6, 2079 Q1, 2080 Q1, 2081 Q2, 2082 Q1

**Constructor:** special member function with the **same name as the class**, **no return type**, called automatically when an object is created, used to initialize data members.

**Types (always list all four):**
1. **Default constructor**: no arguments.
2. **Parameterized constructor**: takes arguments.
3. **Copy constructor**: `ClassName(const ClassName &obj)`; initializes a new object from an existing one.
4. **Default copy constructor**: generated by the compiler if you don't write one (member-wise copy).

(Constructor overloading = having several of these in the same class.)

**Destructor:** `~ClassName()`; called automatically when an object goes out of scope/is deleted. Characteristics: same name as class with `~`, no arguments, no return type, **cannot be overloaded** (only one per class), cannot be inherited, called in **reverse order** of construction.

**Full program (2082 Q1: Student, constructor overloading, read, display, average):**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
    int id;
    string name;
    float marks[3];
public:
    Student() {                                  // default
        id = 0; name = "Unknown";
        for (int i = 0; i < 3; i++) marks[i] = 0;
    }
    Student(int i, string n, float m1, float m2, float m3) {   // parameterized
        id = i; name = n;
        marks[0] = m1; marks[1] = m2; marks[2] = m3;
    }
    Student(const Student &s) {                  // copy
        id = s.id; name = s.name;
        for (int i = 0; i < 3; i++) marks[i] = s.marks[i];
    }
    void read() {
        cout << "Enter id: ";   cin >> id;
        cout << "Enter name: "; cin >> name;     // one word only
        for (int i = 0; i < 3; i++) {
            cout << "Enter marks " << i + 1 << ": ";
            cin >> marks[i];
        }
    }
    void display() const {
        cout << "ID: " << id << ", Name: " << name
             << ", Average: " << average() << endl;
    }
    float average() const { return (marks[0] + marks[1] + marks[2]) / 3; }
    ~Student() { cout << "Destroying " << name << endl; }
};

int main() {
    Student s1;                                  // default
    Student s2(1, "Ram", 80, 70, 90);            // parameterized
    Student s3(s2);                              // copy
    s1.read();
    s1.display(); s2.display(); s3.display();
    return 0;
}
```

**Model Q1 (Customer, 10 objects):** identical pattern. Class with `customerId, name, age`, a default constructor setting defaults, `read()` and `display()`. In `main`:
```cpp
Customer c[10];                       // array of objects uses default constructor
for (int i = 0; i < 10; i++) c[i].read();
for (int i = 0; i < 10; i++) c[i].display();
```

**Constructor in a derived class (2080 Q1, 2 marks):** the derived constructor passes arguments to the base constructor through an **initializer list**. The base constructor runs **first**.
```cpp
class Base { public: Base(int x) { cout << "Base " << x << endl; } };
class Derived : public Base {
public:
    Derived(int x, int y) : Base(x) { cout << "Derived " << y << endl; }
};
```

---

<a id="t8"></a>

### 8. Friend function & friend class
**Appeared:** 2079 Q11, 2080 Q6, 2081 Q2, 2082 Q6

**Friend function:** a non-member function that is allowed to access the `private` and `protected` members of a class. Declared inside the class with the keyword `friend`.
**Friend class:** all member functions of the friend class can access private members of the other class.

**Why needed:** operate on two different classes (the classic "add private members of two classes"), operator overloading with the left operand not an object.

**Properties:** not a member (called without `.`), defined outside the class, not in the class scope, not inherited, friendship is **not mutual** and **not transitive**.

**2080 Q6, add private members of two classes using a friend function:**
```cpp
#include <iostream>
using namespace std;

class B;                          // forward declaration (required!)

class A {
    int x;
public:
    A(int v) : x(v) {}
    friend int addValues(A, B);
};

class B {
    int y;
public:
    B(int v) : y(v) {}
    friend int addValues(A, B);
};

int addValues(A a, B b) { return a.x + b.y; }

int main() {
    A a(10);
    B b(20);
    cout << "Sum = " << addValues(a, b) << endl;   // 30
    return 0;
}
```

**Friend class:**
```cpp
class Engine;
class Car {
    int speed = 100;
    friend class Engine;          // Engine can access Car's private data
};
class Engine {
public:
    void show(Car c) { cout << c.speed; }
};
```

---

<a id="t9"></a>

### 9. Objects as function arguments & returning objects
**Appeared:** 2078 Q7, 2080 Q7, 2081 Q7 (+ 2078 Q3 Time)

Objects can be passed **by value** (copy), **by reference** (no copy, can modify), or **by const reference**. A function can return an object.

**Returning an object (2080 Q7, 2081 Q7):**
```cpp
#include <iostream>
using namespace std;

class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}
    Complex add(Complex c) {           // object as argument
        Complex temp;
        temp.real = real + c.real;
        temp.imag = imag + c.imag;
        return temp;                   // object returned
    }
    void display() { cout << real << " + " << imag << "i" << endl; }
};

int main() {
    Complex c1(2, 3), c2(4, 5);
    Complex c3 = c1.add(c2);
    c3.display();                      // 6 + 8i
    return 0;
}
```

---

<a id="t10"></a>

### 10. Polymorphism cluster (MOST REPEATED: 9 questions)
**Appeared:** Model Q8, 2078 Q9 + Q10, 2079 Q2 + Q12, 2080 Q2, 2081 Q5, 2082 Q7 + Q12. **Learn this fully.**

Sub-questions that repeat: (a) early vs late binding, (b) dynamic polymorphism with `virtual`, (c) abstract vs concrete class, (d) pure virtual function, (e) roles of polymorphism, (f) ways to achieve static polymorphism.

**Static (compile-time) polymorphism:** function overloading, operator overloading, templates. Resolved by the compiler (early binding).
**Dynamic (run-time) polymorphism:** virtual functions + base-class pointer/reference. Resolved at run time (late binding).

| Early binding | Late binding |
|---|---|
| Resolved at compile time | Resolved at run time |
| Also called static binding | Also called dynamic binding |
| Function overloading, operator overloading, normal functions | Virtual functions |
| Faster | Slightly slower (vtable lookup) |
| Based on pointer **type** | Based on the **object** pointed to |

**Dynamic polymorphism example:**
```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { cout << "Base" << endl; }
};
class Derived : public Base {
public:
    void show() override { cout << "Derived" << endl; }
};

int main() {
    Derived d;
    Base* p = &d;       // base pointer to derived object
    p->show();          // prints "Derived" (late binding)
    return 0;
}
```
Remove `virtual` and it prints "Base". Memorize that contrast, it's the whole concept.

**Abstract vs concrete class:**

| Abstract class | Concrete class |
|---|---|
| Has at least one **pure virtual function** | No pure virtual functions |
| **Cannot** create objects | Can create objects |
| Meant as a base class/interface | Can be used directly |
| Derived class must override pure virtual functions | |

**Pure virtual function:** `virtual void area() = 0;`, declared with no body in the base class. (TS analogue: an `abstract` method.)
```cpp
class Shape {                               // abstract
public:
    virtual double area() = 0;
    virtual ~Shape() {}                     // virtual destructor
};
class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14159 * r * r; }
};
```

**Virtual destructor:** make the base destructor `virtual` so `delete basePtr;` also calls the derived destructor (otherwise memory leak/undefined behaviour).

**Roles of polymorphism (2081 Q5):** code reusability, extensibility (add new derived classes without changing existing code), one interface/many implementations, simplifies code (one loop calls the right function for every shape/employee), supports run-time decision making.

**2080 Q2, Employee with virtual `CalculateSalary()`:**
```cpp
#include <iostream>
using namespace std;

class Employee {
public:
    virtual double CalculateSalary() { return 0; }
    virtual ~Employee() {}
};
class HourlyEmployee : public Employee {
    double rate; int hours;
public:
    HourlyEmployee(double r, int h) : rate(r), hours(h) {}
    double CalculateSalary() override { return rate * hours; }
};
class SalariedEmployee : public Employee {
    double monthly;
public:
    SalariedEmployee(double m) : monthly(m) {}
    double CalculateSalary() override { return monthly; }
};

int main() {
    HourlyEmployee h(500, 40);
    SalariedEmployee s(30000);
    Employee* e1 = &h;
    Employee* e2 = &s;
    cout << "Hourly salary: "   << e1->CalculateSalary() << endl;  // 20000
    cout << "Salaried salary: " << e2->CalculateSalary() << endl;  // 30000
    return 0;
}
```

---

<a id="t11"></a>

### 11. File handling (6/6 papers, GUARANTEED, but mostly memorization)
**Appeared:** Model Q12, 2078 Q12, 2079 Q8, 2080 Q9, 2081 Q1, 2082 Q11

Needs `#include <fstream>`. Three classes: `ofstream` (write), `ifstream` (read), `fstream` (both).
**Stream:** a sequence of bytes flowing between the program and a device (keyboard, screen, file). `cin`/`cout` are streams too.

Modes: `ios::in`, `ios::out`, `ios::app` (append), `ios::binary`, `ios::trunc`, `ios::ate`.
Detect end of file: `while (fin.get(ch))` or `while (getline(fin, line))` or `fin.eof()`.

**(a) Read text from keyboard → write to test.txt → read back (Model Q12):**
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    string text;
    cout << "Enter text: ";
    getline(cin, text);

    ofstream fout("test.txt");
    fout << text << endl;
    fout.close();

    ifstream fin("test.txt");
    string line;
    while (getline(fin, line))
        cout << line << endl;
    fin.close();
    return 0;
}
```

**(b) Copy file 1 into file 2 (2078 Q12):**
```cpp
ifstream fin("file1.txt");
ofstream fout("file2.txt");
char ch;
while (fin.get(ch))
    fout.put(ch);
fin.close();
fout.close();
```
(Wrap in `main` with the includes.)

**(c) Display data.txt and count lines, words, characters (2082 Q11):**
```cpp
#include <iostream>
#include <fstream>
#include <cctype>
using namespace std;

int main() {
    ifstream fin("data.txt");
    if (!fin) { cout << "Cannot open file" << endl; return 1; }

    char ch, last = '\n';
    int lines = 0, words = 0, chars = 0;
    bool inWord = false;

    while (fin.get(ch)) {
        cout << ch;
        chars++;
        if (ch == '\n') lines++;
        if (isspace(ch)) inWord = false;
        else if (!inWord) { inWord = true; words++; }
        last = ch;
    }
    if (last != '\n') lines++;        // last line without trailing newline
    fin.close();

    cout << "\nLines: " << lines << "\nWords: " << words
         << "\nCharacters: " << chars << endl;
    return 0;
}
```

**(d) Read integer; if < 100 write to SMALL.TXT else LARGE.TXT (2081 Q1):**
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    int n;
    cout << "Enter an integer: ";
    cin >> n;
    ofstream fout;
    if (n < 100) fout.open("SMALL.TXT");
    else         fout.open("LARGE.TXT");
    fout << n << endl;
    fout.close();
    return 0;
}
```

**(e) Binary files + reading/writing objects (2080 Q9, 2081 Q1 part):**
- Open with `ios::binary`.
- Write: `fout.write((char*)&obj, sizeof(obj));`
- Read: `fin.read((char*)&obj, sizeof(obj));`
- **Use `char name[30]`, not `string`, in classes you write as binary.** `string` holds a pointer internally, so the file stores garbage.

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Student {
public:
    int id;
    char name[30];
    void read()    { cout << "ID & name: "; cin >> id >> name; }
    void display() { cout << id << " " << name << endl; }
};

int main() {
    Student s;
    s.read();
    ofstream fout("student.dat", ios::binary);
    fout.write((char*)&s, sizeof(s));
    fout.close();

    Student t;
    ifstream fin("student.dat", ios::binary);
    while (fin.read((char*)&t, sizeof(t)))
        t.display();
    fin.close();
    return 0;
}
```

---

<a id="t12"></a>

### 12. Inheritance (7 questions)
**Appeared:** Model Q2, 2078 Q1, 2079 Q3, 2080 Q1 + Q4, 2081 Q3, 2082 Q2

**Inheritance:** deriving a new class (derived/child) from an existing class (base/parent) so it reuses the base's members.

**Types (draw a small diagram for each):**
1. **Single**: A → B
2. **Multiple**: A, B → C (two base classes)
3. **Multilevel**: A → B → C
4. **Hierarchical**: A → B, A → C
5. **Hybrid**: a combination (e.g. multilevel + multiple)

**Access table (2080 Q4):**

| Base member | Public inheritance | Protected inheritance | Private inheritance |
|---|---|---|---|
| public | public | protected | private |
| protected | protected | protected | private |
| private | not accessible | not accessible | not accessible |

Private members of the base are **never** accessible in the derived class. `protected` = accessible in the class and its derived classes, not outside.

**Order of execution (2079 Q3, 2080 Q1, 2081 Q3, 2082 Q2):**
- **Constructors:** base → derived (top-down). Multiple inheritance: in the order bases are listed in the class declaration.
- **Destructors:** derived → base (reverse order).

```cpp
#include <iostream>
using namespace std;

class A { public: A() { cout << "A ctor\n"; } ~A() { cout << "A dtor\n"; } };
class B : public A { public: B() { cout << "B ctor\n"; } ~B() { cout << "B dtor\n"; } };
class C : public B { public: C() { cout << "C ctor\n"; } ~C() { cout << "C dtor\n"; } };

int main() {
    C obj;
    return 0;
}
/* Output:
A ctor
B ctor
C ctor
C dtor
B dtor
A dtor
*/
```

**Employee → Typist (Model Q2, 2078 Q1, appears twice, learn it):**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Employee {
    int Eid;
    string Ename;
    float Salary;
public:
    void read() {
        cout << "Enter id, name, salary: ";
        cin >> Eid >> Ename >> Salary;
    }
    void display() const {
        cout << "ID: " << Eid << ", Name: " << Ename
             << ", Salary: " << Salary << endl;
    }
};

class Typist : public Employee {
    int typing_speed;
public:
    void read() {
        Employee::read();                       // call base version
        cout << "Enter typing speed: ";
        cin >> typing_speed;
    }
    void display() const {
        Employee::display();
        cout << "Typing speed: " << typing_speed << endl;
    }
};

int main() {
    Typist t1, t2;
    t1.read();
    t2.read();
    t1.display();
    t2.display();
    return 0;
}
```

**Aggregation vs inheritance (2079 Q7):** inheritance = **"is-a"** (Dog is an Animal); aggregation = **"has-a"** (Car has an Engine, one class contains an object of another). Inheritance couples classes tightly; aggregation is looser.

---

<a id="t13"></a>

### 13. Ambiguity & virtual base class
**Appeared:** Model Q9, 2079 Q7, 2081 Q12, 2082 Q9

**Ambiguity:** the compiler can't decide which member to use because the same name is reachable by two paths.

**Case 1: multiple inheritance, same function name in two bases.** Fix with the scope resolution operator `::` (or override in the derived class).
```cpp
class A { public: void show() { cout << "A\n"; } };
class B { public: void show() { cout << "B\n"; } };
class C : public A, public B { };

int main() {
    C c;
    // c.show();      // ERROR: ambiguous
    c.A::show();      // fix
    c.B::show();
}
```

**Case 2: multipath (diamond) inheritance.** `D` inherits from `B` and `C`, both of which inherit from `A`, so `D` gets **two copies** of `A`'s members. `d.x` is ambiguous. **Fix: virtual base class**, which makes only **one shared copy** of `A`.
```cpp
#include <iostream>
using namespace std;

class A { public: int x; A() { x = 10; } };
class B : virtual public A { };
class C : virtual public A { };
class D : public B, public C { };

int main() {
    D d;
    cout << d.x << endl;     // 10 (without 'virtual' this is a compile error)
    return 0;
}
```

---

<a id="t14"></a>

### 14. Operator overloading (HARDEST SYNTAX, 6 questions)
**Appeared:** Model Q3, 2079 Q3, 2080 Q3, 2081 Q8 + Q12, 2082 Q3

**Definition:** giving an existing operator an additional meaning for user-defined types. Syntax: `returnType operator<symbol>(args)`. TS cannot do this, so there's no shortcut: memorize the shapes below.

**Rules/restrictions (2081 Q12 "purposes", Model Q3):**
- Cannot overload: `::` (scope), `.` (member access), `.*`, `?:` (ternary), `sizeof`.
- Cannot create new operators or change precedence/associativity/number of operands.
- At least one operand must be a user-defined type.
- Member operator function: unary → 0 arguments, binary → 1 argument (left operand is the calling object).

**Purpose:** natural syntax for user types (`c1 + c2`), readable code, extends the language.

**(a) Binary `+` (2079 Q3: Point, 2080 Q3: Time):**
```cpp
#include <iostream>
using namespace std;

class Point {
    int x, y;
public:
    Point(int a = 0, int b = 0) : x(a), y(b) {}
    Point operator+(const Point &p) const {
        return Point(x + p.x, y + p.y);
    }
    void display() const { cout << "(" << x << ", " << y << ")" << endl; }
};

int main() {
    Point p1(1, 2), p2(3, 4);
    Point p3 = p1 + p2;
    p3.display();                 // (4, 6)
    return 0;
}
```

**Time `+` (2080 Q3), same pattern, with carry:**
```cpp
class Time {
    int h, m, s;
public:
    Time(int hh = 0, int mm = 0, int ss = 0) : h(hh), m(mm), s(ss) {}
    Time operator+(const Time &t) const {
        Time r;
        r.s = s + t.s;
        r.m = m + t.m + r.s / 60;  r.s %= 60;
        r.h = h + t.h + r.m / 60;  r.m %= 60;
        return r;
    }
    void display() const { cout << h << ":" << m << ":" << s << endl; }
};
```

**(b) Unary `++`, pre vs post (Model Q3, 2081 Q8):** the dummy `int` parameter is what makes it **post**-increment.
```cpp
class Student {
    int age;
public:
    Student(int a = 0) : age(a) {}
    Student& operator++()    { ++age; return *this; }          // pre:  ++s
    Student  operator++(int) { Student t = *this; age++; return t; }   // post: s++
    void display() const { cout << "Age: " << age << endl; }
};

int main() {
    Student s(20);
    ++s;  s.display();    // 21
    s++;  s.display();    // 22
}
```
(For 2081 Q8, the simple version `void operator++() { age++; }` is enough.)

**Negation:** `Point operator-() const { return Point(-x, -y); }`

**(c) Comparison `==`:**
```cpp
bool operator==(const Point &p) const { return x == p.x && y == p.y; }
```

**(d) String concatenation with `+`:**
```cpp
#include <iostream>
#include <cstring>
using namespace std;

class MyString {
    char str[100];
public:
    MyString(const char* s = "") { strcpy(str, s); }
    MyString operator+(const MyString &o) const {
        MyString r;
        strcpy(r.str, str);
        strcat(r.str, o.str);
        return r;
    }
    void show() const { cout << str << endl; }
};
// MyString a("Hello "), b("World"); (a + b).show();
```

**2082 Q3, `Number` class with `+`, `==`, and int ↔ Number conversion:**
```cpp
#include <iostream>
using namespace std;

class Number {
    int value;
public:
    Number(int v = 0) : value(v) {}                    // int -> Number
    operator int() const { return value; }             // Number -> int
    Number operator+(const Number &n) const { return Number(value + n.value); }
    bool operator==(const Number &n) const { return value == n.value; }
    void display() const { cout << value << endl; }
};

int main() {
    Number n1(10), n2(20);
    Number n3 = n1 + n2;
    n3.display();                          // 30
    cout << (n1 == n2 ? "Equal" : "Not equal") << endl;

    Number n4 = 50;                        // int -> Number (constructor)
    int x = n3;                            // Number -> int (conversion operator)
    cout << x << endl;                     // 30
    return 0;
}
```
> Trap: don't write `n1 + 5` in `main`. With both the converting constructor and `operator int`, it's ambiguous. Stick to `Number + Number`.

---

<a id="t15"></a>

### 15. Type conversion (basic ↔ class ↔ class)
**Appeared:** Model Q7, 2078 Q8, 2081 Q10, 2082 Q3

Three types:
1. **Basic → class:** use a **constructor** with one argument.
2. **Class → basic:** use a **conversion operator function** `operator type()`; no return type, no arguments.
3. **Class → class:** constructor in the destination class **or** conversion operator in the source class.

**Model Q7, float → Distance (feet, inches), treating the float as feet:**
```cpp
#include <iostream>
using namespace std;

class Distance {
    int feet;
    float inch;
public:
    Distance() : feet(0), inch(0) {}
    Distance(float f) {                    // basic -> class
        feet = (int)f;
        inch = (f - feet) * 12;
    }
    operator float() const {               // class -> basic
        return feet + inch / 12;
    }
    void display() const { cout << feet << " ft " << inch << " in" << endl; }
};

int main() {
    Distance d = 5.5f;                     // float -> Distance
    d.display();                           // 5 ft 6 in
    float f = d;                           // Distance -> float
    cout << f << endl;                     // 5.5
    return 0;
}
```

**Class → class sketch:**
```cpp
class Meter { public: float m; Meter(float x = 0) : m(x) {} };
class Feet {
public:
    float f;
    Feet(const Meter &mt) { f = mt.m * 3.28; }   // constructor in destination
};
// Meter a(2); Feet b = a;
```

---

<a id="s4"></a>

## 4. Quick hits (10-minute skim, all easy, mostly 1 appearance)

**Memory management operators `new`/`delete` (2078 Q4):**
```cpp
int* p = new int;            *p = 5;     delete p;
int* arr = new int[5];       delete[] arr;
```
`new` allocates on the heap and returns a pointer; `delete` frees it; use `delete[]` for arrays. No garbage collector, so forgetting `delete` = memory leak.

**Call by value vs call by reference (2078 Q5):**
```cpp
void swapVal(int a, int b) { int t = a; a = b; b = t; }        // copies, originals unchanged
void swapRef(int &a, int &b) { int t = a; a = b; b = t; }      // originals changed
```

**`setw` and `setprecision` (2081 Q11), need `#include <iomanip>`:**
```cpp
cout << setw(10) << 42 << endl;                 // right-aligned in width 10
cout << setprecision(3) << 3.14159 << endl;     // 3.14 (3 significant digits)
cout << fixed << setprecision(2) << 3.14159;    // 3.14 (2 digits after decimal)
```
`endl` = newline + flush.

**Namespace (2079 Q10):** a named scope that prevents name collisions.
```cpp
namespace Math { int pi = 3; }
cout << Math::pi;
```

**Structure vs class (2079 Q4, 2081 Q2):** the only real difference in C++ is **default access: struct = public, class = private**. In C++ a struct can have member functions, constructors, and inheritance, so **yes, you can do OOP with structures** (2079 Q4). C structs cannot have functions.

**Function overloading vs overriding (2080 Q11):**

| Overloading | Overriding |
|---|---|
| Same name, different parameters | Same name **and** same signature |
| Same class | Base and derived class |
| Compile-time | Run-time (needs `virtual`) |

**Define member function outside the class (2079 Q11):**
```cpp
class A { public: void show(); };
void A::show() { cout << "Hello"; }       // :: scope resolution
```

**Static polymorphism (Model Q3 part 1):** function overloading, operator overloading, function/class templates.

---

<a id="s5"></a>

## 5. Skip list

**Safe to skip completely (appeared once, and not a pattern):**
- Quadratic class (2079 Q2): just a constructor with default arguments, so if you've done topic 7 and topic 2 you could do it anyway, but don't prepare it specifically.
- Time class with `const` objects and `const` member functions (2078 Q3): it's a `const` trap. Use 2080's `operator+` Time program if Time comes up.
- Random file access (`seekg`, `seekp`, `tellg`): in the syllabus and lab sheet, **never asked in 5 papers + model.**
- Pointer arithmetic, storage classes, class-template inheritance, "rules for using templates": syllabus only.

**Skim, don't study:** `new`/`delete`, call by value/reference, namespaces, overloading vs overriding, structure vs class, aggregation vs inheritance. They're easy, appear rarely, and are the ones you'd drop if you chose to answer 8 of 9.

**Do not skip:** constructors, exceptions, file handling, polymorphism, inheritance. These are in **every** paper.

**Section A picking strategy:** Pick the two where you can write a complete program you've rehearsed:
- Employee→Typist, Student/Customer constructor program, or Employee virtual `CalculateSalary()` = safest.
- Operator-overloading programs are fine if you've memorized the `+` shape.
- Avoid theory-heavy 3-part questions (e.g. 2079 Q1: "template + why terminate + types of constructor") unless you know all parts, since partial credit across three parts is hard to control.

---

<a id="s6"></a>

## 6. Study plan

**Foundations + easiest marks (~3-4 hrs)**
- Cheat sheet (section 2). Compile and run "Hello World" on an online compiler to remove fear of syntax.
- Topics 1-4 (features, default/inline, static, `this`).
- Topic 5 (exceptions).
- Topic 6 (templates).
- Topic 7 (constructors/destructors): **write the Student program from memory.**

**The heavy hitters (~4 hrs)**
- Topic 8 (friend), topic 9 (objects as arguments/returns).
- Topic 12 (inheritance): constructor order + Employee→Typist from memory.
- Topic 13 (ambiguity, virtual base).
- Topic 10 (polymorphism): early/late binding table, abstract vs concrete, Employee salary program.

**Hardest syntax + files (~4 hrs)**
- Topic 14 (operator overloading): write `+`, pre/post `++`, `==` from memory until you stop looking.
- Topic 15 (type conversion).
- Topic 11 (file handling): write programs (a)-(d) from memory.
- Quick hits (section 4).

**Exam day (before the paper):** re-do on paper, timed, one Section A style program each for: constructors, inheritance, polymorphism, operator `+`, file read/write. Then reread the tables in topics 10, 12, 13 (early vs late, abstract vs concrete, access table).

**Test yourself:** Pick any past paper, give yourself 3 hours, handwrite answers. Check against this file only after.

---

<a id="s7"></a>

## 7. Exam-writing tips

- Comment minimally, but **always** write the class, the constructor/function, and a `main()`. Examiners award marks for structure.
- **Don't forget the semicolon after `class ... };`**. The most common handwritten-code error.
- Don't skip the `#include` lines or `using namespace std;`.
- For theory: definition → points → example. Four sentences + a program gets full marks on a 5-marker.
- If you forget a detail, write the program anyway. Partial marks for correct structure beat a blank page.
- For "list/explain types" questions, **name every type** (e.g. all 4 constructor types, all 5 inheritance types) even if you only explain a couple well.
