---
title: Introduction to Java Design Patterns
date: 2025-10-24T23:02:00.000+08:00
categories:
  - Programming Techniques
tags:
  - Code
  - Java
  - Programming
weight: 1
---
博客内容主要参考黑马程序员视频课程的设计模式笔记，面向《设计模式：可复用面向对象软件的基础》中介绍收录的经典的23个设计模式，进行阐述和介绍

# 初识设计模式

软件设计模式（Software Design Pattern），又称**设计模式**，是一套被反复使用、多数人知晓的、经过分类编目的、**代码设计经验的总结**。它描述的是在软件设计过程中不断发生的问题，以及该问题的解决方案。

- 设计模式的分类：
  
  - 创建型模式：描述如何创建对象，特点是“**对象的创建与使用分离**”。主要包含<u>单例、原型、工厂方法、抽象工厂、建造者</u>5种类型。
    
  - 结构型模式：描述如何将类或者对象**按某种布局组成更大的结构，丰富其功能**。主要包含：<u>代理、适配器、桥接、装饰、外观、享元、组合</u>7种类型。
    
  - 行为型模式：描述类与对象之间**怎样相互协作共同完成**单个对象无法完成的任务，以及**如何分配职责**。主要包含<u>模板方法、策略、命令、职责链、状态、观察者、中介者、迭代器、访问者、备忘录、解释器</u>11种类型。
    

## 软件设计原则

在软件开发中，为了提高软件系统的可维护性和可复用性，增加软件的可扩展性和灵活性，程序员要尽量根据一些原则来进行开发，以下介绍6条原则。

- **开闭原则**：对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。最方便的方式是使用接口和抽象类。
  软件中易变的细节可以从抽象派生来的实现类来进行扩展，<u>当软件需要发生变化时，只需要根据需求重新派生一个实现类来扩展</u>就可以。
  
- **里氏代换原则**：面向对象设计的基本原则。任何父类可以出现的地方，子类一定可以出现。即，<u>子类可以扩展父类的功能，但不能改变父类原有的功能</u>。也即子类继承以实现新功能时尽量不要重写父类方法。需要重写应该通过接口和抽象类进行扩展。
  
- **依赖倒转原则**：<u>高层模块不应该依赖低层模块，两者都应该依赖其抽象</u>；抽象不应该依赖细节，细节应该依赖抽象，即**面向抽象编程**，不要对实现编程。
  直观一点说，可扩展的变量应该是一个接口，而不是具体的实现类。
  
- **接口隔离原则**：一个类对另一个类的依赖应该建立在最小的接口上，一个类依赖的两个类（接口）之间不应该有重叠。
  
- **迪米特法则**：最少知识原则。当前对象本身、当前对象的成员对象、当前对象所创建的对象、当前对象的方法参数等，这些对象同当前对象存在关联、聚合或组合关系，可以直接访问这些对象的方法。如果两个软件实体无须直接通信，那么就不应当发生直接的相互调用，可以通过第三方转发该调用。
  
- **合成复用原则**：尽量先使用组合或者聚合等关联关系来实现，其次才考虑使用继承关系来实现。<u>即尽量使用接口进行组合，而不是直接进行分类的继承</u>。
  
  - 优势：维持了类的封装性，“黑箱复用”，而不是像继承复用一样将父类的实现细节暴露给子类，且耦合度低，灵活性高，动态引用。
    

# 创建者模式

描述如何创建对象，特点是“**对象的创建与使用分离**”。

## 单例设计模式

Single Pattern是java中最简单的设计模式之一，提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，**该类负责创建自己的对象**，同时确保**只有单个对象**被创建。这个类提供了一种**访问其唯一的对象的方式**，可以直接访问，**不需要实例化**该类的对象

单例模式主要有两种分类：

- 饿汉式：类加载就会导致该单实例对象被创建
  
- 懒汉式：类加载不会导致该单实例对象被创建，而是首次使用该对象时才会创建
  

### 单例模式的实现

#### 饿汉式——静态变量方式

```java
public class Singleton(){
    //私有构造方法
    private Sinbleton(){}
    
    // 类静态变量的直接初始化
    // 随着类加载而创建
    private static Singleton instance = new Singleton();
    // 也可以在静态代码块初始化
    static {
        instance = new Singleton();
    }    

    public static Singleton getInstance(){
        return instance;    
    }
}
```

优势在于提前的初始化，问题在于如果该对象足够大的话，而一直没有使用就会造成内存的浪费

#### 懒汉式——双重检查锁单例模式

```java
public class Singleton(){
    //私有构造方法
    private Sinbleton(){}
    
    private static Singleton instance;
 
    public static synchronized Singleton getInstance(){
        if(instance == null){
            instance = new Singleton();
        }
        return instance;    
    }

    // 双重检查锁方式
    public static Singleton getInstance(){
        if(instance == null){
            synchronized(Singleton.class){
                if(instance == null){
                    instance = new Singleton();
                }
            }
        }
        return instance;    
    }
}
```

