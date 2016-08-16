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


## 1.1例子

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

# 2.通则

