---
uuid: bbaf2102-c0ab-11ec-92a1-7557b2313227
title: Guava Ordering
categories: Java
tags:
  - guava
abbrlink: acc53003
---

# Guava Ordering类

Ordering(排序)可以被看作是一个丰富的比较具有增强功能的链接，多个实用方法，多类型排序功能等。

## 	类声明

以下是com.google.common.collect.Ordering<T>类的声明：

```java
@GwtCompatible
public abstract class Ordering<T> extends Object implements Comparator<T>
```

## 	类方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **static Ordering<Object> allEqual()**  	返回一个排序，它把所有的值相等，说明“没有顺序。”通过这个顺序以任何稳定的排序算法的结果，在改变没有顺序元素。 |
| 2    | **static Ordering<Object> arbitrary()**  	返回一个任意顺序对所有对象，其中compare(a, b) == 0 意味着a == b（身份平等）。 |
| 3    | **int binarySearch(List<? extends T> sortedList, T key)**  	搜索排序列表使用键的二进制搜索算法。 |
| 4    | **abstract int compare(T left, T right)**  比较两个参数的顺序。 |
| 5    | **<U extends T> Ordering<U> compound(Comparator<? super U> secondaryComparator)**  			返回首先使用排序这一点，但它排序中的“tie”，然后委托给secondaryComparator事件。 |
| 6    | **static <T> Ordering<T> compound(Iterable<? extends Comparator<? super T>> comparators)**  			返回一个排序它尝试每个给定的比较器，以便直到一个非零结果找到，返回该结果，并返回零仅当所有比较器返回零。 |
| 7    | **static <T> Ordering<T> explicit(List<T> valuesInOrder)**  返回根据它们出现的定列表中的顺序比较对象进行排序。 |
| 8    | **static <T> Ordering<T> explicit(T leastValue, T... remainingValuesInOrder)**  返回根据它们所赋予本方法的顺序进行比较的对象进行排序。 |
| 9    | **static <T> Ordering<T> from(Comparator<T> comparator)**  返回基于现有的比较实例进行排序。 |
| 10   | **<E extends T> List<E> greatestOf(Iterable<E> iterable, int k)**  	返回根据这个顺序给出迭代，为了从最大到最小的k个最大的元素。 |
| 11   | **<E extends T> List<E> greatestOf(Iterator<E> iterator, int k)**  返回从给定的迭代器按照这个顺序，从最大到最小k个最大的元素。 |
| 12   | **<E extends T> ImmutableList<E> immutableSortedCopy(Iterable<E> elements)**  			返回包含的元素排序这种排序的不可变列表。 |
| 13   | **boolean isOrdered(Iterable<? extends T> iterable)**  返回true如果在迭代后的第一个的每个元素是大于或等于在它之前，根据该排序的元素。 |
| 14   | **boolean isStrictlyOrdered(Iterable<? extends T> iterable)**  返回true如果在迭代后的第一个的每个元素是严格比在它之前，根据该排序的元素更大。 |
| 15   | **<E extends T> List<E> leastOf(Iterable<E> iterable, int k)**  	返回根据这个顺序给出迭代，从而从低到最大的k个最低的元素。 |
| 16   | **<E extends T> List<E> leastOf(Iterator<E> elements, int k)**  	返回第k从给定的迭代器，按照这个顺序从最低到最大至少元素。 |
| 17   | **<S extends T> Ordering<Iterable<S>> lexicographical()**  	返回一个新的排序它通过比较对应元素两两直到非零结果发现排序迭代;规定“字典顺序”。 |
| 18   | **<E extends T> E max(E a, E b)**  	返回两个值按照这个顺序的较大值。 |
| 19   | **<E extends T> E max(E a, E b, E c, E... rest)**  返回指定的值，根据这个顺序是最大的。 |
| 20   | **<E extends T> E max(Iterable<E> iterable)**  	返回指定的值，根据这个顺序是最大的。 |
| 21   | **<E extends T> E max(Iterator<E> iterator)**  	返回指定的值，根据这个顺序是最大的。 |
| 22   | **<E extends T> E min(E a, E b)**  	返回两个值按照这个顺序的较小者。 |
| 23   | **<E extends T> E min(E a, E b, E c, E... rest)**  返回最少指定的值，根据这个顺序。 |
| 24   | **<E extends T> E min(Iterable<E> iterable)**  返回最少指定的值，根据这个顺序。 |
| 25   | **<E extends T> E min(Iterator<E> iterator)**  返回最少指定的值，根据这个顺序。 |
| 26   | **static <C extends Comparable> Ordering<C> natural()**  返回使用值的自然顺序排序序列化。 |
| 27   | **<S extends T> Ordering<S> nullsFirst()**  返回对待null小于所有其他值，并使用此来比较非空值排序。 |
| 28   | **<S extends T> Ordering<S> nullsLast()**  返回对待null作为大于所有其他值，并使用这个顺序来比较非空值排序。 |
| 29   | **<F> Ordering<F> onResultOf(Function<F,? extends T> function)**  	返回一个新的排序在F上，首先应用功能给它们，然后比较使用此这些结果的顺序元素。 |
| 30   | **<S extends T> Ordering<S> reverse()**  	返回相反顺序; 顺序相当于Collections.reverseOrder（Comparator）。 |
| 31   | **<E extends T> List<E> sortedCopy(Iterable<E> elements)**  返回包含的元素排序此排序可变列表;使用这个只有在结果列表可能需要进一步修改，或可能包含null。 |
| 32   | **static Ordering<Object> usingToString()**  返回由它们的字符串表示的自然顺序，toString()比较对象进行排序。 |

