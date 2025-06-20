# Rust 中基于观察者模式、模板方法模式与回调机制的按钮点击事件示例

本示例展示了如何在 Rust 中结合**观察者模式**、**模板方法模式**以及**回调机制**的设计思想，实现一个 UI 控件（按钮）的事件驱动系统。

---

## 设计模式与概念

### 观察者模式

- **目的：** 定义一对多的依赖关系，当一个对象状态发生变化时，所有依赖者都会自动收到通知并更新。  
- **本示例中体现为：**  
  - `Button` 作为**主题对象**（发布者），维护一个监听器（观察者）列表。  
  - 每个监听器实现 `ClickListener` trait（观察者接口）。  
  - 当按钮被点击时，通知所有已注册的监听器，调用它们的 `on_click()` 方法。  

### 模板方法模式（隐式体现）

- **目的：** 在一个方法中定义算法的骨架，将某些步骤延迟到子类或回调实现中。  
- **本示例中体现为：**  
  - `Button::click()` 方法定义了按钮点击事件的固定流程：打印点击日志，然后依次通知监听器。  
  - 对点击事件的具体响应逻辑延迟到各监听器实现的 `on_click()` 方法，从而支持行为的灵活定制。  

### 回调机制

- **目的：** 将部分具体行为委托给用户定义的回调接口，实现代码逻辑与具体业务响应的解耦。  
- **本示例中体现为：**  
  - 通过 `ClickListener` trait 定义回调接口，允许用户实现自定义的事件处理逻辑。  
  - `Button` 持有多个实现该接口的回调对象，并在事件发生时统一调用，实现灵活的多路事件分发。  

---

该设计模式组合保证了事件驱动程序中的**低耦合**、**高扩展性**和**职责分离**，非常适合各种基于事件的业务场景。
