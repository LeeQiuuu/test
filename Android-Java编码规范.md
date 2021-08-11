## 2.1.2 android java code standard



# android编码规范

## 目的

> 规范App端android代码规范，形成统一的风格，易于开发和维护；

## 命名规范

### 包名

- 全部`小写`，连续的单词只是简单地连接起来，`不使用下划线`，采用反域名命名规则，全部使用小写字母。
- 一级包名是顶级域名，通常为`com`、`edu`、`gov`、`net`、`org`等，二级包名为公司名，三级包名根据应用进行命名，后面就是对包名的划分了，关于包名的划分，推荐采用PBF（按功能分包Package By Feature）。

### 类名

- 类名都以`UpperCamelCase`风格编写，`大驼峰`命名法，尽量避免缩写，除非该缩写是众所周知的，比如HTML、URL，如果类名称中包含单词缩写，则单词缩写的每个字母均应大写。 类描述例如： `Activity`类`Activity`为后缀标识欢迎页面类`WelcomeActivity`； `Adapter`类`Adapter`为后缀标识新闻详情适配器`NewsDetailAdapter`； `Service`类以`Service`为后缀标识时间服务`TimeService`； `BroadcastReceiver`类以`Receiver`为后缀标识推送接收`JPushReceiver`； `ContentProvider`类以`Provider`为后缀标识`ShareProvider`； 工具方法类`Utils`或`Manager`为后缀标识线程池管理类：`ThreadPoolManager`； 日志工具类：`LogUtils`（`Logger`也可）； 自定义的共享基础类以Base开头`BaseActivity,BaseFragment`；

### 方法名

- 方法名都以`lowerCamelCase`风格编写,`小驼峰`命名法。 方法名例如： `initXX()`初始化相关方法，使用`init`为前缀标识，如初始化布局`initView()`； `isXX()`,`checkXX()`方法返回值为`boolean`型的请使用`is`/`check`为前缀标识； `getXX()`返回某个值的方法，使用get为前缀标识； `setXX()`设置某个属性值；

### 常量名命名

- 常量名命名模式为`CONSTANT_CASE`，全部`字母大写`，用`下划线分隔`单词。那到底什么算是一个常量？每个常量都是一个`static final`字段，但不是所有`static final`字段都是常量。在决定一个字段是否是一个常量时，得考虑它是否真的感觉像是一个常量。例如，如果观测任何一个该实例的状态是可变的，则它几乎肯定不会是一个常量。只是永远不打算改变的对象一般是不够的，它要真的一直不变才能将它示为常量。

### 其他

- 变量名以`lowerCamelCase`风格编写，`小驼峰`命名法。不能使用单个字符命名。除了循环变量，且尽量避免过短的缩写；
- 参数名以`lowerCamelCase`风格编写，`小驼峰`命名法，参数应该避免用单个字符命名。
- 局部变量`lowerCamelCase`风格编写，`小驼峰`命名法，比起其它类型的名称，局部变量名可以有更为宽松的缩写。虽然缩写更宽松，但还是要避免用单字符进行命名，除了临时变量和循环变量。即使局部变量是final和不可改变的，也不应该把它示为常量，自然也不能用常量的规则去命名它。
- 对于表示集合或者数组的非常量字段名，我们可以添加后缀来增强字段的可读性，比如：集合添加如下后缀：`List、Map、Set`。数组添加如下后缀：`Arr`。 例如：`mIvAvatarList`、`userArr`、`firstNameSet`。 注意：如果数据类型不确定的话，比如表示的是很多书，那么使用其复数形式来表示也可，例如mBooks。

### 选择好名称

类的名称通常是用来解释类是什么的名词或者名词短语：`List`、 `PersonReader`。

方法的名称通常是动词或动词短语，说明该方法做什么：`close`、`readPersons`。 修改对象或者返回一个新对象的名称也应遵循建议。例如`sort` 是对一个集合就地排序，而 `sorted` 是返回一个排序后的集合副本。

名称应该表明实体的目的是什么，所以最好避免在名称中使用无意义的单词 （`Manager`、 `Wrapper` 等）。

当使用首字母缩写作为名称的一部分时，如果缩写由两个字母组成，就将其大写（IOStream）； 而如果缩写更长一些，就只大写其首字母（XmlFormatter、 HttpInputStream）。

## 代码样式规范

### 使用标准大括号样式

- 左大括号不单独占一行，与其前面的代码位于同一行：

  > ```
  > class MyClass {
  >  int func() {
  >    if (something) {
  >      //...
  >    } else if(something else) {
  >      //...
  >    } else {
  >      //...
  >    }
  >  }
  > }
  > ```

- 我们需要在条件语句周围添加大括号。如果整个条件语句（条件和主体）适合放在同一行，那么您可以（但不是必须）将其全部放在一行上。例如，我们接受以下样式：

> ```
> if(condition){
>   body();
> }
> 同样也接受以下样式：
> if(condition)body();
> 但不接受以下样式：
> if(condition)
> body();//bad!
> ```

- 习惯写完代码后快捷键 `CTRL+ALT+L`格式化下代码。

### 编写简短方法

在可行的情况下，尽量编写短小精炼的方法。我们了解，有些情况下较长的方法是恰当的，因此对方法的代码长度没有做出硬性限制。如果某个方法的代码超出40行，请考虑是否可以在不破坏程序结构的前提下对其拆解。

### 行长限制

代码中每一行文本的长度都应该不超过100个字符。虽然关于此规则存在很多争论，但最终决定仍是以100个字符为上限，如果行长超过了100（AS窗口右侧的竖线就是设置的行宽末尾），我们通常有两种方法来缩减行长。

