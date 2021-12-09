# Class类

+ 直接通过一个class的静态变量class获取
+ 如果我们有一个实例变量，可以通过该实例变量提供的getClass()方法获取
+ 如果知道一个class的完整类名，可以通过静态方法Class.forName()获取

## Kotlin

要获取对静态已知的 Kotlin 类的引用，可以使用 类字面值 语法

```
val c = MyClass::class
```

该引用是 [KClass](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-class/index.html) 类型的值

请注意，Kotlin 类引用与 Java 类引用不同。要获得 Java 类引用， 请在 `KClass` 实例上使用 `.java` 属性

### 绑定的类引用（自 1.1 起）

通过使用对象作为接收者，可以用相同的 `::class` 语法获取指定对象的类的引用

### 与 Java 反射的互操作性

在 JVM 平台上，标准库包含反射类的扩展，它提供了与 Java 反射对象之间映射（参见 `kotlin.reflect.jvm` 包

```
class A(val p: Int)

fun main() {
    println(A::p.javaGetter) // 输出 "public final int A.getP()"
    println(A::p.javaField)  // 输出 "private final int A.p"
}
```

获得对应于 Java 类的 Kotlin 类，请使用 `.kotlin` 扩展属性

```
fun getKClass(o: Any): KClass<Any> = o.javaClass.kotlin
```

