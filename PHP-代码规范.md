***

### \# 通用约定：

- 代码缩进全部用tab，在编辑器里面设置tab存为制表符，不要存为空格。不要打一堆空格来做缩进。(艾芙要吐槽，我们应该用四个空格代替tab)。
- SVN / Git 中新建文件编码类型统一用utf-8编码（不带BOM）。
- Unix 风格的换行: LF
- 所有可以直接访问的url中包含的文件名都是小写，如果是多个词组成，则用下划线连接。
- 行宽：120 字符


### \# 代码规范
```php
<?php // 开头必须使用 <?php
// panxiaoliang@baixing.com 每个文件必须注明owner的邮箱

require_once('cg_conf/config.inc.php'); // require_once必须有括弧，并且左括弧前面没有空格

class CodingStandard { // 大括号前面加空格，类名开头字母大写，多个字母首字母大写
    private $attribute; // 属性注释直接注释在后方

    // 数组格式
    public $color = [
        '1' => 'red', // 用Tab缩进一次
        '2' => 'blue',
        '3' => 'yellow',
        '4' => [
            '1' => 'green',	// 在前面的数组对齐列之后再tab缩进一次
            '2' => 'gray', // 最后一个元素也添加逗号
        ], // 数组的结尾与声明的变量最前面对齐
    ]; // 数组的结尾与数组变量声明的地方对齐


    public $number = [1, 2, 3, 4]; // 对于简单数组，可以放一行

    // 方法的注释采用双斜线，尽量在一行内完成
    // 除非是文档性质的注释，例如 /** @var \MUser $user */
    function foo($i, $list) { // 1.function名后面的(前面没有空格 2.多个参数，如果有逗号，那么逗号后面要有空格
        for ($j = 0; $j < $i; $j++) { // for后面加空格
            echo "This is no.{$j}, content is {$list[$j]}"; // echo语句不加括号。

            // echo语句里面用单引号还是双引号，根据实际情况定
            echo '&lttable border="0" cellspacing="5" cellpadding="5"&gt'; 
        }
        if ($i > 0) { // 1.if后面加空格 2.操作符前后都要有空格
            return $i % 2; // 操作符前后是有空格的
        } else { // else前后也要有空格
            return null;
        }

        if ($j == $i) return 1; // if里面只有一句语句且较短的情况，建议写成一行，如果要拆成多行，则前后建议加上括号。

        $count = count($_SERVER); // 在外面写赋值
        if ($count > 10) echo 'pass'; // if里面只做布尔判断，不要写赋值语句
    }

    public static function testFunction() { // 静态非静态方法命名都遵守驼峰原则
    }
}

$s = new CodingStandard(); // new一个对象，后面必须加括弧
$s->foo(10, $s->color); // 函数后面的括弧不要有空格，函数里面超过一个参数，逗号后面就要有空格
CodingStandard::testFunction(); // 静态代码的调用方式唯一，仅限双冒号调用方式
```
php文件**不要**以 ?> 结尾。

### \# 文献

- [Zend Framework Coding Standard for PHP](http://framework.zend.com/manual/1.12/en/coding-standard.html)
- [WordPress Coding Standards](http://codex.wordpress.org/WordPress_Coding_Standards)
- [Drupal Coding Standards](http://drupal.org/coding-standards)
- [Pear Coding Standards](http://pear.php.net/manual/en/standards.php)