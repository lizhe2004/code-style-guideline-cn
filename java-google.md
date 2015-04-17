#Google Java����淶���İ�

[TOC]

##1 ����

���ĵ������ض�����Google��˾����java���Ա�д��Դ��ı���淶�����ҽ���javaԴ�ļ���ѭ���淶ʱ�����ǲ�˵���Ƿ���Google���ġ�

ͬ����������ָ��һ�������������۵����ݲ��������������ʽ�������������⣬���������������͵Ĺ���Լ���ͱ���淶��Ȼ����������Ҫ���н����������ձ���ѭ�Ĳ��ɴ�����Ӳ�Թ涨�����ұ������һЩû����ȷǿ���ԵĽ���(�������˻��ǹ���)��

###1.1 ����˵��

�ڱ��ĵ��У���������������

����ࡱ���ڱ�ʾ�����ݰ�����һ������ͨ���ࡢenumö���ࡢ�ӿڻ���ע�����ͣ�`@interface`����
Other "terminology notes" will appear occasionally throughout the document.
����commentָ����ʵ��ע�͡����ǲ���ʹ��"�ĵ�ע�ͣ�documentation comments��"һ�ʣ���ʮʹ��һ�����õ����Javadoc�������档
 
###1.2 ָ��˵��

���ĵ��е�ʵ�����벢���Ǳ�׼�ġ������˵��������Щ�����Ƿ���Google���ģ��������ǲ�����˵������չʾ�����Ψһ��ʽ����������ѡ�����Щ��ʽ����ʽ��������Ϊ�������ǿ��ִ�С�

##2 Դ�ļ�����Ҫ��

###2.1 �ļ���

Դ�ļ��������������Ķ�����������Լ�`.java`��չ����ɣ���������ǶԴ�Сд���еġ�

###2.2 �ļ����룺UTF-8

Դ�ļ��ǲ���UTF-8���б���ġ�

###2.3 �����ַ�
 
####2.3.1�հ��ַ�
�����н������������⣬ASCIIˮƽ����ַ���0X20������ע�����ո��ַ�����Ψһ����Դ�ļ��е������ֵĿհ��ַ�������ζ�ţ�
�ַ����е����������հ��ַ�����Ҫת�塣
 
Tab�ַ�(Ҳ���Ʊ��)��������������
 
####2.3.2����ת������

���ھ�������ת�����е��ַ�(`\b`��`\t`��`\n`��`\f`��`\r`��`\"`��`\'`��`\\`)������ʹ��ת�����У����Ƕ�Ӧ��ʮ��������ֵ������`\012`������Unicode������`\u000a`��ת�����
 
####2.3.3��ASCII�ַ�
���������ķ�ASCII�ַ���������ʹ��������Unicode�ַ�������`��`������ʹ�õȼ۵�Unicodeת���������`\u221e`)���ⶼ�ǿ��Եģ������ȡ�������ַ�ʽ�������ڶԴ�����Ķ�����⡣

    С��ʾ����ʹ��Unicodeת���������£���ʱ��������ʹ��������Unicode�ַ�������£�˵���Ե�ע���Ƿǳ��а����ġ�
 
���ӣ�

 
��������
 
 
<table>
    <tr>
        <td>
        ����
        </td>
         <td>����</td>
    </tr>
    <tr>
        <td>
        String unitAbbrev = "��s";
        </td>
         <td>�ţ�����û��ע��Ҳ�Ƿǳ������ġ�</td>
    </tr>
        <tr>
        <td>String unitAbbrev = "\u03bcs"; // "��s"</td>
         <td>�ɣ�����û��������ô����</td>
    </tr>
    <tr>
        <td>String unitAbbrev = "\u03bcs"; // ϣ����ĸmu��"s"</td>
         <td>��, ��׸�������׳��ִ���</td>
    </tr>       
    <tr>
        <td>String unitAbbrev = "\u03bcs";</td>
         <td>����߲��������ʲô������</td>
    </tr>
    <tr>
        <td>return '\ufeff' + content; // BOM��byte order mark���ַ�</td>
         <td>��: �Դ�ӡ���������ַ�ʹ��ת���, ���ڱ�Ҫ����������ע�͡�</td>
    </tr>
</table>
 
    С��ʾ����Զ��Ҫ��Ϊ�־���һЩ��������ȷ�ش����ASCII�ַ���������Ĵ���ɶ��Ա������ĳ����޷������ASCII�ַ����������Щ����ͻ��޷��������У����Ǳ����޸���Щ����

 
##3 Դ�ļ��ṹ

Դ�ļ�����(��˳��):

 1. ��Ȩ��Ϣ��������ڵĻ���  
 2. ������ 
 3. importָ�� 
 4. ֻ��һ��������

�ļ��еĸ�����֮����һ�����н��зָ���

 
###3.1 ���֤���Ȩ��Ϣ��������ڵĻ���

 
������֤���Ȩ��Ϣ����ĳ���ļ��Ļ�������Ӧ�÷������
 
###3.2 ������

The package statement is not line-wrapped. The column limit (Section 4.4, Column limit: 80 or 100) does not apply to package statements.
��������䲻�ܻ��С������ƣ�4.4С�ڣ������ƣ�80��100�����������ڰ�������

3.3 Import statements 
###3.3 Importָ�����
3.3.1 No wildcard imports 
####3.3.1 Importָ�����
Wildcard imports, static or otherwise, are not used.
��Ҫʹ��ͨ���ʽ��import��static����������import��
3.3.2 No line-wrapping 

####3.3.2 ��Ҫ���� 
Import statements are not line-wrapped. The column limit (Section 4.4, Column limit: 80 or 100) does not apply to import statements.
Importָ��ܻ��С������ƣ�4.4С�ڣ������ƣ�80��100������������importָ�

