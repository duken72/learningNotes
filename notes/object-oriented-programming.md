<!-- omit in toc -->
# Object-Oriented Programming

The 4 pillars of OOP (Object-Oriented Programming):

1. Encapsulation: Group related variables, functions together
   > The best functions are those with no parameters! [(Robert C. Martin)](https://www.goodreads.com/author/show/45372.Robert_C_Martin)
2. Abstraction:
   - Have fewer properties & methods
   - Reduce impact of change
3. Inheritance: Eliminate redundant code
4. Polymorphism (in many forms)

-------

<!-- omit in toc -->
## Table of Contents

- [Inheritance](#inheritance)
- [Polymorphism](#polymorphism)
  - [Duck Typing (Dynamic Typing)](#duck-typing-dynamic-typing)
  - [Operator Overloading](#operator-overloading)
  - [Method Overloading](#method-overloading)
  - [Method Overriding](#method-overriding)

-------

## Inheritance

-------

## Polymorphism

Use in:

- Loose coupling
- Dependency injection
- Interface

4 ways:

- Duck typing
- Operator overloading
- Method overloading
- Method overriding

### Duck Typing (Dynamic Typing)

Example:

```python
class StudentA:
    def learn(self):
        return 1+2
class StudentB:
    def learn(self):
        return 3+4

class MathClass:
    def teach(self, student):
        return student.learn()
```

### Operator Overloading

For magic methods:

- Python:

  ```python
  __add__, __sub__, __mul__, __div__
  ```

- C++:

  ```cpp
  // Overload + operator to add two Rectangle objects.
  Rectangle operator+(const Rectangle& r) {
    Rectangle rect;
    rect.length = this->length + r.length;
    rect.height = this->height + r.height;
    return rect;
  }
  ```

### Method Overloading

Actually not there in Python, but is available in C++

```cpp
void print(int i) {
  cout << " Here is int " << i << endl;
}
void print(double  f) {
  cout << " Here is float " << f << endl;
}
void print(char const *c) {
  cout << " Here is char* " << c << endl;
}
```

### Method Overriding

Also, for interface?

- Python:

  ```python
  class A:
      def show(self):
          return 0
  class B(A):
      def show(self):
          return 1
  ```

- C++:

  ```cpp
  class Base
  {
  public:
    virtual void print() {
      std::cout << "Base class" << std::endl;
    }
  }

  class Derived : public Base
  {
  public:
    void print() {
      std::cout << "Derived class" << std::endl;
    } override
  }
  ```

-------
