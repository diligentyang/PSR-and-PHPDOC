关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)

# 1. 概述

本PSR是关于由文件路径自动载入对应类的相关规范，本规范是可互操作的，可以作为任一自动载入规范的补充，其中包括[PSR-0](http://www.php-fig.org/psr/psr-0/)，此外，本 PSR 还包括自动载入的类对应的文件存放路径规范。

# 2. 详细说明

1. 此处的类泛指class类、接口、traits可复用代码块以及其它类似结构。
2. 一个完全限定的类名称有以下形式:

```php
\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>

```

 + 完全限定类名**必须**要有一个顶级命名空间，被称为 "vendor namespace"。
 + 完全限定类名**可以**有一个或多个子命名空间。
 + 完全限定类名**必须**有一个终止的类名。
 + 在完全限定类名的任何部分中，下划线都没有特殊的意义。 
 + 所有的类名**必须**以大小写敏感的方式引用。
 
3. 