# 抽象工厂模式

## 与工厂方法模式的区别

- 工厂方法模式中
    - 具体工厂负责生产具体的产品
    - 一个具体工厂中只有一个工厂方法或者一组重载工厂方法
- 抽象工厂模式
    - 一个工厂可以提供多个产品对象，而不是单一的产品对象

## 实现

```
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

## 参考资料

- [抽象工厂模式(Abstract Factory)](https://design-patterns.readthedocs.io/zh_CN/latest/creational_patterns/abstract_factory.html)