上述的**双重检查锁单例模式（Double-Checked Locking Singleton）** 是一种非常好的单例实现模式，解决了单例、性能、线程安全问题，看上去完美无缺，但仍然存在一定问题。在多线程的情况下，可能会出现 **空指针问题**，出现问题的原因是JVM在实例化对象的时候会进行优化和指令重排序操作。解决方式可以使用```volatile```关键字，保证变量的可见性与有序性。

```java
public class Singleton(){
    //私有构造方法
    private Sinbleton(){}
    
    private static volatile Singleton instance;
    // 双重检查锁方式
    public static Singleton getInstance(){
        if(instance == null){
            synchronized(Singleton.class){
                if(instance == null){
                    instance = new Singleton();
                }
            }
        }
        return instance;    
    }
}
```

> **volatile详解**：上面的代码会出现问题的主要原因在于，new Singleton() **并不是一个原子操作**，在JVM底层，上述操作大致会被编译为三步操作：
> 
> 1. 分配内存空间
>   
> 2. 调用构造函数初始化对象
>   
> 3. 将内存地址赋值给变量 instance
>   
> 
> JVM 和 CPU 只保证指令在单一线程中一致，为了优化性能，可能会**重新排序指令**，可能重排序为：
> 
> 1. 分配内存空间
>   
> 2. 将内存地址赋值给变量 instance
>   
> 3. 调用构造函数初始化对象
>   
> 
> 这时线程便可能拿到一个未完全构造的对象。而**volatile**关键字便是用来解决这样的问题。它有两个关键作用：
> 
> 1. **禁止指令重排序优化**：保证在写入 instance 变量时，对象的构造操作（初始化）**一定在前**，
>   
> 2. **保证可见性（visibility）**：当一个线程修改了 instance，其他线程能立即看到最新的值，避免出现线程读到旧值的情况。
>   

#### 懒汉式——静态内部类实现

```java
   public class Singleton {
   
       //私有构造方法
       private Singleton() {}
   
       private static class SingletonHolder {
           private static final Singleton INSTANCE = new Singleton();
       }
   
       //对外提供静态方法获取该对象
       public static Singleton getInstance() {
           return SingletonHolder.INSTANCE;
       }
   }
```

第一次加载Singleton类时不会去初始化INSTANCE，只有第一次调用getInstance，虚拟机加载SingletonHolder并初始化INSTANCE，这样不仅能确保线程安全，也能保证 Singleton 类的唯一性。

#### 枚举方式

枚举类实现单例模式是极力推荐的单例实现模式，因为枚举类型是线程安全的，并且只会装载一次，写法简单，且是所用单例实现中唯一一种不会被破坏的单例实现模式（普通单例类若实现了 Serializable 接口，在反序列化时可能创建新对象），也是Effective Java推荐的写法。枚举方式是一种饿汉方式，由JVM保证单例和反序列化。

```java
public enum Singleton {
    INSTANCE;
}
// 使用方式
Singleton singleton = Singleton.INSTANCE;
```

### 存在的问题

#### 破坏单例模式

通过**序列化和反射**，除了枚举方式外，即使使用单例类，也能创建多个对象。

##### 序列化与反序列化

```java
  public class Singleton implements Serializable {
  
      //私有构造方法
      private Singleton() {}
  
      private static class SingletonHolder {
          private static final Singleton INSTANCE = new Singleton();
      }
  
      //对外提供静态方法获取该对象
      public static Singleton getInstance() {
          return SingletonHolder.INSTANCE;
  
      }
  }
  
    public class Test {
      public static void main(String[] args) throws Exception {
          //往文件中写对象
          //writeObject2File();
          //从文件中读取对象
          Singleton s1 = readObjectFromFile();
          Singleton s2 = readObjectFromFile();
  
          //判断两个反序列化后的对象是否是同一个对象,输出结果为false！
          System.out.println(s1 == s2);
      }
  
      private static Singleton readObjectFromFile() throws Exception {
          //创建对象输入流对象
          ObjectInputStream ois = new ObjectInputStream(new FileInputStream("C:\\Users\\Think\\Desktop\\a.txt"));
          //第一个读取Singleton对象
          Singleton instance = (Singleton) ois.readObject();
  
          return instance;
      }
  
      public static void writeObject2File() throws Exception {
          //获取Singleton类的对象
          Singleton instance = Singleton.getInstance();
          //创建对象输出流
          ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("C:\\Users\\Think\\Desktop\\a.txt"));
          //将instance对象写出到文件中
          oos.writeObject(instance);
      }
  }
```

解决方式：为类添加**readResolve**方法

```java
  public class Singleton implements Serializable {
  
      //私有构造方法
      private Singleton() {}
  
      private static class SingletonHolder {
          private static final Singleton INSTANCE = new Singleton();
      }
  
      //对外提供静态方法获取该对象
      public static Singleton getInstance() {
          return SingletonHolder.INSTANCE;
      }
      
      /**
       * 下面是为了解决序列化反序列化破解单例模式
       */
      private Object readResolve() {
          return SingletonHolder.INSTANCE;
      }
  }
```

