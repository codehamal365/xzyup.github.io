---
uuid: bbaf2108-c0ab-11ec-92a1-7557b2313227
title: Guava Suppliers
categories: Java
tags:
  - guava
abbrlink: e620e81e
---

## 类方法

| S.N  | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | static <F, T> Supplier<T> compose(Function<? super F, T> function, Supplier<F> supplier) |
| 2    | static <T> Supplier<T> memoize(Supplier<T> delegate)         |
| 3    | static <T> Supplier<T> memoizeWithExpiration                 |
| 4    | static <T> Supplier<T> ofInstance(@Nullable T instance)      |
| 5    | static <T> Supplier<T> synchronizedSupplier(Supplier<T> delegate) |
| 6    | static <T> Function<Supplier<T>, T> supplierFunction()       |

---tion()       |

---