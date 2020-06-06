# Collections集合工具类的方法
* `java.utils.Collections`是集合工具类，用来对集合进行操作。部分方法如下：
:::alert-warning
- `public static <T> boolean addAll(Collection<T> c, T... elements)  `:往集合中添加一些元素。
- `public static void shuffle(List<?> list) 打乱顺序`:打乱集合顺序。
- `public static <T> void sort(List<T> list)`:将集合中元素按照默认规则排序。
- `public static <T> void sort(List<T> list，Comparator<? super T> )`:将集合中元素按照指定规则排序。
:::

其中最后一个方法：
`public static <T> void sort(List<T> list，Comparator<? super T> )`:将集合中元素按照指定规则排序。

<font color=tomato>如何指定规则 ? </font>
***
###### 默认规则是怎么定义出来的呢？
两个对象之间比较大小，那么在JAVA中提供了两种比较实现的方式，一种是比较死板的采用`java.lang.Comparable`接口去实现，一种是灵活的当我需要做排序的时候在去选择的`java.util.Comparator`接口完成。  

那么我们采用的`public static <T> void sort(List<T> list)`这个方法完成的排序，实际上要求了被排序的类型需要实现Comparable接口完成比较的功能，在String类型上如下：

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
```
String类实现了这个接口，并完成了比较规则的定义，但是这样就把这种规则写死了，无法修改规则


那么这个时候我们可以使用

`public static <T> void sort(List<T> list，Comparator<? super T> )`方法灵活的完成，这个里面就涉及到了Comparator这个接口，位于位于java.util包下，排序是comparator能实现的功能之一,该接口代表一个比较器，比较器具有可比性！顾名思义就是做排序的，通俗地讲需要比较两个对象谁排在前谁排在后，那么比较的方法就是：


` public int compare(String o1, String o2)`：比较其两个参数的顺序。

>两个对象比较的结果有三种：大于，等于，小于。
如果要按照升序排序，
则o1 小于o2，返回（负数），相等返回0，01大于02返回（正数）
如果要按照降序排序
则o1 小于o2，返回（正数），相等返回0，01大于02返回（负数）


案例：
```java
public class CollectionsDemo3 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();
        list.add("cba");
        list.add("aba");
        list.add("sba");
        list.add("nba");
        //排序方法  按照第一个单词的降序
        Collections.sort(list, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o2.charAt(0) - o1.charAt(0);
            }
        });
        System.out.println(list);
    }
}
// [sba, nba, cba, aba]
```