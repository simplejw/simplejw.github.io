---
layout: post
title:  Base
date:   2021-12-27 21:02:12 +0800
categories: java doc
parent: Java
nav_order: 2
---

# 遍历语句

```
// 遍历循环
int[] primes = new int[] { 2, 3, 5, 7, 11, 13, 17, 19, 23, 29 };
for(int n : primes)
     System.out.println(n);


// for循环
for(int i = 0; i < words.length; i++) {
     if (i > 0) System.out.print(", ");
     System.out.print(words[i]);
}
```


# try/catch/finally语句

```
try {
   // 正常情况下，这里的代码从上到下运行，没有问题
   // 但是，有时可能抛出异常
   // 可能是throw语句直接抛出
   // 也可能是调用的方法间接抛出
}
catch (SomeException e1) {
   // 这段代码中的语句用于处理SomeException或其子类类型的异常对象
   // 在这段代码中，可以使用名称e1引用那个异常对象
}
catch (AnotherException | YetAnotherException e2) {
   // 这段代码中的语句用于处理AnotherException、YetAnotherException
   // 或二者的子类类型的异常。在这段代码中，使用名称e2引用传入的异常对象
}
finally {
   // 不管try子句的结束方式如何，这段代码中的语句都会执行：
   //   1）正常结束：到达块的末尾
   //   2）由break、continue或return语句导致
   //   3）抛出异常，由上述catch子句处理
   //   4）抛出异常，未被捕获处理
   // 但是，如果在try子句中调用了System.exit()，解释器会立即退出
   // 不执行finally子句
}
```

# 定义类的句法

类声明可以包含修饰符关键字。除访问控制修饰符（public、protected 等）之外，还可以使用：

- abstract

abstract 修饰的类未完全实现，不能实例化。只要类中有 abstract 修饰的方法，这个类就必须使用 abstract 声明。

- final

final 修饰符指明这个类无法被扩展。类不能同时声明为 abstract 和 final。

- strictfp

如果类声明为 strictfp，那么其中所有的方法都声明为 strictfp。这个修饰符极少使用。

# 类 static

- 和类字段一样，类方法也使用 static 修饰符声明，类方法不能使用任何实例字段或实例方法，因为类方法不关联在类的实例身上。
- 实例方法处理类的具体实例（对象），只要声明方法时没使用 static 关键字，这个方法默认就是实例方法。实例方法没有这种限制，不管类中的成员有没有声明为 static，实例方法都可以使用。

# 类 构造方法

- 构造方法的名称始终和类名一样。

- 声明构造方法时不指定返回值类型，连 void 都不用。

- 构造方法的主体初始化对象。可以把主体的作用想象为设定 this 引用的内容。

- 构造方法不能返回 this 或任何其他值。

- 只要构造方法的参数列表不同，为一个类定义多个构造方法完全是合法的。编译器会根据提供的参数数量和类型判断你想使用的是哪个构造方法。定义多个构造方法和方法重载的原理类似。

# 类 super

- 使用 super() 调用构造方法和使用 this() 调用构造方法有同样的限制：

- 只能在构造方法中像这样使用 super()；

- 必须在构造方法的第一个语句中调用超类的构造方法，甚至要放在局部变量声明之前。

# 访问控制和继承

- 一个 Java 类只能继承一个类。

- 子类继承超类中所有可以访问的实例字段和实例方法；

- 如果子类和超类在同一个包中定义，那么子类继承所有没使用 private 声明的实例字段和方法；

- 如果子类在其他包中定义，那么它继承所有使用 protected 和 public 声明的实例字段和方法；

- 使用 private 声明的字段和方法绝不会被继承；类字段和类方法也一样；

- 构造方法不会被继承。

- 类继承超类的所有实例字段和实例方法（但不继承构造方法）；

- 在类的主体中始终可以访问这个类定义的所有字段和方法，而且还可以访问继承自超类的可访问的字段和方法。

# 定义接口

- 接口中所有强制方法都隐式使用 abstract 声明，不能有方法主体，要使用分号。可以使用 abstract 修饰符，但一般习惯省略。

- 接口定义公开的 API。接口中的所有成员都隐式使用 public 声明，而且习惯省略不必要的 public 修饰符。如果在接口中使用 protected 或 private 定义方法，会导致编译时错误。

