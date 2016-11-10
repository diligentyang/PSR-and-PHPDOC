 针对PSR-0标准主要提到了以下几点：

# 要求

- 一个完全合格的命名空间和类名必须有以下的结构“`\<提供者名称>\(<命名空间>\)*<类名>`”
- 每个命名空间必须有顶级的命名空间（“提供者”）
- 每个命名空间可以有任意多个子命名空间
- 每个命名空间在被从文件系统加载时必须被转换为“操作系统路径分隔符”（DIRECTORY_SEPARATOR ）
- 每个“`_`”字符在“类名”中被转换为DIRECTORY_SEPARATOR 。“`_`”符号在命名空间中没有这个含义
- 符合命名标准的命名空间和类名必须以“.php”结尾来加载文件
- 提供商名称，命名空间，类名可以由大小写字母组成，其中命名空间和类名是大小写敏感的以保证多系统兼容性
- 如果文件不存在需要返回false

# 例子

```
\Doctrine\Common\IsolatedClassLoader => /path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php

\Symfony\Core\Request => /path/to/project/lib/vendor/Symfony/Core/Request.php

\Zend\Acl => /path/to/project/lib/vendor/Zend/Acl.php

\Zend\Mail\Message => /path/to/project/lib/vendor/Zend/Mail/Message.php
```

# 下划线在命名空间和类名中的使用

```
\namespace\package\Class_Name => /path/to/project/lib/vendor/namespace/package/Class/Name.php

\namespace\package_name\Class_Name => /path/to/project/lib/vendor/namespace/package_name/Class/Name.php
```

设置这个标准是为了保证最基本的共同点。你可以通过实现5.3的SplClassLoader来测试这个标准。

# 扩展例子

提供一个函数来展示如何使用上述标准。

```
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');

```

# SplClassloader的实现

接下来这个gist实现了SplClassLoader可以加载你按照上面标准来实现的通用类库，这是5.3里面推荐的加载方式。
http://gist.github.com/221634




