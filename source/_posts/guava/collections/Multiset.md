---
uuid: bbaf6f25-c0ab-11ec-92a1-7557b2313227
title: Guava Multiset
categories: Java
tags:
  - guava
abbrlink: 6b775b82
---

# Guava Multiset接口

Multiset接口扩展设置有重复的元素，并提供了各种实用的方法来处理这样的元素在集合中出现。

## 接口声明

以下是com.google.common.collect.Multiset<E>接口的声明：

```java
@GwtCompatible
public interface Multiset<E> extends Collection<E>
```

## 接口方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **boolean add(E element)**  添加一个出现的指定元素这个multiset。 |
| 2    | **int add(E element, int occurrences)**  增加大量的元素到这个multiset。 |
| 3    | **boolean contains(Object element)**  确定此多集是否包含指定的元素。 |
| 4    | **boolean containsAll(Collection<?> elements)**  返回true，如果这个多集至少包含一个出现的指定集合中的所有元素。 |
| 5    | **int count(Object element)**  返回出现的元素的在该multiset的数目（元素的数量）。 |
| 6    | **Set<E> elementSet()**  返回集包含在此多集不同的元素。      |
| 7    | **Set<Multiset.Entry<E>> entrySet()**  返回此多集的内容的视图，分组在Multiset.Entry实例中，每一个都提供了多集的一个元素和元素的计数。 |
| 8    | **boolean equals(Object object)** 比较指定对象与此multiset是否相等。 |
| 9    | **int hashCode()**  返回此multiset的哈希码。                 |
| 10   | **Iterator<E> iterator()**  返回一个迭代在这个集合中的元素。 |
| 11   | **boolean remove(Object element)**  移除此多集multiset的单个出现的指定元素，如果存在。 |
| 12   | **int remove(Object element, int occurrences)**  删除了一些出现，从该多集multiset的指定元素。 |
| 13   | **boolean removeAll(Collection<?> c)**  删除所有这一切都包含在指定集合（可选操作）在此集合的元素。 |
| 14   | **boolean retainAll(Collection<?> c)**  保持那些包含在指定collection（可选操作）在此只集合中的元素。 |
| 15   | **int setCount(E element, int count)**  添加或删除，使得该元素达到所期望的计数的元件的必要出现。 |
| 16   | **boolean setCount(E element, int oldCount, int newCount)**  			有条件设置元素的计数为一个新值，如在setCount（对象，INT）中所述，条件是该元素预期的当前计数。 |
| 17   | **String toString()**  返回该对象的字符串表示。              |

## 方法继承

此接口继承从以下接口方法：

- java.util.Collection

## Multiset 示例

使用所选择的编辑器创建下面的java程序，比如说 C:/> Guava

*GuavaTester.java*

```java
import java.util.Iterator;
import java.util.Set;

import com.google.common.collect.HashMultiset;
import com.google.common.collect.Multiset;

public class GuavaTester {

   public static void main(String args[]){
      //create a multiset collection
      Multiset<String> multiset = HashMultiset.create();
      multiset.add("a");
      multiset.add("b");
      multiset.add("c");
      multiset.add("d");
      multiset.add("a");
      multiset.add("b");
      multiset.add("c");
      multiset.add("b");
      multiset.add("b");
      multiset.add("b");
      //print the occurrence of an element
      System.out.println("Occurrence of 'b' : "+multiset.count("b"));
      //print the total size of the multiset
      System.out.println("Total Size : "+multiset.size());
      //get the distinct elements of the multiset as set
      Set<String> set = multiset.elementSet();
      //display the elements of the set
      System.out.println("Set [");
      for (String s : set) {			
         System.out.println(s);		    
      }
      System.out.println("]");
      //display all the elements of the multiset using iterator
      Iterator<String> iterator  = multiset.iterator();
      System.out.println("MultiSet [");
      while(iterator.hasNext()){
         System.out.println(iterator.next());
      }
      System.out.println("]");		
      //display the distinct elements of the multiset with their occurrence count
      System.out.println("MultiSet [");
      for (Multiset.Entry<String> entry : multiset.entrySet())
      {
         System.out.println("Element: "+entry.getElement() +", Occurrence(s): " + entry.getCount());		    
      }
      System.out.println("]");		

      //remove extra occurrences 
      multiset.remove("b",2);
      //print the occurrence of an element
      System.out.println("Occurence of 'b' : "+multiset.count("b"));
   }	
}
```
