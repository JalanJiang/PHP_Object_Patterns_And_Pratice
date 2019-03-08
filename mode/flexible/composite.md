## 组合模式

- 将 一组对象 组合为可以像 单个对象 一样被使用的结构
- 原则：组合类（包含局部类）和局部类具有同样的接口

## 实现

### 局部类

```php
// 战斗单元
abstract class Unit {
    abstract function bombardStrength();
}

// 射手
class Archer extends Unit {
    function bombardStrength() {
        return 4;
    }
}

// 激光炮
class LaserCannonUnit extends Unit {
    function bombardStrength() {
        return 44;
    }
}
```

### 组合类

```php
// 军队
class Army {
    private $units = array();

    function addUnit( Unit $unit ) {
        array_push( $this->units, $unit );
    }

    function bombardStrength() {
        $ret = 0;
        foreach( $this->units as $unit ) {
            $ret += $unit->bombardStrength();
        }
        return $ret;
    }
}
```

### 创建对象

```php
$unit1 = new Archer(); 
$unit2 = new LaserCannonUnit(); 
$army = new Army();
$army->addUnit( $unit1 ); 
$army->addUnit( $unit2 ); 
print $army->bombardStrength();
```

## 优点

- 灵活：一切类都共享了一个父类型
- 简单：只需要设计简单的接口，无需区分一个对象是组合对象还是局部对象

## 缺陷

- 随着引入复杂的规则，代码会变得越来越难以维护
- 不能很好地在关系数据库中保存数据