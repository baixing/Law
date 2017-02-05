***

## \# 编码原则
- 简明易懂；代码是给人看的，不仅仅只是给机器执行的
- 编码规范，命名风格统一
- 适当明确的代码注释

## \# 适用原则
- 所有新代码、新类、新需求开发采用本套编码规范
- 对于老代码、老类上的小范围修改延续该类的原有风格以保持局部的代码格式一致性，后续重构逐步演进

## \# 规范用语说明
- 可以：表示允许操作
- 最好：最优的处理方式，非强制要求
- 一般：正常情况下按照规范执行，除非有特殊情况
- 必须：强制要求
- 没有以上用语的内容为要求按规范执行

## \# 编码规范概要：

### 特别注意点
- 缩进用tab，不用空格 (与PSR-2规范不同)
- 类声明、函数声明、方法声明的{不换行（与PSR-2规范不同）
- 每个类文件要有owner邮箱和类功能说明
- 类变量、属性、方法命名采用驼峰命名，如camelNaming()
- 全局函数采用小写加下划线的命名，如array_map()
- 类名采用首字母大写不加下划线，如VipController
- 每个类单独一个文件
- 代码行行宽：120 字符，最好不超过80字符
- 命名长度：不超过40个字符，最好不超过25个字符
- 方法内代码块长度不超过2屏幕（80行），最好不超过1屏幕（40行）；超过了要求拆分方法
- 方法内代码块嵌套层级不超过4级，最好不超过3级；超过了要求重构逻辑或抽象方法

## \# 工具配置
- [PhpStorm配置指南](https://github.com/baixing/haojing/wiki/PhpStorm-配置指南)

## \# 代码检查
- 提交代码和Code Review时按代码规范进行代码检查
- PhpStorm可以通过编辑区右侧滚动条的标识来确定代码干净程度
 - 黄色为有代码warning，如命名空间未使用、变量使用时未定义、变量定义未使用等
 - 红色为代码有错误，如没有写结尾的;或{}未匹配成对等
 - 编辑区右侧滚动条最顶部显示绿色的勾，标识代码已整理干净

### 代码示例
```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

/**
 * 这个类是用于做代码示例的
 */
abstract class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    const CONST_NAME = 'nothing';

    protected static $foo;

    abstract protected function zim();

    final public static function bar() {
        // method body
    }

    /**
     * 这个是用来做注释描述的函数
     * 下面几行的参数类型描述对齐为建议非强制，phpstorm自动格式化支持这里的对齐，对齐更加直观
     * 
     * @param int   $arg1 参数1
     * @param bool  $arg2 参数2
     * @param array $arg3 参数3
     */
    public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
        // method body
    }
}
```

## \# 编码规范细节：

### PHP文件
- 文件编码类型统一用utf-8编码（不带BOM）
- 文件末尾留一个空行
- 仅含PHP代码的文件最后的?>标签忽略
- 文件名
 - 类文件：类名.php
 - 配置文件：全小写字母多单词用_分隔.php

### 代码行
- 行宽：120 字符，最好不超过80字符
- Unix 风格的换行: LF
- 代码行结尾不带空格
- 适当添加空行来区分代码块增加代码可读性
- 每行不超过一条语句

### 缩进
- 代码缩进全部用tab（与PSR-2不一致，特别注意）

### 关键词
- PHP关键词采用全小写

### 命名原则
- 新的概念命名需要在项目内部达成共识，与现有概念命名风格保持一致；现有概念参见[百姓概念命名与缩写规范](https://github.com/baixing/haojing/wiki/百姓概念命名与缩写规范（草案）)
- 变量命名、方法命名统一采用驼峰格式，如camelFormat
- 全局函数命名采用全小写字母加_格式，如array_map；全局函数只作为PHP函数库的补充，涉及业务的全局函数要求放到相关的类中
- 类名采用单词首字母大写格式，如OrderController；带类功能后缀，如-Controller, -Exception, -Operator, -Factory, -Storage, -Cache等
- 命名中的单词一般不建议缩写和拼音，除非常用单词太长或多个单词组成的命名超长时可以缩写，详见参见[百姓概念命名与缩写规范](https://github.com/baixing/haojing/wiki/百姓概念命名与缩写规范（草案）)
- 命名长度：不超过40个字符，最好不超过25个字符

### 代码注释
- 注释规范遵循[PHP Doc规范](https://www.phpdoc.org/docs/latest/references/phpdoc/index.html)
- 所有类必须有owner邮箱注释；所有核心类注释必须有类描述和owner邮箱；这里的核心类是指可能会被多处调用到的类及底层的类
- 所有核心关键方法、函数注释必须包含描述、参数说明、返回值说明，必须时可以有具体函数逻辑；这里的核心关键方法、函数是指可能会被多次调用的方法或核心类中的方法
- 代码不明确的地方建议增加注释，存在复杂功能逻辑要求有明确的描述性注释
- 注释可以用中文

### 完整类名与自动加载（PSR-4）

这里的类指所有类、接口、trait和其他相似的结构

\\\<NamespaceName>(\\\<SubNamespaceNames>)*\\\<ClassName>
- 完整类名称要求顶级命名空间为供应商命名空间（Haojing NG已按这个规范，非NG代码不做此项限定）
- 完整类名称可以有一个或多个子命名空间
- 完整类名称末尾必须有一个类名
- _作为完整类名称的分隔符 
- 所有类目是字母大小写敏感的
- 自动加载文件时，完整类名称的前面命名空间对应文件夹名称，最后的类名加.php对应文件名
- 自动加载实现不能抛出异常，不能抛出任何级别的错误，不能返回值

### 命名空间的使用
- 当存在时，use命名空间必须在namespace定义之后空一行空行
- 当存在时，所有use命名空间必须在namespace定义之后
- 每行声明必须使用一个use关键词
- use代码块之后必须有一行空行

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

### 类、属性、方法

这里的类指所有类、接口、trait
- 首行为<?php，后面不跟空格
- 第二行写文件创建人邮箱，如// owner@baixing.com，后面空一行
- extends和implements关键字必须与类名字在一行
- {放在类名声明末尾同一行，}必须在代码块后面一行

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    // constants, properties, methods
}
```

- implements列表可以分拆成多行，每个一行；这么做时，第一项必须在下一行，并且之后每行只能有一个接口

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable {
    // constants, properties, methods
}
```

### 常量
- 类常量必须使用全部大写，单词间使用_分隔
```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

class ClassName {
    const CONST_NAME = 'nothing';
}
```

### 属性

- 所有属性必须有可见性声明
- var关键字不能用于声明属性
- 每个语句不能定义多余一个属性
- 属性名称不能使用前导_来指示protected或private的可见性
- 对象类型的属性，需要用如/* @var ClassName $param */的注释指示变量对象类型；这个注释可以写成三行的格式

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

class ClassName {
    /* @var ClassName $foo */
    public $foo = null;
}
```

### 方法

- 可见性必须被声明在所有方法上
- 方法名称不能使用前导_来指示protected或private的可见性
- 方法名之后不能有空格。{在)同一行，}必须在代码块后面一行。(后不能有空格，)前不能有空格
- 方法内代码块长度不超过2屏幕（80行），最好不超过1屏幕（40行）；超过了要求拆分方法
- 方法内代码块嵌套层级不超过4级，最好不超过3级；超过了要求重构逻辑或抽象方法

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

class ClassName {
    public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
        // method body
    }
}
```

### 方法参数

- 在参数列表中，每个逗号前不能有空格，逗号后必须有一个空格
- 带默认值的参数必须在参数列表的最后
- 参数列表可以被分成多行，每个子序列带一个缩进；当这么做时，列表的第一项必须在下一行，并且之后每行一个参数
- 当参数列表被分成多行时，)必须放置在{的一行，且中间有一个空格
- 参数如果是特定类型的对象的，该参数前显示声明对象类型
- 方法参数建议不超过5个参数，一般不超过8个参数；如超过了，要求重构函数或以数据、对象作为参数传递

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

class ClassName {
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

abstract, final和static
- 当存在时，abstract和final声明必须在可见性声明之前
- 当存在时，static声明必须在可见性声明之后

```php
<?php
// nanzhimin@baixing.com

namespace Vendor\Package;

abstract class ClassName {
    protected static $foo;

    abstract protected function zim();

    final public static function bar() {
        // method body
    }
}
```

### 方法与函数调用

- 方法与函数调用时，方法或函数名与(之间不能有空格，(之后不能有空格，)之前不能有空格。在参数列表中，每个逗号前不能有空格，逗号后必须有一个空格

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

- 参数列表可以被分成多行，每个子序列带一个缩进；当这么做时，列表的第一项必须在下一行，并且之后每行一个参数

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```
```php
<?php
// 参数换行原则：要么所有参数都在一行，参数要换行就每个参数单独放一行（包括第一个参数也需要单独一行）
// 可行的写法示例如下：

// 写法一：推荐这种，比较清晰
$query =  new AndQuery(
    new Query('type', \Verify\GuaranteedContract::TYPE),
    new Query('user', $user),
    new Query('status', EnumVerifyRequest::ACCEPT)
);
$vr = findOne('VerifyRequest', $query, ['size' => 20]);

// 写法二：喜欢行数少的同学可能会偏好这种
$vr = findOne('VerifyRequest', new AndQuery(
        new Query('type', \Verify\GuaranteedContract::TYPE),
        new Query('user', $user),
        new Query('status', EnumVerifyRequest::ACCEPT)
), ['size' => 20]);

// 写法三：这种也可以，但显得行数比较多，不太推荐
$vr = findOne(
        'VerifyRequest', 
        new AndQuery(
            new Query('type', \Verify\GuaranteedContract::TYPE),
            new Query('user', $user),
            new Query('status', EnumVerifyRequest::ACCEPT)
        ), 
        ['size' => 20]
);
```
- 函数或方法调用的)后不直接跟取键值操作
```php
<?php
/* 这种写法不推荐，原因为：
 * 1. 潜在报notice的可能；这个代码在确保函数返回数组且包含token键值时没问题，
 *    但哪天有同学觉得需要对$uid做个有效性检查，非法$uid直接返回false或null，
 *    于是就会出notice，这个是一种潜在的问题，因为我们没法保证代码不会被别人改
 * 2. 代码写起来没有那么清晰，特别是当函数调用或参数很长时
 */
$token = $this->getAccessTokenAndTtl($uid)['token'];

// 推荐以下替代两种写法，中间变量使得函数返回值结果的含义也会更清晰

// 写法一：增加临时变量，适合一次性调用的场景
$tokenTtl = $this->getAccessTokenAndTtl($uid);
$token = array_get($tokenTtl, 'token');

// 写法二：增加接口，适合多次调用的场景
public function getAccessToken($uid) {
    $tokenTtl = $this->getAccessTokenAndTtl($uid);
    return array_get($tokenTtl, 'token');
}
// 调用时访问新接口
$token = $this->getAccessToken($uid);
```
### 控制结构的代码基本规范

- 控制关键字后必须有一个空格
- (后不能有空格，)前不能有空格
- )和{之间必须有一个空格
- 结构体必须有一个缩进
- }必须在代码块下面一行
- 条件语句里不包含赋值语句

### if, elseif, else

- elseif代替else if，使得看起来是一个关键字
- 其他格式如下

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

### swith, case
```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

### while, do while
```
<?php
while ($expr) {
    // structure body
}

do {
    // structure body;
} while ($expr);
```

### for
```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### foreach
```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### try, catch
```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

### 闭包
- 闭包的声明中在function关键词后必须有一个空格，在use关键词前后都必须有一个空格
- {必须与声明在一行，}必须在代码块的下一行
- 其他空格逗号规则与函数定义相同
- 闭包的各种写法参考如下例子

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
    // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
    // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};
```
```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```
```php
<?php
$value = implode(
    ',',
    array_map(
        function ($v) {
            return $v instanceof Node ? $v->id : $v;
        },
        $uid
    )
);
$value = implode(',', array_map(function ($v) {
    return $v instanceof Node ? $v->id : $v;
},$uid));
```

## \# 修订说明
- 考虑到目前代码风格不一，结合PSRs规范、原来的百姓网编码规范以及现有代码习惯综合考虑，形成了本套编码规范
- 本套编码规范与PSRs规范主要区别
 - 缩进采用tab，不用空格
 - 类声明、函数声明、方法声明的{不换行

### \# 文献

- [PHP Standards Recommendations](http://www.php-fig.org/psr/)
- [PHP 代码规范](https://github.com/baixing/Law/wiki/PHP-代码规范)
- [百姓网php编码规范2010-09-16](http://iweb.baixing.com/wiki/index.php/PHP编码规范)

## \# 相关规范
- [MySQL开发规范](https://github.com/baixing/haojing/wiki/MySQL开发规范)
- [Mysql规范化建表](https://github.com/baixing/haojing/wiki/Mysql规范化建表)
