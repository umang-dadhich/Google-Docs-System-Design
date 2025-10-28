# Document Editor — Applying OOP & SOLID Design Principles

This project demonstrates how to design a **Document Editor (like Google Docs)** using **Object-Oriented Programming (OOP)** and **SOLID design principles** in C++.

It contrasts two implementations:
1. **Bad Design:** A tightly coupled, procedural-style implementation that violates SOLID principles.
2. **Better Design:** A modular, extensible system following OOP and SOLID best practices.

---

## Overview

This project simulates a simple **Document Editor**, capable of:
- Adding text and images  
- Rendering formatted content  
- Saving the final document to a file  
- Supporting extensibility for new features  

The goal is to showcase how **software design patterns** and **SOLID principles** make systems easier to scale and maintain.

---

## 1. Bad Design — Without SOLID Principles

### Summary
The initial version of the Document Editor stores all document elements as strings and uses conditional checks at runtime to determine whether an element is text or an image.

### Example Problem
```cpp
if (element.substr(element.size() - 4) == ".jpg" || element.substr(element.size() - 4) == ".png")
    result += "[Image: " + element + "]";
else
    result += element;
```
### 1. Why It’s a Bad Design

Single Responsibility Violation:
One class (DocumentEditor) handles multiple unrelated tasks such as text processing, image handling, rendering, and file saving.

Open/Closed Violation:
Adding new elements (like videos or tables) requires modifying existing code.

Liskov Substitution Violation:
No abstraction layer for interchangeable components.

Interface Segregation Violation:
The class does everything, forcing all features into one interface.

Dependency Inversion Violation:
High-level logic depends directly on low-level file I/O operations instead of abstractions.

### 2. Better Design — Following SOLID Principles

The improved version follows OOP concepts like abstraction, inheritance, and polymorphism, while strictly applying SOLID principles.

Key Classes

DocumentElement (Abstract Base Class):

Defines a render() interface.

Enables polymorphism for document elements.

Concrete Elements:

TextElement → handles text.

ImageElement → handles images.

NewLineElement and TabSpaceElement → handle formatting.

Document:

Maintains a list of DocumentElement objects.

Renders them sequentially into a complete document.

Persistence Interface:

Abstracts the saving mechanism.

Implementations: FileStorage, DBStorage.

DocumentEditor:

High-level module that coordinates document creation and persistence.

Depends only on abstractions, not concrete implementations.

In short, the bad design works for now—but it’s rigid, hard to extend, and difficult to test.
