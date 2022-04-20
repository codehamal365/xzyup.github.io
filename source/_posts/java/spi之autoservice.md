---
title: SPI之autoservice
tags:
  - spi
abbrlink: '4871'
---


之前提到SPI需要在/META-INF/service路径下，以对应api为文件名具体实现类为内容的文件，这样做比较麻烦。我们可以利用Google Auto Service是如何利用Annotation Processor来帮助实现SPI的。

具体实现如下：

引入依赖

```xml
 <dependency>
            <groupId>com.google.auto.service</groupId>
            <artifactId>auto-service</artifactId>
            <version>1.0</version>
            <optional>true</optional>
        </dependency>
```

```java
@AutoService(StandardService.class)
public class CStandardServiceImpl implements StandardService {
    @Override
    public void offerService() {
        System.out.println("c service");
    }
}
```

我们分析下其中的具体实现。

首先看一下auto-service-annotation库，只有一个AutoService注解定义，其value值即为SPI的服务接口类，如下所示：

```java

/**
 * An annotation for service providers as described in {@link java.util.ServiceLoader}. The
 * annotation processor generates the configuration files that allow the annotated class to be
 * loaded with {@link java.util.ServiceLoader#load(Class)}.
 *
 * <p>The annotated class must conform to the service provider specification. Specifically, it must:
 *
 * <ul>
 *   <li>be a non-inner, non-anonymous, concrete class
 *   <li>have a publicly accessible no-arg constructor
 *   <li>implement the interface type returned by {@code value()}
 * </ul>
 */
@Documented
@Retention(CLASS)
@Target(TYPE)
public @interface AutoService {
  /** Returns the interfaces implemented by this service provider. */
  Class<?>[] value();
}

```

可以看出，其注解仅保留于源码级别，用于编译时Annotation Processor的源码分析，并利用分析结果进行META-INF/services下的服务文件生成。

 仅接着，就要正式看一下auto-service的具体实现了，核心代码主要就是AutoServiceProcessor.java以及熟悉的META-INF/services/javax.annotation.processing.Processor服务文件。看过上节的人可能就要说了这是SPI，然而实际并非如此，这实际上是Annotation Processor的实现格式。

 Annotation Processor的代码实现核心包括一个实现Processor接口的类（一般继承AbstractProcessor抽象类）和一个Processor服务文件（内容就是实现类，例如AutoService的实现类com.google.auto.service.processor.AutoServiceProcessor）。虽然和SPI类似，甚至在实现方式上可以看成是Processor接口的SPI服务，但是SPI属于运行时，Annotation Processor属于编译时行为，两者还是有本质区别的。
![](https://raw.githubusercontent.com/xzyup/image/master/202203191602916.png)

如上引用一个比较经典的图，Javac的Annotation Processing实际上是一个循环的过程，在每一轮（Round）结束后，编译器会判断是否有新的代码生成，如有则进入下一轮分析新代码并调用注解处理器，如无代码生成，此时会再进行最后一轮，通知Annotation Processor处理结束，大家需要特别注意这最后一轮的概念。

接下来就看看AutoServiceProcessor是如何实现的：

1. getSupportedAnnotationType：该方法返回值表示了注解处理器所处理的注解类型，AutoServiceProvider当然就是AutoService注解；除了覆写该方法外，还可以通过@SupportedAnnotationTypes注解来替代。

   ~~~java
   @Override
   public ImmutableSet<String> getSupportedAnnotationTypes() {
       return ImmutableSet.of(AutoService.class.getName());
   }
   ~~~

2. getSupportedSourceVersion：该方法返回值表示了注解处理器所支持的最新JDK版本，同样也可使用@SupportedSourceVersion来替代。 

   ```java
   @Override
   public SourceVersion getSupportedSourceVersion() {
       return SourceVersion.latestSupported();
   }
   ```

3. 此外在AutoServiceProcessor类上还有一个不容忽视的注解@SupportedOptions，它也一样有一个相同的方法getSupportedOptions，该注解表示所支持的javac编译参数选项，在javac中可以通过-Akey[=value]这种方式指定该参数选项，但是实际上如果不指定@SupportedOptions，而传入了该参数，javac编译器会提示警告信息：
   AutoServiceProcessor提供了debug和verify两个选项，debug选项传入时（-Adebug），会开启Debug日志，如下所示：

   ```java
   private void log(String msg) {
       if (processingEnv.getOptions().containsKey("debug")) {
           processingEnv.getMessager().printMessage(Kind.NOTE, msg);
       }
   }
   ```

    而verify则表示是否强制检查@AutoService的标注类和@AutoService的value所对应的服务接口是否实现关系。

4. 还有一个比较重要的成员变量processingEnv，它在AbstractProcessor的init方法中传入，实际上就是编译期上下文工具级，除了上述示例中getOptions方法获取编译选项、getMessager方法获取消息对象用于消息打印（如下所示）外；此外还有一个getFiler方法获取Filer对象，用于生成源文件、class文件和辅助文件，可以说是Annotation Processor的核心，后续生成服务文件时将会用到，此外还有getTypeUtils和getElementUtils等代码工具类。

5. 最为核心的就是process方法（如下所示），其返回值表示该注解的处理是否继续传给后续的注册处理器，入参annotations和我们之前所定义的getSupportedAnnotationTypes相对应，RoundEnvironment就表示每一轮注解处理的上下文环境（看一下直接的注解处理流程图就明白了），代码实现很清晰，AutoService先收集每一轮的代码信息，判断其标签并缓存待生成的服务文件信息，直到最后一轮没有新代码生成时，开始生成或更新服务配置文件。

   ```java
   private boolean processImpl(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
       if (roundEnv.processingOver()) {
           generateConfigFiles();
       } else {
           processAnnotations(annotations, roundEnv);
       }
       return true;
   }
   ```

6. 而processAnnotations是如何收集信息的呢？也很简单，就是找到每一轮的所有AutoService标注的类文件，并获取各个类文件中@AutoService里面标注的服务接口，将服务接口名和服务实现类名称缓存值Multimap中

7. 最后，根据Multimap中的信息，生成META-INF/services下服务文件，而生成的核心方法就是使用Filer，具体逻辑带大家简单看一下，首先是检查是否已有META-INF/services/下对应的服务文件，如果有则将其内容读取并缓存值列表中(allServices)：



总的说来AutoService实现还是很简单的，利用Annotation Processor机制为各个SPI服务以及Annotation Processor生成META-INF/services文件下的服务文件，但是确实是理解Annotation Processor机制的比较好的入门方式。目前还没有涉及到代码的生成，接下来的章节就将看看如何在注解处理器中生成代码。

---

