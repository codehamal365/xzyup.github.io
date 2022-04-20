---
title: Guava Splitter
tags:
  - guava
abbrlink: d667
---

# Splitter常见用法

## 基本用法

~~~java
@Test
void testSplitter() {
  String str = "java#python#golang#default";
  List<String> list = Splitter.on("#").splitToList(str);
  assertEquals(4, list.size());
}
~~~

## Omit empty strings

~~~java
@Test
void testSplitterOmitEmptyStrings() {
  String str = "java#python#golang#";
  List<String> list = Splitter.on("#").omitEmptyStrings().splitToList(str);
  assertEquals(3, list.size());
}
~~~

## Splitter limit

~~~java
@Test
void testSplitterLimit() {
  String str = "java#python#golang#";
  List<String> list = Splitter.on("#").limit(2).splitToList(str);
  assertEquals(2, list.size());
  assertEquals("python#golang#", list.get(1));
}
~~~

## Splitter map

~~~java
@Test
void testSplitterMap() {
  String str = "k1=v1&k2=v2&k3=v3";
  Map<String,String> map = Splitter.on("&").withKeyValueSeparator("=").split(str);
  assertEquals(3, map.size());
  assertEquals("v1", map.get("k1"));
}
~~~

Splitter fixed length

~~~java
@Test
void testSplitterFixedLength() {
  String str = "aaaabbbbccccdddd";
  List<String> list = Splitter.fixedLength(4).splitToList(str);
  assertEquals(4, list.size());
  assertEquals("aaaa", list.get(0));
  assertEquals("dddd", list.get(3));
}
~~~

---