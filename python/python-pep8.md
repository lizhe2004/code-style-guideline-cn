 
#PEP 8——Python编码风格指南
标签（空格分隔）： Python PEP8 编码规范
---
[TOC]
 
#介绍
This document gives coding conventions for the Python code comprising the standard library in the main Python distribution. Please see the companion informational PEP describing style guidelines for the C code in the C implementation of Python [1] .
本文提供的编码规范用于Python主发行版中的标准库的那些代码。对于Python的C语言实现中的C代码，请参考其他的PEP。

This document and PEP 257 (Docstring Conventions) were adapted from Guido's original Python Style Guide essay, with some additions from Barry's style guide [2] .
本文档和PEP 257(Docstring约定)改编自Guido的早起的Python风格指南文章，并且添加了一些Barry的风格指南的内容。
This style guide evolves over time as additional conventions are identified and past conventions are rendered obsolete by changes in the language itself.
本风格指南会随着时间不断演化，因为会有新的约定被大家所认同，而又有一些老的约定会由于语言本身的改变而逐渐被废弃。
Many projects have their own coding style guidelines. In the event of any conflicts, such project-specific guides take precedence for that project.

A Foolish Consistency is the Hobgoblin of Little Minds
One of Guido's key insights is that code is read much more often than it is written. The guidelines provided here are intended to improve the readability of code and make it consistent across the wide spectrum of Python code. As PEP 20 says, "Readability counts".

A style guide is about consistency. Consistency with this style guide is important. Consistency within a project is more important. Consistency within one module or function is most important.

But most importantly: know when to be inconsistent -- sometimes the style guide just doesn't apply. When in doubt, use your best judgment. Look at other examples and decide what looks best. And don't hesitate to ask!

In particular: do not break backwards compatibility just to comply with this PEP!

Some other good reasons to ignore a particular guideline:

When applying the guideline would make the code less readable, even for someone who is used to reading code that follows this PEP.
To be consistent with surrounding code that also breaks it (maybe for historic reasons) -- although this is also an opportunity to clean up someone else's mess (in true XP style).
Because the code in question predates the introduction of the guideline and there is no other reason to be modifying that code.
When the code needs to remain compatible with older versions of Python that don't support the feature recommended by the style guide.
##Code lay-out
##代码布局
###Indentation
###缩进
Use 4 spaces per indentation level.
每一级缩进使用4个空格。
Continuation lines should align wrapped elements either vertically using Python's implicit line joining inside parentheses, brackets and braces, or using a hanging indent  . When using a hanging indent the following considerations should be applied; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.
续行应该将换行的元素垂直对齐，可以使用Python的圆括号、方括号、花括号中的隐式的连接符，也可以使用悬挂式缩进[5]。当采用悬挂式缩进方式时，应该符合下列考虑条件：第一行不应该有参数，而且应该能够清楚无误地将后面采用缩进的行作为后续行从其他行中区分出来。
Yes:
```python
# Aligned with opening delimiter.
# 使用分隔符来对齐
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# More indentation included to distinguish this from the rest.
# 多使用一些缩进来与其他行进行区分
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
# 悬挂式缩进应该增加一个级别。
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```
No:
```python
# Arguments on first line forbidden when not using vertical alignment.
# 当不使用垂直对齐方式时，第一行不能有参数
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# Further indentation required as indentation is not distinguishable.
# 需要增加额外的缩进，因为现在的续行的缩进不够明显，不能将其与其他行的缩进区分开来
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```
The 4-space rule is optional for continuation lines.
 对于续行而言，4个空格的规定是可选的。
Optional:
```python
# Hanging indents *may* be indented to other than 4 spaces.
# 悬挂式缩进的空格个数*可以*不为4。
foo = long_function_name(
  var_one, var_two,
  var_three, var_four)
```
When the conditional part of an if -statement is long enough to require that it be written across multiple lines, it's worth noting that the combination of a two character keyword (i.e. if ), plus a single space, plus an opening parenthesis creates a natural 4-space indent for the subsequent lines of the multiline conditional. This can produce a visual conflict with the indented suite of code nested inside the if -statement, which would also naturally be indented to 4 spaces. This PEP takes no explicit position on how (or whether) to further visually distinguish such conditional lines from the nested suite inside the if -statement. Acceptable options in this situation include, but are not limited to:
当if语句由于条件判断部分太长而需要跨多行时，值得注意的是，这一两个字母的关键字（比如if）加上一个空格，再加上一个左括号，就使得需要在这一多行的条件语句的后面添加4个空格的缩进，这是很自然的事情。   这可能会与if语句所嵌套的那套分支代码产生视觉上的冲突，因为很自然地，分支执行代码也是缩进4个空格的。对于如何（或者是否要）将条件判断语句与if语句中的分支代码明确地区分出来，本PEP文档没有明确的立场。对于这种情况，下面的选项都是可以接受的，但是又不限于此：

