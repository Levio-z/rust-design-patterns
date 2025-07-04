# Memento Pattern - 备忘录模式（Rust 实现）

> “在不破坏封装性的前提下，捕获并保存一个对象的内部状态，以便以后将其恢复到先前的状态。”

---

## 模式简介

备忘录模式（Memento Pattern）是一种行为型设计模式，允许对象将其内部状态快照保存起来，并在需要时恢复。它通常用于实现撤销（Undo）/重做（Redo）机制、状态回滚等功能。

该模式的关键在于：状态的封装性和可恢复性，而不会暴露对象的内部实现细节。

---

## 设计结构

```text
┌───────────────┐
│ Originator    │ ← 业务对象，状态的拥有者
└─────┬─────────┘
      │ create/restore
      ▼
┌───────────────┐
│ Memento       │ ← 状态快照（不可变）
└───────────────┘
      ▲
      │ 存储管理
┌─────┴─────────┐
│ Caretaker     │ ← 快照管理者（栈、历史等）
└───────────────┘
```

- Originator：拥有状态的对象，能创建和恢复 Memento
- Memento：表示状态的快照对象（只读、不可变）
- Caretaker：保存并管理多个快照，提供撤销/重做支持

---

## Rust 实现思路

- 使用 `struct Memento` 保存状态字符串的快照，实现 `Clone` trait
- `Editor` 作为 Originator，提供 `create_memento()` 和 `restore()` 方法
- `History` 作为 Caretaker，内部使用 `Vec<Memento>` 管理历史记录
- 保持封装性：Editor 不暴露内部实现，Memento 不被外部写入

示例核心逻辑：

- 编辑器输入内容后保存快照
- 多次撤销恢复上一个状态
- 保证状态封装性与可恢复性

---

## 典型使用场景

| 使用场景     | 示例                   |
|--------------|------------------------|
| 文本编辑器   | Ctrl+Z 撤销功能         |
| 游戏存档     | 保存/加载玩家进度       |
| 事务操作     | 分布式事务回滚         |
| GUI 状态保存 | 恢复表单填写内容       |
| 配置管理     | 回退到旧版本设置       |

---

## 扩展建议

- 泛型化支持任意对象状态
- 快照持久化（如 JSON / 文件系统）
- 支持重做（Redo）功能，引入双栈结构
- 和命令模式联动，实现可撤销操作命令

---

