## 2.1.3 android kotlin code standard



# kotlin编码规范

## 目的

> 规范App端android代码规范，形成统一的风格，易于开发和维护；

## 命名规范

在 Kotlin 中，详细命名规范可以参考`android-java-code-standard`，以下我简单列举一些：

- 包的名称总是小写且不使用下划线（org.example.project）。 。
- 类与对象的名称以大写字母开头并使用驼峰风格：

> ```
> open class DeclarationProcessor { /*……*/ }
> object EmptyDeclarationProcessor : DeclarationProcessor() { /*……*/ }
> ```

### 函数名

- 函数、属性与局部变量的名称以小写字母开头、使用驼峰风格而不使用下划线：

> ```
> fun processDeclarations() { /*……*/ }
> var declarationCount = 1
> ```

### 属性名

- 常量名称（标有 const 的属性，或者保存不可变数据的没有自定义 get 函数的顶层/对象 val 属性）应该使用大写、下划线分隔的名称

> ```
> const val MAX_COUNT = 8
> val USER_NAME_FIELD = "UserName"
> ```

- 保存可变数据的顶层/对象属性的名称应该使用驼峰风格名称：

> ```
> val mutableCollection: MutableSet<String> = HashSet()
> ```

- 保存单例对象引用的属性的名称可以使用与 object 声明相同的命名风格：

> ```
> val PersonComparator: Comparator<Person> = /*...*/
> ```

- 对于枚举常量，可以使用大写、下划线分隔的名称 （enum class Color { RED, GREEN }）也可使用首字母大写的常规驼峰名称，具体取决于用途。

### 幕后属性的名称

- 如果一个类有两个概念上相同的属性，一个是公共 API 的一部分，另一个是实现细节，那么使用下划线作为私有属性名称的前缀：

> ```
> class C {
>    private val _elementList = mutableListOf<Element>()
> 
>    val elementList: List<Element>
>         get() = _elementList
> }
> ```

### 格式化

- 使用 4 个空格缩进。不要使用 tab。

对于花括号，将左花括号放在结构起始处的行尾，而将右花括号放在与左括结构横向对齐的单独一行。

> ```
> if (elements != null) {
>    for (element in elements) {
>        // ……
>    }
> }
> ```

注：在 Kotlin 中，分号是可选的，因此换行很重要。语言设计采用 Java 风格的花括号格式，如果尝试使用不同的格式化风格，那么可能会遇到意外的行为。

### 横向空白

- 在二元操作符左右留空格`( a + b )`。例外：不要在`“range to”`操作符`( 0..i )`左右留空格。不要在一元运算符左右留空格`( a++ )`
- 在控制流关键字`( if、 when、 for 以及 while )`与相应的左括号之间留空格。
- 不要在主构造函数声明、方法声明或者方法调用的左括号之前留空格。

> ```
> class A(val x: Int)
> fun foo(x: Int) { …… }
> fun bar() {
> foo(1)
> }
> ```

- 绝不在`(、 [之后或者 ]、 )`之前留空格。
- 绝不在`.`或者`?.`左右留空格：

> ```
> foo.bar().filter { it > 2 }.joinToString()
> foo?.bar()
> ```

- 在 // 之后留一个空格：// 这是一条注释
- 不要在用于指定类型参数的尖括号前后留空格：

> ```
> class Map<K, V> { …… }
> ```

- 不要在`::`前后留空格：Foo::class、 String::length
- 不要在用于标记可空类型的`?`前留空格：String?
- 作为一般规则，避免任何类型的水平对齐。将标识符重命名为不同长度的名称不应该影响声明或者任何用法的格式。

### 冒号

- 在以下场景中的`:`之前留一个空格： 当它用于分隔类型与超类型时； 当委托给一个超类的构造函数或者同一类的另一个构造函数时； 在 object 关键字之后。 而当分隔声明与其类型时，不要在 : 之前留空格。 在 : 之后总要留一个空格。

> ```
> abstract class Foo<out T : Any> : IFoo {
>    abstract fun foo(a: Int): T
> }
> 
> class FooImpl : Foo() {
>    constructor(x: String) : this(x) { /*……*/ }
>   
>    val x = object : IFoo { /*……*/ } 
> }
> ```

### 类头格式化

- 具有少数主构造函数参数的类可以写成一行：

> ```
> class Person(id: Int, name: String)
> ```

- 具有较长类头的类应该格式化，以使每个主构造函数参数都在带有缩进的独立的行中。 另外，右括号应该位于一个新行上。如果使用了继承，那么超类的构造函数调用或者所实现接口的列表应该与右括号位于同一行：

> ```
> class Person(
>    id: Int,
>    name: String,
>    surname: String
> ) : Human(id, name) { /*……*/ }
> ```

- 对于多个接口，应该将超类构造函数调用放在首位，然后将每个接口应放在不同的行中：

> ```
> class Person(
>    id: Int,
>    name: String,
>    surname: String
> ) : Human(id, name),
>     KotlinMaker { /*……*/ }
> ```

