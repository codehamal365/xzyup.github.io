---
uuid: bbaf2103-c0ab-11ec-92a1-7557b2313227
title: Guava Preconditions
categories: Java
tags:
  - guava
abbrlink: 492d887f
---

## Preconditions

[Preconditions](https://www.yiibai.com/guava/guava_preconditions_class.html)提供静态方法来检查方法或构造函数，被调用是否给定适当的参数。它检查的先决条件。其方法失败抛出IllegalArgumentException。

Preconditions主要提供了四类检查

- checkArgument
  - static void checkArgument(boolean expression)
  - static void checkArgument(boolean expression, String errorMessageTemplate, Object... errorMessageArgs)

- checkState
  - public static void checkState(boolean expression) 
  - public static void checkState(
        boolean expression,
        @Nullable String errorMessageTemplate,
        @Nullable Object @Nullable ... errorMessageArgs)

- checkNotNull
  - public static <T extends @NonNull Object> T checkNotNull(
        T reference, @Nullable Object errorMessage)
  - public static <T extends @NonNull Object> T checkNotNull(
        T reference,
        @Nullable String errorMessageTemplate,
        @Nullable Object @Nullable ... errorMessageArgs) 

- checkElementIndex
  - public static int checkElementIndex(int index, int size)

相关的用法比较简单，可自行查看源码后使用。

不过这里所做的检查都抛的是基本异常类型，可能大多数不符合业务异常，所以使用可能不会太多。
