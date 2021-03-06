### 3.3.5 **boolean类型**
1.占1位  
2.整型值与布尔值之间不能转换
## 3.4 变量
`$`是个合法的变量名字符，只用在java编译器或其他工具生成的名字中  
### 3.4.1 **变量初始化**
1.声明一个变量之后，必须用赋值语句对变量显式初始化，否则编译器报错。  
2.不区分变量的声明与定义
### 3.4.1 **常量**
1.`final`关键字修饰，这个变量只能被赋值一次，一旦被赋值后就不能再修改。`final int NUM = 10;`  
2.`const`是保留关键字，但未被使用
## 3.5 运算符
1.`整数/0`将产生`ArithmeticException`异常，`浮点数/0`将会得到无穷大或NaN结果。  
2.`strictfp`关键字要求使用严格的浮点计算
### 3.5.1 **数学函数与常量**
1.`Math.sqrt()`计算平方根  
2.`Math.pow()`计算幂值
### 3.5.2 **类型转换**
```mermaid
graph LR
D(char)-->C
A(byte)-->B(short)
B-->C(int)
C-->E(long)-->G(double)
C.->F(float)-->G
E.->F
C-->G
```
### 3.5.3 **强制转换**
不要将`boolean`与任何数值类型进行强制转换，必要时使用条件表达式：`b ? 1 : 0`
### 3.5.4 **结合赋值与运算符**
结合赋值（如`+=`）得到的值，其类型与左侧操作数的类型不同，就会发生强制类型转换。  
```java
int x = 0;  
x += 3.5; // (int) x = x + 3.5;
```
### 3.5.6 **关系与boolean运算符**
`&&`和`||`运算符是按照“短路”方法来求值的
### 3.5.7 **位运算符**
*算术移位*——扩展符号位  
*逻辑移位*——扩展0  
`>>` 扩展符号位  
`<<` 扩展低位填0  
`>>` 扩展高位0  
*g++ >> 为算术移位实现，没有>>>运算符*
### 3.5.8 **运算符优先级**
|运算符|结合性|
|:-|:-|
|[].()(方法调用)|从左到右|
|！~++--+(一元运算符:正)-(一元运算符:负)()(强制类型转换)new|从右向左|
|*/%|从左向右|
|+-|从左向右|
|== ！=|从左向右|
|&|从左向右|
|^|从左向右|
|||从左向右|
|&&|从左向右|
||||从左向右|
|?:|从右向左|
|= += -= *= /= %= &= \|= ^= <<= >>= >>> =|从右向左
1. `.`运算符优先级高于`()强制类型转换`运算符优先级  
```java
int a = (int)parent.son.getNum();
```
## 3.6 字符串
### 3.6.1 **子串 substring()方法**
`substring()`方法从字符串提取出一个新的子串并返回
### 3.6.2 **拼接**
1.java使用`+`运算符实现字符串的拼接；  
2.一个字符串对象与一个其他类型进行拼接时，后者将会被转为字符串；  
3.java中的任何对象都可以转换为String类型。  
### 3.6.3 **不可变字符串**
java中字符串中的字符不能被修改，字符串为*不可变字符串*。不可变字符串的优点：编译器可以让字符串共享。java中只有**字符串常量**是共享的，通过`new`返回的字符串不相等
```java
String str1 = "java\u2122";
String str2 = "ava\u2122"
String str3 = str1.substring(1); // str3内容与str2一样
System.out.println(str2.hashcode());
System.out.println(str3.hashcode());
************************************************
输出：
hashcode: 100907840, 3014614
```
`substring()`方法会`new`申请一块内存并将子串拷贝进去，因此`str2`和`str3`的hashcode不相等，不是同一块内存（对象），编译器无法共享。
### 3.6.4 **检测字符串是否相等**
1.使用`equals()`方法检测两个字符串是否相等：`s.equals(t)`，返回`true`，相等；返回`false`，不相等。  
2.使用`compareTo()`方法检测两个字符串是否相等：`s.compareTo(t)`，返回`0`，相等；返回`<0`，s小于t（按字典序比较第一个不相等的字符的差值）；返回`>0`，s大于t。  
3.不能使用`==`运算符比较两个字符串相等，`==`只是比较字符串的引用值是否相等，即是否是指向同一块内存，不能比较字符串的内容。
### 3.6.5 **空串与null串**
**空串**：`s.length() == 0`或者`s.equals("")`。  
**null串**：s == null。
### 3.6.6 **码点与代码单元**
大多数Unicode字符使用一个代码单元即可表示，但是辅助字符可能需要两个。  
**码点**：字符串中每个字符对应的编码值；  
**代码单元**：字符串由多少个编码单元构成，有可能一个码点对应多个编码单元。
```java
String str = "\uD835\uDD46hi"; // str = "𝕆hi"，IDEA输入
System.out.println(str); // 𝕆hi
System.out.println(str.length()); // 4
System.out.println(str.codePointsCount(0, str.length())); //3
System.out.println(str.charAt(1)); // 返回的是𝕆第二个代码单元并不是'h'。
```
**字符串遍历码点方法**：
```java
int codePoint = s.codePointAt(i);
if (Character.isSupplementaryCodePoint(codePoint)) {
    i += 2;
} else {
    i++;
}
``` 
*CharSequence*类型是一种接口类型，所有的字符串都属于此接口
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence{}
```
### 3.6.9 **构建字符串 StringBuilder**
1.创建对象：`StringBuilder str = new StringBuilder()`  
2.添加元素：`str.append()`  
3.转成字符串：`str.toString()`
## 3.7 输入输出
### 3.7.1 **读取输入**
构造一个`Scanner`对象并与标准输入流`System.in`相关联：  
`Scanner in = new Scanner(System.in);`。  
1.`nextInt()`如果输入的数据超出int范围则会报`InputMismatchException`异常。
### 3.7.2 **格式化输出**
1.使用`String.format()`方法返回一个给定格式的字符串。  