```python
# No extra indentation.
# 没有多余缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# Add a comment, which will provide some distinction in editors
# supporting syntax highlighting.
# 添加一条注释来在编辑器中提供一些不同之处
# 支持与语法高亮
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    # 当两种条件都为true时，我们可以执行操作
    do_something()

# Add some extra indentation on the conditional continuation line.
# 在条件判断语句所在行添加一些额外的缩进
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```
The closing brace/bracket/parenthesis on multi-line constructs may either line up under the first non-whitespace character of the last line of list, as in:
在多行的代码结构中，右花括号/中括号/小括号可以排在列出的元素的最后一行的第一个非空格字符的下面，比如：
```python
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```
or it may be lined up under the first character of the line that starts the multi-line construct, as in:
也可以排在该多行代码结构的起始行的第一个字符下面。
```python
my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
```
Tabs or Spaces?
Tab键还是空格键？
Spaces are the preferred indentation method.
空格是首选的缩进方法。
Tabs should be used solely to remain consistent with code that is already indented with tabs.
Tab符只能用在哪些已经使用tab符来进行缩进的代码中用来保持一致性。
Python 3 disallows mixing the use of tabs and spaces for indentation.
Python 3 不允许将tab和空格键混合使用用于缩进。
Python 2 code indented with a mixture of tabs and spaces should be converted to using spaces exclusively.
Python 2 中混合使用tab和空格来进行缩进的代码必须转换成仅仅使用空格。

When invoking the Python 2 command line interpreter with the -t option, it issues warnings about code that illegally mixes tabs and spaces. When using -tt these warnings become errors. These options are highly recommended!
当使用-t 选项来调用Python 2的命令行解释器时，它对那些非法混合使用tab和空格的代码会发出警告。而当使用-tt选项时，这些warning就会变成error。强烈推荐使用这些选项。
Maximum Line Length
行的最大长度
Limit all lines to a maximum of 79 characters.
所有行的最大长度是79个字符。
For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters.
对于那些结构化限制比较少的连贯的比较长的文本块（docstring或者注释），每行的长度应该限制为72个字符。
Limiting the required editor window width makes it possible to have several files open side-by-side, and works well when using code review tools that present the two versions in adjacent columns.
对所要求的编辑器的窗口宽度进行限制就可以并排打开多个文件了，而当使用代码review工具来在相邻的两列窗口中分别显示两个版本的内容时，效果很好。
The default wrapping in most tools disrupts the visual structure of the code, making it more difficult to understand. The limits are chosen to avoid wrapping in editors with the window width set to 80, even if the tool places a marker glyph in the final column when wrapping lines. Some web based tools may not offer dynamic line wrapping at all.
大部分的工具的默认换行功能会破坏代码的可视化结构，使得代码更加难以理解。选择这个数值作为限制是用于避免在窗口宽度设为80的编辑器中出现代码换行的情况。

Some teams strongly prefer a longer line length. For code maintained exclusively or primarily by a team that can reach agreement on this issue, it is okay to increase the nominal line length from 80 to 100 characters (effectively increasing the maximum length to 99 characters), provided that comments and docstrings are still wrapped at 72 characters.
有一些团队更加倾向于更长一些的行最大长度。如果代码只由或者主要由一个团队维护，并且这个团队能够在这个问题上达成一致，那么在将注释和docstring的长度保留在72个字符串的限制的前提下，行最大长度从80增加到100个字符（）是没有问题的。

The Python standard library is conservative and requires limiting lines to 79 characters (and docstrings/comments to 72).
Python标准库是保守的，它要求将每行限制为79个字符（docstring/注释 则限制为72个字符）。
The preferred way of wrapping long lines is by using Python's implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation.

对于那些比较长的行进行换行的首先方式是使用Python中花括号、中括号、圆括号里面的隐含的连续符。可以通过将圆括号中的表达式换行来把较长的行产分成多行。这种续行的使用方式应该优先于使用右斜杠（\）符号的方式。
Backslashes may still be appropriate at times. For example, long, multiple with -statements cannot use implicit continuation, so backslashes are acceptable:
有些时候，右斜杠可以比较合适的。比如，比较长的多行的 with语句不能使用隐式的连接方式，所以右斜杠是可以接受的：

```python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```
(See the previous discussion on multiline if-statements for further thoughts on the indentation of such multiline with -statements.)
（参考之前对多行的if语句的讨论，来对这种多行的with语句中的缩进作进一步思考）
Another such case is with assert statements.
另一个使用右斜杠的例子就是 `assert`语句。

Make sure to indent the continued line appropriately. The preferred place to break around a binary operator is after the operator, not before it. Some examples:
要确保对续行进行适当的缩进。在二进制操作符处进行换行的首先位置是该操作符的后面，而不是前面。比如
```python
class Rectangle(Blob):

    def __init__(self, width, height,
                 color='black', emphasis=None, highlight=0):
        if (width == 0 and height == 0 and
                color == 'red' and emphasis == 'strong' or
                highlight > 100):
            raise ValueError("sorry, you lose")
        if width == 0 and height == 0 and (color == 'red' or
                                           emphasis is None):
            raise ValueError("I don't think so -- values are %s, %s" %
                             (width, height))
        Blob.__init__(self, width, height,
                      color, emphasis, highlight)
```
Blank Lines
###空行
Separate top-level function and class definitions with two blank lines.
用两个空行来将最上层的方法与类定义分开。
Method definitions inside a class are separated by a single blank line.
使用一个空行来将类里面的方法定义分开
Extra blank lines may be used (sparingly) to separate groups of related functions. Blank lines may be omitted between a bunch of related one-liners (e.g. a set of dummy implementations).
可以多使用一些空行（尽量少用这种方式）来将一些相关的方法进行分组。在一批相关的单行代码(比如一组dummy实现)之间的空行可以省略。

