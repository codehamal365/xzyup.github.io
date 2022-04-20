---
uuid: bbaef9fb-c0ab-11ec-92a1-7557b2313227
title: Guava CaseFormat
categories: Java
tags:
  - guava
abbrlink: 995f4974
---

## 枚举常量

| S.N. | 枚举常量和说明                                               |
| ---- | ------------------------------------------------------------ |
| 1    | **LOWER_CAMEL**  			Java变量的命名规则，如“lowerCamel”。 |
| 2    | **LOWER_HYPHEN**  			连字符连接变量的命名规则，如“lower-hyphen”。 |
| 3    | **LOWER_UNDERSCORE**  			C ++变量命名规则，如“lower_underscore”。 |
| 4    | **UPPER_CAMEL**  			Java和C++类的命名规则，如“UpperCamel”。 |
| 5    | **UPPER_UNDERSCORE**  			Java和C++常量的命名规则，如“UPPER_UNDERSCORE”。 |

## 方法

| S.N. | 方法及说明                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **Converter<String,String> converterTo(CaseFormat targetFormat)**  			返回一个转换，从这个格式转换targetFormat字符串。 |
| 2    | **String to(CaseFormat format, String str)**  			从这一格式指定格式的指定字符串 str 转换。 |
| 3    | **static CaseFormat valueOf(String name)**  			返回此类型具有指定名称的枚举常量。 |
| 4    | **static CaseFormat[] values()**  			返回一个包含该枚举类型的常量数组中的顺序被声明。 |

## 例子

```java
// test-world
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.LOWER_HYPHEN, "test_world"));
// test_world
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.LOWER_UNDERSCORE, "test_world"));
// testWorld
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.LOWER_CAMEL, "test_world"));
// TestWorld
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.UPPER_CAMEL, "test_world"));
// TEST_WORLD
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.UPPER_UNDERSCORE, "test_world"));
```

---_world"));
```

---