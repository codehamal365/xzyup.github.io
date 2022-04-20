---
uuid: bbaf6f24-c0ab-11ec-92a1-7557b2313227
title: Guava Multimap
categories: Java
tags:
  - guava
abbrlink: 1eced4e5
---

#  Guava Multimap类

多重映射接口扩展映射，使得其键一次可被映射到多个值。

## 接口声明

以下是com.google.common.collect.Multimap<K，V>接口的声明：

```java
@GwtCompatible
public interface Multimap<K,V>
```

## 接口方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **Map<K,Collection<V>> asMap()**  返回此multimap中的视图，从每个不同的键在键的关联值的非空集合映射。 |
| 2    | **void clear()**  	将删除所有multimap中的键值对，留下空。 |
| 3    | **boolean containsEntry(Object key, Object value)**  	返回true如果此多重映射包含至少一个键 - 值对用键键和值value。 |
| 4    | **boolean containsKey(Object key)**  返回true，如果这个multimap中至少包含一个键值对的键key。 |
| 5    | **boolean containsValue(Object value)**  	返回true，如果这个multimap至少包含一个键值对的值值。 |
| 6    | **Collection<Map.Entry<K,V>> entries()**  返回包含在此multimap中，为Map.Entry的情况下，所有的键 - 值对的视图集合。 |
| 7    | **boolean equals(Object obj)**  比较指定对象与此多重映射是否相等。 |
| 8    | **Collection<V> get(K key)**  返回，如果有的话，在这个multimap中键关联的值的视图集合。 |
| 9    | **int hashCode()**  	返回此多重映射的哈希码。             |
| 10   | **boolean isEmpty()**  	返回true，如果这个multimap中未包含键 - 值对。 |
| 11   | **Multiset<K> keys()**  返回一个视图集合包含从每个键值对这个multimap中的关键，没有折叠重复。 |
| 12   | **Set<K> keySet()**  	Returns a view collection of all distinct keys contained in this multimap. |
| 13   | **boolean put(K key, V value)**  	存储键 - 值对在这个multimap中。 |
| 14   | **boolean putAll(K key, Iterable<? extends V> values)**  			存储一个键 - 值对在此multimap中的每个值，都使用相同的键 key。 |
| 15   | **boolean putAll(Multimap<? extends K,? extends V> multimap)**  			存储了所有键 - 值对多重映射在这个multimap中，通过返回 multimap.entries() 的顺序. |
| 16   | **boolean remove(Object key, Object value)**  	删除一个键 - 值对用键键，并从该多重映射的值的值，如果这样的存在。 |
| 17   | **Collection<V> removeAll(Object key)**  	删除与键键关联的所有值。 |
| 18   | **Collection<V> replaceValues(K key, Iterable<? extends V> values)**  			存储与相同的键值，替换任何现有值的键的集合。 |
| 19   | int size() 返回此多重映射键 - 值对的数量。                   |
| 20   | **Collection<V> values()**  	返回一个视图集合包含从包含在该multimap中的每个键 - 值对的值，而不发生重复 (so values().size() == size()). |

## Multimap 示例

使用所选择的任何编辑器创建下面的java程序 **C:/> Guava**

*GuavaTester.java*

```java
import java.util.Collection;
import java.util.List;
import java.util.Map;
import java.util.Set;

import com.google.common.collect.ArrayListMultimap;
import com.google.common.collect.Multimap;

public class GuavaTester {
   public static void main(String args[]){
      GuavaTester tester = new GuavaTester();
      Multimap<String,String> multimap = tester.getMultimap();

      List<String> lowerList = (List<String>)multimap.get("lower");
      System.out.println("Initial lower case list");
      System.out.println(lowerList.toString());
      lowerList.add("f");
      System.out.println("Modified lower case list");
      System.out.println(lowerList.toString());

      List<String> upperList = (List<String>)multimap.get("upper");
      System.out.println("Initial upper case list");
      System.out.println(upperList.toString());
      upperList.remove("D");
      System.out.println("Modified upper case list");
      System.out.println(upperList.toString());

      Map<String, Collection<String>> map = multimap.asMap();
      System.out.println("Multimap as a map");
      for (Map.Entry<String,  Collection<String>> entry : map.entrySet()) {
         String key = entry.getKey();
         Collection<String> value =  multimap.get("lower");
         System.out.println(key + ":" + value);
      }

      System.out.println("Keys of Multimap");
      Set<String> keys =  multimap.keySet();
      for(String key:keys){
         System.out.println(key);
      }

      System.out.println("Values of Multimap");
      Collection<String> values = multimap.values();
      System.out.println(values);
   }	

   private Multimap<String,String> getMultimap(){
      //Map<String, List<String>>
      // lower -> a, b, c, d, e 
      // upper -> A, B, C, D

      Multimap<String,String> multimap = ArrayListMultimap.create();		

      multimap.put("lower", "a");
      multimap.put("lower", "b");
      multimap.put("lower", "c");
      multimap.put("lower", "d");
      multimap.put("lower", "e");

      multimap.put("upper", "A");
      multimap.put("upper", "B");
      multimap.put("upper", "C");
      multimap.put("upper", "D");		
      return multimap;		
   }
}
```

---;		
   }
}
```

---