Use blank lines in functions, sparingly, to indicate logical sections.
在函数中有节制地使用空行来将代码分块，来表明它们是不同的逻辑代码块。

Python accepts the control-L (i.e. ^L) form feed character as whitespace; Many tools treat these characters as page separators, so you may use them to separate pages of related sections of your file. Note, some editors and web-based code viewers may not recognize control-L as a form feed and will show another glyph in its place.
Python把 control-L (也就是^L)换页符是为空白符号；许多工具把它们当作页分隔符来进行处理，所以你可以使用它们来将你的文件分页，将相关联的代码块分到一页里。注意：有一些编辑器和基于web的代码查看器可能不把control-L当作换页，会在相应的地方显示一个图像字符。

Source File Encoding
###源文件编码
Code in the core Python distribution should always use UTF-8 (or ASCII in Python 2).
核心的Python发行版中的代码总是应该使用UTF-8(或者在Python 2中使用ASCII码)。

Files using ASCII (in Python 2) or UTF-8 (in Python 3) should not have an encoding declaration.
使用ASCII(在Python 2）或者UTF-8(在Python 3)的文件不应该需要进行编码声明。

In the standard library, non-default encodings should be used only for test purposes or when a comment or docstring needs to mention an author name that contains non-ASCII characters; otherwise, using \x , \u , \U , or \N escapes is the preferred way to include non-ASCII data in string literals.
在标准库中，非默认的编码应该只能用于测试目的，或者用于在注释或docstring中记录包含非ASCII字符的作者姓名；否则以字符串文字（string literals）的形式包含非ASCII码数据的首选方式是使用\x , \u , \U , or \N 转义符。

For Python 3.0 and beyond, the following policy is prescribed for the standard library (see PEP 3131 ): All identifiers in the Python standard library MUST use ASCII-only identifiers, and SHOULD use English words wherever feasible (in many cases, abbreviations and technical terms are used which aren't English). In addition, string literals and comments must also be in ASCII. The only exceptions are (a) test cases testing the non-ASCII features, and (b) names of authors. Authors whose names are not based on the latin alphabet MUST provide a latin transliteration of their names.
对于Python 3.0以及更新的版本，相对应的策略已经在标准库（见PEP 3131）中进行了规定：所有在Python标准库中的标识符必须使用ASCII标识符，并且应该在可行的情况下使用英文单词（在许多情况下会使用非英文的缩略词和技术术语）。另外，字符串文字和注释必须同样使用ASCII。唯一的例外是(a)测试非ASCII的功能的测试用例 (b)作者的名字。如果作者的名字不是基于拉丁字母的，那么必须提供对应的拉丁翻译。
Open source projects with a global audience are encouraged to adopt a similar policy.
我们鼓励具有国际受众的开源项目采用类似的策略。
Imports
Imports should usually be on separate lines, e.g.:
Import语句通常应该分在不同的行，比如

Yes:
```python
     import os
     import sys
```
No:
```python
 import sys, os
```
It's okay to say this though:
下面这种方式是可以的：
```python
from subprocess import Popen, PIPE
```
Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants.
Import语句每次都是放在文件的开头，它位于模块的注释和docstring以及模块的全局变量和常量之间。
Imports should be grouped in the following order:
Import语句应该按照下面的顺序进行分组：

standard library imports
标准库import语句
related third party imports
相关的第三方库import语句
local application/library specific imports
本地应用/库的指定的import语句
You should put a blank line between each group of imports.
你应该在每组import之间插入一个空行。
Put any relevant __all__ specification after the imports.
在import语句后面可以放入任何相关的__all__声明。
Absolute imports are recommended, as they are usually more readable and tend to be better behaved (or at least give better error messages) if the import system is incorrectly configured (such as when a directory inside a package ends up on sys.path ):
建议使用绝对的import，因为这种方式通常可读性更强，并且在import系统配置错误（比如 当某个包里面的路径没有在sys.path出现）的情况下，表现往往会更加好一些。
```python
import mypkg.sibling
from mypkg import sibling
from mypkg.sibling import example
```
However, explicit relative imports are an acceptable alternative to absolute imports, especially when dealing with complex package layouts where using absolute imports would be unnecessarily verbose:
然而，相对于绝对import，显式的相对import也是一种可以接受的选择，特别是当处理复杂的包结构，而使用绝对import会显得特别繁琐和啰嗦的时候。
```python
from . import sibling
from .sibling import example
```
Standard library code should avoid complex package layouts and always use absolute imports.
标准库代码应该避免复杂的包结构，并且始终使用绝对import。

Implicit relative imports should never be used and have been removed in Python 3.
不能使用隐式的相对import，并且这种隐式的相对import已经在Python 3中移掉了。

When importing a class from a class-containing module, it's usually okay to spell this:
当从某个包含类的模块中导入类时，下面这种拼写方式是可以的：
```python
from myclass import MyClass
from foo.bar.yourclass import YourClass
```
If this spelling causes local name clashes, then spell them
如果这种方式导致本地命名冲突，就要用下面这种方式：
```python
import myclass
import foo.bar.yourclass
```
and use "myclass.MyClass" and "foo.bar.yourclass.YourClass".
然后使用`"myclass.MyClass"` 和 `"foo.bar.yourclass.YourClass"`

Wildcard imports ( from <module> import * ) should be avoided, as they make it unclear which names are present in the namespace, confusing both readers and many automated tools. There is one defensible use case for a wildcard import, which is to republish an internal interface as part of a public API (for example, overwriting a pure Python implementation of an interface with the definitions from an optional accelerator module and exactly which definitions will be overwritten isn't known in advance).
应该避免使用通配符形式的import (`from <module> import *`)，因为  而让读者和许多自动化工具搞不清楚哪些名称在当前命名空间出现。有一种使用通配符形式的import的用例是情有可原的，那就是将某个内部接口重新发布为公开的API的一部分（比如，按照某个accelerator模块的定义将某个接口的纯Python实现进行重写，而并不能提前知道哪些接口将被重写）

When republishing names this way, the guidelines below regarding public and internal interfaces still apply.
当采用这种方式
String Quotes
字符串引号

In Python, single-quoted strings and double-quoted strings are the same. This PEP does not make a recommendation for this. Pick a rule and stick to it. When a string contains single or double quote characters, however, use the other one to avoid backslashes in the string. It improves readability.
在Python中，单引号的字符串和双引号的字符串是相同的。本PEP规范并不对此进行要求。只要选择一种方式并一直用下去就可以了。当字符串包含单引号或者双引号字符串时，选择使用另一种方式可以避免在字符串中出现右下划线。这会增加可读性。
For triple-quoted strings, always use double quote characters to be consistent with the docstring convention in PEP 257 .
对于三个引号的字符串，
Whitespace in Expressions and Statements
表达式和代码语句中的空白
Pet Peeves
Avoid extraneous whitespace in the following situations:

Immediately inside parentheses, brackets or braces.

Yes:
```python
spam(ham[1], {eggs: 2})
```
No:
```python
spam( ham[ 1 ], { eggs: 2 } )
```
Immediately before a comma, semicolon, or colon:

Yes: if x == 4: print x, y; x, y = y, x
No:  if x == 4 : print x , y ; x , y = y , x
However, in a slice the colon acts like a binary operator, and should have equal amounts on either side (treating it as the operator with the lowest priority). In an extended slice, both colons must have the same amount of spacing applied. Exception: when a slice parameter is omitted, the space is omitted.

Yes:
```python
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
```
No:
```python
ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : upper]
ham[ : upper]
```
Immediately before the open parenthesis that starts the argument list of a function call:

Yes: spam(1)
No:  spam (1)
Immediately before the open parenthesis that starts an indexing or slicing:

Yes: dct['key'] = lst[index]
No:  dct ['key'] = lst [index]
More than one space around an assignment (or other) operator to align it with another.

Yes:
```python
x = 1
y = 2
long_variable = 3
```
No:
```python
x             = 1
y             = 2
long_variable = 3
```
Other Recommendations
Always surround these binary operators with a single space on either side: assignment ( = ), augmented assignment ( += , -= etc.), comparisons ( == , < , > , != , <> , <= , >= , in , not in , is , is not ), Booleans ( and , or , not ).

If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority(ies). Use your own judgment; however, never use more than one space, and always have the same amount of whitespace on both sides of a binary operator.

Yes:
```python
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```
No:
```python
i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```
Don't use spaces around the = sign when used to indicate a keyword argument or a default parameter value.

Yes:
```python
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```
No:
```python
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```
Do use spaces around the = sign of an annotated function definition. Additionally, use a single space after the : , as well as a single space on either side of the -> sign representing an annotated return value.

Yes:
```python
def munge(input: AnyStr):
def munge(sep: AnyStr = None):
def munge() -> AnyStr:
def munge(input: AnyStr, sep: AnyStr = None, limit=1000):
```
No:
```
def munge(input: AnyStr=None):
def munge(input:AnyStr):
def munge(input: AnyStr)->PosInt:
```
Compound statements (multiple statements on the same line) are generally discouraged.

Yes:
```
if foo == 'blah':
    do_blah_thing()
do_one()
do_two()
do_three()
```
Rather not:
```
if foo == 'blah': do_blah_thing()
do_one(); do_two(); do_three()
```
While sometimes it's okay to put an if/for/while with a small body on the same line, never do this for multi-clause statements. Also avoid folding such long lines!

Rather not:
```
if foo == 'blah': do_blah_thing()
for x in lst: total += x
while t < 10: t = delay()
```
Definitely not:
```
if foo == 'blah': do_blah_thing()
else: do_non_blah_thing()

try: something()
finally: cleanup()

do_one(); do_two(); do_three(long, argument,
                             list, like, this)

if foo == 'blah': one(); two(); three()
```
Comments
Comments that contradict the code are worse than no comments. Always make a priority of keeping the comments up-to-date when the code changes!

Comments should be complete sentences. If a comment is a phrase or sentence, its first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!).

If a comment is short, the period at the end can be omitted. Block comments generally consist of one or more paragraphs built out of complete sentences, and each sentence should end in a period.

You should use two spaces after a sentence-ending period.

When writing English, follow Strunk and White.

Python coders from non-English speaking countries: please write your comments in English, unless you are 120% sure that the code will never be read by people who don't speak your language.

Block Comments
Block comments generally apply to some (or all) code that follows them, and are indented to the same level as that code. Each line of a block comment starts with a # and a single space (unless it is indented text inside the comment).

Paragraphs inside a block comment are separated by a line containing a single # .

Inline Comments
Use inline comments sparingly.

An inline comment is a comment on the same line as a statement. Inline comments should be separated by at least two spaces from the statement. They should start with a # and a single space.

Inline comments are unnecessary and in fact distracting if they state the obvious. Don't do this:
```
x = x + 1                 # Increment x
```
But sometimes, this is useful:
```
x = x + 1                 # Compensate for border
```
Documentation Strings
Conventions for writing good documentation strings (a.k.a. "docstrings") are immortalized in PEP 257 .

Write docstrings for all public modules, functions, classes, and methods. Docstrings are not necessary for non-public methods, but you should have a comment that describes what the method does. This comment should appear after the def line.

PEP 257 describes good docstring conventions. Note that most importantly, the """ that ends a multiline docstring should be on a line by itself, e.g.:
```
"""Return a foobang

Optional plotz says to frobnicate the bizbaz first.
"""
```
For one liner docstrings, please keep the closing """ on the same line.

Version Bookkeeping
If you have to have Subversion, CVS, or RCS crud in your source file, do it as follows.
```
__version__ = "$Revision$"
# $Source$
```
These lines should be included after the module's docstring, before any other code, separated by a blank line above and below.

Naming Conventions
The naming conventions of Python's library are a bit of a mess, so we'll never get this completely consistent -- nevertheless, here are the currently recommended naming standards. New modules and packages (including third party frameworks) should be written to these standards, but where an existing library has a different style, internal consistency is preferred.

Overriding Principle
Names that are visible to the user as public parts of the API should follow conventions that reflect usage rather than implementation.

Descriptive: Naming Styles
There are a lot of different naming styles. It helps to be able to recognize what naming style is being used, independently from what they are used for.

The following naming styles are commonly distinguished:

b (single lowercase letter)

B (single uppercase letter)

lowercase

lower_case_with_underscores

UPPERCASE

UPPER_CASE_WITH_UNDERSCORES

CapitalizedWords (or CapWords, or CamelCase -- so named because of the bumpy look of its letters [3] ). This is also sometimes known as StudlyCaps.

Note: When using abbreviations in CapWords, capitalize all the letters of the abbreviation. Thus HTTPServerError is better than HttpServerError.

mixedCase (differs from CapitalizedWords by initial lowercase character!)

Capitalized_Words_With_Underscores (ugly!)

There's also the style of using a short unique prefix to group related names together. This is not used much in Python, but it is mentioned for completeness. For example, the os.stat() function returns a tuple whose items traditionally have names like st_mode , st_size , st_mtime and so on. (This is done to emphasize the correspondence with the fields of the POSIX system call struct, which helps programmers familiar with that.)

The X11 library uses a leading X for all its public functions. In Python, this style is generally deemed unnecessary because attribute and method names are prefixed with an object, and function names are prefixed with a module name.

In addition, the following special forms using leading or trailing underscores are recognized (these can generally be combined with any case convention):

_single_leading_underscore : weak "internal use" indicator. E.g. from M import * does not import objects whose name starts with an underscore.

single_trailing_underscore_ : used by convention to avoid conflicts with Python keyword, e.g.

Tkinter.Toplevel(master, class_='ClassName')
__double_leading_underscore : when naming a class attribute, invokes name mangling (inside class FooBar, __boo becomes _FooBar__boo ; see below).

__double_leading_and_trailing_underscore__ : "magic" objects or attributes that live in user-controlled namespaces. E.g. __init__ , __import__ or __file__ . Never invent such names; only use them as documented.

Prescriptive: Naming Conventions
Names to Avoid
Never use the characters 'l' (lowercase letter el), 'O' (uppercase letter oh), or 'I' (uppercase letter eye) as single character variable names.

In some fonts, these characters are indistinguishable from the numerals one and zero. When tempted to use 'l', use 'L' instead.

Package and Module Names
Modules should have short, all-lowercase names. Underscores can be used in the module name if it improves readability. Python packages should also have short, all-lowercase names, although the use of underscores is discouraged.

Since module names are mapped to file names, and some file systems are case insensitive and truncate long names, it is important that module names be chosen to be fairly short -- this won't be a problem on Unix, but it may be a problem when the code is transported to older Mac or Windows versions, or DOS.

When an extension module written in C or C++ has an accompanying Python module that provides a higher level (e.g. more object oriented) interface, the C/C++ module has a leading underscore (e.g. _socket ).

Class Names
Class names should normally use the CapWords convention.

The naming convention for functions may be used instead in cases where the interface is documented and used primarily as a callable.

Note that there is a separate convention for builtin names: most builtin names are single words (or two words run together), with the CapWords convention used only for exception names and builtin constants.

Exception Names
Because exceptions should be classes, the class naming convention applies here. However, you should use the suffix "Error" on your exception names (if the exception actually is an error).

Global Variable Names
(Let's hope that these variables are meant for use inside one module only.) The conventions are about the same as those for functions.

Modules that are designed for use via from M import * should use the __all__ mechanism to prevent exporting globals, or use the older convention of prefixing such globals with an underscore (which you might want to do to indicate these globals are "module non-public").

Function Names
Function names should be lowercase, with words separated by underscores as necessary to improve readability.

mixedCase is allowed only in contexts where that's already the prevailing style (e.g. threading.py), to retain backwards compatibility.

Function and method arguments
Always use self for the first argument to instance methods.

Always use cls for the first argument to class methods.

If a function argument's name clashes with a reserved keyword, it is generally better to append a single trailing underscore rather than use an abbreviation or spelling corruption. Thus class_ is better than clss . (Perhaps better is to avoid such clashes by using a synonym.)

Method Names and Instance Variables
Use the function naming rules: lowercase with words separated by underscores as necessary to improve readability.

Use one leading underscore only for non-public methods and instance variables.

To avoid name clashes with subclasses, use two leading underscores to invoke Python's name mangling rules.

Python mangles these names with the class name: if class Foo has an attribute named __a , it cannot be accessed by Foo.__a . (An insistent user could still gain access by calling Foo._Foo__a .) Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed.

Note: there is some controversy about the use of __names (see below).

Constants
Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include MAX_OVERFLOW and TOTAL .

Designing for inheritance
Always decide whether a class's methods and instance variables (collectively: "attributes") should be public or non-public. If in doubt, choose non-public; it's easier to make it public later than to make a public attribute non-public.

Public attributes are those that you expect unrelated clients of your class to use, with your commitment to avoid backward incompatible changes. Non-public attributes are those that are not intended to be used by third parties; you make no guarantees that non-public attributes won't change or even be removed.

We don't use the term "private" here, since no attribute is really private in Python (without a generally unnecessary amount of work).

Another category of attributes are those that are part of the "subclass API" (often called "protected" in other languages). Some classes are designed to be inherited from, either to extend or modify aspects of the class's behavior. When designing such a class, take care to make explicit decisions about which attributes are public, which are part of the subclass API, and which are truly only to be used by your base class.

With this in mind, here are the Pythonic guidelines:

Public attributes should have no leading underscores.
公共属性不应该前置下划线
If your public attribute name collides with a reserved keyword, append a single trailing underscore to your attribute name. This is preferable to an abbreviation or corrupted spelling. (However, notwithstanding this rule, 'cls' is the preferred spelling for any variable or argument which is known to be a class, especially the first argument to a class method.)
如果你的公共属性的名字和某个保留关键字冲突的话，在你的属性名后面添加一个下划线后缀。这种方式要好于使用缩写或者更改拼写。（但是，尽管有这么一条规则，但是对于那些已经知道是一个class的变量或者参数，‘cls’任然是首选拼写，尤其是类方法中的第一个参数）。

Note 1: See the argument name recommendation above for class methods.
注意 1： 对于class方法可参阅上面的参数命名建议。
For simple public data attributes, it is best to expose just the attribute name, without complicated accessor/mutator methods. Keep in mind that Python provides an easy path to future enhancement, should you find that a simple data attribute needs to grow functional behavior. In that case, use properties to hide functional implementation behind simple data attribute access syntax.

 - 对于简单的共有数据属性，最好的方式是直接暴露属性名称，而不要使用复杂的访问和赋值方法。要记住的是，为了便于未来的扩展，Python提供了一种简单的方式，你会发现，简单的数据属性需要扩充函数行为。在这种情况下，使用properties来将函数实现隐藏在简单的数据属性访问语法的背后。
```
class Movie(object):
    def __init__(self, title, rating, runtime, budget, gross):
        self._budget = None

        self.title = title
        self.rating = rating
        self.runtime = runtime
        self.gross = gross
        self.budget = budget

    @property
    def budget(self):
        return self._budget

    @budget.setter
    def budget(self, value):
        if value < 0:
            raise ValueError("Negative value not allowed: %s" % value)
        self._budget = value

    def profit(self):
        return self.gross - self.budget


m = Movie('Casablanca', 97, 102, 964000, 1300000)
print m.budget       # calls m.budget(), returns result
try:
    m.budget = -100  # calls budget.setter(-100), and raises ValueError
except ValueError:
    print "Woops. Not allowed"
```
Note 1: Properties only work on new-style classes.
注意 1： Properties 只能在新型类中使用。
Note 2: Try to keep the functional behavior side-effect free, although side-effects such as caching are generally fine.
注意 2： 尽量保持函数行为没有副作用，尽管想缓存caching这样的副作用一般是没有问题的。

Note 3: Avoid using properties for computationally expensive operations; the attribute notation makes the caller believe that access is (relatively) cheap.
注意 3： 避免对那些很耗费计算的操作使用properties；这种属性表示法会让掉用房认为对其进行访问的代价是（相对）比较便宜的。
If your class is intended to be subclassed, and you have attributes that you do not want subclasses to use, consider naming them with double leading underscores and no trailing underscores. This invokes Python's name mangling algorithm, where the name of the class is mangled into the attribute name. This helps avoid attribute name collisions should subclasses inadvertently contain attributes with the same name.
如果你打算继承某个类，并且你不希望子类使用某些属性，可以考虑用双前置下划线来对这些属性命名，不要带后置下划线。它会调用Python的name managling算法，类的名字会被修改为属性名。这有助于避免子类无意中包含的属性的名字和父类的属性名相同而相冲突。
Note 1: Note that only the simple class name is used in the mangled name, so if a subclass chooses both the same class name and attribute name, you can still get name collisions.
注意 1：

Note 2: Name mangling can make certain uses, such as debugging and __getattr__() , less convenient. However the name mangling algorithm is well documented and easy to perform manually.

Note 3: Not everyone likes name mangling. Try to balance the need to avoid accidental name clashes with potential use by advanced callers.

Public and internal interfaces
##共开的接口和内部接口
Any backwards compatibility guarantees apply only to public interfaces. Accordingly, it is important that users be able to clearly distinguish between public and internal interfaces.
所有向后兼容性的保证只适用于公开的接口。因此，让用户能够清楚地将公开接口和内部接口区分出来是非常重要的。
Documented interfaces are considered public, unless the documentation explicitly declares them to be provisional or internal interfaces exempt from the usual backwards compatibility guarantees. All undocumented interfaces should be assumed to be internal.
文档所记录下来的接口被认为是公开的，除非文档显式地将它们声明为临时或者内部接口来免除通常的向后兼容性的保证。所有没有记录下来的接口都应该被假定为是内部的接口。
To better support introspection, modules should explicitly declare the names in their public API using the __all__ attribute. Setting __all__ to an empty list indicates that the module has no public API.
为了更好地支持自省（introspection），模块应该显式地使用__all_属性在它们的公开的API中来声明它们的名字。将没有公开API的模块的__all__设置为空的list。
Even with __all__ set appropriately, internal interfaces (packages, modules, classes, functions, attributes or other names) should still be prefixed with a single leading underscore.


An interface is also considered internal if any containing namespace (package, module or class) is considered internal.

Imported names should always be considered an implementation detail. Other modules must not rely on indirect access to such imported names unless they are an explicitly documented part of the containing module's API, such as os.path or a package's __init__ module that exposes functionality from submodules.

Programming Recommendations
##编程建议
Code should be written in a way that does not disadvantage other implementations of Python (PyPy, Jython, IronPython, Cython, Psyco, and such).

For example, do not rely on CPython's efficient implementation of in-place string concatenation for statements in the form a += b or a = a + b . This optimization is fragile even in CPython (it only works for some types) and isn't present at all in implementations that don't use refcounting. In performance sensitive parts of the library, the ''.join() form should be used instead. This will ensure that concatenation occurs in linear time across various implementations.

Comparisons to singletons like None should always be done with is or is not , never the equality operators.

Also, beware of writing if x when you really mean if x is not None -- e.g. when testing whether a variable or argument that defaults to None was set to some other value. The other value might have a type (such as a container) that could be false in a boolean context!

Use is not operator rather than not ... is . While both expressions are functionally identical, the former is more readable and preferred.

Yes:
```
if foo is not None:
```
No:
```
if not foo is None:
```
When implementing ordering operations with rich comparisons, it is best to implement all six operations ( __eq__ , __ne__ , __lt__ , __le__ , __gt__ , __ge__ ) rather than relying on other code to only exercise a particular comparison.

To minimize the effort involved, the functools.total_ordering() decorator provides a tool to generate missing comparison methods.

PEP 207 indicates that reflexivity rules are assumed by Python. Thus, the interpreter may swap y > x with x < y , y >= x with x <= y , and may swap the arguments of x == y and x != y . The sort() and min() operations are guaranteed to use the < operator and the max() function uses the > operator. However, it is best to implement all six operations so that confusion doesn't arise in other contexts.

Always use a def statement instead of an assignment statement that binds a lambda expression directly to an identifier.

Yes:
```
def f(x): return 2*x
```
No:
```
f = lambda x: 2*x
```
The first form means that the name of the resulting function object is specifically 'f' instead of the generic '<lambda>'. This is more useful for tracebacks and string representations in general. The use of the assignment statement eliminates the sole benefit a lambda expression can offer over an explicit def statement (i.e. that it can be embedded inside a larger expression)

Derive exceptions from Exception rather than BaseException . Direct inheritance from BaseException is reserved for exceptions where catching them is almost always the wrong thing to do.

Design exception hierarchies based on the distinctions that code catching the exceptions is likely to need, rather than the locations where the exceptions are raised. Aim to answer the question "What went wrong?" programmatically, rather than only stating that "A problem occurred" (see PEP 3151 for an example of this lesson being learned for the builtin exception hierarchy)

Class naming conventions apply here, although you should add the suffix "Error" to your exception classes if the exception is an error. Non-error exceptions that are used for non-local flow control or other forms of signaling need no special suffix.

Use exception chaining appropriately. In Python 3, "raise X from Y" should be used to indicate explicit replacement without losing the original traceback.

When deliberately replacing an inner exception (using "raise X" in Python 2 or "raise X from None" in Python 3.3+), ensure that relevant details are transferred to the new exception (such as preserving the attribute name when converting KeyError to AttributeError, or embedding the text of the original exception in the new exception message).

When raising an exception in Python 2, use raise ValueError('message') instead of the older form raise ValueError, 'message' .

The latter form is not legal Python 3 syntax.

The paren-using form also means that when the exception arguments are long or include string formatting, you don't need to use line continuation characters thanks to the containing parentheses.

When catching exceptions, mention specific exceptions whenever possible instead of using a bare except: clause.

For example, use:
```
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```
A bare except: clause will catch SystemExit and KeyboardInterrupt exceptions, making it harder to interrupt a program with Control-C, and can disguise other problems. If you want to catch all exceptions that signal program errors, use except Exception: (bare except is equivalent to except BaseException: ).

A good rule of thumb is to limit use of bare 'except' clauses to two cases:

If the exception handler will be printing out or logging the traceback; at least the user will be aware that an error has occurred.
If the code needs to do some cleanup work, but then lets the exception propagate upwards with raise . try...finally can be a better way to handle this case.
When binding caught exceptions to a name, prefer the explicit name binding syntax added in Python 2.6:
```
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))
```
This is the only syntax supported in Python 3, and avoids the ambiguity problems associated with the older comma-based syntax.

When catching operating system errors, prefer the explicit exception hierarchy introduced in Python 3.3 over introspection of errno values.

Additionally, for all try/except clauses, limit the try clause to the absolute minimum amount of code necessary. Again, this avoids masking bugs.

Yes:
```
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)
```
No:
```
try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```
When a resource is local to a particular section of code, use a with statement to ensure it is cleaned up promptly and reliably after use. A try/finally statement is also acceptable.

Context managers should be invoked through separate functions or methods whenever they do something other than acquire and release resources. For example:

Yes:
```
with conn.begin_transaction():
    do_stuff_in_transaction(conn)
```
No:
```
with conn:
    do_stuff_in_transaction(conn)
```
The latter example doesn't provide any information to indicate that the __enter__ and __exit__ methods are doing something other than closing the connection after a transaction. Being explicit is important in this case.

Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as return None , and an explicit return statement should be present at the end of the function (if reachable).

Yes:
```
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None

def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)
```
No:
```
def foo(x):
    if x >= 0:
        return math.sqrt(x)

def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```
Use string methods instead of the string module.

String methods are always much faster and share the same API with unicode strings. Override this rule if backward compatibility with Pythons older than 2.0 is required.

Use ''.startswith() and ''.endswith() instead of string slicing to check for prefixes or suffixes.

startswith() and endswith() are cleaner and less error prone. For example:

Yes: if foo.startswith('bar'):
No:  if foo[:3] == 'bar':
Object type comparisons should always use isinstance() instead of comparing types directly.

Yes: if isinstance(obj, int):

No:  if type(obj) is type(1):
When checking if an object is a string, keep in mind that it might be a unicode string too! In Python 2, str and unicode have a common base class, basestring, so you can do:

if isinstance(obj, basestring):
Note that in Python 3, unicode and basestring no longer exist (there is only str ) and a bytes object is no longer a kind of string (it is a sequence of integers instead)

For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

Yes: if not seq:
     if seq:

No: if len(seq)
    if not len(seq)
Don't write string literals that rely on significant trailing whitespace. Such trailing whitespace is visually indistinguishable and some editors (or more recently, reindent.py) will trim them.

Don't compare boolean values to True or False using == .

Yes:   if greeting:
No:    if greeting == True:
Worse: if greeting is True:
The Python standard library will not use function annotations as that would result in a premature commitment to a particular annotation style. Instead, the annotations are left for users to discover and experiment with useful annotation styles.

It is recommended that third party experiments with annotations use an associated decorator to indicate how the annotation should be interpreted.

Early core developer attempts to use function annotations revealed inconsistent, ad-hoc annotation styles. For example:

[str] was ambiguous as to whether it represented a list of strings or a value that could be either str or None .
The notation open(file:(str,bytes)) was used for a value that could be either bytes or str rather than a 2-tuple containing a str value followed by a bytes value.
The annotation seek(whence:int) exhibited a mix of over-specification and under-specification: int is too restrictive (anything with __index__ would be allowed) and it is not restrictive enough (only the values 0, 1, and 2 are allowed). Likewise, the annotation write(b: bytes) was also too restrictive (anything supporting the buffer protocol would be allowed).
Annotations such as read1(n: int=None) were self-contradictory since None is not an int . Annotations such as source_path(self, fullname:str) -> object were confusing about what the return type should be.
In addition to the above, annotations were inconsistent in the use of concrete types versus abstract types: int versus Integral and set/frozenset versus MutableSet/Set.
Some annotations in the abstract base classes were incorrect specifications. For example, set-to-set operations require other to be another instance of Set rather than just an Iterable .
A further issue was that annotations become part of the specification but weren't being tested.
In most cases, the docstrings already included the type specifications and did so with greater clarity than the function annotations. In the remaining cases, the docstrings were improved once the annotations were removed.
The observed function annotations were too ad-hoc and inconsistent to work with a coherent system of automatic type checking or argument validation. Leaving these annotations in the code would have made it more difficult to make changes later so that automated utilities could be supported.
Footnotes

[5]	 Hanging indentation is a type-setting style where all the lines in a paragraph are indented except the first line. In the context of Python, the term is used to describe a style where the opening parenthesis of a parenthesized statement is the last non-whitespace character of the line, with subsequent lines being indented until the closing parenthesis.
References
[1]	 PEP 7 , Style Guide for C Code, van Rossum
[2]	 Barry's GNU Mailman style guide http://barry.warsaw.us/software/STYLEGUIDE.txt
[3]	 http://www.wikipedia.com/wiki/CamelCase
[4]	 PEP 8 modernisation, July 2013 http://bugs.python.org/issue18472
Copyright
This document has been placed in the public domain.

Source: https://hg.python.org/peps/file/tip/pep-0008.txt



致谢：
本文参考了http://wiki.hiaero.net/doku.php?id=python:pep8一文特此表示感谢。




