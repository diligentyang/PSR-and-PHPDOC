这一部分标准包括，哪些应该被认为是标准的编码元素，以确保共享的PHP代码间具有较高程度的技术互通性。

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 

# 1.概览

- PHP文件**必须**只使用 `<?php` 和 `<?` 这两种标签。
- PHP文件**必须**以不带BOM的UTF-8编码。
- PHP文件中**应该**只定义类、函数、常量等声明，或其他会产生从属效应 的操作（如：生成文件输出以及修改.ini配置文件等），但是**不应该**同时做着两件事情。
- 命名空间以及类必须符合 PSR 的自动加载规范：[PSR-0](http://www.php-fig.org/psr/psr-0/) 或 [PSR-4](http://www.php-fig.org/psr/psr-4/) 中的一个；
- 类的命名**必须**遵循以大写开头的驼峰命名规则（`StudlyCaps`）。
- 类中的常量所有字母都**必须**大写，单词间用下划线分隔。
- 方法名**必须**符合以小写开头的驼峰命名法（`camelCase`）。


# 2.文件

## 2.1PHP标签

PHP代码**必须使用**`<?php ?>`长标签或`<?= ?>`短标签输出。**一定不能**使用其他标签。

## 2.2字符编码

PHP代码**必须**只可使用不带BOM的UFT-8编码

## 2.3从属效应（副作用）

一个文件**应该**要不就只定义声明（类，函数，常亮等），要不就只有产生从属效应的逻辑操作，但**不应该**两者都有。

短语“副作用”（side effects）意味着执行的逻辑仅仅从包含文件，而没有直接关系到声明类，函数，常量等。

“从属效应”包含却不仅限于：生成输出、直接的 require 或 include、连接外部服务、修改 ini 配置、抛出错误或异常、修改全局或静态变量、读或写文件等。

下面是一个同时拥有声明和从属效应的例子，应该避免：

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}


```

下面是一个只包含声明而没有包含`side effects`的例子，应该被模仿：

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}


```