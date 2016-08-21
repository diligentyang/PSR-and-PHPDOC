本文描述了日志类库的通用接口规范。

主要目标是让类库获得一个 `Psr\Log\LoggerInterface`对象并且通过简单和通用的方式来写日志。有自定义需求的框架和`CMS`系统，**可以**根据情况扩展这个接口，但是**应该**和本文档保持兼容。这能确保使用第三方类库文件时仍能写到集中的应用程序日志中。

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 
单词`implementor(实现者)`在这个文档中被解释为：在日志相关的库或框架实现`LoggerInterface`接口的人。用这些实现者开发出来的类库的人都被称作`user(用户)`。