# 单例模式

是一种对于全局变量的改进。

- 意图：保证一个类仅有一个实例，并提供一个访问它的全局访问点。
- 主要解决：一个全局使用的类频繁地创建与销毁。
- 何时使用：当您想控制实例数目，节省系统资源的时候。
- 如何解决：判断系统是否已经有这个单例，如果有则返回，如果没有则创建。

## 全局变量的问题

- 将类捆绑于特定环境，**破坏了封装**
- 不受保护
- 容易引起冲突

## 解决方法

**通过方法调用来传递对象实例**，需要保证：

- 传递对象可以被系统中的任何对象使用
- 传递对象不应该被存储在会被覆写的全局变量中
- 整个系统中不应超过一个传递对象

## 实现

### 防止从外部创建实例

```php
class Preferences 
{
    private $props = array();
    
    // 将构造方法定义为私有
    private function __construct() {}
    
    ......
}
```

### 对象的间接实例化

借用静态方法和静态属性来间接实例化对象。

```php
class Preferences 
{
    private $props = array();
    
    // 设置为静态、私有，不能在外部访问
    private static $instance;
    
    // 将构造方法定义为私有
    private function __construct() {}
    
    // public属性，可以在任何地方被调用
    public static function getInstance()
    {
        if (empty(self::$instance)) {
            self::$instance = new Preferences();
        }
        return self::$instance;
    }
    
    public function setProperty($key, $val)
    {
        $this->props[$key] = $val;
    }
    
    public function getProperty($key) 
    {
        return $this->props[$key];
    }
    
}
```

## 调用

```php
$pref = Preferences::getInstance();
$pref->setProperty("name", "matt");

unset($pref); //移除引用

$pref2 = Preferences::getInstance();
print $pref2->getProperty("name") . "\n"; //属性未丢失
```

## 参考资料

- [单例模式](http://www.runoob.com/design-pattern/singleton-pattern.html)