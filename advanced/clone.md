# 复制对象

- PHP 中，对象的赋值和传递都是通过引用进行的

```php
class CopyMe {}
$first = new CopyMe();
$second = $first;
// PHP5 后：$second 和 $first 指向同一个对象
// 这两个变量包含指向同一个对象的引用
```

## clone 关键字

`clone` 使用 "值复制" 方式（by-value copy）新生成一个对象。

```php
class CopyMe {}
$first = new CopyMe();
$second = clone $first;
// $second 和 $first 是两个不同的对象
```

注：

- 在复制对象属性时只复制引用

若不希望对象属性在复制后被共享，可以显示地在 `__clone()` 方法中复制指向的对象：

```
function __clone()
{
    $this->id = 0;
    $this->account = clone $this->account; //不希望账户被共享，进行复制
}
```

## __clone() 控制复制什么

- 当在一个对象上调用 `clone` 关键字时，`__clone()` 方法就会被自动调用

```php
<?php
class Person {
    private $name;    
    private $age;    
    private $id;    

    function __construct( $name, $age ) {
        $this->name = $name;
        $this->age = $age;
    }

    function setId( $id ) {
        $this->id = $id;
    }
    
    function __clone() {
        // 重新赋值
        $this->id = 0; // id 属性被重设为 0 
    }
}

$person = new Person( "bob", 44 );
$person->setId( 343 );
// 产生了一个新副本
$person2 = clone $person;
print_r( $person );
print_r( $person2 );

?>
```