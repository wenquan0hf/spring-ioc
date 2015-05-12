Spring的bean工厂不仅允许用String值和其他bean的引用作为bean组件的属性值，还支持更复杂的值，例如数组、java.util.List、java.util.Map和java.util.Properties。数组、set、list和map中的值不仅可以是String类型，也可以是其他bean的引用；map中的键、Properties的键和值都必须是String类型的；map中的值可以是set、list或者map类型 。

例如：

Null:

<property name=“bar”><null/></property>

List和数组：

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