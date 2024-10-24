---
title: PHP grammar
categories: [Memo]
tags: [PHP,Note]
---

弱类型语言，自动识别合适的类型。

<!--more-->

- 变量：
```php
<?php
$a = "123";
$x = 5;
$y = false;
?>
```

- 输出
	- echo - 可以输出一个或多个字符串
	- print - 只允许输出一个字符串，返回值总为 1
	- 注：echo 输出的速度比 print 快， echo 没有返回值，print有返回值1。

- EOF（heredoc）
```php
<?php
$name = "run"
$a= <<<EOF
		"abc"$name
		"123"
EOF;
?>
```
	- PHP 定界符 EOF 的作用就是按照原样，包括换行格式什么的，输出在其内部的东西；
	- 可以解析变量名，双引号内的转义字符，html格式，不能解析函数。

- 类型比较
```php
== //值相等
=== //值和类型都相同

```

- 字符串
	- strlen() - 字符串长度
	- strpos("指定文本","指定查找内容") - 返回文本中第一个指定内容的位置
	- 字符串链接，并置运算符
```php
<?php
$a = "hello";
$b = $a . "world";
echo $b; //pring "hello world"
?>
```

- 条件判断
	- if
	- if...else...
	- if...elseif...else
	- switch

- 数组
```php
<?php
$cars=array("Volvo","BMW","Toyota");//数值数组

count($cars); //get lenght of array


$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");//关联数组
echo "Peter is " . $age['Peter'] . " years old.";


?>


//关联数组遍历
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
 
foreach($age as $x=>$x_value)
{
    echo "Key=" . $x . ", Value=" . $x_value;
    echo "<br>";
}
?>
```

- 排序
```php
//数值数组排序
sort(array);//升
rsort(array);//降

//关联数组排序
asort(array);//按值升序
ksort(array);//按key升序

```

- 超全局变量
	- $\_REQUEST - 收集html表单提交的数据
	- $\_POST
	- $\_GET - 使用get时，变量会显示在url中

- 魔术常量
	- \_LINE\_ - 当前行号
	- \_FILE\_ - 文件路径+文件名
	- \_DIR\_ - 文件目录
	- \_FUNCTION\_ - 函数名
	- \_CLASS\_ - 类名
	- \_TRAIT\_ - ？
	- \_METHOD\_ - 类的方法名
	- \_NAMESPACE\_ - 当前命名空间

- 面向对象
```php
//构造函数
fuction __construct($par1,$par2){
	$this->url = $par1;
	$this->title = $par2;
}

//析构函数
fuction __destruct(){
	...
}
```




