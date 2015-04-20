#Google Java编码规范中文版

[TOC]

##1 介绍

本文档**完整**地定义了Google公司使用java™语言编写源代码时所采用的编码规范。当且仅当java源文件遵循本规范时，我们才说它是符合Google风格的。

同其他编码风格指南一样，我们所讨论的内容不仅仅包括编码格式美观与否的问题，还囊括了其他类型的惯例约定或编码规范。然而，本文主要集中介绍的是我们所普遍遵循的**硬性规定**（**hard-and-fast rules**），并且避免提出一些不是很确定是否可以强制实施的建议(不论是由人还是工具来实施)。

###1.1 术语说明

在本文档中，除非另外声明：

单词class “类”用于表示的内容包括一个“普通”类、enum枚举类、接口或者注解类型（`@interface`）。
Other "terminology notes" will appear occasionally throughout the document.
词语comment指的是实现注释（implementation comments）。我们并不使用"文档注释（documentation comments）"一词，而是使用一个常用的术语“Javadoc”来代替。

###1.2 指南说明

本文档中的实例代码并不是标准。这就是说，尽管这些例子是符合Google风格的，但是它们并不能说明这是展示代码的唯一方式。不能将例子中所选择的那些本来是可选的格式化样式作为规则进行强制实施。

##2 源文件基本要素

###2.1 文件名

源文件名由它所包含的顶层类的名称以及`.java`扩展名组成，类的名称是对大小写敏感的。

###2.2 文件编码：UTF-8

源文件是采用UTF-8进行编码的。

###2.3 特殊字符

####2.3.1 空白字符
除了行结束符序列（译注：是指"\r\n"这种字符串）以外，ASCII水平间隔字符（0X20）（译注：即空格字符）是唯一能在源文件中出现的空白字符。这意味着：

1. 字符串中的所有其他空白字符都需要进行转义。
2.  Tab字符(也名制表符)**不能**用于缩进。


####2.3.2 特殊转义字符

对于那些具有特殊转义字符的字符(`\b`、`\t`、`\n`、`\f`、`\r`、`\"`、`\'`和`\\`)，我们使用转义字符，而非对应的十六进制数值（比如`\012`）或者Unicode（比如`\u000a`）转义符。

####2.3.3 非ASCII字符
对于其他的非ASCII字符，不管是使用真正的Unicode字符（比如`∞`）还是使用等价的Unicode转义符（比如`\u221e`)，这都是可以的，这仅仅取决于哪种方式能使代码**更加易于阅读和理解**。

`小提示：在使用Unicode转义符的情况下，有时候甚至是使用真正的Unicode字符的情况下，用注释来进行解释是非常有帮助的。`

例子：


| 案例 | 讨论 |
| -- | -- |
| ```String unitAbbrev = "μs";``` | 优，即便没有注释也是非常清晰的 |
| ```String unitAbbrev = "\u03bcs"; // "μs"``` | 可，但是没有必要这么做。|
|```String unitAbbrev = "\u03bcs"; // 希腊字母mu，"s" ```| 可, 累赘并且容易出现错误|
|```String unitAbbrev = "\u03bcs";``` | 差，读者不清楚这是什么东西。 |
|```return '\ufeff' + content; // BOM（byte order mark）字符``` | 好: 对打印不出来的字符使用转义符, 并在必要的情况下添加注释。 |




> 小提示：永远不要因为恐惧有一些程序不能正确地处理非ASCII字符而就让你的代码可读性变差。
> 如果真的出现无法处理非ASCII字符的情况，那些程序无法工作了，那么需要修复的是那些程序。
>

##3 源文件结构

一份源文件(按顺序)包含:

 1. 版权信息（如果存在的话）
 2. 包声明语句
 3. import语句
 4. 只有一个顶级类

在文件中，各部分之间要用一个空行进行分隔。


###3.1 许可证或版权信息（如果存在的话）


如果许可证或版权信息属于某个文件的话，它就应该放在这里。

###3.2 包声明语句

包声明语句不能换行。列限制（4.4小节，列限制：80或100）的规则不适用于包声明语句。

###3.3 Import语句
3.3.1 No wildcard imports
####3.3.1 Import指令语句
Wildcard imports, static or otherwise, are not used.
不要使用通配符式的import、static或者其他的import。
3.3.2 No line-wrapping

####3.3.2 不要换行
Import statements are not line-wrapped. The column limit (Section 4.4, Column limit: 80 or 100) does not apply to import statements.
Import指令不能换行。列限制（4.4小节，列限制：80或100）规则不适用于import指令。

3.3.3 Ordering and spacing
####3.3.3 顺序和间隔
Import statements are divided into the following groups, in this order, with each group separated by a single blank line:
Import指令语句会被按照下面的顺序分成几组，每组之间使用一个空行进行分割：

 1. 将所有的静态imports放到一组中
 2. `com.google` imports (只有当源文件在`com.google`包空间时)
 3. 第三方的包的imports，按照ASCII码排列顺序将每个顶级包分为一组，比如：`android`, `com`, `junit`, `org`, `sun`
 4. `java` imports
 5. `javax` imports

