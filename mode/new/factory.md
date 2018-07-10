# 工厂方法模式

- 在代码关注于抽象类型时如何创建对象实例时，用特定的类来处理实例化
- 是一种代替 `new` 操作的一种模式

## 实现

- 把创建者类与要生产的产品类分离开
    - 避免直接使用 `switch` 来区分要实例化的对象，减少"代码坏味道"
- 建立用于生产"产品"的"工厂"
- 每一种"产品"都有与之对应、用于生产它的"工厂"

```php
<?php
    //解码器（产品）
    abstract class ApptEncoder
    {
        abstract function encode();
    }
    
    //解码器的某一类型
    abstract class BloggsApptEncoder
    {
        function encode()
        {
            return "Appointment data encode in BloggsCal format\n";
        }
    }
    
    //生产者（用于产生解码器）
    abstract class CommsManager
    {
        //三个抽象方法
        abstract function getHeaderText();
        abstract function getApptEncoder();
        abstract function getFooterText();
    }
    
    //生产者的某一类型
    class BloggsCommsManager extends CommsManager
    {
        function getHeaderText()
        {
            return "Bloggs header\n";
        }
        
        function getApptEncoder()
        {
            //生产Bloggs类型的产品
            return new BloggsApptEncoder();
        }
        
        function getFooterText()
        {
            return "Bloggs footer\n";
        }
    }
?>
```

## 例子

## 人类工厂

```php
<?php
    interface abstracted{
        public function realCreate();
    }
    //女人类
    class Woman{
        public function action(){
            echo '这是女人';
        }
    }
    //男人类
    class Man{
        public function action(){
            echo '这是男人';
        }
    }
    //创建女人
    class WomanCreator implements abstracted {
        public $chromosome;//染色体
        public function realCreate(){
            if ($this->chromosome == "xx") {
                return new Woman();
            }
        }
    }
    //创建男人
    class ManCreator implements abstracted {
        public $chromosome;
        public function realCreate(){
            if ($this->chromosome == "xy" || $this->chromosome == "xyy") {
                return new Man();
            }
        }
    }
    //人类工厂
    class PersonFactory{
        public function create($what){
            $create = $what."Creator";
            return $create = new $create();
        }
    }
    $create = new PersonFactory();
    $instance = $create->create('Woman');
    $instance->chromosome = "xx";
    $instance->realCreate()->action();
?>
```