- 对于具有很长超类型列表的类，在冒号后面换行，并横向对齐所有超类型名：

> ```
> class MyFavouriteVeryLongClassHolder :
>    MyLongHolder<MyFavouriteVeryLongClass>(),
>    SomeOtherInterface,
>    AndAnotherOne {
>   
>   fun foo() { /*...*/ }
> }
> ```

### 修饰符

- 注解通常放在单独的行上，在它们所依附的声明之前，并使用相同的缩进：

> ```
> @Target(AnnotationTarget.PROPERTY)
> annotation class JsonExclude
> ```

- 无参数的注解可以放在同一行：

> ```
> @JsonExclude @JvmField
> var x: String
> ```

- 无参数的单个注解可以与相应的声明放在同一行：

> ```
> @Test fun foo() { /*……*/ }
> ```

### 表达式函数体格式化

- 如果函数的表达式函数体与函数声明不适合放在同一行，那么将 = 留在第一， 并将表达式函数体缩进 4 个空格。

> ```
> fun f(x: String, y: String, z: String) =
>    veryLongFunctionCallWithManyWords(andLongParametersToo(), x, y, z)
> ```

### 属性格式化

- 对于非常简单的只读属性，请考虑单行格式：

> ```
> val isEmpty: Boolean get() = size == 0
> ```

- 对于更复杂的属性，总是将 get 与 set 关键字放在不同的行上：

> ```
> val foo: String
>    get() { /*……*/ }
> ```

- 对于具有初始化器的属性，如果初始化器很长，那么在等号后增加一个换行并将初始化器缩进四个空格：

> ```
> private val defaultCharset: Charset? =
>    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
> ```

### 格式化控制流语句

- else、 catch、 finally 关键字以及 do/while 循环的 while 关键字与之前的花括号放在相同的行上：

> ```
> if (condition) {
>    // 主体
> } else {
>    // else 部分
> }
> 
> try {
>    // 主体
> } finally {
>    // 清理
> }
> ```

- 在 when 语句中，如果一个分支不止一行，可以考虑用空行将其与相邻的分支块分开：

> ```
> private fun parsePropertyValue(propName: String, token: Token) {
>    when (token) {
>        is Token.ValueToken ->
>            callback.visitValue(propName, token.value)
> 
>        Token.LBRACE -> { // ……
>        }
>    }
> }
> ```

- 将短分支放在与条件相同的行上，无需花括号。

> ```
> when (foo) {
>    true -> bar() // 支持
>    false -> { baz() } // 不赞成
> }
> ```

### Lambda 表达式格式化

- 在 lambda 表达式中，应该在花括号左右以及分隔参数与代码体的箭头左右留空格。 如果一个调用接受单个 lambda 表达式，应该尽可能将其放在圆括号外边传入。

> ```
> list.filter { it > 10 }
> ```

- 如果为 lambda 表达式分配一个标签，那么不要在该标签与左花括号之间留空格：

> ```
> fun foo() {
>    ints.forEach lit@{
>        // ……
>    }
> }
> ```

- 在多行的 lambda 表达式中声明参数名时，将参数名放在第一行，后跟箭头与换行符：

> ```
> appendCommaSeparated(properties) { prop ->
>    val propertyValue = prop.get(obj)  // ……
> }
> ```

- 如果参数列表太长而无法放在一行上，请将箭头放在单独一行：

> ```
> foo {
>   context: Context,
>   environment: Env
>   ->
>   context.configureEnv(environment)
> }
> ```

## 代码仓库规范

> **master**：主分支，用于备份及查看； **dev**：开发分支，用于日常项目开发及调试； **release**：项目结版及后期维护拉取代码发布等； **test**：日常测试及无关项目功能的临时使用分支；

- 项目代码在发版、重大更改、重要功能添加，都需要进行代码提交；
- 在不影响项目其他功能及模块的原则上，必须每日提交代码推送远程仓库分支；
- 提交代码，必须写清楚修改的内容，包括：新增或修改了什么功能、调整了什么地方、修复了什么BUG等；
- 项目发版必须打版本号Tag；
- 在项目发版或重大更新及调整之后，需要发起master分支合并请求，用SE主导；
- 重要更新及发版之后，需要发起主分支Master合并请求；

## 编程习惯

- 应遵循模块化、功能化原则，降低耦合，提高模块及框架的可扩展性；
- 应遵循面向对象、面向函数式编程，少用全局类型变量，少用临时参数；
- 任何选择型代码块需要全部考虑选择类型，任何返回型代码块需要考虑所有返回的可能性；
- 功能逻辑或需求应考虑所有异常或非正常调用及请求，而非简单的完成需求。
- 一般情况下，任何请求和调用应该有相应的回调或反馈；
- 你敲的每行代码，应思考是否是最优代码，是否是冗余代码，是否可以改善？
- 多与其他人沟通，多探讨代码逻辑、代码的严谨性；
- 新增功能及bug修复，应考虑修改的代码是否会影响其他功能；