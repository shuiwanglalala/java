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

## Blog

[先有Class还是先有Object？](https://www.zhihu.com/question/30301819/answer/47539163)

但“[鸡蛋问题](https://www.zhihu.com/search?q=鸡蛋问题&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A47539163})”仍然存在：在一个已经启动完毕、可以使用的Java对象系统里，必须要有一个java.lang.Class实例对应java.lang.Object这个类；而java.lang.Class是java.lang.Object的派生类，按“一般思维”前者应该要在后者完成初始化之后才可以初始化…

事实是：这些相互依赖的核心类型完全可以在“混沌”中一口气都初始化好，然后对象系统的状态才叫做完成了“bootstrap”，后面就可以按照Java对象系统的一般规则去运行

在“混沌”（[boostrap过程](https://www.zhihu.com/search?q=boostrap过程&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A47539163})）里，

- JVM可以为对象系统中最重要的一些核心类型先分配好内存空间，让它们进入[**已分配空间**]但[**尚未完全初始化**]状态。此时这些对象虽然已经分配了空间，但因为状态还不完整所以尚不可使用。
- 然后，通过这些分配好的空间把这些核心类型之间的引用关系串好。到此为止所有动作都由JVM完成，尚未执行任何Java字节码。
- 然后这些核心类型就进入了[**完全初始化**]状态，对象系统就可以开始自我运行下去，也就是可以开始执行Java字节码来进一步完成Java系统的初始化了。



作者：RednaxelaFX
链接：https://www.zhihu.com/question/30301819/answer/47539163
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。