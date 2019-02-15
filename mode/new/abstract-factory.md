# 抽象工厂模式

## 与工厂方法模式的区别

- 工厂方法模式中
    - 具体工厂负责生产具体的产品
    - 一个具体工厂中只有一个工厂方法或者一组重载工厂方法
- 抽象工厂模式
    - 一个工厂可以提供多个产品对象，而不是单一的产品对象

## 实现

```php
<?php
// 抽象工厂
abstract class CommsManager
{
    const APPT    = 1;
    const TTD     = 2;
    const CONTACT = 3;

    abstract function getHeaderText();
    abstract function make($flag_int);
    abstract function getFooterText();
}

// 具体的工厂
class BloggsCommsManager extends CommsManager
{
    function getHeaderText()
    {
        return "BloggsCal header\n";
    }

    function make($flag_int)
    {
        switch ($flag_int) {
            case self::APPT:
                return new BloggsApptEncoder();
            case self:TTD:
                return new BloggsContactEncoder();
            case self:TTD:
                return new BloggsTtdEncoder();
        }
    }

    function getFotterText()
    {
        return "BloggsCal fotter\n";
    }
}
?>
```

## 原型模式

### 概念

- 用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象

### 实现

- 创建一个保存具体产品的工厂

```php
<?php

class Sea {}
class EarthSea extends Sea {}
class MarsSea extends Sea {}

class Plains {}
class EarthPlains extends Plains {}
class MarsPlains extends Plains {}

class Forest {}
class EarthForest extends Forest {}
class MarsForest extends Forest {}

class TerrainFactory {
    private $sea;
    private $forest;
    private $plains;

    // 将原型对象传给要发动创建的对象
    function __construct( Sea $sea, Plains $plains, Forest $forest ) {
        $this->sea = $sea;
        $this->plains = $plains;
        $this->forest = $forest;
    }

    // 请求原型对象拷贝它们自己来完成创建
    function getSea( ) {
        return clone $this->sea; // 返回在初始化时缓存的 Sea 对象的一个副本
    }

    function getPlains( ) {
        return clone $this->plains;
    }

    function getForest( ) {
        return clone $this->forest;
    }
}

$factory = new TerrainFactory( new EarthSea(),
    new EarthPlains(),
    new EarthForest() );
print_r( $factory->getSea() );
print_r( $factory->getPlains() );
print_r( $factory->getForest() );
?>

```

##### clone

关于 `clone` 见：[使用 __clone() 复制对象](/advanced/clone.md)。

## 参考资料

- [PHP设计模式之原型模式](https://segmentfault.com/a/1190000007531872)
- [抽象工厂模式(Abstract Factory)](https://design-patterns.readthedocs.io/zh_CN/latest/creational_patterns/abstract_factory.html)