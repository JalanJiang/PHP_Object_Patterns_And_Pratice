# 使用继承

使用 `extends` 关键字。

## 构造方法和继承

- 派生类没有定义构造方法，实例化时会自动调用父类的构造方法
- 在子类中定义构造方法时，需要传递参数给父类的构造方法，否则你得到的可能是一个构造不完整的对象
- 子类默认继承父类的 `public` 和 `protected` 方法，没有继承 `private` 方法或属性

调用父类的构造方法使用 `parent` 关键字。

```
parent::__construct()
```

要引用一个类而不是对象的方法，可以使用 `::` 而不是 `->`。

```
public function __construct($title, $playLength)
{
    // 调用父类构造方法
    parent::__construct($title);
    // 在自己的构造方法中单独处理某些变量
    $this->playLenght = $playLength;
}
```

## 调用被覆写的方法