以上方式只对于饿汉式有效，需要提前创建出一个对象。懒汉式也可以通过添加代码实现。

源码解析：

```java
  public final Object readObject() throws IOException, ClassNotFoundException{
      ...
      // if nested read, passHandle contains handle of enclosing object
      int outerHandle = passHandle;
      try {
          Object obj = readObject0(false);//重点查看readObject0方法
      .....
  }
      
  private Object readObject0(boolean unshared) throws IOException {
  	...
      try {
  		switch (tc) {
  			...
  			case TC_OBJECT:
  				return checkResolve(readOrdinaryObject(unshared));//重点查看readOrdinaryObject方法
  			...
          }
      } finally {
          depth--;
          bin.setBlockDataMode(oldMode);
      }    
  }
      
  private Object readOrdinaryObject(boolean unshared) throws IOException {
  	...
  	//isInstantiable 返回true，执行 desc.newInstance()，通过反射创建新的单例类，
      obj = desc.isInstantiable() ? desc.newInstance() : null; 
      ...
      // 在Singleton类中添加 readResolve 方法后 desc.hasReadResolveMethod() 方法执行结果为true
      if (obj != null && handles.lookupException(passHandle) == null && desc.hasReadResolveMethod()) {
      	// 通过反射调用 Singleton 类中的 readResolve 方法，将返回值赋值给rep变量
      	// 这样多次调用ObjectInputStream类中的readObject方法，继而就会调用我们定义的readResolve方法，所以返回的是同一个对象。
      	Object rep = desc.invokeReadResolve(obj);
       	...
      }
      return obj;
  }
```

##### 反射方式

反射也会破坏单例模式

```java
  public class Singleton {
      //私有构造方法
      private Singleton() {}
      
      private static volatile Singleton instance;
  
      //对外提供静态方法获取该对象
      public static Singleton getInstance() {
  
          if(instance != null) {
              return instance;
          }
  
          synchronized (Singleton.class) {
              if(instance != null) {
                  return instance;
              }
              instance = new Singleton();
              return instance;
          }
      }
  }
  
   public class Test {
      public static void main(String[] args) throws Exception {
          //获取Singleton类的字节码对象
          Class clazz = Singleton.class;
          //获取Singleton类的私有无参构造方法对象
          Constructor constructor = clazz.getDeclaredConstructor();
          //取消访问检查
          constructor.setAccessible(true);
  
          //创建Singleton类的对象s1
          Singleton s1 = (Singleton) constructor.newInstance();
          //创建Singleton类的对象s2
          Singleton s2 = (Singleton) constructor.newInstance();
  
          //判断通过反射创建的两个Singleton对象是否是同一个对象,输出为false！
          System.out.println(s1 == s2);
      }
  }
```

解决方式：在构造函数中添加额外的代码，避免反射调用构造函数。**只对于饿汉式有效**，因为它提前创建了对象

```java
  public class Singleton {
  
      //私有构造方法
      private Singleton() {
          /*
             反射破解单例模式需要添加的代码
          */
          if(instance != null) {
              throw new RuntimeException();
          }
      }
      
      private static volatile Singleton instance;
  
      //对外提供静态方法获取该对象
      public static Singleton getInstance() {
  
          if(instance != null) {
              return instance;
          }
  
          synchronized (Singleton.class) {
              if(instance != null) {
                  return instance;
              }
              instance = new Singleton();
              return instance;
          }
      }
  }
```

### JDK源码解析

**Runtime**类使用的就是单例模式，具体使用的是饿汉式，源码如下：

```java
   public class Runtime {
       private static Runtime currentRuntime = new Runtime();
   
       /**
        * Returns the runtime object associated with the current Java application.
        * Most of the methods of class <code>Runtime</code> are instance
        * methods and must be invoked with respect to the current runtime object.
        *
        * @return  the <code>Runtime</code> object associated with the current
        *          Java application.
        */
       public static Runtime getRuntime() {
           return currentRuntime;
       }
   
       /** Don't let anyone else instantiate this class */
       private Runtime() {}
   
   
       ...
   }
    public class RuntimeDemo {
       public static void main(String[] args) throws IOException {
           //获取Runtime类对象
           Runtime runtime = Runtime.getRuntime();
   
           //返回 Java 虚拟机中的内存总量。
           System.out.println(runtime.totalMemory());
           //返回 Java 虚拟机试图使用的最大内存量。
           System.out.println(runtime.maxMemory());
   
           //创建一个新的进程执行指定的字符串命令，返回进程对象
           Process process = runtime.exec("ipconfig");
           //获取命令执行后的结果，通过输入流获取
           InputStream inputStream = process.getInputStream();
           byte[] arr = new byte[1024 * 1024* 100];
           int b = inputStream.read(arr);
           System.out.println(new String(arr,0,b,"gbk"));
       }
   }
```
