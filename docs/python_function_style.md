## 资料来源：
* https://github.com/oldratlee/translations/blob/master/a-practical-introduction-to-functional-programming/README.md

## 函数式编程
函数式编程的特质：

* 不可变数据1（immutable data）、一等公民的函数2（first class function）和尾调用优化3（tail call optimisation）。这些是有助于函数式编程的语言特性。
* map、reduce、管道、递归（recursing）、柯里化4（currying）以及高阶函数的使用。这些是用于编写函数式代码的编程技术。
* 并行化5（parallelization）、惰性求值6（lazy evaluation）和确定性7（determinism）。这些是函数式程序的优点。

**核心思想**
无视这一切。函数式代码的核心特质就一条：**无副作用（the absence of side effects）**。即代码逻辑不依赖于当前函数之外的数据，并且也不会更改当前函数之外的数据。所有其他的『函数式』特质都可以从这一条派生出来。在你学习过程中，请以此作为指南针。

**非函数式**

```
a = 0
def increment():
    global a
    a += 1
```
**函数式**
```
def increment(a):
    return a + 1
```

## f-string

```python
val = 'Geeks'
print(f"{val}for{val} is a portal for {val}.")

name = 'Tushar'
age = 23
print(f"Hello, My name is {name} and I'm {age} years old.")
```
