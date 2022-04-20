---
uuid: bbaef9fc-c0ab-11ec-92a1-7557b2313227
title: Guava CharMatcher
categories: Java
tags:
  - guava
abbrlink: 383fc378
---

CharMatcher提供了各种方法来处理各种JAVA char类型值。

## 类声明

以下是com.google.common.base.CharMatcher类的声明：

```
@GwtCompatible(emulated=true)
public final class CharMatcher
   extends Object
```

## 字体

| S.N. | 字段及说明                                                   |
| ---- | :----------------------------------------------------------- |
| 1    | **static CharMatcher ANY**  			匹配任意字符。       |
| 2    | **static CharMatcher ASCII**  			确定字符是否为ASCII码，这意味着它的代码点低于128。 |
| 3    | **static CharMatcher BREAKING_WHITESPACE**  	确定一个字符是否是一个破空白（即，一个空格可以解释为格式目的词之间休息）。 |
| 4    | **static CharMatcher DIGIT**  			确定一个字符是否是根据Unicode数字。 |
| 5    | **static CharMatcher INVISIBLE**  			确定一个字符是否是看不见的;也就是说，如果它的Unicode类是任何SPACE_SEPARATOR，LINE_SEPARATOR，PARAGRAPH_SEPARATOR，控制，FORMAT，SURROGATE和PRIVATE_USE根据ICU4J。 |
| 6    | **static CharMatcher JAVA_DIGIT**  			确定一个字符是否是按照Java的定义一个数字。 |
| 7    | **static CharMatcher JAVA_ISO_CONTROL**  			确定一个字符是否是所指定的Character.isISOControl(char)ISO控制字符。 |
| 8    | **static CharMatcher JAVA_LETTER**  			确定一个字符是否是按照Java的定义的字母。 |
| 9    | **static CharMatcher JAVA_LETTER_OR_DIGIT**  			确定一个字符是否是按照Java的定义，一个字母或数字。 |
| 10   | **static CharMatcher JAVA_LOWER_CASE**  			确定一个字符是否是按照Java定义的小写。 |
| 11   | **static CharMatcher JAVA_UPPER_CASE**  			确定一个字符是否是按照Java定义的大写。 |
| 12   | **static CharMatcher NONE**  			匹配任何字符。      |
| 13   | **static CharMatcher SINGLE_WIDTH**  			确定一个字符是否是单宽度（不是双倍宽度）。 |
| 14   | **static CharMatcher WHITESPACE**  			决定根据最新的Unicode标准是否字符是空白，如图所示这里。 |

## 构造函数

| S.N. | 构造函数 & 描述                                              |
| ---- | ------------------------------------------------------------ |
| 1    | **protected CharMatcher()**  			构造方法，供子类使用。 |

## 类方法

