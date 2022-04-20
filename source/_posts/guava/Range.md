---
title: Guava Range
tags:
  - guava
abbrlink: '4225'
---

Range 表示一个间隔或一个序列。它被用于获取一组数字/串在一个特定范围之内。

## 类声明

以下是com.google.common.collect.Range<C>类的声明：

```
@GwtCompatible
public final class Range<C extends Comparable>
   extends Object
      implements Predicate<C>, Serializable
```

## 方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **static <C extends Comparable<?>> Range<C> all()**  			返回包含C型的每一个值范围 |
| 2    | **boolean apply(C input)Deprecated.**   			只有提供满足谓词接口;使用包含(C)来代替。 |
| 3    | **static <C extends Comparable<?>> Range<C> atLeast(C endpoint)**  			返回包含大于或等于终点(endpoint)的所有值的范围内。 |
| 4    | **static <C extends Comparable<?>> Range<C> atMost(C endpoint)**  			返回包含的所有值小于或等于终点的范围内。 |
| 5    | **Range<C> canonical(DiscreteDomain<C> domain)**  			返回此范围内，在给定域中的规范形式。 |
| 6    | **static <C extends Comparable<?>> Range<C> closed(C lower, C upper)**  			返回包含大于所有值或等于降低且小于或等于上限的范围内。 |
| 7    | **static <C extends Comparable<?>> Range<C> closedOpen(C lower, C upper)**  			返回包含大于或等于下限和所有值严格大于上限以下的范围内。 |
| 8    | **boolean contains(C value)**  			返回true，如果值是这个范围的范围之内。 |
| 9    | **boolean containsAll(Iterable<? extends C> values)**  			如果值每一个元素都包含在这个范围内，则返回 true。 |
| 10   | **static <C extends Comparable<?>> Range<C> downTo(C endpoint, BoundType boundType)**  			返回的范围内的给定的端点，它可以是包容性（闭合）或专用（开），没有上限。 |
| 11   | **static <C extends Comparable<?>> Range<C> encloseAll(Iterable<C> values)**  			返回包含所有给定值的最小范围内。 |
| 12   | **boolean encloses(Range<C> other)**  			返回true，如果其他的边界不在该范围的边界之外延伸。 |
| 13   | **boolean equals(Object object)**  			返回true，如果对象是具有相同端点和绑定类型，这个范围内的范围。 |
| 14   | **static <C extends Comparable<?>> Range<C> greaterThan(C endpoint)**  			返回一个包含所有值严格大于端点的范围内。 |
| 15   | **int hashCode()**  			返回此范围内的哈希码。       |
| 16   | **boolean hasLowerBound()**  			如果此范围内具有更低的终点返回true。 |
| 17   | **boolean hasUpperBound()**  			如果此范围内有上端点返回true。 |
| 18   | **Range<C> intersection(Range<C> connectedRange)**  			返回由两者范围和connectedRange封闭，如果这样的范围存在的最大范围。 |
| 19   | **boolean isConnected(Range<C> other)**  			如果存在这是由两者此范围和其他封闭（可能为空）的范围，则返回true。 |
| 20   | **boolean isEmpty()**  			返回true，如果这个范围是形式 [v..v)  或 (v..v]. |
| 21   | **static <C extends Comparable<?>> Range<C> lessThan(C endpoint)**  			返回一个包含所有值严格小于端点的范围内。 |
| 22   | **BoundType lowerBoundType()**  			返回类型这个范围的下限：如果范围包括它的下端点BoundType.CLOSED，如果没有BoundType.OPEN。 |
| 23   | **C lowerEndpoint()**  			返回该范围的较低端点。    |
| 24   | **static <C extends Comparable<?>> Range<C> open(C lower, C upper)**  			返回一个包含所有值严格大于下限和严格比上端更小一个范围。 |
| 25   | **static <C extends Comparable<?>> Range<C> openClosed(C lower, C upper)**  			返回包含所有值严格低于更大且小于或等于上限的范围内。 |
| 26   | **static <C extends Comparable<?>> Range<C> range(C lower, BoundType lowerType, C upper, BoundType upperType)**  			返回包含任何值由下到上，每个端点可以是包容性（关闭）或专用（开）的范围。 |
| 27   | **static <C extends Comparable<?>> Range<C> singleton(C value)**  			返回包含只在给定范围内的值。 |
| 28   | **Range<C> span(Range<C> other)**  			返回最小的范围包围两者这个范围和other等。 |
| 29   | **String toString()**  			返回该范围内的字符串表示，如“[3..5）”（其他实例列在类文档）。 |
| 30   | **BoundType upperBoundType()**  			返回类型此范围的上限：如果范围包括其上的端点返回BoundType.CLOSED，如果没有返回BoundType.OPEN。 |
| 31   | **C upperEndpoint()**  			返回此范围的上限端点。    |
| 32   | **static <C extends Comparable<?>> Range<C> upTo(C endpoint, BoundType boundType)**  			返回一个范围，没有下限到给定的端点，它可以是包容性（闭合）或专用（开）。 |

## Range 例子

```java
public class GuavaTester {

   public static void main(String args[]){
      GuavaTester tester = new GuavaTester();
      tester.testRange();
   }

   private void testRange(){

      //create a range [a,b] = { x | a <= x <= b}
      Range<Integer> range1 = Range.closed(0, 9);
      System.out.print("[0,9] : ");
      printRange(range1);		
      System.out.println("5 is present: " + range1.contains(5));
      System.out.println("(1,2,3) is present: " + range1.containsAll(Ints.asList(1, 2, 3)));
      System.out.println("Lower Bound: " + range1.lowerEndpoint());
      System.out.println("Upper Bound: " + range1.upperEndpoint());

      //create a range (a,b) = { x | a < x < b}
      Range<Integer> range2 = Range.open(0, 9);
      System.out.print("(0,9) : ");
      printRange(range2);

      //create a range (a,b] = { x | a < x <= b}
      Range<Integer> range3 = Range.openClosed(0, 9);
      System.out.print("(0,9] : ");
      printRange(range3);

      //create a range [a,b) = { x | a <= x < b}
      Range<Integer> range4 = Range.closedOpen(0, 9);
      System.out.print("[0,9) : ");
      printRange(range4);

      //create an open ended range (9, infinity
      Range<Integer> range5 = Range.greaterThan(9);
      System.out.println("(9,infinity) : ");
      System.out.println("Lower Bound: " + range5.lowerEndpoint());
      System.out.println("Upper Bound present: " + range5.hasUpperBound());

      Range<Integer> range6 = Range.closed(3, 5);	
      printRange(range6);

      //check a subrange [3,5] in [0,9]
      System.out.println("[0,9] encloses [3,5]:" + range1.encloses(range6));

      Range<Integer> range7 = Range.closed(9, 20);	
      printRange(range7);
      //check ranges to be connected		
      System.out.println("[0,9] is connected [9,20]:" + range1.isConnected(range7));

      Range<Integer> range8 = Range.closed(5, 15);	

      //intersection
      printRange(range1.intersection(range8));

      //span
      printRange(range1.span(range8));
   }

   private void printRange(Range<Integer> range){		
      System.out.print("[ ");
      for(int grade : ContiguousSet.create(range, DiscreteDomain.integers())) {
         System.out.print(grade +" ");
      }
      System.out.println("]");
   }
}
```

---