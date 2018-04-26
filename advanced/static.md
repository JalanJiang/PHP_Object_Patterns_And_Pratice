# 静态方法和属性

可以通过类来访问的方法和属性都是静态（`static`）的。

## 静态方法

- 以类作为作用域的函数
- 不能访问类中的普通属性，因为普通属性属于对象
- 可以访问类中的静态属性

## 访问

### 外部访问

使用 `ClassName::staticSomething`：

```php
class StaticExample 
{
    static public $aNum = 0;
    static public function sayHello() 
    {
        print "hello";
    }
}

print StaticExample::$aNum;
StaticExample::staticExample;
```

### 内部访问

使用 `self::staticSomething`：

**`self`指向当前类，就像伪变量 `$this` 指向当前对象一样。**

```php
class StaticExample 
{
    static public $aNum = 0;
    static public function sayHello() 
    {
        self::$aNum++;
        print "hello";
    }
}
```

## 为什么使用静态访问和属性？

- 静态属性在代码的任何地方都可用
    - 无需在对象之间传递实例
    - 无需将实例存放在局部变量中
- 类中的每个实例都可以访问类中定义的静态属性
    - 可以利用静态属性设置值（这个值可以被类中的所有对象使用）
- 无需因为一个简单功能而实例化对象

**如果一个方法没有使用任何实例的属性或方法，就没有理由不把它定义为 `static`。**
       