| S.N. | 方法 & 描述                                                  |
| ---- | ------------------------------------------------------------ |
| 1    | **CharMatcher and(CharMatcher other)**  			返回一个匹配器，匹配两种匹配器和其他任何字符。 |
| 2    | **static CharMatcher anyOf(CharSequence sequence)**  			返回一个字符匹配匹配任何字符出现在给定的字符序列。 |
| 3    | **boolean apply(Character character)**  			不推荐使用。只有提供满足谓词接口;用匹配（字符）代替。 |
| 4    | **String collapseFrom(CharSequence sequence, char replacement)**  			返回输入字符序列的字符串拷贝，每个组连续的字符匹配此匹配由单一的替换字符替换。 |
| 5    | **int countIn(CharSequence sequence)**  			返回一个字符序列中发现匹配的字符的数目。 |
| 6    | **static CharMatcher forPredicate(Predicate<? super Character> predicate)**  			返回与相同的行为给定的基于字符的谓词匹配，但运行在原始的字符，而不是实例。 |
| 7    | **int indexIn(CharSequence sequence)**  			返回第一个匹配字符的索引中的一个字符序列，或-1，如果没有匹配的字符存在。 |
| 8    | **int indexIn(CharSequence sequence, int start)**  			返回第一个匹配字符的索引中的一个字符序列，从给定位置开始，或-1，如果没有字符的位置之后匹配。 |
| 9    | **static CharMatcher inRange(char startInclusive, char endInclusive)**  			返回一个字符匹配匹配给定范围内的任何字符（两个端点也包括在内）。 |
| 10   | **static CharMatcher is(char match)**  			返回一个字符匹配匹配只有一个指定的字符。 |
| 11   | **static CharMatcher isNot(char match)**  			返回一个字符匹配匹配除了指定的任何字符。 |
| 12   | **int lastIndexIn(CharSequence sequence)**  			返回最后一个匹配字符的索引中的字符序列，或-1，如果没有匹配的字符存在。 |
| 13   | **abstract boolean matches(char c)**  			确定给定字符一个true或false值。 |
| 14   | **boolean matchesAllOf(CharSequence sequence)**  			确定给定字符一个true或false值。 |
| 15   | **boolean matchesAnyOf(CharSequence sequence)**  			返回true如果字符序列包含至少一个匹配的字符。 |
| 16   | **boolean matchesNoneOf(CharSequence sequence)**  			返回true，如果一个字符序列中没有匹配的字符。 |
| 17   | **CharMatcher negate()**  			返回一个匹配器，不受此匹配匹配任何字符。 |
| 18   | **static CharMatcher noneOf(CharSequence sequence)**  			返回一个字符匹配器匹配不存在于给定的字符序列的任何字符。 |
| 19   | **CharMatcher or(CharMatcher other)**  			返回一个匹配器，匹配任何匹配或其他任何字符。 |
| 20   | **CharMatcher precomputed()**  			返回一个字符匹配功能上等同于这一个，但它可能会快于原来的查询;您的里程可能会有所不同。 |
| 21   | **String removeFrom(CharSequence sequence)**  			返回包含的字符序列的所有非匹配的字符，为了一个字符串。 |
| 22   | **String replaceFrom(CharSequence sequence, char replacement)**  			返回输入字符序列的字符串副本，其中每个字符匹配该匹配器由一个给定的替换字符替换。 |
| 23   | **String replaceFrom(CharSequence sequence, CharSequence replacement)**  			返回输入字符序列的字符串副本，其中每个字符匹配该匹配器由一个给定的替换序列替换。 |
| 24   | **String retainFrom(CharSequence sequence)**  			返回包含的字符序列的所有字符匹配，为了一个字符串。 |
| 25   | **String toString()**  			返回此CharMatcher，如CharMatcher.or（WHITESPACE，JAVA_DIGIT）的字符串表示。 |
| 26   | **String trimAndCollapseFrom(CharSequence sequence, char replacement)**  			折叠匹配字符完全一样collapseFrom一组如collapseFrom(java.lang.CharSequence, char) 做的一样，不同之处在于，无需更换一组被移除的匹配字符在开始或该序列的结束。 |
| 27   | **String trimFrom(CharSequence sequence)**  			返回输入字符序列省略了所有匹配器从一开始，并从该串的末尾匹配字符的字符串。 |
| 28   | **String trimLeadingFrom(CharSequence sequence)**  			返回输入字符序列，它省略了所有这些匹配的字符串开始处匹配字符的字符串。 |
| 29   | **String trimTrailingFrom(CharSequence sequence)**  			返回输入字符序列，它省略了所有这些匹配的字符串的结尾匹配字符的字符串。 |

In olden times, our `StringUtil` class grew unchecked, and had many methods like these:

- `allAscii`
- `collapse`
- `collapseControlChars`
- `collapseWhitespace`
- `lastIndexNotOf`
- `numSharedChars`
- `removeChars`
- `removeCrLf`
- `retainAllChars`
- `strip`
- `stripAndCollapse`
- `stripNonDigits`

They represent a partial cross product of two notions:

1. what constitutes a "matching" character?
2. what to do with those "matching" characters?

To simplify this morass, we developed `CharMatcher`.

Intuitively, you can think of a `CharMatcher` as representing a particular class of characters, like digits or whitespace. Practically speaking, a `CharMatcher` is just a boolean predicate on characters -- indeed, `CharMatcher` implements [`Predicate<Character>`] -- but because it is so common to refer to "all whitespace characters" or "all lowercase letters," Guava provides this specialized syntax and API for characters.

