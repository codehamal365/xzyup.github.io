---
title: Guava Joiner
tags:
  - guava
abbrlink: 91b8
---

# Joiner常见用法

## Join list

~~~java
@Test
void testJoinerList() {
  List<String> list = List.of("java", "python", "golang");
  String join = Joiner.on("#").join(list);
  assertEquals("java#python#golang", join);
}
~~~

## Join list skip null

~~~java
@Test
void testJoinerListSkipNull() {
  List<Object> list = new ArrayList<>();
  list.add("java");
  list.add("python");
  list.add("golang");
  list.add(null);
  String join = Joiner.on("#").skipNulls().join(list);
  assertEquals("java#python#golang", join);
}
~~~

## Join list use default null

~~~java
@Test
void testJoinerListUseForNull() {
  List<Object> list = new ArrayList<>();
  list.add("java");
  list.add("python");
  list.add("golang");
  list.add(null);
  String join = Joiner.on("#").useForNull("default").join(list);
  assertEquals("java#python#golang#default", join);
}
~~~

## Join map

~~~java
@Test
void testJoinerMap() {
  Map<String, String> map = Map.of("k1", "v1", "k2", "v2", "k3", "v3");
  String join = Joiner.on("&").withKeyValueSeparator("=").join(map);
  assertTrue(join.contains("="));
}
~~~

Join appender

~~~java
@Test
void testJoinerAppender() {
  List<String> list = List.of("java", "python", "golang");
  StringBuilder builder = new StringBuilder();
  StringBuilder join = Joiner.on("#").appendTo(builder, list);
  assertSame(builder, join);
}
~~~

---