#Google Java编码规范中文版

[TOC]

##1 介绍

本文档**完整**地定义了Google公司使用java™语言编写源代码时所采用的编码规范。当且仅当java源文件遵循本规范时，我们才说它是符合Google风格的。

同其他编码风格指南一样，我们所讨论的内容不仅仅包括编码格式美观与否的问题，还囊括了其他类型的惯例约定或编码规范。然而，本文主要集中介绍的是我们所普遍遵循的**硬性规定**（**hard-and-fast rules**），并且避免提出一些有争议不是很确定是否可以强制实施的建议(不论是由人还是工具来实施)。

###1.1 术语说明

在本文档中，除非另外声明：

单词class “类”用于表示的内容包括一个“普通”类、enum枚举类、接口或者注解类型（`@interface`）。
词语comment指的是实现注释（implementation comments）。我们并不使用"文档注释（documentation comments）"一词，而是使用另一个常用的术语“Javadoc”来代替。
其他“术语说明”将会在本文档中其他地方出现。

###1.2 指南说明

本文档中的实例代码并不是标准。这就是说，尽管这些例子是符合Google风格的，但是它们并不能说明这是展示代码的唯一方式。不能将例子中所选择的那些格式化样式作为规则进行强制实施，它们只是可选的样式而已。

##2 源文件基本要素

###2.1 文件名

源文件的文件名是由该文件所包含的顶层类的类名以及`.java`扩展名组成的，类的名称是对大小写敏感的。

###2.2 文件编码：UTF-8

源文件采用UTF-8进行编码。

###2.3 特殊字符

####2.3.1 空白字符
除了行结束符序列（line terminator sequence）（译注：是指"\r\n"这种换行符字符串）以外，ASCII水平间隔字符（0X20）（译注：即空格字符）是唯一能在源文件中出现的空白字符。这意味着：

1. 字符串中的所有其他空白字符都需要进行转义。
2.  Tab字符(也叫制表符)**不能**用于缩进。


####2.3.2 特殊转义字符

对于那些具有特殊转义字符的字符(`\b`、`\t`、`\n`、`\f`、`\r`、`\"`、`\'`和`\\`)，我们使用转义字符，而非对应的八进制数值（比如`\012`）或者Unicode（比如`\u000a`）转义符。

####2.3.3 非ASCII字符
对于其他的非ASCII字符，不管是直接使用真正的Unicode字符（比如`∞`）还是使用等价的Unicode转义符（比如`\u221e`)，都是可以的，这仅仅取决于哪种方式能使代码**更加易于阅读和理解**。

`小提示：在使用Unicode转义符，有时候甚至是直接使用真正的Unicode字符的情况下，写一些注释来进行解释是非常有帮助的。`

例子：


| 案例  | 讨论 |
| --   | --   |
| `String unitAbbrev = "μs";` | 优，即便没有注释也是非常清晰的 |
| ```String unitAbbrev = "\u03bcs"; // "μs"``` | 可，但是没有必要这么做。|
|```String unitAbbrev = "\u03bcs"; // 希腊字母mu，"s" ```| 可, 累赘并且容易出现错误|
|```String unitAbbrev = "\u03bcs";``` | 差，读者不清楚这是什么东西。 |
|```return '\ufeff' + content; // BOM（byte order mark）字符``` | 好: 对打印不出来的字符使用转义符, 并在必要的情况下添加注释。 |




> 小提示：永远不要因为恐惧有一些程序不能正确地处理非ASCII字符而就不是用它，这会让你的代码可读性变差。
> 如果真的出现无法处理非ASCII字符的情况而使得那些程序无法工作了，那么需要由那些程序来解决。
>

##3 源文件结构

一份源文件(按顺序)包含:

 1. 许可证或版权信息（如果存在的话）
 2. 包声明语句
 3. import语句
 4. 一个顶级类（只能有一个）

在文件中，各部分之间要用一个空行进行分隔。


###3.1 许可证或版权信息（如果存在的话）


如果一个文件包含许可证或版权信息的话，这些信息就应该放在文件开头。

###3.2 包声明语句

包声明语句不能换行（译注：没有长度限制）。列限制（4.4小节，列限制：80或100）的规则不适用于包声明语句。

###3.3 Import语句

####3.3.1 禁止在Import语句中使用通配符
不要在import语句中使用通配符，不管是静态import 还是其他import。

