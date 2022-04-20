---
uuid: bbaf2104-c0ab-11ec-92a1-7557b2313227
title: Guava Predicates
categories: Java
tags:
  - guava
abbrlink: 447154f8
---

## 类方法

| S.N  | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | public static <T> Predicate<T> alwaysTrue()                  |
| 2    | public static <T> Predicate<T> alwaysFalse()                 |
| 3    | public static <T> Predicate<T> isNull()                      |
| 4    | public static <T> Predicate<T> notNull()                     |
| 5    | public static <T> Predicate<T> and(Iterable<? extends Predicate<? super T>> components) |
| 6    | public static <T> Predicate<T> and(Predicate<? super T>... components) |
| 7    | public static <T> Predicate<T> and(Predicate<? super T> first, Predicate<? super T> second) |
| 8    | public static <T> Predicate<T> or(Iterable<? extends Predicate<? super T>> components) |
| 9    | public static <T> Predicate<T> or(Predicate<? super T>... components) |
| 10   | public static <T> Predicate<T> or(Predicate<? super T> first, Predicate<? super T> second) |
| 11   | public static <T> Predicate<T> equalTo(@Nullable T target)   |
| 12   | public static Predicate<Object> instanceOf(Class<?> clazz)   |
| 13   | public static Predicate<Class<?>> subtypeOf(Class<?> clazz)  |
| 14   | public static <T> Predicate<T> in(Collection<? extends T> target) |
| 15   | public static <A, B> Predicate<A> compose(Predicate<B> predicate, Function<A, ? extends B> function) |
| 16   | public static Predicate<CharSequence> containsPattern(String pattern) |
| 17   | public static Predicate<CharSequence> contains(Pattern pattern) |

---ern pattern) |

---