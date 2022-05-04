---
uuid: bbaf6f20-c0ab-11ec-92a1-7557b2313227
title: plantuml 思维导图
categories: Uml
tags:
  - plantuml
abbrlink: d9642643
---


# [思维导图](https://plantuml.com/zh/mindmap-diagram)

## OrgMode 语法

同时兼容OrgMode语法。

~~~
@startmindmap
* Debian
** Ubuntu
*** Linux Mint
*** Kubuntu
*** Lubuntu
*** KDE Neon
** LMDE
** SolydXK
** SteamOS
** Raspbian with a very long name
*** <s>Raspmbc</s> => OSMC
*** <s>Raspyfi</s> => Volumio
@endmindmap
~~~

![image-20211028140424528](https://raw.githubusercontent.com/xzyup/image/master/202203191700213.png)

## Markdown语法

~~~
@startmindmap
* root node
	* some first level node
		* second level node
		* another second level node
	* another first level node
@endmindmap
~~~

![image-20211028140553231](https://raw.githubusercontent.com/xzyup/image/master/202203191700605.png)

## 运算符

你可以使用下面的运算符来决定图形方向

~~~
@startmindmap
+ OS
++ Ubuntu
+++ Linux Mint
+++ Kubuntu
+++ Lubuntu
+++ KDE Neon
++ LMDE
++ SolydXK
++ SteamOS
++ Raspbian
-- Windows 95
-- Windows 98
-- Windows NT
--- Windows 8
--- Windows 10
@endmindmap
~~~

![image-20211028140722407](https://raw.githubusercontent.com/xzyup/image/master/202203191700398.png)

## Multilines

You can use `:` and `;` to have multilines box.

~~~
@startmindmap
* Class Templates
**:Example 1
<code>
template <typename T>
class cname{
void f1()<U+003B>
...
}
</code>
;
**:Example 2
<code>
other template <typename T>
class cname{
...
</code>
;
@endmindmap
~~~

![image-20211028140848563](https://raw.githubusercontent.com/xzyup/image/master/202203191701547.png)

~~~
@startmindmap
+ root
**:right_1.1
right_1.2;
++ right_2

left side

-- left_1
-- left_2
**:left_3.1
left_3.2;
@endmindmap
~~~

![image-20211028140925260](https://raw.githubusercontent.com/xzyup/image/master/202203191701480.png)

## Colors

It is possible to change node [color](https://plantuml.com/zh/color).

### With inline color

- OrgMode syntax mindmap

  ~~~
  @startmindmap
  *[#Orange] Colors
  **[#lightgreen] Green
  **[#FFBBCC] Rose
  **[#lightblue] Blue
  @endmindmap
  ~~~

  ![image-20211028141140932](https://raw.githubusercontent.com/xzyup/image/master/202203191701909.png)

- Arithmetic notation syntax mindmap

  ~~~
  @startmindmap
  +[#Orange] Colors
  ++[#lightgreen] Green
  ++[#FFBBCC] Rose
  --[#lightblue] Blue
  @endmindmap
  ~~~

  ![image-20211028141246410](https://raw.githubusercontent.com/xzyup/image/master/202203191701869.png)

- Markdown syntax mindmap

  ~~~
  @startmindmap
  *[#Orange] root node
   *[#lightgreen] some first level node
    *[#FFBBCC] second level node
    *[#lightblue] another second level node
   *[#lightgreen] another first level node
  @endmindmap
  ~~~

  ![image-20211028141350247](https://raw.githubusercontent.com/xzyup/image/master/202203191701376.png)



### With style color

- OrgMode syntax mindmap

  ~~~
  @startmindmap
  <style>
  mindmapDiagram {
    .green {
      BackgroundColor lightgreen
    }
    .rose {
      BackgroundColor #FFBBCC
    }
    .your_style_name {
      BackgroundColor lightblue
    }
  }
  </style>
  * Colors
  ** Green <<green>>
  ** Rose <<rose>>
  ** Blue <<your_style_name>>
  @endmindmap
  ~~~

  ![image-20211028141514810](https://raw.githubusercontent.com/xzyup/image/master/202203191701609.png)

- Arithmetic notation syntax mindmap

  ~~~
  @startmindmap
  <style>
  mindmapDiagram {
    .green {
      BackgroundColor lightgreen
    }
    .rose {
      BackgroundColor #FFBBCC
    }
    .your_style_name {
      BackgroundColor lightblue
    }
  }
  </style>
  + Colors
  ++ Green <<green>>
  ++ Rose <<rose>>
  -- Blue <<your_style_name>>
  @endmindmap
  ~~~

  ![image-20211028141615812](https://raw.githubusercontent.com/xzyup/image/master/202203191701587.png)

- Markdown syntax mindmap

  ~~~
  @startmindmap
  <style>
  mindmapDiagram {
    .green {
      BackgroundColor lightgreen
    }
    .rose {
      BackgroundColor #FFBBCC
    }
    .your_style_name {
      BackgroundColor lightblue
    }
  }
  </style>
  * root node
   * some first level node <<green>>
    * second level node <<rose>>
    * another second level node <<your_style_name>>
   * another first level node <<green>>
  @endmindmap
  ~~~

  ![image-20211028141715479](https://raw.githubusercontent.com/xzyup/image/master/202203191701234.png)

## 移除方框

你可以用下划线移除方框图。

~~~
@startmindmap
* root node
** some first level node
***_ second level node
***_ another second level node
***_ foo
***_ bar
***_ foobar
** another first level node
@endmindmap
~~~

![image-20211028141826325](https://raw.githubusercontent.com/xzyup/image/master/202203191702720.png)

~~~
@startmindmap
*_ root node
**_ some first level node
***_ second level node
***_ another second level node
***_ foo
***_ bar
***_ foobar
**_ another first level node
@endmindmap
~~~

![image-20211028141936268](https://raw.githubusercontent.com/xzyup/image/master/202203191702558.png)

~~~
@startmindmap
+ root node
++ some first level node
+++_ second level node
+++_ another second level node
+++_ foo
+++_ bar
+++_ foobar
++_ another first level node
-- some first right level node
--_ another first right level node
@endmindmap
~~~

![image-20211028142027306](https://raw.githubusercontent.com/xzyup/image/master/202203191702633.png)



## 改变图形方向

你可以同时使用图形的左右两侧。

~~~
@startmindmap
* count
** 100
*** 101
*** 102
** 200

left side

** A
*** AA
*** AB
** B
@endmindmap
~~~

![image-20211028142225270](https://raw.githubusercontent.com/xzyup/image/master/202203191702872.png)

## 完整示例

~~~
@startmindmap
caption figure 1
title My super title

* <&flag>Debian
** <&globe>Ubuntu
*** Linux Mint
*** Kubuntu
*** Lubuntu
*** KDE Neon
** <&graph>LMDE
** <&pulse>SolydXK
** <&people>SteamOS
** <&star>Raspbian with a very long name
*** <s>Raspmbc</s> => OSMC
*** <s>Raspyfi</s> => Volumio

header
My super header
endheader

center footer My super footer

legend right
  Short
  legend
endlegend
@endmindmap
~~~

![image-20211028142312553](https://raw.githubusercontent.com/xzyup/image/master/202203191702427.png)

## 改变风格

~~~
@startmindmap
<style>
mindmapDiagram {
    node {
        BackgroundColor lightGreen
    }
    :depth(1) {
      BackGroundColor white
    }
}
</style>
* Linux
** NixOS
** Debian
*** Ubuntu
**** Linux Mint
**** Kubuntu
**** Lubuntu
**** KDE Neon
@endmindmap
~~~

![image-20211028142457629](https://raw.githubusercontent.com/xzyup/image/master/202203191702086.png)

### 无盒

~~~
@startmindmap
<style>
mindmapDiagram {
  node {
    BackgroundColor lightGreen
  }
  boxless {
    FontColor darkgreen
  }
}
</style>
* Linux
** NixOS
** Debian
***_ Ubuntu
**** Linux Mint
**** Kubuntu
**** Lubuntu
**** KDE Neon
@endmindmap
~~~

![image-20211028142552979](https://raw.githubusercontent.com/xzyup/image/master/202203191702867.png)

## Word Wrap

Using `MaximumWidth` setting you can control automatic word wrap. Unit used is pixel. 

~~~
@startmindmap


<style>
node {
    Padding 12
    Margin 3
    HorizontalAlignment center
    LineColor blue
    LineThickness 3.0
    BackgroundColor gold
    RoundCorner 40
    MaximumWidth 100
}

rootNode {
    LineStyle 8.0;3.0
    LineColor red
    BackgroundColor white
    LineThickness 1.0
    RoundCorner 0
    Shadowing 0.0
}

leafNode {
    LineColor gold
    RoundCorner 0
    Padding 3
}

arrow {
    LineStyle 4
    LineThickness 0.5
    LineColor green
}
</style>

* Hi =)
** sometimes i have node in wich i want to write a long text
*** this results in really huge diagram
**** of course, i can explicit split with a\nnew line
**** but it could be cool if PlantUML was able to split long lines, maybe with an option 

@endmindmap
~~~

![image-20211028142657150](https://raw.githubusercontent.com/xzyup/image/master/202203191703508.png)
