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
* 使用场景 : 只需要提供一系列对象给调用者而无需让调用者直到创建一系列对象的细节
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

* 目的 : 复杂对象的构造过程和表示分离
* 使用场景 : 构造过程复杂,并且希望通过可选的步骤一步步构造构造可以具有不同的表示的实例.
* 结构

![BUILDER](./img/builder.png)

`Client` 通过 调用 `Builder`实例(`_builder`) 的 `BuildPart` 方法 提供构造需要的参数,最终通过 `GetResult` 获取 `Product`

* 效果 : 明确的控制和改变对象的表示
* 其他说明 : 着重于一步步构造一个复杂对象

### FACTORY METHOD

* 目的 : 定义一个用于创建对象的接口,让子类决定实例化哪一个类
* 使用场景 : 基类中使用的一个类的实例化延迟到子类
* 结构

![FACTORY METHOD](./img/factory-method.png)

工厂方法指的是定义的抽象方法 `FactoryMethod` 用于获取实例

* 效果 : 为子类提供了Hook
* 其他说明 : 工厂方法其实是模版方法的一个用于构造对象的特例

### PROTOTYPE

* 目的 : 用原型实例指定创建对象的种类,并且通过拷贝这些原型创建新的对象
* 使用场景 : 要实例化的类型是运行时指定的或者避免创建工厂类或者当一个类的实例只能有几个不同状态组合中的一种时,通过克隆已有实例比使用状态手工实例化更方便
* 结构

![PROTOTYPE](./img/prototype.png)

* 效果 : 隐藏具体产品类,运行时刻增加和删除产品,以及其他的模式(原型链,Copy On Write)
* 其他说明 : 使用一个原型管理器, Clone 和 DeepClone

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

* 目的 :
* 使用场景 :
* 结构

![TITLE](./img/image.png)

* 效果 :
* 其他说明 :
