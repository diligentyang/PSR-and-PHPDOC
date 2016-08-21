本文描述了日志类库的通用接口规范。

主要目标是让类库获得一个 `Psr\Log\LoggerInterface`对象并且通过简单和通用的方式来写日志。有自定义需求的框架和`CMS`系统，**可以**根据情况扩展这个接口，但是**应该**和本文档保持兼容。这能确保使用第三方类库文件时仍能写到集中的应用程序日志中。

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 
单词`implementor(实现者)`在这个文档中被解释为：在日志相关的库或框架实现`LoggerInterface`接口的人。用这些实现者开发出来的类库的人都被称作`user(用户)`。

# 1. 规范

## 1.1 基础

`LoggerInterface`接口对外定义了八个方法，分别用来记录[RFC 5424](https://tools.ietf.org/html/rfc5424)中定义的八个等级的日志：debug、 info、 notice、 warning、 error、 critical、 alert 以及 emergency 。

第九个方法`log`,其第一个参数为记录的等级。用一个日志等级常量来调用这个方法**必须**和直接调用指定等级方法的结果一致。如果传入的等级常量参数没有预先定义，则**必须**抛出`Psr\Log\InvalidArgumentException`类型的异常。在不确定的情况下，使用者**不应该**使用自定义的日志等级。