- 提取一个局部变量或方法（最好）。
- 使用换行符将一行换成多行。不过存在以下例外情况：如果备注行包含长度超过100个字符的示例命令或文字网址，那么为了便于剪切和粘贴，该行可以超过100个字符。
- 导入语句行可以超出此限制，因为用户很少会看到它们（这也简化了工具编写流程）。

## 资源文件规范

### 动画资源文件（`anim/`和`animator/`）

安卓主要包含属性动画和视图动画，其视图动画包括补间动画和逐帧动画。属性动画文件需要放在`res/animator/`目录下，视图动画文件需放在`res/anim/`目录下。 命名规则：{模块名_}逻辑名称_anim。 说明：{}中的内容为可选，逻辑名称可由多个单词加下划线组成。 例如：refresh_progress_anim.xml、market_cart_add_adim.xml。 如果是普通的补间动画或者属性动画，可采用：动画类型_方向的命名方式_anim。 例如：fade_in_anim 淡入 fade_out_anim 淡出

### 颜色资源文件（`color/`）

专门存放颜色相关的资源文件。 命名规则：类型_逻辑名称 例如：sel_btn_font.xml。 注：颜色资源也可以放于`res/drawable/`目录，引用时则用`@drawable`来引用，但不要这么做，分开管理。

### 图片资源文件（`drawable/`和`mipmap/`）

【推荐】res/drawable/目录下放的是位图文件（`.png、.9.png、.jpg、.gif`）或编译为可绘制对象资源子类型的XML文件，而`res/mipmap/`目录下放的是不同密度的启动图标，所以`res/mipmap/`只用于存放启动图标，其余图片资源文件都应该放到`res/drawable/`目录下。

### values资源文件（`values/`）

values/资源文件下的文件都以s结尾，如`attrs.xml`、`colors.xml`、`dimens.xml`，起作用的不是文件名称，而是`<resources>`标签下的各种标签，比如`<style>`决定样式，`<color>`决定颜色，所以，可以把一个大的xml文件分割成多个小的文件，比如可以有多个style文件，如`styles.xml`、`styles_home.xml`、`styles_item_details.xml`、`styles_forms.xml`。

#### 颜色colo.xml

- `<color>`的name命名使用下划线命名法，在你的colors.xml文件中应该只是映射颜色的名称一个ARGB值，而没有其它的。不要使用它为不同的按钮来定义ARGB值。

  例如，不要像下面这样做：

  > ```
  > <resources>
  >   <colorname="button_foreground">#FFFFFF</color>
  >   <colorname="button_background">#2A91BD</color>
  > <resources>
  > ```

- 使用这种格式，会非常容易重复定义ARGB值，而且如果应用要改变基色的话会非常困难。同时，这些定义是跟一些环境关联起来的，如`button`或者`comment`，应该放到一个按钮风格中，而不是在`colors.xml`文件中。

  相反，应该这样做：

  > ```
  > <resources>
  >   <colorname="white">#FFFFFF</color>
  >   <colorname="gray_light">#DBDBDB</color>
  > <resources>
  > ```

- 或者用`color_颜色值`，建议用这种，识别度高，引用更方便，看ui效果图只给颜色值，编写布局直接提示就出来了，例如：

  > ```
  > <resources>
  >   <colorname="color_520000">#520000</color>
  > <resources>
  > ```

### 字符串`string.xml`

所有文字都必须放到`string.xml`，除非该应用不支持多语言切换。

## 注释规范

为了减少他人阅读你代码的痛苦值，请在关键地方做好注释。

### 类注释

每个类完成后应该有作者姓名和联系方式的注释，对自己的代码负责。

> ```
> /**
> * <pre>
> *  author:Blankj
> *  e-mail:xxx@xx
> *  time:2017/03/07
> *  desc:xxxx描述
> * </pre>
> */public class WelcomeActivity{
> 		...
> }
> ```

具体可以在AS中自己配制，进入`Settings->Editor->File and Code Templates->Includes->FileHeader`，输入

> ```
> /**
> * <pre>
> *  author:${USER}
> *  e-mail:xxx@xx
> *  time:${YEAR}/${MONTH}/${DAY}
> *  desc:
> * </pre>
> */
> ```

这样便可在每次新建类的时候自动加上该头注释。

### 方法注释

每一个成员方法（包括自定义成员方法、覆盖方法、属性方法）的方法头都必须做方法头注释，在方法前一行输入`/**+回车`或者设置`Fix doc comment（Settings->Keymap->Other->Fix doc comment）`快捷键，AS便会帮你生成模板，我们只需要补全参数即可，如下所示。

> ```
> /**
> * bitmap转byteArr
> *
> * @parambitmapbitmap对象
> * @paramformat格式
> * @return字节数组
> */
> public static byte[] bitmap2Bytes(Bitmap bitmap, CompressFormat format){
>  if (bitmap == null) return null;
>  ByteArrayOutputStream baos = new ByteArrayOutputStream();
>  Bitmap.compress(format, 100, baos);
>  retrun baos.toByteArray();
> }
> ```

### 块注释

块注释与其周围的代码在同一缩进级别。它们可以是/*...*/风格，也可以是//...风格（//后最好带一个空格）。对于多行的/*...*/注释，后续行必须从*开始，并且与前一行的*对齐。在写多行注释时，如果你希望在必要时能重新换行（即注释像段落风格一样），那么使用/*...*/。

### 其他一些注释

AS已帮你集成了一些注释模板，我们只需要直接使用即可，在代码中输入todo、fixme等这些注释模板，回车后便会出现如下注释。//TODO:17/3/14 需要实现，但目前还未实现的功能的说明//FIXME:17/3/14需要修正，甚至代码是错误的，不能工作，需要修复的说明

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