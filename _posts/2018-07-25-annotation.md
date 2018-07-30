---
layout: post
title: 注解的使用及原理
categories: android知识
---

### 1 参考资料 ###

[Android注解快速入门和实用解析](https://mp.weixin.qq.com/s?__biz=MzAxMTI4MTkwNQ==&mid=2650823685&idx=1&sn=6ce37ce7835c950cd1174a695f8e930c&chksm=80b7889bb7c0018d0cf21d96315bebf3300cb7aa652da25ccd76564cdc8b5ad539955ee09530&mpshare=1&scene=1&srcid=0725NyFalaLKsUaZ3r4qBMfi#rd)   

[Java注解处理器](https://race604.com/annotation-processing/)

[Annotation注解APT（共5篇）](https://blog.csdn.net/xuewend/article/details/73498295)   

[【Android】APT](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2018/0423/9629.html)   

[自定义注解和解析器实现ButterKnife](https://mp.weixin.qq.com/s?__biz=MzAxMTg2MjA2OA==&mid=2649842013&idx=1&sn=0267e1974f293501b504d71c18a0430d&chksm=83bf6806b4c8e110ff4443975548e91c5d4ea6fba4b28a9b21b516e97b1be9eed534b5eebd6c&mpshare=1&scene=1&srcid=0726SawhenndU0DEBBNKZclR#rd)   

[Android注解简析](https://blog.csdn.net/johnWcheung/article/details/70230007)      

### 2 相关概念 ###

#### 2.1 注解的作用 ####

例如：  

@Override 就是注解，它的作用是：
1. 检查是否正确的重写了父类中的方法。  
2. 标明代码，这是一个重写的方法。

1、体现在于：检查子类重写的方法名与参数类型是否正确；检查方法 private／final／static 等不能被重写。实际上 @Override 对于应用程序并没有实际影响，从它的源码中可以出来。

2、主要是表现出代码的可读性。

作为 Android 开发中熟知的注解，Override 只是注解的一种体现，更多时候，注解还有以下作用：
- 降低项目的耦合度。
- 自动完成一些规律性的代码。
- 自动生成 java 代码，减轻开发者的工作量。

#### 2.2 元注解 ####

@Override 实现源码如下：

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {
}
```
元注解是由 java 提供的基础注解，负责注解其它注解，如上 Override 被 @Target 和 @Retention 修饰，它们用来说明解释其它注解，位于 sdk/sources/android-25/java/lang/annotation 路径下（在java.lang.annotation包下）。

元注解有：
@Retention：注解保留的生命周期
@Target：注解对象的作用范围。
@Inherited：@Inherited 标明所修饰的注解，在所作用的类上，是否可以被继承。
@Documented：如其名，javadoc 的工具文档化，一般不关心。
@Repeatable //java8 新增的 @Repeatable 注解

**@Retention**：(没有 @Retention 修饰的注解，默认使用的是 CLASS 方式。)

Retention 说标明了注解被生命周期，对应 RetentionPolicy 的枚举，表示注解在何时生效：
SOURCE：只在源码中有效，编译时抛弃，如上面的 @Override。注解在编译成 class 文件后直接丢弃，注解只存在于 Java 源码中。
CLASS：编译 class 文件时生效。注解在 class 文件中可用，当运行 java 程序时，JVM 将注解丢弃。
RUNTIME：运行时才生效。注解在 class 文件中可用，JVM 将在运行期也保留注解，因此可以通过反射机制读取注解的信息。

**@Target**:(没有 @Target 修饰的注解，可以用于修饰任何程序元素。)

Target 标明了注解的适用范围，对应 ElementType 枚举，明确了注解的有效范围。
TYPE：类、接口、枚举、注解类型。
FIELD：类成员（构造方法、方法、成员变量）。
METHOD：方法。
PARAMETER：参数。
CONSTRUCTOR：构造器。
LOCAL_VARIABLE：局部变量。
ANNOTATION_TYPE：注解。
PACKAGE：包声明。
TYPE_PARAMETER：类型参数。
TYPE_USE：类型使用声明。

@Inherited

注解所作用的类，在继承时默认无法继承父类的注解。除非注解声明了 @Inherited。同时 Inherited 声明出来的注，只对类有效，对方法／属性无效。

#### 2.3 自定义注解 ####

编译器允许对一个目标同时使用多个注解。使用多个注解的时候，同一个注解不能重复使用。
注解的定义与接口的定义很像，用 @interface 来定义一个注解（关键字 interface 前面多加了一个 @ 符号）。与其他任何 java 接口一样，注解也将会编译成 clas s文件。下面定义了一个简单的注解：
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Test {
	public int id();
    public String description() default "no description";
}
```

我们可以在注解体中定义元素（相当于注解信息）用于表示某些值。当分析处理注解时，程序或工具就可以利用这些值了.上面注解中定义两个元素 id 和 description。注解的元素的定义与接口中的方法定义几乎一样，但是注解中的元**素必须是以无参的方法来定义**。我们还可以使用关键字 default，指定该元素的默认值。description 元素就有一个默认值 ”no description” ，如果在注解某个方法时没有给出 description 的值，就会使用此元素的默认值。
注解的元素在使用时表现为 name-valu e(名-值)对的形式，必须要置于 @Test 声明之后的括号内。注意，使用注解时**必须要为其所有元素进行赋值，除非其中某个元素有设置默认值**。

注解元素并不什么类型都可以，可用的类型如下所示：
- 所有基本类型（int，float，boolean等） 
- String 
- Class 
- enum 
- Annotation（注解类型也可以作为元素类型） 
- 以上类型的数组

如果你使用了其他类型，那么编译器就会报错。注意，注解是不能使用除了上面以外的普通类（Object）作为元素的类型，这也包括任何包装类型。而且注解也可以作为元素的类型，也就是说注解可以嵌套。
我们把没有元素的注解称为标记注解（market annotation）。

**value元素** 
如果注解中的元素以 value 来命名，并且在应用该注解的时候，如果该元素是唯一需要赋值的一个元素，那么此时无需使用名-值对的这种语法，而只需要在括号内给出 value 元素所需的值即可。这可以应用于任何合法类型的元素。
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Test {

    public int value() ;
    public String description() default "";
}
```
下面会自动为 vaule 值自动赋值为 10。
```java
public class User {

    @Test(10)
    public void test1() {
    }
}
```
注意：如果 description 元素没有默认值，也就是说该注解必须为两个元素进行赋值，那么就不能以自定赋值的方式为元素 vlaue 进行赋值，而必须以名-值对的方式：
```java
//@Test(10,description = "do something") ERROR
    @Test(value = 10,description = "do something")
    public void test1() {
    }
```

**嵌套注解** 

注解元素类型允许存在注解类型，从而实现注解嵌套的功能。我们定义如下两个注解 Extra 和 Student，然后在Student 注解中使用 Extra 注解：
```java
Extra 注解：

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Extra {

    boolean isMonitor() default false;

    String region() default "";

    String hobby() default "";
}

Student注解：

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Student {

    int value() default 0;

    String name() default "";

    int age() default 0;

    Extra  other() default @Extra; //注解元素中可以定义注解类型
}
```
我们在 Student 注解中定义了一个 other 元素，它是 Extra 注解类型。other 元素的默认值是 @Extra，由于在 @Extra 注解类型之后，没有在括号中指明 @Extra 元素的值，因此，other 元素的默认值实际上就是一个所有元素都为默认值的 @Extra 注解。如果要令嵌入的 @Extra 注解中的指定元素赋值，并以此作为 other 元素的默认值，则需要如下定义该元素：
```java
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Student {

    int value() default 0;

    String name() default "";

    int age() default 0;

    Extra other() default @Extra(isMonitor = false, region = "China");//重新指定默认元素
}

我们用 Student 注解来注解如下字段：

public class Member {
    @Student
    String student1;

    @Student(10)
    String student2;

    @Student(name = "Tom", age = 17)
    String student3;

    @Student(name = "jack", other = @Extra(isMonitor = true, region = "Canada"))
    String student4;
}
```
在上面的字段中除了 student4 以外都使用了嵌入的 @Extra 注解的默认值，而 student4 因为情况特殊我们就可以为其嵌套注解 @Extra 中指定额外的信息。

#### 2.4 注解处理器  ####

大多数时候，程序员主要是定义自己的注解，并编写自己的处理器来处理它们。如果没有用来读取注解的工具，那注解也不会比注释更有用。使用注解的过程中，很重要的一个部分就是创建与使用注解处理器。Java 扩展了反射机制的 API,以帮助程序员构造这类工具。同时，它还提供了一个外部工具 apt，帮助程序员解析带有注解的 Java 源代码。

### 3 总结 ###

#### 3.1 注解的实现分类 ####

1. 运行时注解（Runtime）：通过反射实现
2. 编译时注解（Compile time)：通过注解处理器（Annotation Processor）实现

#### 3.2 运行时注解实现 ####

这里我们只说说如何利用反射的方式获取注解。当一个**注解被定义为运行时(RUNTIME)**存在，才可以通过反射的方式获得注解对象。所有被定义的注解都默认继承自 Annotatio n接口（java.lang.annotation 包下），Annotation接口是所有注解类型的父接口。反射中Class、Method、Constructor、Field、Package等类都继承了AnnotatedElement接口（java.lang.reflect 包下），AnnotatedElement接口中提供了四个方法来获取相关程序元素的注解：

方法	说明
- T getAnnotation(Class annotationClass)：	返回改程序元素上存在的、指定类型的注解，如果该类型注解不存在，则返回 null。
- Annotation[] getAnnotations()：返回该程序元素上存在的所有注解。
- boolean isAnnotationPresent(Class annotationClass)：	判断该程序元素上是否包含指定类型的注解，存在则返回 true，否则返回false。
- Annotation[] getDeclaredAnnotations()：返回直接存在于此元素上的所有注解。与此接口中的其他方法不同，该方法将忽略继承的注解。（如果没有注解直接存在于此元素上，则返回长度为零的一个数组。）该方法的调用者可以随意修改返回的数组；这不会对其他调用者返回的数组产生任何影响。
下面使用反射机制，打印出一个类中方法的所有注解信息。 

```java
首先定义一个运行时可用的注解：

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface UseCase {

    public int id() ;
    public String description() default "no description";

}

在User类中的方法上使用这些注解：

public class User {

    @UseCase(id=10,description = "test1 description")
    public void test1() {
    }

    @UseCase(id=20)
    public void test2() {
    }

    @UseCase(id=30,description = "test3 description")
    public void test3() {
    }
}

利用反射机制，输出注解的元素：

public class UserCaseTracker {
    public static void trackUser(Class<?> cl) {

        for (Method m : cl.getDeclaredMethods()) {

            if (m.isAnnotationPresent(UseCase.class)) {  //是否存在UseCase注解
                UseCase uc = m.getAnnotation(UseCase.class);//获取UseCase注解
                System.out.println("id: "+uc.id() + " description: " + uc.description());
            }
        }
    }

    public static void main(String[] args) {
        trackUser(User.class);
    }
}

/* Output:

id: 30description: test3 description
id: 20description: no description
id: 10description: test1 description

*/
```
上面的例子只是为了纯粹展示API的使用。

#### 3.3 编译时注解实现过程 ####

运行时注解 RUNTIME，大多数时候实在运行时使用反射来实现所需效果，这很大程度上影响效率,编译时注解，在编译时生成对应 java 代码，实现注入。

说到编译时注解，就不得不说注解处理器 AbstractProcessor，如果你有注意，一般第三方注解相关的类库，如 bufferKnike、ARouter，都有一个 Compiler 命名的 Module，这里面一般都是注解处理器，用于编译时处理对应的注解。

注解处理器（Annotation Processor）是 javac 的一个工具，它用来在编译时扫描和处理注解（Annotation）。你可以对自定义注解，并注册相应的注解处理器，用于处理你的注解逻辑。

创建项目（在java library 中我们才可以继承解析器 AbstractProcessor，android library 是无法访问的）：

apt-annotation ：**Java library Module**，用于存放自定义注解
apt-processor：**Java library Module**（依赖 apt-annotation、com.squareup:javapoet:1.7.0、com.google.auto.service:auto-service:1.0-rc2），注解处理器，根据 apt-annotation 中的注解，在编译期生成 java 代码

AbstractProcessor 处理过程参考：[Java注解处理器](https://race604.com/annotation-processing/)

Demo 地址：[实现编译时注解 Factory](https://github.com/ADeveloperH/AndroidTest/tree/annotation)

#### 4 常用注解 ####

@Override：表示当前的方法定义将覆盖超类中的方法。如果你不小心拼写错误，或者方法签名对不上被覆盖的方法，编译器就会发出错误。注意， @Override 注解只能用于作用于方法，不能用于作用于其它程序元素。@Override 告诉编译器检查这个方法是否满足重写规则，如果满足编译通过，否则编译报错。

@Deprecated：用于表示某个程序元素（类，方法等）已经过时，编译器将不鼓励使用这个被标注的程序元素。当其他程序使用过时的是程序元素时，编译器会发出警告信息(被画上了中划线)。这种修饰具有一定的 “延续性”：如果我们在代码中通过继承或者覆盖的方式使用了这个过时的类型或者成员，虽然继承或者覆盖后的类型或者成员并不是被声明为@Deprecated，但编译器仍然要报警。

@SuppressWarnings，关闭编译器的警告信息。在java5.0，sun 提供的 javac 编译器为我们提供了 -Xlint 选项来使编译器对合法的程序代码提出警告，此种警告从某种程度上代表了程序错误。例如当我们使用一个泛型类而又没有提供它的类型时，编译器将提示出 unchecked warning 的警告。通常当这种情况发生时，我们就需要查找引起警告的代码。如果它真的表示错误，我们就需要纠正它。例如如果警告信息表明我们代码中的 switch 语句没有覆盖所有可能的 case，那么我们就应增加一个默认的 case 来避免这种警告。有时我们无法避免这种警告，例如，我们使用必须和非泛型的旧代码交互的泛型集合类时，我们不能避免这个 unchecked warning。此时@SuppressWarning 就要派上用场了，在调用的方法前增加 @SuppressWarnings 修饰，告诉编译器停止对此方法的警告。被 @SuppressWarnings 修饰的程序元素(以及在程序元素中的所有子元素)将取消显示指定的编译器警告。通常情况下，如果程序中使用没有泛型限制的集合将会引起编译器警告，当我们使用 @SuppressWarnings 注解来关闭编译器警告时，一定要在插号里使用 name=value 对来为该注解的中的元素设置值，unchecked 字段常被用于抑制未检测的警告，也就是 -Xlint 后的警告名 unchecked。SuppressWarnings 中的元素 value 是一个数组类型，所以我们可以用大括号来声明数组值，表示抑制多个警告，如：@SuppressWarnings({ “rawtypes”, “unchecked” })(因为元素名是 value 所以可以省略)。
SuppressWarnings 注解的常见参数值的简单说明： 
1. all：所有情况的警告。　　　　 
2. unchecked：执行了未检查的转换时的警告，例如当使用集合时没有用泛型 (Generics) 来指定集合保存的类型; 
3. fallthrough：当 Switch 程序块直接通往下一种情况而没有 Break 时的警告; 
4. path：在类路径、源文件路径等中有不存在的路径时的警告; 
5. serial：当在可序列化的类上缺少 serialVersionUID 定义时的警告; 
6. finally：任何 finally 子句不能正常完成时的警告; 
7. unused：变量未被使用的警告; 
8. deprecation：使用了不赞成使用的类或方法时的警告； 
……还有很多。

**Android 注解**有8种类型，分别是 Nullness 注解、资源类型注解、线程注解、变量限制注解、权限注解、结果检查注解、CallSuper 注解、枚举注解(IntDef 和 StringDef)。要使用注解，就必须引入注解库，android-support-annotations (v7 包中已包含)是 Android 官方提供的一个注解库，它提供了许多有用的注解，这些注解的生命周期为源码时期，也就是在编译之后则不再保留，通常用于辅助代码上的静态检查。

**Nullness注解**

也即空指针检查，通常我们如果对一个变量进行主动的赋值为 null，编译器可能会进行可能引发空指针异常的警告，我们可以使用以下注解对这种行为进行控制。

@NonNull：指出一个参数，变量，或方法返回值永远不可为 null。
@Nullable：指出一个参数，变量，或方法返回值可能为 null。

**资源类型注解**

此类注解以 Res 结尾，一共有22个

@AnimatorRes ：指出一个 integer 的参数，成员变量，或方法返回值是一个 animator 资源的引用。

@AnimRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 anim 资源的引用。

@AnyRes：指出一个 integer 的参数，成员变量，或方法返回值是一个任意资源类型的引用。

@ArrayRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 array 资源类型的引用。

@AttrRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 attr 资源的引用。

@BoolRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 boolean 资源的引用。

@ColorRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 color 资源的引用。

@DimenRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 dimen 资源的引用。

@DrawableRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 drawable 资源的引用（包括 @mipmap）。

@FractionRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 fraction 资源的引用。

@IdRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 id 资源的引用。

@IntegerRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 integer 资源的引用。

@InterpolatorRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 interpolator 资源的引用。

@LayoutRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 layout 资源的引用。

@MenuRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 menu 资源的引用。

@PluralsRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 plurals 资源的引用。

@RawRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 raw 资源的引用。

@StringRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 string 资源的引用。

@StyleableRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 styleable 资源的引用。

@StyleRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 style 资源的引用。

@TransitionRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 transition 资源的引用。

@XmlRes：指出一个 integer 的参数，成员变量，或方法返回值是一个 xml 资源的引用。

@ColorInt：限制传入 Hex 颜色值。

**线程注解**

@BinderThread：指出被注解的方法应该只在 binder 线程中被调用。

@MainThread：指出被注解的方法应该只在主线程中被调用。

@WorkerThread：指出被注解的方法应该只在工作线程中被调用。

@UiThread：指出被注解的方法应该只在 UI 线程中被调用。

变量限制注解

@FloatRange：指出一个被注解的元素应该是一个给定范围内的 float 值或 double 值。比如：

```java
@FloatRange(from=0.0,to=1.0)
        public float getAlpha() {
                  ...
         }

```

@IntRange：指出一个被注解的元素应该是一个给定范围内的 int 值或 long 值。

@Size：可以用来限定集合的大小或者限定字符串的长度，还可以做其他限制：

限制最小最大数量：@Size(min=1,max=10 )

数量必须是2的倍数（偶数）: @Size(multiple=2)


权限注解

@RequiresPermission

如果方法的调用需要权限，可以加这个注解，当需要几个权限中的一个时，使用anyOf，如
```java
@RequiresPermission(anyOf = { Manifest.permission.ACCESS_COARSE_LOCATION, Manifest.permission.ACCESS_FINE_LOCATION})

若需要多个权限，使用allOf，如

@RequiresPermission(allOf = { Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE})

若需要单独的标注读和写的权限访问，所以可以用@Read或者@Write标注每一个权限需求
```
结果检查注解

@CheckResult

该注解意味着需要对方法的返回值进行处理，例如：有个方法为
```java
@CheckResult  
public boolean checkValid(String value){  
     return TextUtils.isEmpty(value);  
}  

当调用者直接调用 checkValid(“abc”); 时会报错，这意味着，需要对方法的返回值进行处理，无论返回 true 或 false，需要进行后续操作，不能单单调用一句 checkValid(“abc”);
```
CallSuper注解

@CallSuper

指出一个方法如果被重写了，它必须也被调用。比如Activity的生命周期方法onCreate方法等。

枚举注解

@IdDef和@StringDef

```java
提到最常用的Toast，在API21之前，一般可以这么写

Toast.makeText(context, "msg", 0).show();

但是21之后，0突然被划红线了，查看源码发现，之前是这么写的：

public static final int LENGTH_SHORT = 0;  
public static final int LENGTH_LONG = 1;  

makeText方法中单纯地写着int duration参数，而21之后，成了这样：

@IntDef({LENGTH_SHORT, LENGTH_LONG})  
@Retention(RetentionPolicy.SOURCE)  
public @interface Duration {}  

在makeText的duration参数之前加上了注解@Duration，这就要求传入Duration中的值才不会报警告。

可以想象，@IntDef和@String Def中放入了一个value数组。

在开发中，这两个注解就可以用来限制枚举值了。
```

**Android 其他常见的注解**

Android 从 API16 引入了 annotation 包，包括两个注解 @TargetApi 和 @SuppressLint

@TargetApi (Build.VERSION_CODES.XX) 用于屏蔽**某一**新 api 中才能使用的方法报的 lint 检查出现的错误。

@SuppressLint(“NewApi”) 屏蔽**一切**新 api 中才能使用的方法报的 android lint 错误

当然，这两个注解的作用仅仅是屏蔽lint错误，在方法中还要判断版本做不同的操作，比如：

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.XX) {  
    //高于XX版本进行的操作  
} else {  
    //低于XX版本进行的操作  
} 

```
@SdkConstant

表示一个常量字段应该被输出在SDK工具中使用，例如，添加一个自定义的Action：

```java
@SdkConstant(SdkConstantType.ACTIVITY_INTENT_ACTION)   
public static final String ACTION_MY_TEST = "android.intent.action.MY_TEST";   


则可以这样使用：

Intent myTest = new Intent(Intent.ACTION_MY_TEST);   
mContext.sendBroadcast(myTest);  
```

@Widget

用于类的注解，表示该类是自定义的Widget类