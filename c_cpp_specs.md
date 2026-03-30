# C~
This document summarizes the main C and C++ language concepts variation for C~ (C Wave) language.
This language is intended to replace the C/C++ language.
We expect to propose some code modifier to pass from C to C~; it seems very tricky from C++ to C~.

## 1. Preprocessor and Includes

DELETE(force path) - `#include <header>`: include system headers.
KEEP(force path) - `#include "file.h"`: include user-defined headers.
ADD - `#include "file.h" as prefix` : include with namespace (prefix)
PENDING - `#define NAME value`: define a macro.
PENDING - `#undef NAME`: undefine a macro.
PENDING - `#ifdef`, `#ifndef`, `#if`, `#elif`, `#else`, `#endif`: conditional compilation.
DELETE(native management) - `#pragma`: implementation-defined compiler directives.

## 2. Types and Declarations

- Built-in types:
Modify(Fix the bytes size, it should not depend from arch, make it classes) - `int`(4 bytes), `short`(2 bytes), `long`(4 bytes), `long long`(8 bytes), `char`(1 byte), `float`, `double`, `long double`, `bool`
KEEP  - `unsigned`, `signed`
DELETE  - `wchar_t`, `char16_t`, `char32_t`
KEEP - pointers: `int *p;`
DELETE(retard -_-') - references: `int &r;` (C++)
KEEP - arrays: `int arr[10];`
MODIFY(syntax) - arrays : `{1,2,3}` for `[1,2,3]`
MODIFY(you do not use it because you never can remember the fucking syntax) - function pointers: `int (*fp)(int);`
KEEP - `const`
PENDING  - `volatile`
KEEP  - `static`
PENDING(tricky and error prone, what if we forbid packaged library ?)  - `extern`
DELETE  - `register` (deprecated in C++17, ignored in modern compilers)
DELETE  - `mutable` (C++)

## 3. Variables and Constants

- Variable declaration and initialization:
KEEP(as class int)  - `int x;`
KEEP  - `int x = 5;`
- Constant definitions:
KEEP  - `const int kMax = 100;`
KEEP  - `enum { VALUE = 1 };`
DELETE  - `constexpr` (C++)
- Storage duration:
KEEP  - automatic: local variables
KEEP  - static: `static int x;`
DELETE  - thread-local: `thread_local` (C++11)
KEEP  - dynamic: objects allocated with `malloc/new`

## 4. Functions

- Declaration:
KEEP  - `int add(int a, int b);`
- Definition:
KEEP  - `int add(int a, int b) { return a + b; }`
KEEP - Function overloading (C++): same name, different parameter types.
DELETE - Default arguments (C++): `void f(int x = 10);`
- Inline functions:
PENDING(We want to avoid one jump ? Realy ?)  - `inline int square(int x) { return x * x; }`
- Function pointers:
MODIFY(see function pointers type declaration)  - `int (*func)(int, int) = add;`
- Variadic functions:
MODIFY(create a type any ?)  - C: `int printf(const char *fmt, ...);`

## 5. Control Flow

- Conditional statements:
KEEP  - `if`, `else`
DELETE - `switch`
- Loops:
KEEP  - `for`, `while`, `do { } while`
- Jump statements:
KEEP  - `break`, `return`
DELETE - `continue`, `goto`
- Exception handling:
KEEP  - `try`, `catch`, `throw` (C++)

## 6. Structs and Unions

- `struct`:
DELETE(replace by classes)  - C: `struct Point { int x; int y; };`
- `union`:
KEEP  - `union Value { int i; float f; };`
- `enum`:
DELETE  - C: `enum Color { RED, GREEN, BLUE };`
KEEP(but remove the class keyword)  - C++ scoped enums: `enum class Color { Red, Green, Blue };`

## 7. Classes and Object-Oriented Programming (C++)

- Class definition:
KEEP  - `class MyClass { public: int value; void f(); };`
- Access specifiers:
KEEP  - `public`, `private`, `protected`
- Member functions and data members:
MODIFY(forbidden in header, force definition in source files)  - `void set(int v) { value = v; }`
- Constructors and destructors:
KEEP  - `MyClass() {}`
MODIFY(removed preconstructor setting: `: value(v)`)  - `MyClass(int v) : value(v) {}`
KEEP  - `~MyClass() {}`
MODIFY(force !) - `this` pointer: implicit object pointer inside methods.

## 8. Inheritance (C++)

- Single inheritance:
KEEP  - `class Derived : public Base { ... };`
- Multiple inheritance:
DELETE  - `class Derived : public Base1, public Base2 { ... };`
- Access control for base classes:
KEEP  - `public`, `protected`, `private` inheritance.
- Virtual functions and polymorphism:
DELETE(always virtual)  - `virtual void speak();`
DELETE(always virtual)  - `virtual ~Base();`
- Abstract classes:
DELETE  - `virtual void draw() = 0;`
ADD - `interface InterfaceName{}`
ADD - `class ClassName implements InterfaceName`
- `override` and `final` qualifiers:
DELETE  - `void f() override;`
PENDING  - `virtual void f() final;`

## 9. Templates (C++)

- Function templates:
MODIFY(syntax)  - `template <typename T> T add(T a, T b) { return a + b; }` to `<T> T add(T a, T b) { return a + b; }`
ADD(force templace inheritance type <T:ParentType>) - `<T:ParentType> T add(T a, T b) { return a + b; }`
- Class templates:
MODIFY(syntax)  - `template <typename T> class Vector { ... };` to `class Vector<T> { ... };`
- Template specialization:
DELETE  - full specialization: `template<> class MyClass<int> { ... };`
DELETE  - partial specialization: `template<typename T> class MyClass<T*> { ... };`
- Non-type template parameters:
DELETE  - `template <typename T, int N> class Array { T data[N]; };`

## 10. Namespaces (C++)

- Declaration:
DELETE(see Preprocessor and Includes)  - `namespace math { int add(int a, int b); }`
- Usage:
DELETE  - `using namespace std;`
KEEP  - `using std::string;`
- Nested namespaces:
DELETE  - `namespace outer::inner { ... }`

## 11. Memory Management

- Dynamic allocation:
KEEP  - C: `malloc`, `calloc`, `realloc`, `free`
KEEP  - C++: `new`, `new[]`, `delete`
DELETE(if possible) : `delete[]`

## 12. Operators

KEEP - Arithmetic: `+`, `-`, `*`, `/`, `%`
KEEP - Assignment: `=`, `+=`, `-=`, `*=`, `/=`
KEEP - Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
KEEP - Logical: `&&`, `||`, `!`
KEEP - Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
KEEP - Increment/decrement: `++`, `--`
KEEP - Pointer operators: `*`, `&`, `->`, `.`
KEEP - Member access operators (C++): `.*`, `->*`
- Casts:
KEEP  - C-style: `(int)x`
DELETE  - C++ style: `static_cast<int>(x)`, `dynamic_cast<T*>(p)`, `const_cast<T>(x)`, `reinterpret_cast<T>(x)`
- Operator overloading (C++):
KEEP  - `operator+`, `operator=`, `operator[]`, `operator()`

## 15. Common Patterns and Keywords

DELETE - `typedef` / `using`: type aliases.
DELETE - `extern "C"`: C linkage for interoperability.
DELETE - `volatile`: variable may change unexpectedly.
DELETE - `constexpr`: compile-time constant expression (C++).
DELETE - `noexcept`: function does not throw exceptions (C++).
DELETE - `static_assert`: compile-time assertion (C++11).