3.3.3 Ordering and spacing 
####3.3.3 ˳��ͼ��
Import statements are divided into the following groups, in this order, with each group separated by a single blank line:
Importָ�����ᱻ���������˳��ֳɼ��飬ÿ��֮��ʹ��һ�����н��зָ

 1. �����еľ�̬imports�ŵ�һ���� 
 2. `com.google` imports (ֻ�е�Դ�ļ���`com.google`���ռ�ʱ) 
 3. �������İ���imports������ASCII������˳��ÿ����������Ϊһ�飬���磺`android`, `com`, `junit`, `org`, `sun`
 4. `java` imports
 5. `javax` imports

Within a group there are no blank lines, and the imported names appear in ASCII sort order. (Note: this is not the same as the import statements being in ASCII sort order; the presence of semicolons warps the result.)
ͬ��������֮��û�п��У�����������ݵ����ư���ASCII��˳���������ע�⣺�Ⲣ��ͬ�ڽ�import��䰴��ASCII���˳��������򣬷ֺŵĴ��ڻ���Ž������
3.4 Class declaration 
###3.4 ������

3.4.1 Exactly one top-level class declaration 
####3.4.1 ֻ��һ������������
Each top-level class resides in a source file of its own.
ÿ�������඼������ͬ����Դ�ļ��С�
3.4.2 Class member ordering 

####3.4.2 ���Ա˳��

The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it. Different classes may order their members differently.
һ����ĳ�Ա��˳�����ѧ���о޴��Ӱ�죬���ǲ�������һ����ȷ�ķ�ʽ����ȷ��ν������򡣲�ͬ������ܻ��Բ�ͬ�ķ�ʽ�����ǵĳ�Ա��������

What is important is that each class order its members in some logical order, which its maintainer could explain if asked. For example, new methods are not just habitually added to the end of the class, as that would yield "chronological by date added" ordering, which is not a logical ordering.
��Ҫ����ÿ���඼Ҫ����ĳ���߼�˳���������ĳ�Ա��������һ���ڱ������ʵ���ʱ��ά�����ܹ��������������߼�˳�򡣱��磬�µķ������ܽ���ϰ���Ե���ӵ���Ľ�β�����Ϊ���ʹ�õ���һ�֡�������ӵ�����ǰ������С���˳���Ⲣ����һ���߼�˳��
3.4.2.1 Overloads: never split 
######3.4.2.1 ���أ���Զ��Ҫ�ָ

When a class has multiple constructors, or multiple methods with the same name, these appear sequentially, with no intervening members.
��һ����ӵ�ж�����캯�����߶��ͬ���ķ���ʱ��������Ҫ����������һ���м䲻����������Ա��

4 Formatting 
##4 ��ʽ

Terminology Note: block-like construct refers to the body of a class, method or constructor. Note that, by Section 4.8.3.1 on array initializers, any array initializer may optionally be treated as if it were a block-like construct.
����˵������״�ṹָ�����ࡢ�������߹��캯�������岿�֡���Ҫע����ǣ�����4.8.3.1С���е������ʼ�������е������ʼ��������ѡ���Ե���Ϊ��״�ṹ�����д���
4.1 Braces 
###4.1 ������
4.1.1 Braces are used where optional 
####4.1.1 �ڿ�ѡ������£�ʹ�ô�����
Braces are used with if, else, for, do and while statements, even when the body is empty or contains only a single statement.
��if��else��for��do��while�����ʹ�ô����ţ���ʹִ����Ϊ�ջ���ֻ����һ����䡣

4.1.2 Nonempty blocks: K & R style 
####4.1.2 �ǿմ���飺 K & R ���
Braces follow the Kernighan and Ritchie style ("Egyptian brackets") for nonempty blocks and block-like constructs:
���ڷǿմ�����Լ���״�ṹ��������Ҫ��ѭKernighan��Ritchie��񣨰�������"Egyptian brackets"����
No line break before the opening brace.
��������ǰ���ܻ��С�
Line break after the opening brace.
�����ź��С�
Line break before the closing brace.
��������ǰ����

Line break after the closing brace if that brace terminates a statement or the body of a method, constructor or named class. For example, there is no line break after the brace if it is followed by else or a comma.
ֻ�е���������ĳ�����������캯��������������������岿�ֻ���һ�����Ľ�������ʱ�򣬲�Ҫ�������ź��С����磬�����ź������else���߶��ŵ�ʱ�������ź���Ͳ������ˡ�
Example:
����
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
����ö�����һЩ���������4.8.1С��ö�����л����������
4.1.3 Empty blocks: may be concise 
####4.1.3 �մ���飺
An empty block or block-like construct may be closed immediately after it is opened, with no characters or line break in between ({}), unless it is part of a multi-block statement (one that directly contains multiple blocks: if/else-if/else or try/catch/finally).
һ���յĴ������߿�״�ṹ�����ڣ�{}��֮�䲻�����κ��ַ����߻��У���������ĳ�����־��ж������������һ���֣�һ��ֱ�Ӱ����������������У�if/else-if/else or try/catch/finally��
Example:
���ӣ�
  void doNothing() {}
4.2 Block indentation: +2 spaces 
4.2 ��������+2���ո�

Each time a new block or block-like construct is opened, the indent increases by two spaces. When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block. (See the example in Section 4.1.2, Nonempty blocks: K & R Style.)
ÿ�ο�ʼһ���µĴ������߿�״�ṹʱ������Ҫ���������ո񡣵���������ʱ������Ҫ�ָ���֮ǰ�������㼶�����������Ĳ㼶ͬ�������ڴ�����еĴ����ע�͡�

4.3 One statement per line 
###4.3 ÿ��һ�����

Each statement is followed by a line-break.
ÿ�����ĺ������һ�����з���
4.4 Column limit: 80 or 100 
###4.4 ÿ�е��ַ��������Ϊ80��100

Projects are free to choose a column limit of either 80 or 100 characters. Except as noted below, any line that would exceed this limit must be line-wrapped, as explained in Section 4.5, Line-wrapping.
������Ŀ��������ѡ���ǽ�80����100��Ϊÿ�������ַ����ȡ��������������г������Σ�����Ļ�����Щ��������ַ����ȵĴ����б��밴�յ�4.5С�ڣ����У���˵�����������л��С�

Exceptions:
���⣺

