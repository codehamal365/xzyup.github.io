---
title: Guava Table
tags:
  - guava
abbrlink: 716a
---

# Guava Table接口

Table代表一个特殊的映射，其中两个键可以在组合的方式被指定为单个值。它类似于创建映射的映射。

## 	接口声明

以下是 com.google.common.collect.Table<R，C，V> 接口的声明：

```
@GwtCompatible
public interface Table<R,C,V>
```

## 	接口方法

| S.N. | 方法 & 描述                                                  |
| ---- | ------------------------------------------------------------ |
| 1    | **Set<Table.Cell<R,C,V>> cellSet()**  			返回集合中的所有行键/列键/值三元组。 |
| 2    | **void clear()**  			从表中删除所有映射。           |
| 3    | **Map<R,V> column(C columnKey)**  			返回在给定列键的所有映射的视图。 |
| 4    | **Set<C> columnKeySet()**  			返回一组具有表中的一个或多个值的列键。 |
| 5    | **Map<C,Map<R,V>> columnMap()**  			返回关联的每一列键与行键对应的映射值的视图。 |
| 6    | **boolean contains(Object rowKey, Object columnKey)**  			返回true，如果表中包含与指定的行和列键的映射。 |
| 7    | **boolean containsColumn(Object columnKey)**  			返回true，如果表中包含与指定列的映射。 |
| 8    | **boolean containsRow(Object rowKey)**  			返回true，如果表中包含与指定的行键的映射关系。 |
| 9    | **boolean containsValue(Object value)**  			返回true，如果表中包含具有指定值的映射。 |
| 10   | **boolean equals(Object obj)**  			比较指定对象与此表是否相等。 |
| 11   | **V get(Object rowKey, Object columnKey)**  			返回对应于给定的行和列键，如果没有这样的映射存在值，返回null。 |
| 12   | **int hashCode()**  			返回此表中的哈希码。         |
| 13   | **boolean isEmpty()**  			返回true，如果表中没有映射。 |
| 14   | **V put(R rowKey, C columnKey, V value)**  关联指定值与指定键。 |
| 15   | **void putAll(Table<? extends R,? extends C,? extends V> table)**  复制从指定的表中的所有映射到这个表。 |
| 16   | **V remove(Object rowKey, Object columnKey)**  	如果有的话，使用给定键相关联删除的映射。 |
| 17   | **Map<C,V> row(R rowKey)**  返回包含给定行键的所有映射的视图。 |
| 18   | **Set<R> rowKeySet()**  	返回一组行键具有在表中的一个或多个值。 |
| 19   | **Map<R,Map<C,V>> rowMap()**  返回关联的每一行按键与键列对应的映射值的视图。 |
| 20   | **int size()**  			返回行键/列键/表中的值映射关系的数量。 |
| 21   | **Collection<V> values()**  返回所有值，其中可能包含重复的集合。 |

## Table 例子

选择使用任何编辑器创建以下java程序在 **C:/> Guava**

*GuavaTester.java*

```java
import java.util.Map;
import java.util.Set;

import com.google.common.collect.HashBasedTable;
import com.google.common.collect.Table;

public class GuavaTester {

   public static void main(String args[]){
      //Table<R,C,V> == Map<R,Map<C,V>>
      /*
      *  Company: IBM, Microsoft, TCS
      *  IBM 		-> {101:Mahesh, 102:Ramesh, 103:Suresh}
      *  Microsoft 	-> {101:Sohan, 102:Mohan, 103:Rohan } 
      *  TCS 		-> {101:Ram, 102: Shyam, 103: Sunil } 
      * 
      * */
      //create a table
      Table<String, String, String> employeeTable = HashBasedTable.create();

      //initialize the table with employee details
      employeeTable.put("IBM", "101","Mahesh");
      employeeTable.put("IBM", "102","Ramesh");
      employeeTable.put("IBM", "103","Suresh");

      employeeTable.put("Microsoft", "111","Sohan");
      employeeTable.put("Microsoft", "112","Mohan");
      employeeTable.put("Microsoft", "113","Rohan");

      employeeTable.put("TCS", "121","Ram");
      employeeTable.put("TCS", "122","Shyam");
      employeeTable.put("TCS", "123","Sunil");

      //get Map corresponding to IBM
      Map<String,String> ibmEmployees =  employeeTable.row("IBM");

      System.out.println("List of IBM Employees");
      for(Map.Entry<String, String> entry : ibmEmployees.entrySet()){
         System.out.println("Emp Id: " + entry.getKey() + ", Name: " + entry.getValue());
      }

      //get all the unique keys of the table
      Set<String> employers = employeeTable.rowKeySet();
      System.out.print("Employers: ");
      for(String employer: employers){
         System.out.print(employer + " ");
      }
      System.out.println();

      //get a Map corresponding to 102
      Map<String,String> EmployerMap =  employeeTable.column("102");
      for(Map.Entry<String, String> entry : EmployerMap.entrySet()){
         System.out.println("Employer: " + entry.getKey() + ", Name: " + entry.getValue());
      }		
   }	
}
```

---