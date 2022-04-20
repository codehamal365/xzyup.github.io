---
uuid: bbaf6f23-c0ab-11ec-92a1-7557b2313227
title: Guava Bimap
tags:
  - guava
categories: Java
abbrlink: 872f7cc2
---

# Guava Bimap接口

BiMap是一种特殊的映射其保持映射，同时确保没有重复的值是存在于该映射和一个值可以安全地用于获取键背面的倒数映射。

## 接口声明

以下是com.google.common.collect.Bimap<K，V>接口的声明：

```java
@GwtCompatible
public interface BiMap<K,V> extends Map<K,V>
```

## 接口方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **V forcePut(K key, V value)**  另一种put的形式是默默删除，在put(K, V)运行前的任何现有条目值值。 |
| 2    | **BiMap<V,K> inverse()**  返回此bimap，每一个bimap的值映射到其相关联的键的逆视图。 |
| 3    | **V put(K key, V value)**  关联指定值与此映射中(可选操作)指定的键。 |
| 4    | **void putAll(Map<? extends K,? extends V> map)**  将所有从指定映射此映射(可选操作)的映射。 |
| 5    | **Set<V> values()**  返回此映射中包含Collection的值视图。    |

## 继承的方法

这个类继承自以下接口方法：

- java.util.Map

## BiMap 示例

使用所选择的编辑器创建下面的java程序，比如说 **C:/> Guava**

*GuavaTester.java*

```java
import com.google.common.collect.BiMap;
import com.google.common.collect.HashBiMap;

public class GuavaTester {

   public static void main(String args[]){
      BiMap<Integer, String> empIDNameMap = HashBiMap.create();

      empIDNameMap.put(new Integer(101), "Mahesh");
      empIDNameMap.put(new Integer(102), "Sohan");
      empIDNameMap.put(new Integer(103), "Ramesh");

      //Emp Id of Employee "Mahesh"
      System.out.println(empIDNameMap.inverse().get("Mahesh"));
   }	
}
```

---);
   }	
}
```

---