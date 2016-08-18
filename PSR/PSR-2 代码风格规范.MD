这篇规范是[PSR-1](http://note.youdao.com/http://www.php-fig.org/psr/psr-1/)（基本代码规范）的扩展和继承。

本规通过制定一系列规范化PHP代码的规则，以减少在浏览不同作者的代码时，因代码风格的不同而造成不便。

这个风格规范是从各种各样的项目的共性中延伸出来的。当多名程序员在多个项目中合作时，它有助于有一套准则，在所有的项目中使用。

因此，本指南的好处不是在规则本身，而是在这些规则的共享。 

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 

# 1.概览

- 代码**必须**遵循[PSR-1](http://note.youdao.com/http://www.php-fig.org/psr/psr-1/)基本代码规范。
- 代码**必须**使用四个空格符进行缩进，而不是一个tab键。
- 每行**应该**保持在80个字符以内，软限制**必须**是120个字符，但**一定不能**有硬性限制。
- 每个`namespace`命名空间声明语句和`use`声明语句块后面，**必须**有一个空白行。
- 类的开始花括号(`{`)**必须**写在函数声明后自成一行，结束花括号(`}`)也**必须**写在函数主体后自成一行。
- 方法的开始花括号(`{`)**必须**写在函数声明后自成一行，结束花括号(`}`)也**必须**写在函数主体后自成一行。
- 在所有的属性和方法上都**必须**声明可见性(译者注：`private`，`protected`以及`public`)；`abstract`和`final`**必须**声明在可见性之前；`static`**必须**声明在可见性之后。
- 控制结构的关键词后面**必须**有一个空格符，方法和函数调用**一定不能**有。
- 控制结构的开始花括号(`{`)**必须**写在声明的同一行，而结束花括号(`}`)**必须**写在主体后自成一行。
- 控制结构的开始左括号（`{`）之后**一定不能**有空格，右括号(`}`)之前**一定不能**有空格。


## 1.1 例子

以下这个例子简单的展示了以上的大部分规范。

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}

```

# 2. 通则

## 2.1 基本编码规范

代码**必须符合**[PSR-1](http://www.php-fig.org/psr/psr-1/)的所有规范

## 2.2 文件

所有PHP文件**必须**使用`Unix LF (linefeed)`作为行的结束符。

所有PHP文件**必须**以一个空白行结束。

纯PHP代码文件**必须**省略最后的 ?> 结束标签。

## 2.3 行

行的长度**一定不能**有硬性的约束。

行长度的软性约束一定限制在120个字符以内；如果超过此长度，代码规范检查器**必须**发出警告，**一定不能**报错。

每行**不应该**超过80个字符；超过80个字符的行，**应该**被拆分成多个不超过80个字符的后续行。

在非空白行的后面**一定不能**有多余的空格符。

空行**可以**用来改善可读性和区分相关的代码块。

每行**一定**不能多余一条语句。


## 2.4 缩进

代码**必须**使用四个空格符缩进，**一定不能**使用tab键。

> 备注：只用空格，不于tab混合使用，有助于避免代码差异、打补丁、重阅代码以及注释时产生混淆。使用空格还可以使调整细微的缩进来改变对齐变得简单。

## 2.5 关键字和True/False/Null

PHP关键字**必须**全部小写。

PHP常量true,false和null**必须**全部小写。

# 3. 命名空间以及Use声明

存在命名空间时，其后面**必须**有一个空白行。

所有的use，**必须**在命名空间后声明。

每条`use`声明语句，**必须**只有一个`use`关键字。

`use`声明语句块后面**必须**有一个空白行。

例如：

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```

# 4. 类、属性和方法

此处的“类”泛指所有的class类、接口以及traits可复用代码块。

## 4.1 扩展和继承

关键词`extends`和`implements`**必须**和类名在同一行。

类开始的花括号（`{`）**必须**独占一行，类结束的花括号（`}`）**必须**在类主体后独占一行。

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}

```

`implements`的接口列表也可以分成多行，当这样做时，列表中的第一个接口**必须**放在下一行中，每行**必须**只有一个接口

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}

```

## 4.2 属性

所有属性都**必须**声明可见性。

**一定不能**使用关键字`var`声明一个属性。

每条语句**一定不能**定义超过一个属性。

属性名称**不应该**以单个下划线作为前缀来表示属性是`protected`或`private`。

一个属性的声明应该像下面这样。

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}

```

## 4.3 方法

所有方法都**必须**声明可见性（访问修饰符）。

方法名称**不应该**以单个下划线作为前缀来表示是`protected`或`private`。

方法名称后**一定不能**有空格符，其开始花括号**必须**独占一行，结束花括号也**必须**在方法主体后单独成一行。参数左括号后和右括号前**一定不能**有空格。

一个方法定义应该像下面这样，注意括号，逗号，空格和花括号的位置：

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}

```

## 4.4 方法参数

在参数列表中，每个逗号之前**一定不能**有空格，每个逗号之后**必须**有一个空格。

方法参数中，有默认值的，**必须**放到参数列表的末尾。

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}

```

参数列表**可以**被拆分成分别有一次缩进的多行，这样，列表中的第一项**必须**放在下一行，每一行**必须**只放一个参数。

拆分成多行的参数列表后，结束括号以及方法开始花括号**必须**写在同一行，中间用一个空格分隔，一起自成一行。

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}

```

## 4.5 `abstract`,`final`和`static`

当存在时，`abstract`和`final`声明**必须**放在可见性之前。

当存在时，`static`声明**必须**放在可见性后。

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}

```

## 4.6 方法和函数调用

方法及函数调用时，方法名或函数名与左括号之间**一定不能**有空格，参数右括号前也**一定不能**有空格。在参数列表中，每个逗号之前**一定不能**有空格，每个逗号之后**必须**有一个空格。

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);

```

参数**可以**被拆分成多个有一个缩进的后续行，如果这么做，参数列表中的第一个必须放在下一行，并且每一行只能有一个参数。

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);

```

# 5. 控制结构

控制结构基本样式规范如下：

- 控制结构关键词后**必须**有一个空格。
- 左括号`(`后面**一定不能**有空格。
- 右括号`)`前**一定不能**有空格。
- 右括号`)`和开始花括号`{`之间**必须**有一个空格。
- 结构体**必须**缩进一次。
- 结束花括号`}`**必须**在主体后自成一行。

每个结构体的主题都**必须**被包含在成对的花括号中，这使结构体看起来更加规范以及减少加入新行时，出错的可能性。。