> (译注，也就是禁止使用类似 import java.utils.*这样的语句。）

####3.3.2 禁止换行

不能将一条Import语句换行。列限制（4.4小节，列限制：80或100）规则不适用于import语句。

####3.3.3 顺序和间隔

Import语句要被按照下面的顺序进行分组，每组之间使用一个空行进行分割：

1. 将所有的static import语句放到一组中
2. `com.google`包的 imports语句(只有当源文件在`com.google`包空间时)
3.  第三方的包的imports语句：按照ASCII码的排列顺序将每个顶级包分为一组，比如：`android`, `com`, `junit`, `org`, `sun`
4.  `java` import语句
5.  `javax` import语句

同组里的语句之间没有空行，所导入的内容的名称按照ASCII的顺序进行排序（注意：这并不同于将import语句按照ASCII码的顺序进行排序，分号的存在会干扰结果。）
###3.4 类声明

####3.4.1 只有一个顶级类声明
每个顶级类都位于以其类名来命名的源文件中。
####3.4.2 类成员顺序

一个类的成员的排列顺序会极大地影响人们对这个类的学习和理解效率，但是并不存在一种绝对正确的排序方式。不同的类对它们的成员进行排序的方式可能各不相同。

重要的是每个类都要采用某种合乎逻辑意义的顺序来对它的成员进行排序，这样在被别人问到的时候维护者能够将其解释清楚。比如，新的方法不能仅仅习惯性地添加到类的结尾那里，因为这会导致出现一种“按照添加的日期前后而排列”的顺序，这并不是一种逻辑意义上的顺序。

######3.4.2.1 重载：永远不要将重载函数分开
当一个类拥有多个构造函数或者多个同名的方法时，它们需要连续地列在一起，中间不能有其他成员。

##4 格式

Terminology Note: block-like construct refers to the body of a class, method or constructor. Note that, by Section 4.8.3.1 on array initializers, any array initializer may optionally be treated as if it were a block-like construct.
术语说明：块状结构指的是类、方法或者构造函数的主体部分(译注：花括号中的部分)。需要注意的是，对于4.8.3.1小节中的数组初始化，所有的数组初始化都可以选择性地作为块状结构来进行处理。
###4.1 大括号

####4.1.1 在大括号可用也可不用的情况下，使用大括号

在if、else、for、do和while语句中要使用大括号，即使执行体为空或者只包含一条语句。

####4.1.2 非空代码块： K & R 风格

对于非空代码块以及块状结构，大括号要遵循Kernighan和Ritchie风格（埃及括号"Egyptian brackets"）：
 - 左括号前不能换行。
 - 左括号后换行。
 - 在右括号前换行。
 - 只有当使用右括号来结束某个方法、构造函数或者命名类的主体部分或者一条语句的的时候，才要在右括号后面换行。比如，当括号后面跟着else或者逗号的时候，右括号后面就不换行了。

例子
```java
return new MyClass() {
  @Override public void method() {
    if (condition()) {
      try {
        something();
      } catch (ProblemException e) {
        recover();
      }
    }
  }
};
```
对于枚举类的一些例外的情况会在4.8.1小节枚举类中进行描述。
####4.1.3 空代码块：可以简洁一些
一个空的代码块或者块状结构可以在（{}）之间不包含任何字符或者换行，除非它是某个具有多个代码块的语句的一部分（一种直接包含多个代码块的语句有：`if/else-if/else` 或者 `try/catch/finally`）
例子：
```java
void doNothing() {}
```
4.2 块缩进：+2个空格

在每次开始一段新的代码块或者块状结构时，要增加两个空格的缩进。当代码块结束时，缩进要恢复到之前的缩进层级上来。缩进层级的要求同样适用于代码块中的代码和注释。（可参考4.1.2小节（非空代码块:K&R风格）中的例子）
###4.3 每行一条语句
每条语句的后面要有一个换行符。

###4.4 每行的字符长度限制：为80或100
各个项目可以自行选择是采用80还是100作为每行最大的字符长度。除非遇到下面列出的情形，否则的话，那些超过最大字符长度的代码行必须按照第4.5小节（断行）中说明的那样进行断行。

例外：
 - 不可能遵循最大字符长度限制的行（比如，javadoc中很长的URL，或者一个很长的JSNI方法引用）
 - package和import语句（见3.2小节中的Package语句和3.3小节的Import语句）
 - 注释中包含可能会被复制-粘贴到shell中的命令行指令的行。

###4.5 断行

术语说明：当为了避免超过每行最大字符限制，而将那些本来能够合法地只占用一行的代码分到多行时，这种活动就被称作断行。

并不存在一种全面的、确定性的准则来解释清楚在每种情况下该如何进行断行。很对时候，对同一块代码有好几种合法的断行方式。

>小提示：有可能将方法或者本地变量抽取出来就解决问题了，这样就不再需要进行断行了。

####4.5.1 何处断行

断行的主要最高指导原则是：倾向于在更高一些的语法级别上进行断行。还有：

 
 1. 当在非赋值运算符处进行断行时，断行要在运算符号之前。（译注：比如+号处进行断行的话，+号要处于下一行）（注意：这和 Google公司在其他语言（如C++和JavaScript）的编码风格所采用的做法有所不同）。
 - 这一规则同样适用于下列与运算符类似的符号：点分隔符(`.`)，类型绑定中的`&`符号 (```<T extends Foo & Bar>```)以及 catch代码块中的`竖杠 |`符号 (```catch (FooException | BarException e)```)

 2. 当在某个赋值运算符处断行时，通常是在运算符的后面进行断行，但是在前面断行也是可以接受的。
 - 这一规则也同样适用于("foreach")语句中和赋值运算符类似的冒号。
 3. 方法或者构造函数的名称要和后面的左括号(()保持在同一行。
 4. 逗号（,)要和前面的内容在同一行。
####4.5.2 后续行要缩进至少+4个空格字符

当进行断行时，第一行后面的每一行（也被称为续行）都要至少比第一行多缩进四个空格字符

当有多个续行时，缩进须比要求的+4个字符要多。通常，当且仅当两个续行开头的元素在语法上是并列关系的时候，这两个续行才使用相同的缩进级别。
4.6.3小节的的水平对齐中指出使用数量不定的空格来将某些符号与前面行的符号对齐是一种被阻止的行为。

###4.6 空白

####4.6.1 垂直空白
出现单个空行的位置有：
 1. 某个类的那些相邻的成员（或者初始化器initializer）：字段、构造器、方法、嵌套类、静态初始化器以及实例初始化器之间。
 - 例外：两个相邻的字段(中间没有其他代码)之间的空行是可选的.这种空行主要用于按照需要对字段进行逻辑分组。
 2. 在方法内部，可以按照需要用于对语句进行逻辑分组。
 3. 第一个方法的前面和最后一个方法的后面的空行是可选的（既不鼓励也不反对）。
 4. 根据文档中其他部分的需要进行添加（比如3.3的Import语句小节）
 5. 
多个连续的空行是允许的，但是永远不会进行要求（或者鼓励）这么做。

####4.6.2 水平空白

除了语言或者其他编码规范的要求以外，并且不把文字、注释和Javadoc算在内的话，ASCII空格只可以出现在如下地方：
 
 1. 将同一行中的保留字（比如`if`、`for`或者`catch`）与后面的左括号（`（`）用空格分开。

 2. 将同一行中的保留字（比如`else`或者`catch`）与前面的右花括号(`}`)用空格分开。

 3. 左花括号的前面添加空格。只有下面两种情况可以例外：
  
  - `@SomeAnnotation({a, b})` (不需要空格)
  - `String[][] x = {{"foo"}}; `(在两个花括号之间不需要空格, by item 8 below)
 
 4. 两元和三元运算符的两侧要使用空格（比如 `+`、`-`、`&`、`=`、`a > b ? True : False`）。这也同样适用于和运算符类似的符号：
 
 - 在java泛型编程中的类型边界中的&符号：`<T extends Foo & Bar>`
 
 -  `catch`代码块中用于处理多种异常的竖杠`|`符号。 `catch (FooException | BarException e)`
 -  加强版的for语句（"`foreach`"）中的冒号(`:`）。
 5. `,`、`:`、`;`以及右括号（`）`）的后面
 6. 两个左斜杠(`//`)的两侧使用空格，用来开始该行的注释。在这里，多个空格也是可以的，但是不做强制要求。
 7. 在声明语句的类型名和变量之间要使用空格: ` List<String> list` 
 8. Optional just inside both braces of an array initializer
 8.在数组初始化中大括号里面的空格是可选的。 
 - `new int[] {5, 6}`和`new int[] { 5, 6 }`都是合法的。
>注意： 本规定并不对一行的开始和末尾的空格做出要求和禁止，而只是针对代码内部的空格。

####4.6.3 水平对齐：不需要

术语说明：水平对齐是一种在你的代码中间加入不定数量的额外空格来让本行的某些符号直接出现在上一行的某些符号的下面的实践方式。

这种方式是被接受的，但是Google编码风格并不会对此进行要求。Google甚至于不要求在那些已经采用了这种方式的地方来继续保持这种水平对齐。

下面分别是没有采用对齐和采用了对齐的例子：
```
private int x; // this is fine
private Color color; // this too
```
```
private int   x;      // permitted, but future edits
private Color color;  // may leave it unaligned
```
>小提示：对齐能够增加代码的可读性，但是它也为将来的维护制造了麻烦。设想一下，未来有一处改动本来只需要影响一行。而这一改动可能使得之前格式化好的代码被破坏掉，并且这是允许的。经常，它会提示写代码的人（可能是你自己）来调整相邻行的空格，而这会触发一连串的重新格式化。那最开始的一行改动现在有了一个“爆炸半径”。极端情况下，这可能造成大量无用的工作，就算是在最好的情况下，这也会破坏版本历史信息，减慢代码审查人员的review速度，并且会造成更多的merge冲突。

###4.7 分组圆括号：推荐

只有当作者和评审人员一致认为：去掉分组括号代码也不会被解释错误；而有了分组括号代码也不会更加易读；的时候，可选的分组括号才可以被省略。我们没有理由来假设所有读者都将整个Java操作符优先级表记得清清楚楚。
###4.8 具体结构

####4.8.1 枚举类
在每个枚举常量后面的逗号的后面， 换行与否都是可以的。

对于那些没有方法并且其枚举常量没有文档注释的枚举类可以根据需要选择像数组初始化那样进行格式化（见4.8.3.1小节，数组初始化）
```java
private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
Since enum classes are classes, all other rules for formatting classes apply.
```

####4.8.2 变量声明

#####4.8.2.1 每次声明一个变量
每行变量声明（字段或者局部变量）都只声明一个变量：不要使用像 `int a, b;`这样的变量声明。

#####4.8.2.2 需要的时候再声明，而初始化要尽可能早

不要像已经习惯的那样在所包含的代码块或者块状结构的开头部分声明局部变量。相反，局部变量应该在最靠近其首次使用的地方进行声明以将其作用域最小化。局部变量通常在声明的时候就进行初始化了，或者在声明之后立刻进行初始化。
####4.8.3 数组

#####4.8.3.1 数组初始化：可以是“块状形式”的。
所有的数组初始化都可以根据情况格式化成“块状结构”。下面这些样式都是合法的（并没有详尽地列出全部样式）：
```
new int[] {           new int[] {
  0, 1, 2, 3            0,
}                       1,
                        2,
new int[] {             3,
  0, 1,               }
  2, 3
}                     new int[]
                          {0, 1, 2, 3}
```

#####4.8.3.2 不要使用C语言风格的数组声明
方括号是类型的一部分，而不是变量的一部分，`String[] args`是正确的，不要使用`String args[]`。

####4.8.4 Switch语句

术语说明：在switch代码段的花括号里面的是一组或多组的代码。每组代码包含一个或者多个switch标签（要么是`case FOO:`，要么是`default:`），后面跟着一条或者多条语句。

#####4.8.4.1 缩进

和其他代码块一样，switch代码块的内容也是缩进2个字符。
在switch标签后面会另起一行，如果代码块还没结束，缩进层级加2，。如果switch代码块已经结束了，后面的switch标签会返回到之前的缩进层级。

#####4.8.4.2 落空处理（Fall-through）：注释

在一个switch代码块中，每组代码要么会突然结束（使用`break`、`continue`、`return`或者抛出异常），要么会使用注释来进行标记以表明代码可以继续执行到下一组代码。任何能够表达出代码会继续执行到下一组的含义的注释都是满足要求的（通常是`// fall through`）。switch代码块中的最后一组语句并不需要这个特殊的注释。比如：
```
switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```

#####4.8.4.3 列出default情况
每个switch语句都要包含一组default语句，即便它不包含任何代码。

####4.8.5 注解

作用到类、方法或者构造器上的注解是紧接着列在代码块旁边的，每条注解占一行（也就是每行一条注解）。它们之间的换行符并不构成断行（4.5小节，断行），所以并不会增加缩进层级。比如：
```
@Override
@Nullable
public String getNameIfPresent() { ... }
```
例外：如果只有一个注解并且该注解没有参数，那么它可以和签名（signature）的第一行列在一起，比如：
```
@Override public int hashCode() { ... }
```
作用到字段的注解也可以紧跟着代码块一起排列，但是在这种情况下，多个注解（也有可能是有参数的）是可以列在同一行的；比如：
```
@Partial @Mock DataLoader loader;
```
对于参数和局部变量的注解的格式，并没有具体的规范来进行要求。
#### 4.8.6 注释
#####4.8.6.1 块注释样式

块注释的缩进级别和它所包围的代码的缩进级别相同。它们可以采用 `/* ... */`样式，也可以采用`// ..`样式。对于多行的`/* ... */`注释，后面的注释行必须以`*`开头，`*`号要和上一行的`*`号对齐。
```
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```
不要用由星号或者其他的符号画出的方框来将注释围起来。


>小提示： 当书写多行的注释时，如果你想要在必要的时候用自动化的代码格式化工具来将这些注释重新组织进行断行（段落样式）时，你要使用`/* ... */`样式。大部分格式化工具并不能将`// ...`样式的注释块中的内容重新组织进行断行。

#### 4.8.7 修饰符

当使用类和成员修饰符时，它们要按照Java语言规范中建议的顺序来排列：
```java
public protected private abstract static final transient volatile synchronized native strictfp
```
 
####4.8.8 数字值
 
长整型的数字值要使用大写字母L作为后缀，永远不要使用小写字母（来避免和数字1产生混淆）。比如，使用`3000000000L`而不要使用`3000000000l`。

 
##5 命名

###5.1 适用于所有标识符的通用规范

标识符只能使用大小写形式的ASCII字母和数字以及下划线。所以每个合法的标识符名字都能与正则表达式`\w+`相匹配。

在Google的风格规范中，是不会使用像这些例子`name_`、`mName`、`s_name`和`kName`里特定的前缀或者后缀的。

###5.2 标识符规范

####5.2.1包名

 
包名是全部小写的，由连贯的单词简单地串在一起（没有下划线）。比如`example`, `com.example.deepspace`,而不是`com.example.deepSpace`或`com.example.deep_space`。
 
####5.2.2 类名
 
类名是使用首字母大写的驼峰式（UpperCamelCase）来定义的。
 
类名通常都是名词或者名词短语。比如`Character`或者`ImmutableList`。接口名也可以是名词或者名词短语（比如`List`）,但是有时候，它也可以是形容词或者形容词短语（比如`Readable`）

对于给注解类型进行命名，则没有专门的规则或者完善的约定来进行要求。
 
测试类的名字都是以所要测试的类的名字开头的，并且以Test结尾。比如`HashTest` 或者`HashIntegrationTest`。
 
####5.2.3 方法名
 
方法名采用的是首字母小写的驼峰式（lowerCamelCase）的风格。

方法名通常是动词或者动词短语。比如`sendMessage`或者`stop`。
 
下划线可以出现在JUnit的测试方法名称中，用于将测试方法的名称的各逻辑部分分开。 一种典型的模式就是`test<MethodUnderTest>_<state>`， 比如`testPop_emptyStack`。对于测试方法的命名，并不存在一种所谓的绝对正确的方式。
 
####5.2.4 常量名

常量名使用`CONSTANT_CASE`的格式：全大写，词与词之间采用下划线进行分割。但是到底什么是常量呢？
 
每个常量都是一个静态final字段，但是并不是所有的静态final字段都是常量。在选择使用常量命名规则时，要考虑这个字段是否真的是一个常量。比如，一个实例只要有一项状态信息对外可见并且能够发生变化，那么几乎可以肯定它不是一个常量。仅仅解释说这个对象永远不会发生变化通常是不够的。比如：
```
// Constants
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final Joiner COMMA_JOINER = Joiner.on(',');  // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```
 
它们的名称通常都是名词或者名词短语。
 
####5.2.5 非常量字段的名称
 
非常量字段的名称（静态或者非静态变量）是采用首字母小写的驼峰式的风格来命名的。
 
这些名称一般都是名词或者名词短语，比如`computedValues `或者`index`。
 
####5.2.6 参数名
 
参数名是采用首字母小写的驼峰式的风格来命名的。
 
应该避免使用只有一个字符的参数。
 
####5.2.7 局部变量名
 
局部变量的名字采用的是首字母小写的驼峰式的风格，相对于其他类型的名字，对局部变量的名字进行缩写的空间更大一些。
 
然而，单字符的名字还是要避免的，除非是用于临时变量和循环变量中。
 
即便局部变量是final和immutable的，它也不能被看做是常量，也不应该使用常量名字的样式。
 
####5.2.8 类型变量名
 
任意一个类型变量都应该采用下面两种样式中的一种来进行命名。
 - 单个大写字母，视情况需要后面可以添加一个数字（比如`E`、`T`、`X`、`T2`）
 
 - 以所使用的类的形式来命名（见5.2.2小节，类名），后面跟上一个大写字母T(比如`RequestT`、`FooBarT`)
 
###5.3 驼峰式命名法：
 
有时候，将一个英文短语转换成驼峰式的拼写样式有多重合理的方式，比如当出现类似于`“IPv6”`或者`“iOS”`这样的首字母缩写词或者独特的语法结构时，为了提高可预测性，Google风格规范指定了如下明确的方案。

Beginning with the prose form of the name:
首先列出没有处理过的原始的普通形式的名字：

Convert the phrase to plain ASCII and remove any apostrophes. For example, "Müller's algorithm" might become "Muellers algorithm".
 
 1. 将短语中的撇号（'）删除，将其他所有字符转换成纯ASCII码。比如`"Müller's algorithm"`会变成`"Müllers algorithm"`。

 2. 将结果分割成一个个的单词，分割的依据是空格和所保留的任意标点符号（通常是连接符）。
 - 建议：如果分割出来的单词已经是常用的约定好的驼峰式的拼写样式，那么就要将它再分割成更小的部分（比如将"AdWords"分成"ad words"）。需要注意的是，像`"iOS"`这样的单词并不是真正的驼峰式拼写，它不符合任何一种约定，所以该建议并不适用于它。
Now lowercase everything (including acronyms), then uppercase only the first character of:

 3. 现在，将所有单词都改成小写形式（包括首字母缩写的词），然后将首字母改成大写。
 - 将每个单词的首字母都大写，就构成了首字母大写的驼峰式拼写。
 - 将除了第一个单词之外的其他单词的首字母都大写，就构成了首字母小写的驼峰式拼写。

 4. 最后，将所有的单词连接起来就构成了一个标识符。
Note that the casing of the original words is almost entirely disregarded.
 需要注意的是，原先那些单词的大小写几乎都完全被忽略了。

例子：

|Prose form	         |Correct	     |Incorrect
| -------------          |:-------------:    | -----:|
|"XML HTTP request"      |XmlHttpRequest     |XMLHTTPRequest
|"new customer ID"       |newCustomerId	     |newCustomerID
|"inner stopwatch"       |innerStopwatch     |innerStopWatch
|"supports IPv6 on iOS?" |supportsIpv6OnIos  |supportsIPv6OnIOS
|"YouTube importer"	 |YouTubeImporter    |YoutubeImporter*


*号表示可以接受，但是并不推荐采用

注意：在英语中，有一些单词之间是否使用连接符并不明确：比如`"nonempty"`和`"non-empty"`都是正确的，所以，方法名`checkNonempty`和`checkNonEmpty`也同样都是正确的。
 
##6 编程实践
 
###6.1 @Override：要坚持使用
 
只要是符合语法的，就要使用@Override注解来将方法进行标记。这包括某个类的方法重载了其父类的方法、某个类方法实现了接口方法、某个接口方法重新声明父接口的方法。
 
例外：
    当父方法是@Deprecated的时候，可以将@Override省略掉。
 
###6.2 捕获异常：不能忽略


除了下面列出的情况，对于捕获的异常不作响应进行一些处理基本上可以确定是一个错误的选择。（通常的响应有进行日志记录，或者如果被认为是不可能发生的情况，应该将它作为`AssertionError`重新throw出去。）
 
如果确实不需要在catch代码块中做任何操作，那就需要在注释中解释其正当理由。
```
try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
```
Exception: In tests, a caught exception may be ignored without comment if it is named expected. The following is a very common idiom for ensuring that the method under test does throw an exception of the expected type, so a comment is unnecessary here.
例外：在测试中，如果捕获的异常是符合预期的，那么该异常就可以直接被忽略而不需要添加注释。下面的例子是一种非常常见的用法：保证被测试的方法抛出的异常是所预期的类型，这样就不需要注释了：
```
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```
 
###6.3 静态成员：限定为通过类来进行调用
 
必须对静态类成员的引用进行限制，它必须只能通过类的名称来进行引用，不能通过类所属的类型的引用或者表达式来进行调用：
```
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
```
 
###6.4 Finalizers： 不要使用
 
重载Object.finalize是极其罕见的。
 
>小提示： 不要使用。如果你绝对必须要使用的话，首先仔细地阅读和理解《Effective Java》一书的第7项，“Avoid Finalizers,”， 然后不要使用。
 
##7 Javadoc
 
###7.1格式化
 
####7.1.1 一般格式
 
Javadoc块的基本格式正如你在下面的例子所看到的：
```
/**
 * Multiple lines of Javadoc text are written here,
 * wrapped normally...
 */
public int method(String p1) { ... }
... or in this single-line example:

/** An especially short bit of Javadoc. */
```
 
这种基本样式始终都是合乎要求的。当没有其他子项@标记要列出来并且将整个Javadoc块（包括注释标记）放到一行中就足够时，可以使用单行的形式来代替。
 
####7.1.2 段落
 
位于“@标记”（如果有展示的话）之前的那些段落之间要有一个空行-也就是只包含着一个对齐的星号（*）的行。除了第一段之外的其他段落都需要在第一个单词之前添加一个<p>标记,它们之间不能有空格。
 
####7.1.3 @标记
 
所使用的所有标准的"@标记"都要按照`@param`、`@return`、 `@throws`、 `@deprecated`的顺序进行排列，并且它们的描述内容不能为空。
当@标记子项不能在一行中写完时，后续行要相对于@符号的位置缩进4个（或者更多）的空格。

 
###7.2 摘要片段（summary fragment）
 
每个类和成员的Javadoc都是从一段简洁的摘要片段开始的。这个片段非常重要：在像类和方法的索引这样的某种上下文中，它是唯一出现的文本。
 
这个片段是一个名词短语或者动词短语，而不是一条完整的句子。它既不会以`A {@code Foo} is a...`或者`This method returns...`这样的文字开头，也不会像`Save the record..`那样组成完成的命令式的句子。但是，由于该片段是首字母大写的，并且有标点符号，使得它看起来好像是一条完整的句子。
 
>**小提示**: 一个常见的错误就是以`/** @return the customer ID */`这样的形式来编写简单的Javadoc。这种方式是错误的，它应该改成`/** Returns the customer ID. */`。

 
###7.3 何处使用Javadoc

 
至少，Javadoc需要出现在每个public类以及该类的public或protected成员。只有在下面这些情况下例外：
 
其他的类和成员任然根据需要是有Javadoc的。不管什么时候，只要注释是用于定义类、方法或者字段的所有用途时，那么这条注释就应该写成Javadoc（这样就更加一致和对工具友好。）
 
####7.3.1 例外：自解释的方法
 
对于那些“简单、显而易见”的像`getFoo`这样的方法，Javadoc是可有可无的,在这种情况下，除了说“返回foo”之外，确实没有什么其他值得说的了。

>**重要提示**：当读者需要了解某些非常重要的信息时，拿着本条款来作为省略Javadoc信息的挡箭牌是不合适的。比如，有一个名为`getCanonicalName`的方法，如果读者不知道术语（canonical name）的含义，那么我们就不能（借口说Javadoc的内容只是`/** 返回规范化的名称（ canonical name）. */` 而）省略它的文档！

 
####7.3.2 例外:重载
 
对于那些将父类方法进行重载的方法，Javadoc并不总是需要提供的。

参考来源：
[@囧虎张建伟的博客][1]


  [1]: http://www.blogjava.net/zh-weir/archive/2014/02/08/409608.html