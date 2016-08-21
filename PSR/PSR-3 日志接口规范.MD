本文描述了日志类库的通用接口规范。

主要目标是让类库获得一个 `Psr\Log\LoggerInterface`对象并且通过简单和通用的方式来写日志。有自定义需求的框架和`CMS`系统，**可以**根据情况扩展这个接口，但是**应该**和本文档保持兼容。这能确保使用第三方类库文件时仍能写到集中的应用程序日志中。

关键词 “必须”("MUST")、“一定不可/一定不能”("MUST NOT")、“需要”("REQUIRED")、
 “将会”("SHALL")、“不会”("SHALL    NOT")、“应该”("SHOULD")、“不该”("SHOULD NOT")、
 “推荐”("RECOMMENDED")、“可以”("MAY")和”可选“("OPTIONAL")的详细描述可参见 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
 
单词`implementor(实现者)`在这个文档中被解释为：在日志相关的库或框架实现`LoggerInterface`接口的人。用这些实现者开发出来的类库的人都被称作`user(用户)`。

# 1. 规范

## 1.1 基础

- `LoggerInterface`接口对外定义了八个方法，分别用来记录[RFC 5424](https://tools.ietf.org/html/rfc5424)中定义的八个等级的日志：debug、 info、 notice、 warning、 error、 critical、 alert 以及 emergency 。
- 第九个方法`log`,其第一个参数为记录的等级。用一个日志等级常量来调用这个方法**必须**和直接调用指定等级方法的结果一致。如果传入的等级常量参数没有预先定义，则**必须**抛出`Psr\Log\InvalidArgumentException`类型的异常。在不确定的情况下，使用者**不应该**使用自定义的日志等级。

## 1.2 信息

- 每个方法都接受一个字符串类型或者是有`__toString()`方法的对象作为记录信息参数。实现者**可以**对传入的对象有特殊的处理。如果不是这样，实现者**必须**把它转换成字符串。
- `message`参数中**可能**包含一些可以被上下文数组所替换的占位符。

其中占位符**必须**与上下文数组中的键名保持一致。

占位符名字**必须**使用一对花括号来作为分隔符。在占位符和分隔符之间**一定不能**有任何空格。

占位符的名称**应该**只由`A-Z`、`a-z,0-9`、下划线`_`、以及英文的句号`.`组成，其它的字符作为以后占位符规范的保留字。

实现者**可以**通过对占位符采用不同的转义和转换策略，来生成最终的日志。而用户在不知道上下文的前提下，**不应该**提前转义占位符。

下面提供一个占位符替换的例子，仅作为参考：

```php
 /**
   * Interpolates context values into the message placeholders.
   */
  function interpolate($message, array $context = array())
  {
      // build a replacement array with braces around the context keys
      $replace = array();
      foreach ($context as $key => $val) {
          // check that the value can be casted to string
          if (!is_array($val) && (!is_object($val) || method_exists($val, '__toString'))) {
              $replace['{' . $key . '}'] = $val;
          }
      }

      // interpolate replacement values into the message and return
      return strtr($message, $replace);
  }

  // a message with brace-delimited placeholder names
  $message = "User {username} created";

  // a context array of placeholder names => replacement values
  $context = array('username' => 'bolivar');

  // echoes "User bolivar created"
  echo interpolate($message, $context);
  
```

## 1.3 上下文

- 每个记录函数都接受一个上下文数组参数，用来存储不适合在字符串中填充的信息。它**可以**装载任何信息，所以实现者**必须**确保能正确处理其装载的信息，对于其装载的数据，**一定不能**抛出异常，或产生PHP出错、警告或提醒信息（error、warning、notice）。
- 如果在上下文参数中传入了一个异常对象，它**必须**以`exception`作为键名。记录异常信息是一种常见的模式，并且可以在日志系统支持的情况下从异常中提取出整个调用栈。实现者在使用它时，**必须**确保键名为 '`exception`'的键值是否真的是一个`Exception`，毕竟它**可以**装载任何信息。

## 1.4 助手类和接口

- `Psr\Log\AbstractLogger`类让你通过继承它并实现通用的`log`方法来方便的实现`LoggerInterface`接口。而其他八个方法将会把消息和上下文转发给`log`方法。
- 同样地，使用`Psr\Log\LoggerTrait`也只需实现其中的`log`方法。不过，需要特别注意的是，在traits可复用代码块还不能实现接口前，还需要`implement LoggerInterface`。
- `Psr\Log\NullLogger`是和接口一起提供的。它在没有可用的日志记录器时，**可以**为使用日志接口的用户们提供一个后备的“黑洞”。然而，当上下文的构建非常消耗资源时，带条件检查的日志记录或许是更好的办法。
- `Psr\Log\LoggerAwareInterface`只有一个`setLogger(LoggerInterface $logger)`方法，它可以在框架中用来随意设置一个日志记录器。
- 