- 接口不能定义任何实例字段。字段是实现细节，而接口是规格不是实现。在接口中只能定义同时使用 static 和 final 声明的常量。

- 接口不能实例化，因此不定义构造方法。

- 接口中可以包含嵌套类型。嵌套类型隐式使用 public 和 static 声明。4.4 节会完整介绍嵌套类型。

从 Java 8 开始，接口中可以包含静态方法。Java 之前的版本不允许这么做，这被广泛认为是 Java 语言的一个设计缺陷。

# 枚举

- 不能泛型化；

- 可以实现接口；

- 不能被扩展；

- 如果枚举中的所有值都有实现主体，那么只能定义为抽象方法；

- 只能有一个私有（或使用默认访问权限）的构造方法。

- 都（隐式）扩展 java.lang.Enum 类；

# lambda

`(p, q) -> { /* 方法主􏷮 */ }`

- lambda 表达式必须出现在期望使用接口类型实例的地方；

- 期望使用的接口类型必须只有一个强制方法；

- 这个强制方法的签名要完全匹配 lambda 表达式。

# 线程

- NEW

已经创建线程，但还没在线程对象上调用 start() 方法。所有线程一开始都处于这个状态。

- RUNNABLE

线程正在运行，或者当操作系统调度线程时可以运行。

- BLOCKED

线程中止运行，因为它在等待获得一个锁，以便进入声明为 synchronized 的方法或代码块。本节后面会详细介绍声明为 synchronized 的方法和代码块。

- WAITING

线程中止运行，因为它调用了 Object.wait() 或 Thread.join() 方法。

- TIMED_WAITING

线程中止运行，因为它调用了 Thread.sleep() 方法，或者调用了 Object.wait() 或 Thread.join() 方法，而且传入了超时时间。

- TERMINATED

线程执行完毕。线程对象的 run() 方法正常退出，或者抛出了异常。

----------------

> 线程的生命周期
![线程的生命周期](/assets/images/java_thread.png)

# java 集合

> 集合类及其继承关系
![集合类](/assets/images/java_map.png)

-------------

> 实现Set接口的类
![实现Set接口的类](/assets/images/java_set.png)

--------------

> 实现List接口的类
![实现List接口的类](/assets/images/java_list.png)

--------------

> 实现Map接口的类
![实现Map接口的类](/assets/images/java_map1.png)
![实现Map接口的类](/assets/images/java_map2.png)

# 函数式方式处理集合

1. 过滤器
> 这个模式把集合中的每个元素代入一段代码（返回 true 或 false），然后使用“通过测试”（即代入元素的那段代码返回 true）的元素构建一个新集合。
```
String[] input = {"tiger", "cat", "TIGER", "Tiger", "leopard"}; 
List<String> cats = Arrays.asList(input);
String search = "tiger";
String tigers = cats.stream()
				.filter(s -> s.equalsIgnoreCase(search))
				.collect(Collectors.joining(", ")); 
System.out.println(tigers);
```

2. 映射
> 映射模式把一种类型元素组成的集合转换成另一种类型元素组成的集合。
```
String[] input = {"tiger", "cat", "TIGER", "Tiger", "leopard"}; 
List<String> cats = Arrays.asList(input);
List<Integer> namesLength = cats.stream()
                .map(String::length)
                .collect(Collectors.toList());
System.out.println(namesLength);
```

3. 遍历
> 在 Java 中经常需要处理可变的数据，所以新的集合 API 提供了一个方法，在遍历集合时修改元素——forEach() 方法。不是说 map() 或 filter() 方法一定不能修改元素。不要使用这两个方法修改元素，这只是一种约定，每个 Java 程序员都要遵守。
```
List<String> pets = Arrays.asList("dog", "cat", "fish", "iguana", "ferret");
pets.stream().forEach(s -> System.out.println(s));
```

4. 化简
> 这个方法实现的是化简模式，包含一系列相关的类似运算，有时也称为合拢或聚合运算。
```
double sumPrimes = ((double)Stream.of(2, 3, 5, 7, 11, 13, 17, 19, 23)
       .reduce(10, (x, y) -> {return x + y;}));
System.out.println("Sum of some primes: " + sumPrimes);
```

# 正则表达式
![正则表达式1](/assets/images/java_regex1.png)
![正则表达式2](/assets/images/java_regex2.png)
