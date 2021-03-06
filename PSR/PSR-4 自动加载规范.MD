关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)

# 1. 概述

本PSR是关于由文件路径自动载入对应类的相关规范，本规范是可互操作的，可以作为任一自动载入规范的补充，其中包括[PSR-0](http://www.php-fig.org/psr/psr-0/)，此外，本 PSR 还包括自动载入的类对应的文件存放路径规范。

# 2. 详细说明

1. 此处的类泛指class类、接口、traits可复用代码块以及其它类似结构。
2. 一个完全限定的类名称有以下形式:
 1. 完全限定类名**必须**要有一个顶级命名空间，被称为"vendor namespace"。
 2. 完全限定类名**可以**有一个或多个子命名空间。
 3. 完全限定类名**必须**有一个终止的类名。
 4. 在完全限定类名的任何部分中，下划线都没有特殊的意义。 
 5. 所有的类名**必须**以大小写敏感的方式引用。
 
3. 当加载一个对应于一个完全限定的类名称的文件时...
 1. 在完全限定类命中，连续的一个或几个子命名空间构成的`命名空间前缀`（不包括顶级命名空间的分隔符）至少对应着至少一个`基础目录`
 2. 在 命名空间前缀后的连续的子命名空间名称对应着 基础目录下的子目录，其中的命名空间分隔符表示目录分隔符，子目录名称**必须**和子命名空间名大小写匹配。 
 3. 终止类名**必须**与对应的以**.php**为后缀的文件同名。

4. 自动加载器（autoloader）的实现**一定不能**抛出异常、**一定不能**触发任一级别的错误信息以及**不应该**有返回值。

# 3. 例子

下面的表显示了符合规范完整类名、命名空间前缀和文件基目录所对应的文件路径。

完整的限定类名 | 命名空间前缀 | 文件基目录 | 文件路径
--- | --- | --- | ---
`\Acme\Log\Writer\File_Writer`| `Acme\Log\Writer` | `./acme-log-writer/lib/` | `./acme-log-writer/lib/File_Writer.php`
`\Aura\Web\Response\Status` | `Aura\Web` | `/path/to/aura-web/src/` | `/path/to/aura-web/src/Response/Status.php`
`\Symfony\Core\Request` | `Symfony\Core` | `/vendor/Symfony/Core/` | `./vendor/Symfony/Core/Request.php`
`\Zend\Acl` | `Zend` | `/usr/includes/Zend/` | `/usr/includes/Zend/Acl.php`

关于本规范的实现，可参阅[相关实例](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md)。

注意：实例并不属于规范的一部分，且随时会有所变动。
