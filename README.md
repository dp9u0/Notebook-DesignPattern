# Notebool-DesignPattern

[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu) [![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)

[Notebook系列](https://github.com/dp9u0/Notebook)

* [Notebool-DesignPattern](#notebool-designpattern)
  * [面向对象设计原则](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%AE%BE%E8%AE%A1%E5%8E%9F%E5%88%99)
  * [创建](#%E5%88%9B%E5%BB%BA)
    * [ABSTRACT FACTORY](#abstract-factory)
    * [BUILDER](#builder)
    * [FACTORY METHOD](#factory-method)
    * [PROTOTYPE](#prototype)
    * [SINGLETON](#singleton)
  * [结构](#%E7%BB%93%E6%9E%84)
    * [ADAPTER](#adapter)
    * [BRIDGE](#bridge)
    * [COMPOSITE](#composite)
    * [DECORATOR](#decorator)
    * [FACADE](#facade)
    * [FLYWEIGHT](#flyweight)
    * [PROXY](#proxy)
  * [行为](#%E8%A1%8C%E4%B8%BA)
    * [CHAIN OF RESPONSIBILITY](#chain-of-responsibility)
    * [COMMAND](#command)
    * [INTERPRETER](#interpreter)
    * [ITERATOR](#iterator)
    * [MEDIATOR](#mediator)
    * [MEMENTO](#memento)
    * [OBSERVER](#observer)
    * [STATE](#state)
    * [STRATEGY](#strategy)
    * [TEMPLATE METHOD](#template-method)
    * [VISITOR](#visitor)

## 面向对象设计原则

1. 开闭原则(`Open Close Principle`) : 对扩展开放,对修改关闭.增加功能时,不能去修改原有的代码,而是要扩展原有代码.
2. 职责单一原则(`Single responsibility principle`) : 每个类应该只负责一个职责,否则就应该拆分该类.
3. 里氏替换原则(`Liskov Substitution Principle`) : 任何基类可以出现的地方,子类一定可以出现. LSP是继承复用的基石,只有当衍生类可以替换掉基类,软件单位的功能不受到影响时,基类才能真正被复用,而衍生类也能够在基类的基础上增加新的行为.里氏代换原则是对开闭原则的补充.实现开闭原则的关键步骤就是抽象化.而基类与子类的继承关系就是抽象化的具体实现,所以里氏代换原则是对实现抽象化的具体步骤的规范.
4. 依赖倒转原则(`Dependence Inversion Principle`) : 依赖于抽象而不依赖于具体.
5. 接口隔离原则(`Interface Segregation Principle`) : 客户端不应该依赖它不需要的接口,一个类对另一个类的依赖应该建立在最小的接口上.
6. 迪米特原则(`Demeter Principle`) : 又称为最少知道原则,一个类对自己依赖的类知道的越少越好.无论被依赖的类多么复杂,都应该将这些复杂的逻辑封装在其内部,提供给外部的仅仅是极少的接口或者方法.这样当被依赖的类变化时,才能最小的影响该类.
7. 合成复用原则(`Composite Reuse Principle`) : 多使用组合,少用继承. 防止继承的滥用.

## 创建

### ABSTRACT FACTORY

* 目的 : 提供一个接口,可以创建一系列对象.创建一系列对象时无需指定具体的类.
* 使用场景 : 隐藏创建一系列对象的细节
* 结构
  
![ABSTRACT FACTORY](./img/abstract-factory.png)

运行时刻创建一个 `ConcreteFactory` 类的实例,`AbstractFactory` 将产品对象的创建延迟到它的 `ConcreteFactory` 子类.

* 效果

  * 优点 : 1. 分离了具体的类 2. 保持产品一直性: 一个工厂创建一个系列产品
  * 缺点 : 不方便扩展,增加一个产品`AbstractFactory` 和所有的`ConcreteFactory` 就需要增加一个`CreateProduct`方法.(解决方案 : `AbstractFactory` 只提供一个 `Create` 方法, 通过传递参数的方式确定获取哪种类型 `Product`)

* 其他说明 : 实现`ConcreteFactory`可以通过以下两种方式

  * `Product` 可以通过 `Prototype` 模式, 只需要一个`ConcreteFactory`,`CreateProduct` 通过 `Product` 的原型复制一个出来即可.(创建 `ConcreteFactory`时,指定`Product`系列即可)

  * 也可以每个系列的 `Product` 对应一个类型的 `ConcreteFactory` (`Factory Method`)

### BUILDER

### FACTORY METHOD

### PROTOTYPE

### SINGLETON

## 结构

### ADAPTER

### BRIDGE

### COMPOSITE

### DECORATOR

### FACADE

### FLYWEIGHT

### PROXY

## 行为

### CHAIN OF RESPONSIBILITY

### COMMAND

### INTERPRETER

### ITERATOR

### MEDIATOR

### MEMENTO

### OBSERVER

### STATE

### STRATEGY

### TEMPLATE METHOD

### VISITOR
