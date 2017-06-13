# 4:通过私有构造器强化不可实例化的能力

## 1.背景

有的时候，你可能需要只包含静态方法和静态域的类。这些类的名声很不好，因为有些人在面向对象的语言中滥用这样的类来编写过程化的程序，尽管如此，他们也确实有他们特有的用处。

## 2.方案

我们可以利用用这种类，以java.lang.Math 或者 java.util.Arrays 的方式，把基本类型的值或者数组类型上的相关方法组织起来。

我们也可以通过 java.util.Collections 的方式，把实现特定接口的对象上的静态方法（包括工厂方法）组织起来。

最后还可以利用这种类，吧 final 类上的方法组织起来，以取代扩展该类的做法。

## 3.问题

这样的工具类不希望被实例化，实例对它没有任何意义。然而，在缺少显示构造器的情况下，编译器会自动提供一个公有的、无参的缺省构造器。用户可以利用这个构造器创建出工具类的实例。这种被无意识实例化的类是不应该的。

## 4.解决

解决方案很简单，就是手动将无参构造器私有化：

```java
public class Test {
    private Test() {
        throw new AcertionError();
    }
}
```

## 5.副作用

这种做法会使得他的子类不能被实例化。因为子类的所有构造器都会显示或者隐式的调用父类的构造器，这种情况下，子类就没有可用的父类构造器了。