But the utility of a `CharMatcher` is in the *operations* it lets you perform on occurrences of the specified class of characters: trimming, collapsing, removing, retaining, and much more. An object of type `CharMatcher` represents notion 1: what constitutes a matching character? It then provides many operations answering notion 2: what to do with those matching characters? The result is that API complexity increases linearly for quadratically increasing flexibility and power. Yay!

```
String noControl = CharMatcher.javaIsoControl().removeFrom(string); // remove control characters
String theDigits = CharMatcher.digit().retainFrom(string); // only the digits
String spaced = CharMatcher.whitespace().trimAndCollapseFrom(string, ' ');
  // trim whitespace at ends, and replace/collapse whitespace into single spaces
String noDigits = CharMatcher.javaDigit().replaceFrom(string, "*"); // star out all digits
String lowerAndDigit = CharMatcher.javaDigit().or(CharMatcher.javaLowerCase()).retainFrom(string);
  // eliminate all characters that aren't digits or lowercase
```

**Note:** `CharMatcher` deals only with `char` values; it does not understand supplementary Unicode code points in the range 0x10000 to 0x10FFFF. Such logical characters are encoded into a `String` using surrogate pairs, and a `CharMatcher` treats these just as two separate characters.

### Obtaining CharMatchers

Many needs can be satisfied by the provided `CharMatcher` factory methods:

- [`any()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#any--)
- [`none()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#none--)
- [`whitespace()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#whitespace--)
- [`breakingWhitespace()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#breakingWhitespace--)
- [`invisible()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#invisible--)
- [`digit()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#digit--)
- [`javaLetter()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLetter--)
- [`javaDigit()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaDigit--)
- [`javaLetterOrDigit()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLetterOrDigit--)
- [`javaIsoControl()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaIsoControl--)
- [`javaLowerCase()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLowerCase--)
- [`javaUpperCase()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaUpperCase--)
- [`ascii()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#ascii--)
- [`singleWidth()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#singleWidth--)

Other common ways to obtain a `CharMatcher` include:

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`anyOf(CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#anyOf-java.lang.CharSequence-) | Specify all the characters you wish matched. For example, `CharMatcher.anyOf("aeiou")` matches lowercase English vowels. |
| [`is(char)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#is-char-) | Specify exactly one character to match.                      |
| [`inRange(char, char)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#inRange-char-char-) | Specify a range of characters to match, e.g. `CharMatcher.inRange('a', 'z')`. |

Additionally, `CharMatcher` has [`negate()`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#negate--), [`and(CharMatcher)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#and-com.google.common.base.CharMatcher-), and [`or(CharMatcher)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#or-com.google.common.base.CharMatcher-). These provide simple boolean operations on `CharMatcher`.

### Using CharMatchers

`CharMatcher` provides a [wide variety](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#method_summary) of methods to operate on occurrences of the specified characters in any `CharSequence`. There are more methods provided than we can list here, but some of the most commonly used are:

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`collapseFrom(CharSequence, char)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#collapseFrom-java.lang.CharSequence-char-) | Replace each group of consecutive matched characters with the specified character. For example, `WHITESPACE.collapseFrom(string, ' ')` collapses whitespaces down to a single space. |
| [`matchesAllOf(CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#matchesAllOf-java.lang.CharSequence-) | Test if this matcher matches all characters in the sequence. For example, `ASCII.matchesAllOf(string)` tests if all characters in the string are ASCII. |
| [`removeFrom(CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#removeFrom-java.lang.CharSequence-) | Removes matching characters from the sequence.               |
| [`retainFrom(CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#retainFrom-java.lang.CharSequence-) | Removes all non-matching characters from the sequence.       |
| [`trimFrom(CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#trimFrom-java.lang.CharSequence-) | Removes leading and trailing matching characters.            |
| [`replaceFrom(CharSequence, CharSequence)`](https://guava.dev/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#replaceFrom-java.lang.CharSequence-java.lang.CharSequence-) | Replace matching characters with a given sequence.           |

(Note: all of these methods return a `String`, except for `matchesAllOf`, which returns a `boolean`.)

例子

~~~java
@Test
void testCharMatcher() {
  // 统计字符串中字符的个数
  assertEquals(3, CharMatcher.is('#').countIn("#hello#world#"));
  // 保留某些字符
  assertEquals("bc", CharMatcher.inRange('b', 'c').retainFrom("abcdefg"));
}
~~~

---defg"));
}
~~~

---