Within a group there are no blank lines, and the imported names appear in ASCII sort order. (Note: this is not the same as the import statements being in ASCII sort order; the presence of semicolons warps the result.)
同组里的语句之间没有空行，所导入的内容的名称按照ASCII的顺序进行排序（注意：这并不同于将import语句按照ASCII码的顺序进行排序，分号的存在会干扰结果。）
3.4 Class declaration
###3.4 类声明

3.4.1 Exactly one top-level class declaration
####3.4.1 只有一个顶级类声明
Each top-level class resides in a source file of its own.
每个顶级类都存在于同名的源文件中。
3.4.2 Class member ordering

####3.4.2 类成员顺序

The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it. Different classes may order their members differently.
一个类的成员的顺序对易学性有巨大的影响，但是并不存在一种正确的方式来明确如何进行排序。不同的类可能会以不同的方式对它们的成员进行排序。

What is important is that each class order its members in some logical order, which its maintainer could explain if asked. For example, new methods are not just habitually added to the end of the class, as that would yield "chronological by date added" ordering, which is not a logical ordering.
重要的是每个类都要采用某种逻辑顺序来对它的成员进行排序，一种在被别人问到的时候维护者能够将其解释清楚的逻辑顺序。比如，新的方法不能仅仅习惯性地添加到类的结尾那里，因为这会使得导致一种“按照添加的日期前后而排列”的顺序，这并不是一种逻辑顺序。
3.4.2.1 Overloads: never split
######3.4.2.1 重载：永远不要分割开

When a class has multiple constructors, or multiple methods with the same name, these appear sequentially, with no intervening members.
当一个类拥有多个构造函数或者多个同名的方法时，它们需要连续地列在一起，中间不能有其他成员。

4 Formatting
##4 格式

Terminology Note: block-like construct refers to the body of a class, method or constructor. Note that, by Section 4.8.3.1 on array initializers, any array initializer may optionally be treated as if it were a block-like construct.
术语说明：块状结构指的是类、方法或者构造函数的主体部分。需要注意的是，对于4.8.3.1小节中的数组初始化，所有的数组初始化都可以选择性地作为块状结构来进行处理。
4.1 Braces
###4.1 大括号
4.1.1 Braces are used where optional
####4.1.1 在可选的情况下，使用大括号
Braces are used with if, else, for, do and while statements, even when the body is empty or contains only a single statement.
在if、else、for、do和while语句中使用大括号，即使执行体为空或者只包含一条语句。

4.1.2 Nonempty blocks: K & R style
####4.1.2 非空代码块： K & R 风格
Braces follow the Kernighan and Ritchie style ("Egyptian brackets") for nonempty blocks and block-like constructs:
对于非空代码块以及块状结构，大括号要遵循Kernighan和Ritchie风格（埃及括号"Egyptian brackets"）：
No line break before the opening brace.
在左括号前不能换行。
Line break after the opening brace.
左括号后换行。
Line break before the closing brace.
在右括号前换行

Line break after the closing brace if that brace terminates a statement or the body of a method, constructor or named class. For example, there is no line break after the brace if it is followed by else or a comma.
只有当右括号是某个方法、构造函数或者所命名的类的主体部分或者一条语句的结束符的时候，才要在右括号后换行。比如，当括号后面跟着else或者逗号的时候，右括号后面就不换行了。
Example:
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
A few exceptions for enum classes are given in Section 4.8.1, Enum classes.
对于枚举类的一些例外情况在4.8.1小节枚举类中会进行描述。
4.1.3 Empty blocks: may be concise
####4.1.3 空代码块：
An empty block or block-like construct may be closed immediately after it is opened, with no characters or line break in between ({}), unless it is part of a multi-block statement (one that directly contains multiple blocks: if/else-if/else or try/catch/finally).
一个空的代码块或者块状结构可以在（{}）之间不包含任何字符或者换行，除非它是某个多种具有多个代码块的语句的一部分（一种直接包含多个代码块的语句有：if/else-if/else or try/catch/finally）
Example:
例子：
  void doNothing() {}
4.2 Block indentation: +2 spaces
4.2 块缩进：+2个空格

Each time a new block or block-like construct is opened, the indent increases by two spaces. When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block. (See the example in Section 4.1.2, Nonempty blocks: K & R Style.)
每次开始一个新的代码块或者块状结构时，缩进要增加两个空格。当代码块结束时，缩进要恢复到之前的缩进层级上来。缩进的层级同样适用于代码块中的代码和注释。

4.3 One statement per line
###4.3 每行一条语句

Each statement is followed by a line-break.
每条语句的后面具有一个换行符：
4.4 Column limit: 80 or 100
###4.4 每行的字符长度最大为80或100

Projects are free to choose a column limit of either 80 or 100 characters. Except as noted below, any line that would exceed this limit must be line-wrapped, as explained in Section 4.5, Line-wrapping.
各个项目可以随意选择是将80还是100作为每行最大的字符长度。除非遇到下面列出的情形，否则的话，那些超过最大字符长度的代码行必须按照第4.5小节（换行）中说明的那样进行换行。

Exceptions:
例外：

Lines where obeying the column limit is not possible (for example, a long URL in Javadoc, or a long JSNI method reference).
不可能遵循最大字符长度限制的行（比如，javadoc中很长的URL，或者一个很长的JSNI方法引用）
package and import statements (see Sections 3.2 Package statement and 3.3 Import statements).
package和import语句（见3.2小节中的Package语句和3.3小节的Import语句
Command lines in a comment that may be cut-and-pasted into a shell.
注释中可能会被复制-粘贴到shell中的命令行。
4.5 Line-wrapping
4.5 换行

