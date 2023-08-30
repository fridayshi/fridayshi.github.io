---
layout: post
title:  "Abstract Factory（抽象工厂）"
date:   2023-08-30 22:35:00 +0800
categories: code
---
[](Abstract Factory（抽象工厂）)

以下是一个使用 C++ 实现的简单抽象工厂模式的示例：

```cpp
#include <iostream>

// Abstract Product A
class AbstractProductA {
public:
    virtual void operationA() = 0;
};

// Concrete Product A1
class ConcreteProductA1 : public AbstractProductA {
public:
    void operationA() override {
        std::cout << "ConcreteProductA1 operationA" << std::endl;
    }
};

// Concrete Product A2
class ConcreteProductA2 : public AbstractProductA {
public:
    void operationA() override {
        std::cout << "ConcreteProductA2 operationA" << std::endl;
    }
};

// Abstract Product B
class AbstractProductB {
public:
    virtual void operationB() = 0;
};

// Concrete Product B1
class ConcreteProductB1 : public AbstractProductB {
public:
    void operationB() override {
        std::cout << "ConcreteProductB1 operationB" << std::endl;
    }
};

// Concrete Product B2
class ConcreteProductB2 : public AbstractProductB {
public:
    void operationB() override {
        std::cout << "ConcreteProductB2 operationB" << std::endl;
    }
};

// Abstract Factory
class AbstractFactory {
public:
    virtual AbstractProductA* createProductA() = 0;
    virtual AbstractProductB* createProductB() = 0;
};

// Concrete Factory 1
class ConcreteFactory1 : public AbstractFactory {
public:
    AbstractProductA* createProductA() override {
        return new ConcreteProductA1();
    }

    AbstractProductB* createProductB() override {
        return new ConcreteProductB1();
    }
};

// Concrete Factory 2
class ConcreteFactory2 : public AbstractFactory {
public:
    AbstractProductA* createProductA() override {
        return new ConcreteProductA2();
    }

    AbstractProductB* createProductB() override {
        return new ConcreteProductB2();
    }
};

int main() {
    // Create factory 1
    AbstractFactory* factory1 = new ConcreteFactory1();

    // Create products using factory 1
    AbstractProductA* productA1 = factory1->createProductA();
    AbstractProductB* productB1 = factory1->createProductB();

    productA1->operationA(); // Output: ConcreteProductA1 operationA
    productB1->operationB(); // Output: ConcreteProductB1 operationB

    // Create factory 2
    AbstractFactory* factory2 = new ConcreteFactory2();

    // Create products using factory 2
    AbstractProductA* productA2 = factory2->createProductA();
    AbstractProductB* productB2 = factory2->createProductB();

    productA2->operationA(); // Output: ConcreteProductA2 operationA
    productB2->operationB(); // Output: ConcreteProductB2 operationB

    // Clean up
    delete productA1;
    delete productB1;
    delete productA2;
    delete productB2;
    delete factory1;
    delete factory2;

    return 0;
}
```

在这个示例中，我们首先定义了抽象产品类 `AbstractProductA` 和 `AbstractProductB`，并且分别派生出了具体的产品类 `ConcreteProductA1`、`ConcreteProductA2`、`ConcreteProductB1` 和 `ConcreteProductB2`。然后，我们定义了抽象工厂类 `AbstractFactory`，其中包含创建产品的纯虚函数。接着，我们派生出了具体的工厂类 `ConcreteFactory1` 和 `ConcreteFactory2`，分别实现了创建不同产品的方法。最后，在 `main` 函数中使用具体的工厂来创建产品，并调用其操作方法。

运行这个示例将输出以下结果：

```
ConcreteProductA1 operationA
ConcreteProductB1 operationB
ConcreteProductA2 operationA
ConcreteProductB2 operationB
```

这个示例展示了抽象工厂模式的基本结构和使用方法。通过使用抽象工厂模式，客户端代码可以通过抽象的工厂接口来创建产品，而无需直接指定具体的产品类，从而实现了解耦。这样可以更容易地切换和扩展产品系列，同时保持客户端代码的一致性。