## 	方法继承

这个类从以下类继承的方法：

- java.lang.Object

## 	Ordering 示例

使用所选择的编辑器，创建下面的java程序比如 C:/> Guava

GuavaTester.java

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import com.google.common.collect.Ordering;

public class GuavaTester {
   public static void main(String args[]){
      List<Integer> numbers = new ArrayList<Integer>();
      numbers.add(new Integer(5));
      numbers.add(new Integer(2));
      numbers.add(new Integer(15));
      numbers.add(new Integer(51));
      numbers.add(new Integer(53));
      numbers.add(new Integer(35));
      numbers.add(new Integer(45));
      numbers.add(new Integer(32));
      numbers.add(new Integer(43));
      numbers.add(new Integer(16));

      Ordering ordering = Ordering.natural();
      System.out.println("Input List: ");
      System.out.println(numbers);		
         
      Collections.sort(numbers,ordering );
      System.out.println("Sorted List: ");
      System.out.println(numbers);
         
      System.out.println("======================");
      System.out.println("List is sorted: " + ordering.isOrdered(numbers));
      System.out.println("Minimum: " + ordering.min(numbers));
      System.out.println("Maximum: " + ordering.max(numbers));
         
      Collections.sort(numbers,ordering.reverse());
      System.out.println("Reverse: " + numbers);

      numbers.add(null);
      System.out.println("Null added to Sorted List: ");
      System.out.println(numbers);		

      Collections.sort(numbers,ordering.nullsFirst());
      System.out.println("Null first Sorted List: ");
      System.out.println(numbers);
      System.out.println("======================");

      List<String> names = new ArrayList<String>();
      names.add("Ram");
      names.add("Shyam");
      names.add("Mohan");
      names.add("Sohan");
      names.add("Ramesh");
      names.add("Suresh");
      names.add("Naresh");
      names.add("Mahesh");
      names.add(null);
      names.add("Vikas");
      names.add("Deepak");

      System.out.println("Another List: ");
      System.out.println(names);

	  Collections.sort(names,ordering.nullsFirst().reverse());
      System.out.println("Null first then reverse sorted list: ");
      System.out.println(names);
   }
}
```