Lines where obeying the column limit is not possible (for example, a long URL in Javadoc, or a long JSNI method reference).
��������ѭ����ַ��������Ƶ��У����磬javadoc�кܳ���URL������һ���ܳ���JSNI�������ã�
package and import statements (see Sections 3.2 Package statement and 3.3 Import statements).
package��import��䣨��3.2С���е�Package����3.3С�ڵ�Import���
Command lines in a comment that may be cut-and-pasted into a shell.
ע���п��ܻᱻ����-ճ����shell�е������С�
4.5 Line-wrapping 
4.5 ����

Terminology Note: When code that might otherwise legally occupy a single line is divided into multiple lines, typically to avoid overflowing the column limit, this activity is called line-wrapping.
����˵������

There is no comprehensive, deterministic formula showing exactly how to line-wrap in every situation. Very often there are several valid ways to line-wrap the same piece of code.
��������һ��ȫ��ġ�ȷ���Ե�׼�������������ÿ������¸���ν��л��С��ܶ�ʱ�򣬶�ͬһ������кü��ֺϷ��Ļ��з�ʽ��

Tip: Extracting a method or local variable may solve the problem without the need to line-wrap.
С��ʾ�����������߱��ر�����ȡ�����п��ܾͽ�������ˣ���������Ҫ���л����ˡ�

4.5.1 Where to break 
####4.5.1 �δ�����
The prime directive of line-wrapping is: prefer to break at a higher syntactic level. Also:
���е���Ҫ���ָ��ԭ���ǣ��������ڸ���һЩ���﷨�����Ͻ��ж��С����У�

When a line is broken at a non-assignment operator the break comes before the symbol. (Note that this is not the same practice used in Google style for other languages, such as C++ and JavaScript.)
���ڷǸ�ֵ����������ж���ʱ������Ҫ���������֮ǰ������ע������+�Ŵ����ж��еĻ���+��Ҫ������һ�У���ע�⣺��� Google��˾���������ԣ���C++��JavaScript���ı����������õ�����������ͬ����

This also applies to the following "operator-like" symbols: the dot separator (.), the ampersand in type bounds (<T extends Foo & Bar>), and the pipe in catch blocks (catch (FooException | BarException e)).
��һ����ͬ����������������������Ƶķ��ţ���ָ���(.)�����Ͱ��е�&���� (<T extends Foo & Bar>)�Լ� catch������е����ܷ��� (catch (FooException | BarException e))

When a line is broken at an assignment operator the break typically comes after the symbol, but either way is acceptable.
����ĳ����ֵ�����������ʱ��ͨ������������ĺ�����ж��У�������ǰ�����Ҳ�ǿ��Խ��ܵġ�

This also applies to the "assignment-operator-like" colon in an enhanced for ("foreach") statement.
��һ����Ҳͬ��������("foreach")����к͸�ֵ��������Ƶ�ð�š�

