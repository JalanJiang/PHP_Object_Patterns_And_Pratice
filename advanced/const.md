# 常量属性

满足要求：

- 需要在类的所有实例中都能访问某个属性
- 属性值无需改变

特性：

- 只包含基本数据类型的值
- 只能通过类而不能通过类的实例访问
- 一旦设置后不能改变

## 定义

```
class ShopProduct
{
    cosnt AVAILABLE = 0;
}
```

## 引用

```
print ShopExample::AVAILABLE;
```