---
uuid: bbaf210a-c0ab-11ec-92a1-7557b2313227
title: SPI机制
categories: Java
tags:
  - spi
abbrlink: f13620b0
---

# Java中SPI机制

# 1 SPI是什么

SPI全称Service Provider Interface，是Java提供的一套用来被第三方实现或者扩展的API，它可以用来启用框架扩展和替换组件。

整体机制图如下：

![](https://raw.githubusercontent.com/xzyup/image/master/202203191602301.png)

Java SPI 实际上是“**基于接口的编程＋策略模式＋配置文件**”组合实现的动态加载机制。

系统设计的各个抽象，往往有很多不同的实现方案，在面向的对象的设计里，一般推荐模块之间基于接口编程，模块之间不对实现类进行硬编码。一旦代码里涉及具体的实现类，就违反了可拔插的原则，如果需要替换一种实现，就需要修改代码。为了实现在模块装配的时候能不在程序里动态指明，这就需要一种服务发现机制。
 Java SPI就是提供这样的一个机制：为某个接口寻找服务实现的机制。有点类似IOC的思想，就是将装配的控制权移到程序之外，在模块化设计中这个机制尤其重要。所以SPI的核心思想就是**解耦**。

# 2 使用场景

概括地说，适用于：**调用者根据实际使用需要，启用、扩展、或者替换框架的实现策略**

比较常见的例子：

- 数据库驱动加载接口实现类的加载
   JDBC加载不同类型数据库的驱动
- 日志门面接口实现类加载
   SLF4J加载不同提供商的日志实现类
- Spring
   Spring中大量使用了SPI,比如：对servlet3.0规范对ServletContainerInitializer的实现、自动类型转换Type Conversion SPI(Converter SPI、Formatter SPI)等
- Dubbo
   Dubbo中也大量使用SPI的方式实现框架的扩展, 不过它对Java提供的原生SPI做了封装，允许用户扩展实现Filter接口

# 3 使用介绍

要使用Java SPI，需要遵循如下约定：

- 1、当服务提供者提供了接口的一种具体实现后，在jar包的META-INF/services目录下创建一个以“接口全限定名”为命名的文件，内容为实现类的全限定名；
- 2、接口实现类所在的jar包放在主程序的classpath中；
- 3、主程序通过java.util.ServiceLoder动态装载实现模块，它通过扫描META-INF/services目录下的配置文件找到实现类的全限定名，把类加载到JVM；
- 4、SPI的实现类必须携带一个不带参数的构造方法；

## 示例代码

## song-parser 项目

song-parser 项目定义了通用的歌曲解析接口，并不提供具体的解析实现。在 song-parser 项目定义了下面两个关键的接口和类：Parser 接口、ParserManager 类。

- Parser 接口

  定义了抽象的解析方法，传入歌曲的数据，返回歌曲的信息。

  ```java
  public interface Parser {
      Song parse(byte[] data) throws Exception;
  }
  ```

- ParseManager 类

  主要包括两个三个部分：

  `loadInitialParsers()` 用于程序启动时初始化所有的歌曲解析器。

  `ParserManager.registerParser()`用于歌曲解析器的注册。

  `ParserManager.getSong()`提供了获取歌曲信息的方法。

  ```java
  public class ParserManager {
  
      private final static CopyOnWriteArrayList<ParserInfo> registeredParsers = new CopyOnWriteArrayList<>();
  
      static {
          loadInitialParsers();
          System.out.println("SongParser initialized");
      }
  
      private static void loadInitialParsers() {
          ServiceLoader<Parser> loadedParsers = ServiceLoader.load(Parser.class);
          Iterator<Parser> driversIterator = loadedParsers.iterator();
          try{
              while(driversIterator.hasNext()) {
                  driversIterator.next();
              }
          } catch(Throwable t) {
              // Do nothing
          }
      }
  
      public static synchronized void registerParser(Parser parser) {
          registeredParsers.add(new ParserInfo(parser));
      }
  
      public static Song getSong(byte[] data) {
          for (ParserInfo parserInfo : registeredParsers) {
              try {
                  Song song = parserInfo.parser.parse(data);
                  if (song != null) {
                      return song;
                  }
              } catch (Exception e) {
                  //wrong parser, ignored it.
              }
          }
          throw new ParserNotFoundException("10001", "Can not find corresponding data:" + new String(data));
      }
  }
  ```

  其实上面的几个方法对应了 Service Provider Framework 的四个概念：

  - **Service Interface 服务接口**，这里对应 Song 接口。
  - **Provider Registration API 用户注册接口**，这里对应 ParserManager.registerParser() 方法。
  - **Service Access API 获取服务实例方法**，这里对应 ParserManager.getSong() 方法。
  - **Service Provider Interface 创建服务实现的接口**，这里对应 Parser 接口。

  所有借助 Java SPI 机制实现的框架，除了 **Service Interface 服务接口**不是必须的之外，其他三个都是必须要有的。

  这里我们用 mp3 歌曲解析器为例，来看看到底是如何实现的插件式的歌曲解析的。

  在 song-parse-mp3 项目中有两个类和一个描述文件，分别是：Parser 文件、Parser 类和 Mp3Parser 类。

  - Parser 文件

    该文件位于`/resources/META-INF/services`目录下，包含如下地址：`com.xiaohei.demo.Parser`，表示歌曲解析的具体实现类。

  - Parser 类

    在 Parser 类中，其调用 ParserManager.registerParser() 类将解析器注册到一个 List 集合中。

    ```java
    public class Parser extends Mp3Parser implements com.chenshuyi.demo.Parser {
        static
        {
            try
            {
                ParserManager.registerParser(new Parser());
            }
            catch (Exception e)
            {
                throw new RuntimeException("Can't register parser!");
            }
        }
    }
    ```

  - Mp3Parser 类

    而在 Parser.parse() 方法中，则实现了具体的解析业务逻辑。

    ```java
    public class Mp3Parser implements Parser {
    
        public final byte[] FORMAT = "MP3".getBytes();
    
        public final int FORMAT_LENGTH = FORMAT.length;
    
        @Override
        public Song parse(byte[] data) throws Exception{
            if (!isDataCompatible(data)) {
                throw new Exception("data format is wrong.");
            }
            //parse data by mp3 format type
            return new Song("刘千楚", "mp3", "《北京东路的日子》", 220L);
        }
    
        private boolean isDataCompatible(byte[] data) {
            byte[] format = Arrays.copyOfRange(data, 0, FORMAT_LENGTH);
            return Arrays.equals(format, FORMAT);
        }
    }
    ```

    当我们调用以下语句去获取歌曲信息时，因为 ParserManager.getSong() 是静态方法，所以会先初始化 ParserManager 类。

    ```
    Song song = ParserManager.getSong(mockSongData("MP3"));
    ```

    在 ParserManager 类中有下面这段代码：

    ```java
    static {
        loadInitialParsers();
        System.out.println("SongParser initialized");
    }
    ```

    在 loadInitialParsers() 方法中，调用了 Java 的 ServiceLoader 类获取 Parser 接口的所有实现。

    ```java
    private static void loadInitialParsers() {
        ServiceLoader<Parser> loadedParsers = ServiceLoader.load(Parser.class);
        Iterator<Parser> driversIterator = loadedParsers.iterator();
        try{
            while(driversIterator.hasNext()) {
                driversIterator.next();
            }
        } catch(Throwable t) {
            // Do nothing
        }
    }
    ```

    当 ParserManager 初始化完成之后，就调用 getSong() 静态方法。

    ```java
    public static Song getSong(byte[] data) {
        for (ParserInfo parserInfo : registeredParsers) {
            try {
                Song song = parserInfo.parser.parse(data);
                if (song != null) {
                    return song;
                }
            } catch (Exception e) {
                //wrong parser, ignored it.
            }
        }
        throw new ParserNotFoundException("10001", "Can not find corresponding data:" + new String(data));
    }
    ```

    其实 loadInitialParsers() 方法运行之后，是将所有 Parser 接口的所有视线都放到了 ParserManager.registeredParsers 这个 List 中。

    `[参考地址](https://github.com/chenyurong/song-parser-spi-demo)`

# 4 原理解析

首先看ServiceLoader类的签名类的成员变量：

```java
public final class ServiceLoader<S> implements Iterable<S>{
private static final String PREFIX = "META-INF/services/";

    // 代表被加载的类或者接口
    private final Class<S> service;

    // 用于定位，加载和实例化providers的类加载器
    private final ClassLoader loader;

    // 创建ServiceLoader时采用的访问控制上下文
    private final AccessControlContext acc;

    // 缓存providers，按实例化的顺序排列
    private LinkedHashMap<String,S> providers = new LinkedHashMap<>();

    // 懒查找迭代器
    private LazyIterator lookupIterator;
  
    ......
}
```

参考具体ServiceLoader具体源码，代码量不多，加上注释一共587行，梳理了一下，实现的流程如下：

- 1 应用程序调用ServiceLoader.load方法
   ServiceLoader.load方法内先创建一个新的ServiceLoader，并实例化该类中的成员变量，包括：

  - loader(ClassLoader类型，类加载器)
  - acc(AccessControlContext类型，访问控制器)
  - providers(LinkedHashMap<String,S>类型，用于缓存加载成功的类)
  - lookupIterator(实现迭代器功能)

- 2 应用程序通过迭代器接口获取对象实例
   ServiceLoader先判断成员变量providers对象中(LinkedHashMap<String,S>类型)是否有缓存实例对象，如果有缓存，直接返回。
   如果没有缓存，执行类的装载，实现如下：

- (1) 读取META-INF/services/下的配置文件，获得所有能被实例化的类的名称，值得注意的是，ServiceLoader**可以跨越jar包获取META-INF下的配置文件**，具体加载配置的实现代码如下：

  ```java
          try {
              String fullName = PREFIX + service.getName();
              if (loader == null)
                  configs = ClassLoader.getSystemResources(fullName);
              else
                  configs = loader.getResources(fullName);
          } catch (IOException x) {
              fail(service, "Error locating configuration files", x);
          }
  ```

  (2) 通过反射方法Class.forName()加载类对象，并用instance()方法将类实例化。

  (3) 把实例化后的类缓存到providers对象中，(LinkedHashMap<String,S>类型）然后返回实例对象。