A method or constructor name stays attached to the open parenthesis (() that follows it.
�������߹��캯��������Ҫ�ͺ����������(()������ͬһ�С�

A comma (,) stays attached to the token that precedes it.
���ţ�,)Ҫ��ǰ���������ͬһ�С�

4.5.2 Indent continuation lines at least +4 spaces 
####4.5.2 ������Ҫ��������+4���ո��ַ�
When line-wrapping, each line after the first (each continuation line) is indented at least +4 from the original line.
�����л���ʱ����һ�к����ÿһ�У�Ҳ����Ϊ���У���Ҫ���ٱȵ�һ�ж������ĸ��ո��ַ�
When there are multiple continuation lines, indentation may be varied beyond +4 as desired. In general, two continuation lines use the same indentation level if and only if they begin with syntactically parallel elements.
���ж������ʱ���������Ҫ���+4���ַ�Ҫ�ࡣͨ�������ҽ����������п�ͷ��Ԫ�����﷨���ǲ��й�ϵ��ʱ�����������в�ʹ����ͬ����������

Section 4.6.3 on Horizontal alignment addresses the discouraged practice of using a variable number of spaces to align certain tokens with previous lines.
4.6.3��ˮƽ����С����ָ��ʹ�����������Ŀո�����ĳЩ������ǰ���еķ��Ŷ�����һ�ֱ���ֹ����Ϊ��
4.6 Whitespace 
###4.6 �հ�

4.6.1 Vertical Whitespace 
####4.6.1 ��ֱ�հ�
A single blank line appears:
�������г����ڣ�

Between consecutive members (or initializers) of a class: fields, constructors, methods, nested classes, static initializers, instance initializers.
ĳ�������Щ�����ĳ�Ա�����߳�ʼ����initializer�����ֶΡ���������������Ƕ���ࡢ��̬��ʼ�����Լ�ʵ����ʼ����֮�䡣
Exception: A blank line between two consecutive fields (having no other code between them) is optional. Such blank lines are used as needed to create logical groupings of fields.
���⣺�����������ֶ�(�м�û����������)֮��Ŀ����ǿ�ѡ��.���ֿ�����Ҫ���ڰ�����Ҫ���ֶν����߼����顣
Within method bodies, as needed to create logical groupings of statements.
Optionally before the first member or after the last member of the class (neither encouraged nor discouraged).
�ڷ������ڣ����԰�����Ҫ���ڶ��������߼����顣
��һ��������ǰ������һ�������ĺ���Ŀ����ǿ�ѡ�ģ��Ȳ�����Ҳ�����ԣ���

As required by other sections of this document (such as Section 3.3, Import statements).
�����ĵ����������ֵ���Ҫ������ӣ�����3.3��Importָ��С�ڣ�
Multiple consecutive blank lines are permitted, but never required (or encouraged).
��������Ŀ���������ģ�������Զ�������Ҫ�󣨻��߹�������
4.6.2 Horizontal whitespace 
####4.6.2 ˮƽ�հ�
Beyond where required by the language or other style rules, and apart from literals, comments and Javadoc, a single ASCII space also appears in the following places only.
�������Ի�����������淶��Ҫ�����⣬�������֡�ע�ͺ�Javadoc�����ڵĻ���ASCII�ո�ֻ���Գ��������µط�.
Separating any reserved word, such as if, for or catch, from an open parenthesis (() that follows it on that line
��ͬһ���еı����֣�����if��for����catch�������������ţ������ֿ�
Separating any reserved word, such as else or catch, from a closing curly brace  that precedes it on that line
��ͬһ���еı����֣�����else����catch����ǰ����һ�����(})�ֿ�

Before any open curly brace ({), with two exceptions:
�������ŵ�ǰ��, ����������������⣺
@SomeAnnotation({a, b}) (no space is used)
String[][] x = {{"foo"}}; (no space is required between {{, by item 8 below)

@SomeAnnotation({a, b}) (����Ҫ�ո�)
String[][] x = {{"foo"}}; (��{{֮�䲻��Ҫ�ո�, by item 8 below)


On both sides of any binary or ternary operator. This also applies to the following "operator-like" symbols:
��Ԫ����Ԫ����������ࡣ��Ҳͬ�������ں���������Ƶķ��š�
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
####4.6.3 ˮƽ���룺����Ҫ
Terminology Note: Horizontal alignment is the practice of adding a variable number of additional spaces in your code with the goal of making certain tokens appear directly below certain other tokens on previous lines.
����˵����ˮƽ����
This practice is permitted, but is never required by Google Style. It is not even required to maintain horizontal alignment in places where it was already used.
���ַ�ʽ������ģ�����Google�����񲢲���Դ˽���Ҫ�������ڲ�Ҫ������Щ�Ѿ����������ַ�ʽ�ĵط���������������ˮƽ���롣
Here is an example without alignment, then using alignment:
����ֱ���û�в��ö���Ͳ����˶�������ӣ�
```
private int x; // this is fine
private Color color; // this too
```
```
private int   x;      // permitted, but future edits
private Color color;  // may leave it unaligned
```
Tip: Alignment can aid readability, but it creates problems for future maintenance. Consider a future change that needs to touch just one line. This change may leave the formerly-pleasing formatting mangled, and that is allowed. More often it prompts the coder (perhaps you) to adjust whitespace on nearby lines as well, possibly triggering a cascading series of reformattings. That one-line change now has a "blast radius." This can at worst result in pointless busywork, but at best it still corrupts version history information, slows down reviewers and exacerbates merge conflicts.
С��ʾ�������ܹ��Կɶ�������������������Ϊ������ά���������鷳������һ�£�δ����һ���Ķ�ֵ��ҪӰ��һ�С���һ�Ķ�����ʹ��֮ǰ��ʽ���õĴ��뱻�ƻ�����������������ġ�������������ʾд������ˣ����������Լ��������������еĿո񣬶���ش���һ���������¸�ʽ����

4.7 Grouping parentheses: recommended 
###4.7 ����Բ���ţ��Ƽ�
Optional grouping parentheses are omitted only when author and reviewer agree that there is no reasonable chance the code will be misinterpreted without them, nor would they have made the code easier to read. It is not reasonable to assume that every reader has the entire Java operator precedence table memorized.
ֻ�е�ȥ���������ţ�����Ҳû�л��ᱻ���ʹ��󣻶����˷������ţ�����Ҳ��������׶����������ߺ�������Ա�Ͽ�����˵����ʱ�򣬿�ѡ�ķ������Ųſ��Ա�ʡ�ԡ�����û���������������ж��߶�������Java���������ȼ���ǵ����������
4.8 Specific constructs 
###4.8 ����ṹ
4.8.1 Enum classes 
####4.8.1 ö����
After each comma that follows an enum constant, a line-break is optional.
��ÿ��ö�ٳ�������Ҫ����һ�����ţ� ��������ǿ�ѡ�ġ�
An enum class with no methods and no documentation on its constants may optionally be formatted as if it were an array initializer (see Section 4.8.3.1 on array initializers).
������Щû�з���������ö�ٳ���û���ĵ�ע�͵�ö������Ը�����Ҫѡ���������ʼ���������и�ʽ������4.8.3.1С�ڣ������ʼ����

private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
Since enum classes are classes, all other rules for formatting classes apply.

4.8.2 Variable declarations 
####4.8.2 ��������
4.8.2.1 One variable per declaration 
#####4.8.2.1 ÿ������һ������
Every variable declaration (field or local) declares only one variable: declarations such as int a, b; are not used.
ÿ�б����������ֶλ��߾ֲ���������ֻ����һ����������Ҫʹ���� `int a, b;`�����ı�����
4.8.2.2 Declared when needed, initialized as soon as possible
#####4.8.2.2 ��Ҫ��ʱ��������������ʼ��Ҫ��������
Local variables are not habitually declared at the start of their containing block or block-like construct. Instead, local variables are declared close to the point they are first used (within reason), to minimize their scope. Local variable declarations typically have initializers, or are initialized immediately after declaration.
��Ҫ���Ѿ�ϰ�ߵ��������������Ĵ������߿�״�ṹ�Ŀ�ͷ���������ֲ��������෴���ֲ�����Ӧ����������״�ʹ�õĵط����������Խ�����������С���ֲ�������ͨ����������ʱ��ͽ��г�ʼ���ˣ�����������֮�����̽��г�ʼ����
4.8.3 Arrays 
####4.8.3 ����
4.8.3.1 Array initializers: can be "block-like" 
#####4.8.3.1 �����ʼ���������ǡ���״��ʽ���ġ�
Any array initializer may optionally be formatted as if it were a "block-like construct." For example, the following are all valid (not an exhaustive list):
���е������ʼ�������Ը��������ʽ���ɡ���״�ṹ����������Щ��ʽ���ǺϷ��ģ���û���꾡���г�ȫ����ʽ����
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
#####4.8.3.2 ��Ҫʹ��C���Է�����������
The square brackets form a part of the type, not the variable: String[] args, not String args[].
�����������͵�һ���֣������Ǳ�����һ���֣�`String[] args`����ȷ�ģ���Ҫʹ��`String args[]`��

4.8.4 Switch statements 
####4.8.4 Switch���
Terminology Note: Inside the braces of a switch block are one or more statement groups. Each statement group consists of one or more switch labels (either case FOO: or default:), followed by one or more statements.
����˵������switch�����Ļ������е���һ������Ĵ��롣ÿ��������һ�����߶��switch��ǩ��Ҫô��`case FOO:`��Ҫô��`default:`�����������һ�����߶�����䡣
4.8.4.1 Indentation 
#####4.8.4.1 ����
As with any other block, the contents of a switch block are indented +2.
�����������һ����switch����������Ҳ������2���ַ���
After a switch label, a newline appears, and the indentation level is increased +2, exactly as if a block were being opened. The following switch label returns to the previous indentation level, as if a block had been closed.
��switch��ǩ���������һ�У��������黹û�����������㼶��2�������switch������Ѿ������ˣ���������ݻ᷵�ص�֮ǰ�������㼶��

4.8.4.2 Fall-through: commented 
#####4.8.4.2 ��մ���ע��
Within a switch block, each statement group either terminates abruptly (with a break, continue, return or thrown exception), or is marked with a comment to indicate that execution will or might continue into the next statement group. Any comment that communicates the idea of fall-through is sufficient (typically // fall through). This special comment is not required in the last statement group of the switch block. Example:
��һ��switch������У�ÿ�����Ҫô��ͻȻ��ֹ�ģ�ʹ��`break`��`continue`��`return`�����׳��쳣����Ҫô����ע�������б���������������ִ�е���һ����롣�κ��ܹ���ʾ����մ������˼��ע�Ͷ����㹻�ģ�ͨ����`// fall through`����switch������е����һ����䲢����Ҫ��������ע�͡����磺
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
#####4.8.4.3 �г�default���
Each switch statement includes a default statement group, even if it contains no code.
ÿ��switch��䶼Ҫ����һ��default��䣬�������������κδ��롣

4.8.5 Annotations 
####4.8.5 ע��
Annotations applying to a class, method or constructor appear immediately after the documentation block, and each annotation is listed on a line of its own (that is, one annotation per line). These line breaks do not constitute line-wrapping (Section 4.5, Line-wrapping), so the indentation level is not increased. Example:
Ӧ�õ��ࡢ�������߹������ϵ�ע���ǽ������ĵ���չʾ�ģ�ÿ��ע��ռ��һ�С�����֮��Ļ��з����������Զ����У�4.5С�ڣ��Զ����У������������㼶���������ӡ����磺
```
@Override
@Nullable
public String getNameIfPresent() { ... }
```
Exception: A single parameterless annotation may instead appear together with the first line of the signature, for example:
���⣺���ֻ��һ��ע�Ⲣ�Ҹ�ע��Ҳû�в�������ô�����Ժ�ǩ���ĵ�һ������һ�𣬱��磺
```
@Override public int hashCode() { ... }
```
Annotations applying to a field also appear immediately after the documentation block, but in this case, multiple annotations (possibly parameterized) may be listed on the same line; for example:
Ӧ�õ��ֶε�ע��Ҳ���Խ������ĵ���һ����֣���������������£����ע�⣨Ҳ�п������в����ģ���������ͬһ�У����磺

```
@Partial @Mock DataLoader loader;
```
There are no specific rules for formatting parameter and local variable annotations.
���ڲ����;ֲ�������ע�Ⲣû����ȷ�Ĺ淶�����и�ʽ����
4.8.6 Comments 

4.8.6.1 Block comment style 
#####4.8.6.1 ��ע����ʽ
Block comments are indented at the same level as the surrounding code. They may be in /* ... */ style or // ... style. For multi-line /* ... */ comments, subsequent lines must start with * aligned with the * on the previous line.
��ע�͵����������������Χ�Ĵ��������������ͬ�����ǿ��Բ��� `/* ... */`��ʽ��Ҳ���Բ���`// ..`��ʽ�����ڶ��е�`/* ... */`ע�ͣ������ע���б�����*��ͷ��*��Ҫ����һ�е�*�Ŷ��롣
```
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```
Comments are not enclosed in boxes drawn with asterisks or other characters.
���������ǺŻ��������ķ����������ķ�������ע�Ͱ�������

Tip: When writing multi-line comments, use the /* ... */ style if you want automatic code formatters to re-wrap the lines when necessary (paragraph-style). Most formatters don't re-wrap lines in // ... style comment blocks.
С��ʾ�� ����д���е�ע��ʱ���������Ҫ���Զ������ʽ�������ڱ�Ҫ��ʱ�򣨱���ֶ���ʽ��������Щע��������֯����ʱ����Ҫʹ��`/* ... */`��ʽ���󲿷ָ�ʽ�����߲����ܽ�`// ...`��ʽ��ע�Ϳ��е�����������֯���л��С�
4.8.7 Modifiers 
#### 4.8.7 ���η�
Class and member modifiers, when present, appear in the order recommended by the Java Language Specification:
��ʹ����ͳ�Ա���η�ʱ������Ҫ����Java���Թ淶�н����˳�������У�

`public`��`protected`��`private`��`abstract`��`static`��`final`��`transient` ��`volatile`��`synchronized`��`native`��`strictfp`��
4.8.8 Numeric Literals 
####4.8.8 ��ֵ
long-valued integer literals use an uppercase L suffix, never lowercase (to avoid confusion with the digit 1). For example, 3000000000L rather than 3000000000l.
�����͵�����ֵҪʹ�ô�д��ĸL��Ϊ��׺����Զ��Ҫʹ��Сд��ĸ�������������1���������������磬ʹ��`3000000000L`����Ҫʹ��`3000000000l`��

5 Naming 
##5 ����


5.1 Rules common to all identifiers 
###5.1 ���������б�ʶ����ͨ�ù淶

Identifiers use only ASCII letters and digits, and in two cases noted below, underscores. Thus each valid identifier name is matched by the regular expression \w+ .
��ʶ��ֻ��ʹ��ASCII��ĸ�����֣��� ����ÿ���Ϸ��ı�ʶ�����ֶ�����������ʽ`\w+`��ƥ�䡣
In Google Style special prefixes or suffixes, like those seen in the examples name_, mName, s_name and kName, are not used.
��Google�ķ��淶�У�����Щ����`name_`��`mName`��`s_name`��`kName`���ض���ǰ׺���ߺ�׺�ǲ���ʹ�õġ�

5.2 Rules by identifier type 
###5.2 ��ʶ���淶

5.2.1 Package names 
####5.2.1����

Package names are all lowercase, with consecutive words simply concatenated together (no underscores). For example, com.example.deepspace, not com.example.deepSpace or com.example.deep_space.
������ȫ��Сд�ģ�������ĵ��ʼ򵥵ش���һ��û���»��ߣ�������`example`, `com.example.deepspace`,������`com.example.deepSpace`��`com.example.deep_space`���֡�

5.2.2 Class names 
####5.2.2 ����
Class names are written in UpperCamelCase.
�����ǲ�������ĸ��д���շ�ʽ��UpperCamelCase��������ġ�
Class names are typically nouns or noun phrases. For example, Character or ImmutableList. Interface names may also be nouns or noun phrases (for example, List), but may sometimes be adjectives or adjective phrases instead (for example, Readable).
�����Ǳ�׼�����ʻ������ʶ������`Character`����`ImmutableList`���ӿ���Ҳ���������ʻ������ʶ������`List`��,������ʱ����Ҳ���������ݴʻ������ݴʶ������`Readable`��    

There are no specific rules or even well-established conventions for naming annotation types.
��������ר�ŵĹ���������Ƶ�Լ�������ڸ�ע�����ͽ���������
Test classes are named starting with the name of the class they are testing, and ending with Test. For example, HashTest or HashIntegrationTest.
����������ֶ�������Ҫ���Ե�������ֿ�ͷ�ģ�������Test��β������`HashTest` ����`HashIntegrationTest`��
5.2.3 Method names 
####5.2.3 ������
Method names are written in lowerCamelCase.
���������õ�������ĸ��Ϣ���շ�ʽ��lowerCamelCase���ķ��
Method names are typically verbs or verb phrases. For example, sendMessage or stop.
������ͨ���Ƕ��ʻ��߶��ʶ������`sendMessage`����`stop`��
Underscores may appear in JUnit test method names to separate logical components of the name. One typical pattern is test<MethodUnderTest>_<state>, for example testPop_emptyStack. There is no One Correct Way to name test methods.
�»��߿��Գ�����JUnit�Ĳ��Է������������ڽ����Է��������Ƶĸ��߼����ֽ������֡� һ�ֵ��͵�ģʽ����`test<MethodUnderTest>_<state>`�� ����`testPop_emptyStack`�����ڲ��Է�������������������һ����ν�ġ���ȷ����ʽ��
5.2.4 Constant names 
####5.2.4 ������
Constant names use CONSTANT_CASE: all uppercase letters, with words separated by underscores. But what is a constant, exactly?
������ʹ��`CONSTANT_CASE`�ĸ�ʽ��ȫ��д�������֮������»��߽��зָ���ǵ���ʲô�ǳ����أ�
Every constant is a static final field, but not all static final fields are constants. Before choosing constant case, consider whether the field really feels like a constant. For example, if any of that instance's observable state can change, it is almost certainly not a constant. Merely intending to never mutate the object is generally not enough. Examples:
ÿ����������һ����̬final�ֶΣ����ǲ��������еľ�̬final�ֶζ��ǳ�������ѡ��������������ʱ��Ҫ��������ֶ��Ƿ������һ�����������磬һ��ʵ����ֻҪ��һ��״̬��Ϣ����ɼ������ܹ������仯����ô�������Կ϶�������һ����������������˵���������Զ���ᷢ���仯ͨ���ǲ����ġ����磺
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
���ǵ�����ͨ���������ʻ������ʶ��
5.2.5 Non-constant field names 
####5.2.5 �ǳ����ֶε�����
Non-constant field names (static or otherwise) are written in lowerCamelCase.
�ǳ����ֶε����ƣ���̬���߷Ǿ�̬�������ǲ�������ĸСд���շ�ʽ�ķ���������ġ�
These names are typically nouns or noun phrases. For example, computedValues or index.
��Щ����һ�㶼�����ʻ������ʶ������`computedValues `����`index`��

5.2.6 Parameter names 
####5.2.6 ������

Parameter names are written in lowerCamelCase.
�������ǲ�������ĸСд���շ�ʽ�ķ����������
One-character parameter names should be avoided.
Ӧ�ñ���ʹ��ֻ��һ���ַ��Ĳ�����
5.2.7 Local variable names 
####5.2.7 �ֲ�������
Local variable names are written in lowerCamelCase, and can be abbreviated more liberally than other types of names.
�ֲ����������ֲ��õ�������ĸСд���շ�ʽ�ķ��������������͵����֣��Ծֲ����������ֽ�����д�Ŀռ����һЩ��
However, one-character names should be avoided, except for temporary and looping variables.
Ȼ�������ַ������ֻ���Ҫ����ģ�������������ʱ������ѭ�������С�
Even when final and immutable, local variables are not considered to be constants, and should not be styled as constants.
����ֲ�������final��immutable�ģ���Ҳ���ܱ������ǳ�����Ҳ��Ӧ��ʹ�ó������ֵ���ʽ��
5.2.8 Type variable names 
####5.2.8 ���ͱ�����
Each type variable is named in one of two styles:
����һ�����ͱ�����Ӧ�ò�������������ʽ�е�һ��������������
A single capital letter, optionally followed by a single numeral (such as E, T, X, T2)
�����Ĵ�д��ĸ���������Ҫ����������һ�����֣�����`E`��`T`��`X`��`T2`��
A name in the form used for classes (see Section 5.2.2, Class names), followed by the capital letter T (examples: RequestT, FooBarT).
����ʹ�õ������ʽ����������5.2.2С�ڣ����������������һ����д��ĸT(����`RequestT`��`FooBarT`)
5.3 Camel case: defined 
###5.3 �շ�ʽ��������
Sometimes there is more than one reasonable way to convert an English phrase into camel case, such as when acronyms or unusual constructs like "IPv6" or "iOS" are present. To improve predictability, Google Style specifies the following (nearly) deterministic scheme.
��ʱ���ж��ֺ���ķ�ʽ����һ��Ӣ�Ķ���ת�����շ�ʽ��ƴд��ʽ�����統������`��IPv6��`����`��iOS��`����������ĸ��д���߶��ص��﷨�ṹ����ʱ��Ϊ����߿�Ԥ���ԣ�Google���淶ָ����������ȷ�ķ�����

Beginning with the prose form of the name:


Convert the phrase to plain ASCII and remove any apostrophes. For example, "M��ller's algorithm" might become "Muellers algorithm".
�������е�Ʋ�ţ�'��ɾ���������������ַ�ת���ɴ�ASCII�롣����`"M��ller's algorithm"`����`"M��llers algorithm"`��
Divide this result into words, splitting on spaces and any remaining punctuation (typically hyphens).
������ָ��һ�����ĵ��ʣ��ָ�������ǿո������������������ţ�ͨ�������ӷ�����
Recommended: if any word already has a conventional camel-case appearance in common usage, split this into its constituent parts (e.g., "AdWords" becomes "ad words"). Note that a word such as "iOS" is not really in camel case per se; it defies any convention, so this recommendation does not apply.
���飺����ָ�����ĵ����Ѿ��ǳ��õ�Լ���õ��շ�ʽ��ƴд��ʽ����ô��Ҫ�����ٷָ�ɸ�С�Ĳ��֣����罫`AdWords`�ֳ�`ad words`������Ҫע����ǣ���`"iOS"`�����ĵ��ʲ������������շ�ʽƴд�����������κ�һ��Լ�������Ըý��鲢������������
Now lowercase everything (including acronyms), then uppercase only the first character of:
���ڽ��������ݶ�����Сд����������ĸ��д�Ĵʣ���Ȼ��ֻ������ĸ���д�д����󣬽����еĵ������������͹�����һ����ʶ����
... each word, to yield upper camel case, or
��ÿ�����ʵ�����ĸ����д���͹���������ĸ��д���շ�ʽƴд��
... each word except the first, to yield lower camel case
�����˵�һ������֮����������ʵ�����ĸ����д���͹���������ĸСд���շ�ʽƴд��
Finally, join all the words into a single identifier.
Note that the casing of the original words is almost entirely disregarded. 
��Ҫע����ǣ�ԭ����Щ���ʵĴ�Сд��������ȫ�������ˡ�
Examples:

|Prose form	         |Correct	     |Incorrect
| -------------          |:-------------:    | -----:|
|"XML HTTP request"      |XmlHttpRequest     |XMLHTTPRequest
|"new customer ID"       |newCustomerId	     |newCustomerID
|"inner stopwatch"       |innerStopwatch     |innerStopWatch
|"supports IPv6 on iOS?" |supportsIpv6OnIos  |supportsIPv6OnIOS
|"YouTube importer"	 |YouTubeImporter    |YoutubeImporter*	

*Acceptable, but not recommended.
*�ű�ʾ���Խ��ܣ����ǲ����Ƽ�����
Note: Some words are ambiguously hyphenated in the English language: for example "nonempty" and "non-empty" are both correct, so the method names checkNonempty and checkNonEmpty are likewise both correct.
ע�⣺��Ӣ�������У���һЩ����֮���Ƿ�ʹ�����ӷ�������ȷ������`"nonempty"`��`"non-empty"`������ȷ�ģ�������������`checkNonempty`��`checkNonEmpty`ͬ��Ҳ������ȷ�ġ�
6 Programming Practices 
##6 ���ʵ��
6.1 @Override: always used 
###6.1 @Override��һֱ��Ҫʹ��
A method is marked with the @Override annotation whenever it is legal. This includes a class method overriding a superclass method, a class method implementing an interface method, and an interface method respecifying a superinterface method.
ֻҪ�Ƿ����﷨�ģ���Ҫʹ��@Overrideע�������������б�ǡ������ĳ����ķ����������丸��ķ�����ĳ���෽��ʵ���˽ӿڷ�����ĳ���ӿڷ���������������ڵķ�����
Exception:@Override may be omitted when the parent method is @Deprecated.
���⣺����������@Deprecated��ʱ�򣬿��Խ�@Overrideʡ�Ե���
6.2 Caught exceptions: not ignored 
###6.2 �����쳣�����ܺ���

Except as noted below, it is very rarely correct to do nothing in response to a caught exception. (Typical responses are to log it, or if it is considered "impossible", rethrow it as an AssertionError.)

���������г�����������ڲ�����쳣������Ϊ������Ӧ��������ȷ�ġ�����׼����Ӧ�н�����־��¼�������������Ϊ�ǲ����ܷ����������Ӧ�ý�����Ϊ`AssertionError`����throw��ȥ����
When it truly is appropriate to take no action whatsoever in a catch block, the reason this is justified is explained in a comment.
���ȷʵ����Ҫ��catch����������κβ���������Ҫ��ע���н������������ɡ�
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
���⣺�ڲ����У����������쳣�Ƿ���Ԥ�ڵģ���ô���쳣�Ϳ���ֱ�Ӻ��Զ�����Ҫ���ע�͡������������һ���ǳ��������÷�����֤�����Եķ����׳�һ���������͵��쳣�������Ͳ���Ҫע���ˣ�
```
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```
6.3 Static members: qualified using class 
###6.3 ��̬��Ա���޶�Ϊʹ���������е���

When a reference to a static class member must be qualified, it is qualified with that class's name, not with a reference or expression of that class's type.
�Ծ�̬���Ա�����ñ���������ƣ�������ֻ����������ƽ������ã����������������ڵ����͵����û��߱��ʽ��
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
6.4 Finalizers: not used 
###6.4 Finalizers�� ��Ҫʹ��
It is extremely rare to override Object.finalize.
����Object.finalize�Ǽ��亱���ġ�
Tip: Don't do it. If you absolutely must, first read and understand Effective Java Item 7, "Avoid Finalizers," very carefully, and then don't do it.
С��ʾ�� ��Ҫʹ�á��������Ա���Ҫʹ�õĻ���������ϸ���Ķ�����⡶Effective Java��һ��ĵ�7���Avoid Finalizers,���� Ȼ��Ҫʹ�á�
7 Javadoc 
##7 Javadoc
7.1 Formatting 
###7.1��ʽ��
7.1.1 General form 
####7.1.1 һ���ʽ
The basic formatting of Javadoc blocks is as seen in this example:
Javadoc��Ļ�����ʽ������������������������ģ�
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
���ֻ�����ʽһֱ���Ǳ��Ͽɵġ���û������������Ҫ��¼���ҽ�����Javadoc�飨����ע�ͱ�ǣ��ŵ�һ���о��㹻ʱ������ʹ�õ��е���ʽ�����档
7.1.2 Paragraphs 
####7.1.2 ����
One blank line��that is, a line containing only the aligned leading asterisk (*)��appears between paragraphs, and before the group of "at-clauses" if present. Each paragraph but the first has <p> immediately before the first word, with no space after.
λ�ڡ�@��ǡ�������м�¼�Ļ���֮ǰ����Щ����֮��Ҫ��һ������-Ҳ����ֻ������һ��������Ǻţ�*�����С����˵�һ��֮����������䶼��Ҫ�ڵ�һ������֮ǰ��һ��<p>���,����֮�䲻���пո�
7.1.3 At-clauses 
####7.1.3 @���
Any of the standard "at-clauses" that are used appear in the order @param, @return, @throws, @deprecated, and these four types never appear with an empty description. When an at-clause doesn't fit on a single line, continuation lines are indented four (or more) spaces from the position of the @.
��ʹ�õ�����"@���"��Ҫ����@param�� @return�� @throws�� @deprecated��˳����б�д���������ǵ��������ݲ���Ϊ�ա�
��@����������һ����д��ʱ��������Ҫ�����@���ŵ�λ������4�������߸��ࣩ�Ŀո�

7.2 The summary fragment 
###7.2 
The Javadoc for each class and member begins with a brief summary fragment. This fragment is very important: it is the only part of the text that appears in certain contexts such as class and method indexes.
ÿ����ͳ�Ա��Javadoc���Ǵ�һ�μ��ĸ���Ƭ�ο�ʼ�ġ����Ƭ�ηǳ���Ҫ������Ψһ����������ͷ�������������ĳ���������е��ı���
This is a fragment��a noun phrase or verb phrase, not a complete sentence. It does not begin with A {@code Foo} is a..., or This method returns..., nor does it form a complete imperative sentence like Save the record.. However, the fragment is capitalized and punctuated as if it were a complete sentence.
���Ƭ����һ�����ʶ�����߶��ʶ��������һ�������ľ��ӡ����Ȳ�����`A {@code Foo} is a...`����`This method returns...`���������ֿ�ͷ��Ҳ������`Save the record..`���������ɵ�����ʽ�ľ��ӡ����ǣ����ڸ�Ƭ��������ĸ��д�ģ������б����ţ�ʹ����������������һ�������ľ��ӡ�
Tip: A common mistake is to write simple Javadoc in the form /** @return the customer ID */. This is incorrect, and should be changed to /** Returns the customer ID. */.
С��ʾ
һ�������Ĵ��������`/** @return the customer ID */`��������ʽ����д�򵥵�Javadoc�����ַ�ʽ�Ǵ���ģ���Ӧ�øĳ�`/** Returns the customer ID. */`��

7.3 Where Javadoc is used 
###7.3 �δ�ʹ��Javadoc

At the minimum, Javadoc is present for every public class, and every public or protected member of such a class, with a few exceptions noted below.
���٣�Javadoc��Ҫ������ÿ��public���Լ������public��protected��Ա��ֻ����������Щ��������⣺
Other classes and members still have Javadoc as needed. Whenever an implementation comment would be used to define the overall purpose or behavior of a class, method or field, that comment is written as Javadoc instead. (It's more uniform, and more tool-friendly.)
��������ͳ�Ա��Ȼ������Ҫ����Javadoc�ġ�����ʲôʱ��ֻҪע�������ڶ����ࡢ���������ֶε�������;ʱ����ô����ע�;�Ӧ��д��Javadoc�������͸���һ�ºͶԹ����Ѻá���

7.3.1 Exception: self-explanatory methods 
###7.3.1���⣺�Խ��͵ķ���
Javadoc is optional for "simple, obvious" methods like getFoo, in cases where there really and truly is nothing else worthwhile to say but "Returns the foo".
������Щ���򵥡��Զ��׼�������`getFoo`�����ķ�����Javadoc�ǿ�ѡ��,����������£�����˵������foo��֮�⣬ȷʵû��ʲô����ֵ�������ˡ�
Important: it is not appropriate to cite this exception to justify omitting relevant information that a typical reader might need to know. For example, for a method named getCanonicalName, don't omit its documentation (with the rationale that it would say only /** Returns the canonical name. */) if a typical reader may have no idea what the term "canonical name" means!
��Ҫ��ʾ��Ҳ��ĳЩ�ǳ���Ҫ����Ϣ����������Ҫ�˽�ģ���ô���Ÿ���������Ϊ������Ϣʡ�Ե������ǲ�ǡ���ġ����磬��һ����Ϊ`getCanonicalName`�ķ�����������߲�֪�����canonical name���ĺ��壬��ô���ǾͲ��ܣ����˵Javadoc������ֻ��/** ���ع淶�������ƣ� canonical name��. */ ����ʡ�������ĵ���

7.3.2 Exception: overrides 
####7.3.2 ����:����

Javadoc is not always present on a method that overrides a supertype method.
������Щ�����෽���������صķ�����Javadoc����������Ҫ�ṩ�ġ