---
uuid: bbaef9fd-c0ab-11ec-92a1-7557b2313227
title: Guava Functions
categories: Java
tags:
  - guava
abbrlink: 9a47c4e
---


# Functions

类方法

| S.N  | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | static toStringFunction() 返回object -> tostring             |
| 2    | static identity() 输入和输出一样的值                         |
| 3    | static <K, V> Function<K, V> forMap(Map<K, V> map) 返回FunctionForMapNoDefault,能够获取map的值 |
| 4    | static <K, V> Function<K, V> forMap(Map<K, ? extends V> map, @Nullable V defaultValue) 能够获取defualt值的function |
| 5    | static <A, B, C> Function<A, C> compose(Function<B, C> g, Function<A, ? extends B> f) 组合functions,返回<A,C> 输入是A, 返回值是C |
| 6    | static <T> Function<T, Boolean> forPredicate(Predicate<T> predicate) ，输入值是，返回值是bool值 |
| 7    | static <E> Function<Object, E> constant(@Nullable E value)  返回常量值 |
| 8    | static <T> Function<Object, T> forSupplier(Supplier<T> supplier) |

