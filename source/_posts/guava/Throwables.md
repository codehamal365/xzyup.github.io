---
uuid: bbaf2109-c0ab-11ec-92a1-7557b2313227
title: Guava Throwables
categories: Java
tags:
  - guava
abbrlink: 43913d08
---

# Guava Throwables类

Throwable类提供了相关的Throwable接口的实用方法。

## 	类声明

以下是com.google.common.base.Throwables类的声明：

```java
public final class Throwables extends Object
```

## 	类方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **static List<Throwable> getCausalChain(Throwable throwable)**  			获取一个Throwable的原因链的列表。 |
| 2    | **static Throwable getRootCause(Throwable throwable)**  			返回抛出的最里面的原因。 |
| 3    | **static String getStackTraceAsString(Throwable throwable)**  			返回包含toString()的结果字符串，随后完整抛出，递归的堆栈跟踪。 |
| 4    | **static RuntimeException propagate(Throwable throwable)**  			传播抛出原样如果RuntimeException或Error是一个实例，否则作为最后的报告，把它包装在一个RuntimeException，然后传播。 |
| 5    | **static <X extends Throwable> void propagateIfInstanceOf(Throwable throwable, Class<X> declaredType)**  			传播抛出对象完全按原样，当且仅当它是declaredType的一个实例。 |
| 6    | **static void propagateIfPossible(Throwable throwable)**  			传播抛出对象完全按原样，当且仅当它是RuntimeException或Error的一个实例。 |
| 7    | **static <X extends Throwable> void propagateIfPossible(Throwable throwable, Class<X> declaredType)**  			传播抛出对象完全按原样，当且仅当它是RuntimeException，错误或的declaredType的一个实例。 |
| 8    | **static <X1 extends Throwable,X2 extends Throwable>void propagateIfPossible(Throwable throwable, Class<X1> declaredType1, Class<X2> declaredType2)**  			传播抛出对象完全按原样，当且仅当它是RuntimeException，Error，declaredType1或declaredType2的一个实例。 |

## 继承的方法

这个类继承了以下类方法：

- java.lang.Object

## Throwables示例

创建使用所选择的任何编辑器下面的java程序，比如 **C:/> Guava**

*GuavaTester.java*

```java
import java.io.IOException;

import com.google.common.base.Objects;
import com.google.common.base.Throwables;

public class GuavaTester {
   public static void main(String args[]){
      GuavaTester tester = new GuavaTester();
      try {
         tester.showcaseThrowables();
      } catch (InvalidInputException e) {
         //get the root cause
         System.out.println(Throwables.getRootCause(e));
      }catch (Exception e) {
         //get the stack trace in string format
         System.out.println(Throwables.getStackTraceAsString(e));				
      }

      try {
         tester.showcaseThrowables1();			
      }catch (Exception e) {
         System.out.println(Throwables.getStackTraceAsString(e));				
      }
   }

   public void showcaseThrowables() throws InvalidInputException{
      try {
         sqrt(-3.0);			
      } catch (Throwable e) {
         //check the type of exception and throw it
         Throwables.propagateIfInstanceOf(e, InvalidInputException.class);		
         Throwables.propagate(e);
      }	
   }

   public void showcaseThrowables1(){
      try {			
         int[] data = {1,2,3}; 
         getValue(data, 4);			
      } catch (Throwable e) {        
         Throwables.propagateIfInstanceOf(e, IndexOutOfBoundsException.class);		
         Throwables.propagate(e);
      }	
   }

   public double sqrt(double input) throws InvalidInputException{
      if(input < 0) throw new InvalidInputException();
      return Math.sqrt(input);
   }

   public double getValue(int[] list, int index) throws IndexOutOfBoundsException {
      return list[index];
   }

   public void dummyIO() throws IOException {
      throw new IOException();
   }
}

class InvalidInputException extends Exception {
}
```

---eption {
}
```

---