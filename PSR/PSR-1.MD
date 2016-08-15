这一部分标准包括，哪些应该被认为是标准的编码元素，以确保共享的PHP代码间具有较高程度的技术互通性。

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 

# 1.概览

- PHP文件**必须**只使用 `<?php` 和 `<?` 这两种标签。
- PHP文件**必须**以不带BOM的UTF-8编码。
- PHP文件中**应该**只定义类、函数、常量等声明，或其他会产生从属效应 的操作（如：生成文件输出以及修改.ini配置文件等），但是**不应该**同时做着两件事情。
- 命名空间以及类必须符合 PSR 的自动加载规范：[PSR-0](http://www.php-fig.org/psr/psr-0/) 或 [PSR-4](http://www.php-fig.org/psr/psr-4/) 中的一个；
- 类的命名**必须**遵循以大写开头的驼峰命名规则（`StudlyCaps`）。
- 类中的常量所有字母都**必须**大写，单词间用下划线分隔。
- 方法名必须符合以小写开头的驼峰命名法（`camelCase`）。

 