# 复杂的属性值

Spring 的 bean 工厂不仅允许用 String 值和其他 bean 的引用作为 bean 组件的属性值，还支持更复杂的值，例如数组、java.util.List、java.util.Map和java.util.Properties。数组、set、list和map中的值不仅可以是 String 类型，也可以是其他 bean 的引用；map 中的键、Properties 的键和值都必须是 String 类型的；map 中的值可以是 set、list 或者 map 类型 。

例如：

Null:

```
<property name=“bar”><null/></property>
```

List和数组：

```
<property name=“bar”>

  <list>

    <value>ABC</value>

    <value>123</value>

  </list>

</property>

Map:

<property name=“bar”>

  <map>

    <entry key=“key1”><value>ABC</value></entry>

    <entry key=“key2”><value>123</value></entry>

  </set>

</property>
```