Terminology Note: When code that might otherwise legally occupy a single line is divided into multiple lines, typically to avoid overflowing the column limit, this activity is called line-wrapping.
术语说明：当

There is no comprehensive, deterministic formula showing exactly how to line-wrap in every situation. Very often there are several valid ways to line-wrap the same piece of code.
并不存在一种全面的、确定性的准则来解释清楚在每种情况下该如何进行换行。很对时候，对同一块代码有好几种合法的换行方式。

Tip: Extracting a method or local variable may solve the problem without the need to line-wrap.
小提示：将方法或者本地变量抽取出来有可能就解决问题了，而不再需要进行换行了。

4.5.1 Where to break
####4.5.1 何处断行
The prime directive of line-wrapping is: prefer to break at a higher syntactic level. Also:
换行的主要最高指导原则是：倾向于在更高一些的语法级别上进行断行。还有：

When a line is broken at a non-assignment operator the break comes before the symbol. (Note that this is not the same practice used in Google style for other languages, such as C++ and JavaScript.)
当在非赋值运算符处进行断行时，断行要在运算符号之前。（译注：比如+号处进行断行的话，+号要处于下一行）（注意：这和 Google公司在其他语言（如C++和JavaScript）的编码风格所采用的做法有所不同）。

This also applies to the following "operator-like" symbols: the dot separator (.), the ampersand in type bounds (<T extends Foo & Bar>), and the pipe in catch blocks (catch (FooException | BarException e)).
这一规则同样适用于下列与运算符类似的符号：点分隔符(.)，类型绑定中的&符号 (<T extends Foo & Bar>)以及 catch代码块中的竖杠符号 (catch (FooException | BarException e))

When a line is broken at an assignment operator the break typically comes after the symbol, but either way is acceptable.
当在某个赋值运算符处断行时，通常是在运算符的后面进行断行，但是在前面断行也是可以接受的。

This also applies to the "assignment-operator-like" colon in an enhanced for ("foreach") statement.
这一规则也同样适用于("foreach")语句中和赋值运算符类似的冒号。

