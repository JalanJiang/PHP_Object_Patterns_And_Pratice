# 拦截器

- 可以"拦截"发送到未定义方法/属性的消息
- 也被称为**重载（overloading）**，但与 java/C++ 中的重载截然不同

## 拦截器方法

| 方法 | 描述 |
| ---- | ---- |
| __get($property) | 访问未定义的属性时被调用 |
| __set($property, $value) | 给未定义的属性赋值时被调用 |
| __isset($property) | 对未定义的属性调用 isset() 时被调用 |
| __unset($property) | 对未定义的属性调用 unset() 时被调用 |
| __call($method, $arg_array) | 调用未定义的方法时被调用 |

## __get()

```
<?php
class Person
{
    function __get($property)
    {
        $method = "get{$property}";
        if (method_exists($this, $method)) {
            return $this->$method();
        }
    }

    function getName()
    {
        return "Jalan";
    }
}

$p = new Person();
echo $p->name;
```

## __isset()

- 在未定义属性上调用 `isset()` 时

```
function __isset($property)
{
    $method = "get{$property}";
    return (method_exists($this, $method));
}
```

## __set()

- 给未定义属性赋值时被调用
- 接受两个参数
    - 属性名
    - 要设定的值

```
<?php
class Person
{
    private $_name;

    function __set($property, $value)
    {
        $method = "set{$property}";
        if (method_exists($this, $method)) {
            return $this->$method($value);
        }
    }

    function setName($name)
    {
        $this->_name = $name;
        return $this->_name;
    }
}

$p = new Person();
echo $p->name = "jalan is a good guy";
```

## __unset()

- 当 `unset()` 在一个未定义属性上被调用时

```
function __unset($property)
{
    $method = "set{property}";
    if (method_exists($this, $method)) {
        $this->$method(null); //将属性设置为null
    }
}
```

## __call()

- 当调用类中未定义的方法时
- 接受两个参数
    - 方法的名称
    - 传递给要调用方法的所有参数（数组）
- 返回的任何值都会返回给用户

### 委托

- 一个对象 **转发** 或 **委托** 一个请求给另一个对象
- 被委托一方替原对象处理请求
- 与继承类似，但比继承更具灵活性：委托可以在代码运行时改变使用的对象

```
class PersonWriter
{
    function writeName(Person2 $p)
    {
        print $p->getName();
    }
}

class Person2
{
    private $writer;

    function __construct(PersonWriter $writer)
    {
        $this->writer = $writer;
    }

    function __call($methodName, $args)
    {
        if (method_exists($this->writer, $methodName)) {
            return $this->writer->$methodName($this); //委托 PersonWriter 对象来处理对方法的调用
        }
    }

    function getName()
    {
        return "Jalan";
    }
}

$p2 = new Person2(new PersonWriter());
$p2->writeName();
```