A method or constructor name stays attached to the open parenthesis (() that follows it.
方法或者构造函数的名称要和后面的左括号(()保持在同一行。

A comma (,) stays attached to the token that precedes it.
逗号（,)要和前面的内容在同一行。

4.5.2 Indent continuation lines at least +4 spaces
####4.5.2 后续行要缩进至少+4个空格字符
When line-wrapping, each line after the first (each continuation line) is indented at least +4 from the original line.
当进行换行时，第一行后面的每一行（也被称为续行）都要至少比第一行多缩进四个空格字符
When there are multiple continuation lines, indentation may be varied beyond +4 as desired. In general, two continuation lines use the same indentation level if and only if they begin with syntactically parallel elements.
当有多个续行时，缩进须比要求的+4个字符要多。通常，当且仅当两个续行开头的元素在语法上是并列关系的时候，这两个续行才使用相同的缩进级别。

Section 4.6.3 on Horizontal alignment addresses the discouraged practice of using a variable number of spaces to align certain tokens with previous lines.
4.6.3的水平对齐小节中指出使用数量不定的空格来将某些符号与前面行的符号对齐是一种被阻止的行为。
4.6 Whitespace
###4.6 空白

4.6.1 Vertical Whitespace
####4.6.1 垂直空白
A single blank line appears:
单个空行出现在：

Between consecutive members (or initializers) of a class: fields, constructors, methods, nested classes, static initializers, instance initializers.
某个类的那些相连的成员（或者初始化器initializer）：字段、构造器、方法、嵌套类、静态初始化器以及实例初始化器之间。
Exception: A blank line between two consecutive fields (having no other code between them) is optional. Such blank lines are used as needed to create logical groupings of fields.
例外：两个相连的字段(中间没有其他代码)之间的空行是可选的.这种空行主要用于按照需要对字段进行逻辑分组。
Within method bodies, as needed to create logical groupings of statements.
Optionally before the first member or after the last member of the class (neither encouraged nor discouraged).
在方法体内，可以按照需要用于对语句进行逻辑分组。
第一个方法的前面和最后一个方法的后面的空行是可选的（既不鼓励也不反对）。

As required by other sections of this document (such as Section 3.3, Import statements).
根据文档中其他部分的需要进行添加（比如3.3的Import指令小节）
Multiple consecutive blank lines are permitted, but never required (or encouraged).
多个连续的空行是允许的，但是永远不会进行要求（或者鼓励）。
4.6.2 Horizontal whitespace
####4.6.2 水平空白
Beyond where required by the language or other style rules, and apart from literals, comments and Javadoc, a single ASCII space also appears in the following places only.
除了语言或者其他编码规范的要求以外，不把文字、注释和Javadoc算在内的话，ASCII空格只可以出现在如下地方.
Separating any reserved word, such as if, for or catch, from an open parenthesis (() that follows it on that line
将同一行中的保留字（比如if、for或者catch）与后面的左括号（（）分开
Separating any reserved word, such as else or catch, from a closing curly brace  that precedes it on that line
将同一行中的保留字（比如else或者catch）与前面的右花括号(})分开

Before any open curly brace ({), with two exceptions:
做花括号的前面, 下面两种情况下例外：

@SomeAnnotation({a, b}) (不需要空格)
String[][] x = {{"foo"}}; (在`{` `{`之间不需要空格, by item 8 below)

On both sides of any binary or ternary operator. This also applies to the following "operator-like" symbols:
两元和三元运算符的两侧。这也同样适用于和运算符类似的符号。
the ampersand in a conjunctive type bound: <T extends Foo & Bar>
the pipe for a catch block that handles multiple exceptions: catch (FooException | BarException e)
the colon (:) in an enhanced for ("foreach") statement
After ,:; or the closing parenthesis ()) of a cast
On both sides of the double slash (//) that begins an end-of-line comment. Here, multiple spaces are allowed, but not required.
Between the type and variable of a declaration: List<String> list
Optional just inside both braces of an array initializer
new int[] {5, 6} and new int[] { 5, 6 } are both valid
Note: This rule never requires or forbids additional space at the start or end of a line, only interior space.

4.6.3 Horizontal alignment: never required
####4.6.3 水平对齐：不需要
Terminology Note: Horizontal alignment is the practice of adding a variable number of additional spaces in your code with the goal of making certain tokens appear directly below certain other tokens on previous lines.
术语说明：水平对齐
This practice is permitted, but is never required by Google Style. It is not even required to maintain horizontal alignment in places where it was already used.
这种方式是允许的，但是Google编码风格并不会对此进行要求。甚至于不要求在那些已经采用了这种方式的地方来继续保持这种水平对齐。
Here is an example without alignment, then using alignment:
下面分别是没有采用对齐和采用了对齐的例子：
```
private int x; // this is fine
private Color color; // this too
```
```
private int   x;      // permitted, but future edits
private Color color;  // may leave it unaligned
```
Tip: Alignment can aid readability, but it creates problems for future maintenance. Consider a future change that needs to touch just one line. This change may leave the formerly-pleasing formatting mangled, and that is allowed. More often it prompts the coder (perhaps you) to adjust whitespace on nearby lines as well, possibly triggering a cascading series of reformattings. That one-line change now has a "blast radius." This can at worst result in pointless busywork, but at best it still corrupts version history information, slows down reviewers and exacerbates merge conflicts.
小提示：对齐能够对可读性有所帮助，但是它为将来的维护制造了麻烦。考虑一下，未来有一处改动值需要影响一行。这一改动可能使得之前格式化好的代码被破坏掉，并且这是允许的。经常，它会提示写代码的人（可能是你自己）来调整相邻行的空格，而这回触发一连串的重新格式化。

4.7 Grouping parentheses: recommended
###4.7 分组圆括号：推荐
Optional grouping parentheses are omitted only when author and reviewer agree that there is no reasonable chance the code will be misinterpreted without them, nor would they have made the code easier to read. It is not reasonable to assume that every reader has the entire Java operator precedence table memorized.
只有当去掉分组括号，代码也没有机会被解释错误；而有了分组括号，代码也不会更加易读；并且作者和评审人员认可这种说法的时候，可选的分组括号才可以被省略。我们没有理由来假设所有读者都将整个Java操作符优先级表记得清清楚楚。
4.8 Specific constructs
###4.8 具体结构
4.8.1 Enum classes
####4.8.1 枚举类
After each comma that follows an enum constant, a line-break is optional.
在每个枚举常量后面要跟上一个逗号， 换行与否是可选的。
An enum class with no methods and no documentation on its constants may optionally be formatted as if it were an array initializer (see Section 4.8.3.1 on array initializers).
对于那些没有方法并且其枚举常量没有文档注释的枚举类可以根据需要选择像数组初始化那样进行格式化（见4.8.3.1小节，数组初始化）

private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
Since enum classes are classes, all other rules for formatting classes apply.

4.8.2 Variable declarations
####4.8.2 变量声明
4.8.2.1 One variable per declaration
#####4.8.2.1 每次声明一个变量
Every variable declaration (field or local) declares only one variable: declarations such as int a, b; are not used.
每行变量声明（字段或者局部变量）都只声明一个变量：不要使用像 `int a, b;`这样的变量。
4.8.2.2 Declared when needed, initialized as soon as possible
#####4.8.2.2 需要的时候再声明，而初始化要尽可能早
Local variables are not habitually declared at the start of their containing block or block-like construct. Instead, local variables are declared close to the point they are first used (within reason), to minimize their scope. Local variable declarations typically have initializers, or are initialized immediately after declaration.
不要像已经习惯的那样在所包含的代码块或者块状结构的开头部分声明局部变量。相反，局部变量应该在最靠近其首次使用的地方进行声明以将其作用域最小化局部变量，通常在声明的时候就进行初始化了，或者在声明之后立刻进行初始化。
4.8.3 Arrays
####4.8.3 数组
4.8.3.1 Array initializers: can be "block-like"
#####4.8.3.1 数组初始化：可以是“块状形式”的。
Any array initializer may optionally be formatted as if it were a "block-like construct." For example, the following are all valid (not an exhaustive list):
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
4.8.3.2 No C-style array declarations
#####4.8.3.2 不要使用C语言风格的数组声明
The square brackets form a part of the type, not the variable: String[] args, not String args[].
方括号是类型的一部分，而不是变量的一部分，`String[] args`是正确的，不要使用`String args[]`。

4.8.4 Switch statements
####4.8.4 Switch语句
Terminology Note: Inside the braces of a switch block are one or more statement groups. Each statement group consists of one or more switch labels (either case FOO: or default:), followed by one or more statements.
术语说明：在switch代码块的花括号中的是一组或多组的代码。每组代码包含一个或者多个switch标签（要么是`case FOO:`，要么是`default:`），后面跟着一条或者多条语句。
4.8.4.1 Indentation
#####4.8.4.1 缩进
As with any other block, the contents of a switch block are indented +2.
和其他代码块一样，switch代码块的内容也是缩进2个字符。
After a switch label, a newline appears, and the indentation level is increased +2, exactly as if a block were being opened. The following switch label returns to the previous indentation level, as if a block had been closed.
在switch标签后面会另起一行，如果代码块还没结束，缩进层级加2，。如果switch代码块已经结束了，后面的内容会返回到之前的缩进层级。

4.8.4.2 Fall-through: commented
#####4.8.4.2 落空处理：注释
Within a switch block, each statement group either terminates abruptly (with a break, continue, return or thrown exception), or is marked with a comment to indicate that execution will or might continue into the next statement group. Any comment that communicates the idea of fall-through is sufficient (typically // fall through). This special comment is not required in the last statement group of the switch block. Example:
在一个switch代码块中，每组代码要么是突然中止的（使用`break`、`continue`、`return`或者抛出异常），要么是用注释来进行标记来表明代码可以执行到下一组代码。任何能够表示出落空处理的意思的注释都是足够的（通常是`// fall through`）。switch代码块中的最后一组语句并不需要这个特殊的注释。比如：
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
4.8.4.3 The default case is present
#####4.8.4.3 列出default情况
Each switch statement includes a default statement group, even if it contains no code.
每个switch语句都要包含一组default语句，即便它不包含任何代码。

4.8.5 Annotations
####4.8.5 注解
Annotations applying to a class, method or constructor appear immediately after the documentation block, and each annotation is listed on a line of its own (that is, one annotation per line). These line breaks do not constitute line-wrapping (Section 4.5, Line-wrapping), so the indentation level is not increased. Example:
应用到类、方法或者构造器上的注解是紧接着文档块展示的，每个注解占据一行。它们之间的换行符并不构成自动换行（4.5小节，自动换行）。所以缩进层级并不会增加。比如：
```
@Override
@Nullable
public String getNameIfPresent() { ... }
```
Exception: A single parameterless annotation may instead appear together with the first line of the signature, for example:
例外：如果只有一个注解并且该注解也没有参数，那么它可以和签名的第一行列在一起，比如：
```
@Override public int hashCode() { ... }
```
Annotations applying to a field also appear immediately after the documentation block, but in this case, multiple annotations (possibly parameterized) may be listed on the same line; for example:
应用到字段的注解也可以紧跟着文档块一起出现，但是在这种情况下，多个注解（也有可能是有参数的）可以列在同一行；比如：

```
@Partial @Mock DataLoader loader;
```
There are no specific rules for formatting parameter and local variable annotations.
对于参数和局部变量的注解并没有明确的规范来进行格式化。
4.8.6 Comments

4.8.6.1 Block comment style
#####4.8.6.1 块注释样式
Block comments are indented at the same level as the surrounding code. They may be in /* ... */ style or // ... style. For multi-line /* ... */ comments, subsequent lines must start with * aligned with the * on the previous line.
块注释的缩进级别和它所包围的代码的缩进级别相同。它们可以采用 `/* ... */`样式，也可以采用`// ..`样式。对于多行的`/* ... */`注释，后面的注释行必须以*开头，*号要和上一行的*号对齐。
```
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```
Comments are not enclosed in boxes drawn with asterisks or other characters.
不能用由星号或者其他的符号来画出的方框来将注释包起来。

Tip: When writing multi-line comments, use the /* ... */ style if you want automatic code formatters to re-wrap the lines when necessary (paragraph-style). Most formatters don't re-wrap lines in // ... style comment blocks.
小提示： 当书写多行的注释时，如果你想要用自动代码格式化工具在必要的时候（比如分段样式）来将这些注释重新组织换行时，你要使用`/* ... */`样式。大部分格式化工具并不能将`// ...`样式的注释块中的内容重新组织进行换行。
4.8.7 Modifiers
#### 4.8.7 修饰符
Class and member modifiers, when present, appear in the order recommended by the Java Language Specification:
当使用类和成员修饰符时，它们要按照Java语言规范中建议的顺序来排列：

`public`、`protected`、`private`、`abstract`、`static`、`final`、`transient` 、`volatile`、`synchronized`、`native`、`strictfp`。
4.8.8 Numeric Literals
####4.8.8 数值
long-valued integer literals use an uppercase L suffix, never lowercase (to avoid confusion with the digit 1). For example, 3000000000L rather than 3000000000l.
长整型的字面值要使用大写字母L作为后缀，永远不要使用小写字母（来避免和数字1产生混淆）。比如，使用`3000000000L`而不要使用`3000000000l`。

5 Naming
##5 命名


5.1 Rules common to all identifiers
###5.1 适用于所有标识符的通用规范

Identifiers use only ASCII letters and digits, and in two cases noted below, underscores. Thus each valid identifier name is matched by the regular expression \w+ .
标识符只能使用ASCII字母和数字，。 所以每个合法的标识符名字都能与正则表达式`\w+`相匹配。
In Google Style special prefixes or suffixes, like those seen in the examples name_, mName, s_name and kName, are not used.
在Google的风格规范中，像这些例子`name_`、`mName`、`s_name`和`kName`里特定的前缀或者后缀是不会使用的。

5.2 Rules by identifier type
###5.2 标识符规范

5.2.1 Package names
####5.2.1包名

Package names are all lowercase, with consecutive words simply concatenated together (no underscores). For example, com.example.deepspace, not com.example.deepSpace or com.example.deep_space.
包名是全部小写的，由连贯的单词简单地串在一起（没有下划线）。比如`example`, `com.example.deepspace`,而不是`com.example.deepSpace`或`com.example.deep_space`这种。

5.2.2 Class names
####5.2.2 类名
Class names are written in UpperCamelCase.
类名是才用首字母大写的驼峰式（UpperCamelCase）来定义的。
Class names are typically nouns or noun phrases. For example, Character or ImmutableList. Interface names may also be nouns or noun phrases (for example, List), but may sometimes be adjectives or adjective phrases instead (for example, Readable).
类名是标准的名词或者名词短语。比如`Character`或者`ImmutableList`。接口名也可以是名词或者名词短语（比如`List`）,但是有时候，它也可以是形容词或者形容词短语（比如`Readable`）

There are no specific rules or even well-established conventions for naming annotation types.
并不存在专门的规则或者完善的约定来用于给注解类型进行命名。
Test classes are named starting with the name of the class they are testing, and ending with Test. For example, HashTest or HashIntegrationTest.
测试类的名字都是以所要测试的类的名字开头的，并且以Test结尾。比如`HashTest` 或者`HashIntegrationTest`。
5.2.3 Method names
####5.2.3 方法名
Method names are written in lowerCamelCase.
方法名采用的是首字母消息的驼峰式（lowerCamelCase）的风格
Method names are typically verbs or verb phrases. For example, sendMessage or stop.
方法名通常是动词或者动词短语。比如`sendMessage`或者`stop`。
Underscores may appear in JUnit test method names to separate logical components of the name. One typical pattern is test<MethodUnderTest>_<state>, for example testPop_emptyStack. There is no One Correct Way to name test methods.
下划线可以出现在JUnit的测试方法名称中用于将测试方法的名称的各逻辑部分进行区分。 一种典型的模式就是`test<MethodUnderTest>_<state>`， 比如`testPop_emptyStack`。对于测试方法的命名，并不存在一种所谓的“正确”方式。
5.2.4 Constant names
####5.2.4 常量名
Constant names use CONSTANT_CASE: all uppercase letters, with words separated by underscores. But what is a constant, exactly?
常量名使用`CONSTANT_CASE`的格式：全大写，词与词之间采用下划线进行分割。但是到底什么是常量呢？
Every constant is a static final field, but not all static final fields are constants. Before choosing constant case, consider whether the field really feels like a constant. For example, if any of that instance's observable state can change, it is almost certainly not a constant. Merely intending to never mutate the object is generally not enough. Examples:
每个常量都是一个静态final字段，但是并不是所有的静态final字段都是常量。在选择常量条款来命名时，要考虑这个字段是否真的是一个常量。比如，一个实例的只要有一项状态信息对外可见并且能够发生变化，那么几乎可以肯定它不是一个常量。仅仅解释说这个对象永远不会发生变化通常是不够的。比如：
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
These names are typically nouns or noun phrases.
它们的名称通常都是名词或者名词短语。
5.2.5 Non-constant field names
####5.2.5 非常量字段的名称
Non-constant field names (static or otherwise) are written in lowerCamelCase.
非常量字段的名称（静态或者非静态变量）是采用首字母小写的驼峰式的风格来命名的。
These names are typically nouns or noun phrases. For example, computedValues or index.
这些名称一般都是名词或者名词短语，比如`computedValues `或者`index`。

5.2.6 Parameter names
####5.2.6 参数名

Parameter names are written in lowerCamelCase.
参数名是采用首字母小写的驼峰式的风格来命名。
One-character parameter names should be avoided.
应该避免使用只有一个字符的参数。
5.2.7 Local variable names
####5.2.7 局部变量名
Local variable names are written in lowerCamelCase, and can be abbreviated more liberally than other types of names.
局部变量的名字采用的是首字母小写的驼峰式的风格，相对于其他类型的名字，对局部变量的名字进行缩写的空间更大一些。
However, one-character names should be avoided, except for temporary and looping variables.
然而，单字符的名字还是要避免的，除非是用于临时变量和循环变量中。
Even when final and immutable, local variables are not considered to be constants, and should not be styled as constants.
即便局部变量是final和immutable的，它也不能被看做是常量，也不应该使用常量名字的样式。
5.2.8 Type variable names
####5.2.8 类型变量名
Each type variable is named in one of two styles:
任意一个类型变量都应该采用下面两种样式中的一种来进行命名。
A single capital letter, optionally followed by a single numeral (such as E, T, X, T2)
单个的大写字母，视情况需要后面可以添加一个数字（比如`E`、`T`、`X`、`T2`）
A name in the form used for classes (see Section 5.2.2, Class names), followed by the capital letter T (examples: RequestT, FooBarT).
以所使用的类的形式来命名（见5.2.2小节，类名），后面跟上一个大写字母T(比如`RequestT`、`FooBarT`)
5.3 Camel case: defined
###5.3 驼峰式命名法：
Sometimes there is more than one reasonable way to convert an English phrase into camel case, such as when acronyms or unusual constructs like "IPv6" or "iOS" are present. To improve predictability, Google Style specifies the following (nearly) deterministic scheme.
有时候，有多种合理的方式来将一个英文短语转换成驼峰式的拼写样式，比如当类似于`“IPv6”`或者`“iOS”`这样的首字母缩写或者独特的语法结构出现时。为了提高可预测性，Google风格规范指定了如下明确的方案。

Beginning with the prose form of the name:


Convert the phrase to plain ASCII and remove any apostrophes. For example, "Müller's algorithm" might become "Muellers algorithm".
将短语中的撇号（'）删除，将其他所有字符转换成纯ASCII码。比如`"Müller's algorithm"`会变成`"Müllers algorithm"`。
Divide this result into words, splitting on spaces and any remaining punctuation (typically hyphens).
将结果分割成一个个的单词，分割的依据是空格和所保留的任意标点符号（通常是连接符）。
Recommended: if any word already has a conventional camel-case appearance in common usage, split this into its constituent parts (e.g., "AdWords" becomes "ad words"). Note that a word such as "iOS" is not really in camel case per se; it defies any convention, so this recommendation does not apply.
建议：如果分割出来的单词已经是常用的约定好的驼峰式的拼写样式，那么就要将它再分割成更小的部分（比如将`AdWords`分成`ad words`）。需要注意的是，像`"iOS"`这样的单词并不是真正的驼峰式拼写，它不符合任何一种约定，所以该建议并不适用于它。
Now lowercase everything (including acronyms), then uppercase only the first character of:
现在将所有内容都进行小写（包括首字母缩写的词），然后只将首字母进行大写，最后，将所有的单词连接起来就构成了一个标识符。
... each word, to yield upper camel case, or
将每个单词的首字母都大写，就构成了首字母大写的驼峰式拼写。
... each word except the first, to yield lower camel case
将除了第一个单词之外的其他单词的首字母都大写，就构成了首字母小写的驼峰式拼写。
Finally, join all the words into a single identifier.
Note that the casing of the original words is almost entirely disregarded.
需要注意的是，原先那些单词的大小写几乎都完全被忽视了。
Examples:

|Prose form	         |Correct	     |Incorrect
| -------------          |:-------------:    | -----:|
|"XML HTTP request"      |XmlHttpRequest     |XMLHTTPRequest
|"new customer ID"       |newCustomerId	     |newCustomerID
|"inner stopwatch"       |innerStopwatch     |innerStopWatch
|"supports IPv6 on iOS?" |supportsIpv6OnIos  |supportsIPv6OnIOS
|"YouTube importer"	 |YouTubeImporter    |YoutubeImporter*

*Acceptable, but not recommended.
*号表示可以接受，但是并不推荐采用
Note: Some words are ambiguously hyphenated in the English language: for example "nonempty" and "non-empty" are both correct, so the method names checkNonempty and checkNonEmpty are likewise both correct.
注意：在英文语言中，有一些单词之间是否使用连接符并不明确：比如`"nonempty"`和`"non-empty"`都是正确的，这样，方法名`checkNonempty`和`checkNonEmpty`同样也都是正确的。
6 Programming Practices
##6 编程实践
6.1 @Override: always used
###6.1 @Override：一直都要使用
A method is marked with the @Override annotation whenever it is legal. This includes a class method overriding a superclass method, a class method implementing an interface method, and an interface method respecifying a superinterface method.
只要是符合语法的，就要使用@Override注解来将方法进行标记。这包括某个类的方法重载了其父类的方法、某个类方法实现了接口方法、某个接口方法重新声明负借口的方法。
Exception:@Override may be omitted when the parent method is @Deprecated.
例外：当父方法是@Deprecated的时候，可以将@Override省略掉。
6.2 Caught exceptions: not ignored
###6.2 捕获异常：不能忽略

Except as noted below, it is very rarely correct to do nothing in response to a caught exception. (Typical responses are to log it, or if it is considered "impossible", rethrow it as an AssertionError.)

除了下面列出的情况，对于捕获的异常无所作为不作响应很少是正确的。（标准的响应有进行日志记录，或者如果被认为是不可能发生的情况，应该将它作为`AssertionError`重新throw出去。）
When it truly is appropriate to take no action whatsoever in a catch block, the reason this is justified is explained in a comment.
如果确实不需要在catch代码块中做任何操作，就需要在注释中解释其正当理由。
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
例外：在测试中，如果捕获的异常是符合预期的，那么该异常就可以直接忽略而不需要添加注释。下面的例子是一个非常常见的用法：保证被测试的方法抛出一个与其类型的异常，这样就不需要注释了：
```
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```
6.3 Static members: qualified using class
###6.3 静态成员：限定为使用类来进行调用

When a reference to a static class member must be qualified, it is qualified with that class's name, not with a reference or expression of that class's type.
对静态类成员的引用必须进行限制，它必须只能由类的名称进行引用，不能是是类所属于的类型的引用或者表达式：
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
6.4 Finalizers: not used
###6.4 Finalizers： 不要使用
It is extremely rare to override Object.finalize.
重载Object.finalize是极其罕见的。
Tip: Don't do it. If you absolutely must, first read and understand Effective Java Item 7, "Avoid Finalizers," very carefully, and then don't do it.
小提示： 不要使用。如果你绝对必须要使用的话，首先仔细地阅读和理解《Effective Java》一书的第7项，“Avoid Finalizers,”， 然后不要使用。
7 Javadoc
##7 Javadoc
7.1 Formatting
###7.1格式化
7.1.1 General form
####7.1.1 一般格式
The basic formatting of Javadoc blocks is as seen in this example:
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
The basic form is always acceptable. The single-line form may be substituted when there are no at-clauses present, and the entirety of the Javadoc block (including comment markers) can fit on a single line.
这种基本格式一直都是被认可的。当没有其他子项标记要记录并且将整个Javadoc块（包括注释标记）放到一行中就足够时，可以使用单行的形式来代替。
7.1.2 Paragraphs
####7.1.2 段落
One blank line—that is, a line containing only the aligned leading asterisk (*)—appears between paragraphs, and before the group of "at-clauses" if present. Each paragraph but the first has <p> immediately before the first word, with no space after.
位于“@标记”（如果有记录的话）之前的那些段落之间要有一个空行-也就是只包含着一个对齐的星号（*）的行。除了第一段之外的其他段落都需要在第一个单词之前有一个<p>标记,它们之间不能有空格。
7.1.3 At-clauses
####7.1.3 @标记
Any of the standard "at-clauses" that are used appear in the order @param, @return, @throws, @deprecated, and these four types never appear with an empty description. When an at-clause doesn't fit on a single line, continuation lines are indented four (or more) spaces from the position of the @.
所使用的所有"@标记"都要按照@param、 @return、 @throws、 @deprecated的顺序进行编写，并且它们的描述内容不能为空。
当@标记子项不能在一行中写完时，后续行要相对于@符号的位置缩进4个（或者更多）的空格。

7.2 The summary fragment
###7.2
The Javadoc for each class and member begins with a brief summary fragment. This fragment is very important: it is the only part of the text that appears in certain contexts such as class and method indexes.
每个类和成员的Javadoc都是从一段简洁的概述片段开始的。这个片段非常重要：它是唯一出现在像类和方法索引这样的某种上下文中的文本。
This is a fragment—a noun phrase or verb phrase, not a complete sentence. It does not begin with A {@code Foo} is a..., or This method returns..., nor does it form a complete imperative sentence like Save the record.. However, the fragment is capitalized and punctuated as if it were a complete sentence.
这个片段是一个名词短语或者动词短语，而不是一条完整的句子。它既不会以`A {@code Foo} is a...`或者`This method returns...`这样的文字开头，也不会像`Save the record..`那样组成完成的命令式的句子。但是，由于该片段是首字母大写的，并且有标点符号，使得它看起来好像是一条完整的句子。
Tip: A common mistake is to write simple Javadoc in the form /** @return the customer ID */. This is incorrect, and should be changed to /** Returns the customer ID. */.
小提示
一个常见的错误就是以`/** @return the customer ID */`这样的形式来编写简单的Javadoc。这种方式是错误的，它应该改成`/** Returns the customer ID. */`。

7.3 Where Javadoc is used
###7.3 何处使用Javadoc

At the minimum, Javadoc is present for every public class, and every public or protected member of such a class, with a few exceptions noted below.
至少，Javadoc需要出现在每个public类以及该类的public或protected成员。只有在下面这些情况下例外：
Other classes and members still have Javadoc as needed. Whenever an implementation comment would be used to define the overall purpose or behavior of a class, method or field, that comment is written as Javadoc instead. (It's more uniform, and more tool-friendly.)
其他的类和成员任然根据需要是有Javadoc的。不管什么时候，只要注释是用于定义类、方法或者字段的所有用途时，那么这条注释就应该写成Javadoc（这样就更加一致和对工具友好。）

7.3.1 Exception: self-explanatory methods
###7.3.1例外：自解释的方法
Javadoc is optional for "simple, obvious" methods like getFoo, in cases where there really and truly is nothing else worthwhile to say but "Returns the foo".
对于那些“简单、显而易见”的像`getFoo`这样的方法，Javadoc是可选的,在这种情况下，除了说“返回foo”之外，确实没有什么其他值得做的了。
Important: it is not appropriate to cite this exception to justify omitting relevant information that a typical reader might need to know. For example, for a method named getCanonicalName, don't omit its documentation (with the rationale that it would say only /** Returns the canonical name. */) if a typical reader may have no idea what the term "canonical name" means!
重要提示：也许某些非常重要的信息是许多读者需要了解的，那么拿着该条款来作为将该信息省略的依据是不恰当的。比如，有一个名为`getCanonicalName`的方法，如果读者不知道术语（canonical name）的含义，那么我们就不能（借口说Javadoc的内容只是/** 返回规范化的名称（ canonical name）. */ 而）省略它的文档！

7.3.2 Exception: overrides
####7.3.2 例外:重载

Javadoc is not always present on a method that overrides a supertype method.
对于那些将父类方法进行重载的方法，Javadoc并不总是需要提供的。
