*如果文件内容是纯 PHP 代码，最好在文件末尾删除 PHP 结束标记。
这可以避免在 PHP 结束标记之后万一意外加入了空格或者换行符，会导致PHP开始输出这些空白，而脚本中此时并无输出的意图。--不推荐使用这将如预期中的运行，因为当 PHP 解释器碰到 ?> 结束标记时就简单地将其后内容原样输出（除非马上紧接换行见指令分隔符）直到碰到下一个开始标记；例外是处于条件语句中间时，此时PHP解释器会根据条件判断来决定哪些输出，哪些跳过。
*可以在PHP中使用四对不同的开始和结束标记。其中两种，<?php ?> 和 <script language="php"> </script> 总是可用的。另两种是短标记和 ASP 风格标记，可以在 php.ini 配置文件中打开或关闭。尽管有些人觉得短标记和ASP风格标记很方便，但移植性较差，通常不推荐使用。文件末尾的 PHP 代码段结束标记可以不要，有些情况下当使用 include 或者 require 时省略掉会更好些，这样不期望的空白符就不会出现在文件末尾，之后仍然可以输出响应标头。在使用输出缓冲时也很便利，就不会看到由包含文件生成的不期望的空白符。
*如果只是想得到一个易读懂的类型的表达方式即名称用于调试，用 `gettype()` 函数。如果要将一个变量强制转换为某类型(如在变量前加(string)转换为字符串)，可以对其使用强制转换或者 `settype()` 函数。
gettype()返回参数的类型字符串
```
echo gettype("a");//string

$a=array();
echo gettype($a);//array 

class A{
}
$a=new A();
echo gettype($a);//object

$a=122;
var_dump((string)$a);
```

settype语法：settype(var, type),返回布尔型
```
$a=122;
var_dump(settype($a,"array"));//true
var_dump($a);//array
```

-为什么使用 `$_GET`？
注释：在使用 `$_GET `变量时，所有的变量名和值都会显示在 `URL` 中。所以在发送密码或其他敏感信息时，不应该使用这个方法。不过，正因为变量显示在 URL 中，因此可以在收藏夹中*收藏*该页面。在某些情况下，这是很有用的。
注释：HTTPGET方法不适合大型的变量值；受到url长度的限制
-在IE8 下的URL地址总长度为：4076，超过该长度会自动忽略后面的内容；
-在firefox 25下的URL地址总长度可以达到:7530，超过该长度会访问错误；
-在chrome 29.0.1547.62 的最大总长度达到:7675，超过该长度会访问错误；

-为什么使用 `$_POST`？
通过 `HTTP POST` 发送的变量不会显示在 `URL` 中。 
变量没有长度限制。 
不过，由于变量不显示在 URL 中，所以无法把页面加入书签。

-`$_REQUEST` 变量
PHP 的 `$_REQUEST` 变量包含了 `$_GET, $_POST` 以及 `$_COOKIE`的内容。
PHP 的 `$_REQUEST` 变量可用来取得通过 GET 和 POST 方法发送的表单数据的结果。当同名时，他们的顺序为：`$_COOKIE>$_POST>$_GET`

指定一个布尔值，使用关键字 TRUE 或 FALSE 。两个都不区分大小写。
当转换为 boolean 时，以下值被认为是 FALSE ： 
-布尔值 FALSE 本身 
-整型值 0（零） 
 浮点型值 0.0（零） 
 字符串 "0" 
-空字符串
 不包括任何元素的数组 
 不包括任何成员变量的对象（仅 PHP 4.0 适用） 
-特殊类型 NULL（包括尚未赋值的变量） 
-从空标记生成的 SimpleXML 对象 
所有其它值都被认为是 TRUE （包括任何资源）。 

要使用八进制表达，数字前必须加上 0（零）。要使用十六进制表达，数字前必须加上 0x。要使用二进制表达，数字前必须加上 0b。


#字符串String

###表示方法：单引号、双引号、heredoc和nowdoc格式
单引号只是不对特殊字符转义，会显示转义的反斜线
   `Heredoc`类似双引号字符串结构，特殊字符转义，变量解析
   `Nowdoc`类似单引号字符串结构
   `error_reporting(E_ALL)`;显示所有的错误
echo "This is {$arr['key']}";在双引号字符串中使用数组键值时，要加上花括号

字符串也可以用下标(下标从0开始)查找：$str="fantastic";
echo $str[2];也可以使用$str{2}
strlen($str)获取字符串的长度
$str[2]="z";修改了原字符串相应位置的值
(string)(123);将123转换为字符串 或使用字符串转换函数:strval()

serialize();  unserialize();序列化只是将变量转换为一种特殊的存储格式
ord();chr()字符串的ascii码转换


#数组

php5.4后可以使用[]代替array()定义数组，最后一个会覆盖前面的同名索引对应的值
方括号[]和花括号{}可以互换使用
`unset()`删除某键值对，也可以删除整个数组,没有返回值,改函数删除变量会将变量消失
`array_values()`返回数组中所有的值，并建立数字索引数组
引用数组时，用不着给键名为常量和变量的加上引号，否则php不能解析，如$arr[$var]
count($arr)计算数组的长度
实现数组遍历使用foreach函数
```  
foreach ($variable as $key => $value) {
         //code...
}
```
数组排序 `sort()`,返回布尔值，对原数组进行了修改，一般对索引数组排序
`asort()`
`ksort()`
`array_map()`对数组元素分别应用方法


#NULL（包括尚未赋值的变量）
一个变量被认为是null：不区分大小写
    1、被复值为null
    2、尚未被赋值
    *3、被unset()*
判断：is_null()


#变量

变量名区分大小写
一般是传值赋值，也可使用关键&引用赋值
`isset()`检测一个变量是否已经被初始化并被赋予非null值，当一个变量赋予null时调用isset返回false

PHP全局变量在函数中使用时必须声明为global，否则不可用
``` $a=1;
   function test(){
        echo $a;
   }
   test();//不会输出任何值
```
也可以使用全局数组`$GLOBALS`来访问全局变量
静态局部变量：仅在局部函数域中存在，但当程序执行离开此作用域时，其值并不丢失
```
function test(){
        static $a=0;
        echo $a;
        $a++;
    }//$a仅在第一次调用函数时初始化
```
###可变变量 
```
$a='hello';
$$a='world';等价于$hello='world';
```
###常量：
-对大小写敏感，但一般大写
-`defined()`检测是否定义了某个常量
-常量只能用`define()`定义
###魔术常量
    __LINE__
    __FILE__
    __DIR__
    __FUNCTION__
    __CLASS__
    __TRAIT__
    __METHOD__
    __NAMESPACE__


#表达式
-运算符
    -PHP在*对象赋值时是引用赋值的*
    -两个浮点数不应该被比较,会因为误差导致错误
-错误控制符@
    -放在一个表达式之前，屏蔽表达式产生的错误
-执行运算符
    -反引号``,效果与`shell_exec()`函数相同
-递增递减运算符
    -可以对字符变量使用递增递减，即$a='a'; $a++,按照ascii码计算
-逻辑运算符
    -与：and     &&   *&&优先级更高*
    -或：or      ||   *||优先级更高*
    -非：!
    -异或： xor
-数组运算符
    -+将两个数组连接成一个数组，保留左边的同名元素，右边的被覆盖
     而array_merge()则是左边的被覆盖
    -$a==$b 如果两个数组有相同的键值对，则返回true
    -$a===$b 如果两个数组有相同的键值对，而且顺序和类型都相同，则返回true
-类型运算符`instanceof`，用于确定一个变量是否属于某一类class的实例
    -var_dump($a instanceof MyClass);
    -也可以确定某一个变量是否是继承一个父类的子类
    -还可以确定一个变量是否实现了某个接口的对象的实例


#流程控制

-流程控制的替代语法
    PHP提供了一些流程控制的替代语法，包括`if\while\for\foreach\和switch`，替代的方法是：将左花口号换成冒号，把右花括号换成
    `endif;\endwhile\endfor\endforeach\endswitch`
-`foreach`仅能够应用于数组和对象，而且可以引用赋值
    foreach($arr as $key => &$value),一般在不用时要取消引用unset($value)
    foreach不支持@抑制错误信息
-`list()`将嵌套的数组解包,是一种语言结构，而不是函数
-`break`可以接受一个可选的参数来决定跳出几重循环，默认为1
-`switch`做的是*松散的比较*,switch仅求值一次，而在elseif语句中每次比较都要重新求值
-declare结构,暂时不需了解
-不是所有的语句都可以计时，条件表达式和参数表达式都不可以计时，也就是说程序执行时间不包括这些过程

-`goto`操作符
```
goto a;
echo 'foo';
a:
echo 'bar';
```


#函数

-函数名是大小写无关的，最好是区分大小写，linux区分大小写
-php默认按值传递参数，操作对象默认为引用传递和默认参数
-匿名函数


#类与对象

-每个变量都持有对象的引用，而不是整个对象的拷贝
-对象和实例，对象是对实例的引用，通过克隆的方法可以给已经创建对象的实例建立一个新的实例
    -子类继承父类，重写方法时要把保持参数一致，但构造函数除外
    -`::class`

###类常量
-使用`const`关键字可以定义类常量,不要加$
        const aa='haha';
-调用类常量时，使用self关键字，不要加$,self::aa;(在类内部调用)，在类外部调用可以直接使用类名或对象名::aa；
-自动加载类，`__autoload()`函数,未来可能被弃用，改用spl_autoload_register()函数。

###访问控制
`public    protected     private`
范围解析操作符`::`,可以用来访问静态变量和类常量，在类外使用这些属性和方法时要带类名
    -`self\parent\static`是用于在类定义内部对其属性或方法进行访问的
-static关键字
    -静态属性不能通过一个类实例化的对象来访问，但静态方法可以
-抽象类、抽象方法
```
被声明了抽象的方法只是声明了其调用方式（参数），不能定义其具体的功能实现，介于接口和类之间

继承一个抽象类时，必须定义父类中的所有抽象方法，访问控制至少更为宽松，参数设置必须一致（必须含有父类中的参数，可以添加可选的参数）
```
**接口
    -接口中定义的所有方法都必须是公有的
    -接口中的方法都是只声明不定义
    -类继承接口要实现接口中所有声明方法的定义，形式参数也要一致
    -类可以实现多个接口，用逗号分隔，但不可以继承多个类
    -接口也可以继承
    -接口也可以定义常量，但不能被子类或子接口覆盖
**traits
    -调用关键字：use Traitsname
    -优先级：子类成员覆盖trait中定义的方法，trait覆盖父类中的方法
    -通过逗号分隔，在use声明列出多个trait,可以都插入到一个类中
    -解决冲突`insteadof`关键字和`as`关键字
    -`as`关键字也可以修改trait被引入的访问控制
    -triat可以组合，在一个trait中use多个trait
    -`trait`可以声明抽象方法
    -trait中可以定义静态属性和静态方法
    -trait中可以定义属性，但类中不能定义同名属性，否则出错

**重载：通过魔术方法实现
    -`__set()    __get()      __isset()    __unset() `当对不可访问的属性操作时会调用相应的方法
    -`__call()    __callStatic() ` 当对不可访问的方法或静态方法操作时会调用相应的方法
**遍历对象
    -可以使用`foreach`语句，默认情况下，所有可见属性都将被用于遍历
-魔术方法
```    __construct() __destruct() __call()  __callStatic()  __get()
        __set() __isset() __unset()  __sleep() __wakeup() __toString()
        __ invoke() __set_state()  __clone()
```
-final
属性不能被定义为final,只有类和方法才能被定义为fianl

-对象复制
```
    -通过clone关键字，这将调用新生成的对象中的`__clone()`方法修改属性的值,
    -对象中的`__clone()`方法不能被直接调用，但所有的引用属性仍然会是指向原来的变量的引用
```
-对象的比较
```
    -`==`原则是：如果两个对象的属性和属性值都相等，而且两个对象是同一个类的实例，那么这两个对象相等；
    -`===`原则是：这两个对象变量一定要指向某个类的同一个实例（即同一个对象）
```
-类型约束
类中方法的参数可以指定必须为某一类型;
函数中也可以指定参数的类型

*后期静态绑定*


#正则表达式

`preg_quote("*\()[]")` 将字符串转换为正则表达式（不包括定界符//）

\h 任意水平空白字符(since PHP 5.2.4) 
\H 任意非水平空白字符(since PHP 5.2.4) 
\V 任意非垂直空白字符(since PHP 5.2.4) 
\w 任意单词字符  单词字符指的是任意字母、数字、下划线
\W 任意非单词字符 

###断言 
 
一个断言指定一个必须在*特定位置*匹配的条件， 它们不会从目标字符串中消耗任何字符。
反斜线断言包括： 
\b 单词边界 
\B 非单词边界 
这些断言不能出现在字符类中(但是注意， “\b”在字符类中有不同的意义， 表示的是退格(backspace)字符)
[]叫做字符类

\A， \Z， \z断言不同于传统的^和$(详见下文)， 因为他们永远匹配目标字符串的开始和结尾，而不会受模式修饰符的限制。

前瞻断言(从当前位置向前测试)：`?=`     `?!`
比如/w+(?=;)/匹配一个单词后紧跟着一个分号，但匹配结果不会包含分号
foo(?!bar)匹配所有后面不紧跟bar的foo字符串

后瞻断言(从当前位置向后测试):`?<=`   `?<！`
(?<！foo)bar 用查找任何前面不是foo的bar字符串
多个断言(任意顺序)可以同时出现：
 (?<=\d{3})(?<！999)foo 匹配前面有三个数字但不是 ”999” 的字符串 ”foo”。注意， 每个断言*独立应用*到对目标字符串该点的匹配

##内部选项设置

模式修饰符：PCRE_CASELESS, PCRE_MULTILINE, PCRE_DOTALL, PCRE_UNGREEDY, PCRE_EXTRA, PCRE_EXTENDED and PCRE_DUPNAMES
语法为：`?修饰符`
简写方法：
i       for PCRE_CASELESS  
m       for PCRE_MULTILINE  
s       for PCRE_DOTALL  
x       for PCRE_EXTENDED  
U       for PCRE_UNGREEDY  
X       for PCRE_EXTRA  
J       for PCRE_INFO_JCHANGED  
例如：
在非子组中：
`/ab(?i)c/` 等价于 `/abc/i` 
在子组中有不同：
`/(a(?i)b)c/` 匹配 abc和aBc
在包含分支的子组中,修饰符会穿透到后面的分支：
`/(a(?i)b|c)/` 匹配 ab aB c 和C

##子组
通过圆括号分隔界定();

##重复/量词
{}  * + ?
默认情况下，量词都是贪婪的，加入?禁止贪婪

如果 PCRE_UNGREEDY 选项被设置(一个在 perl 中不可用的选项)， 那么量词默认情况下就是非贪婪的了。但是， 单个的量词可以通过紧跟一个 ? 来使其成为贪婪的。换句话说， PCRE_UNGREEDY 这个选项逆转了贪婪的默认行为。 

量词后面紧跟一个 ”+” 是”占有”性。它会吃掉尽可能多的字符， 并且不关注后面的其他模式，

##后向引用
在一个字符类外面， 反斜线紧跟一个大于 0 (可能还有一位数)的数字就是一个到模式中之前出现的某个捕获组的后向引用。
如：
模式(sens|respons)e and \1ibility

##一次性子组
对于同时有最大值和最小值量词限制的重复项， 在匹配失败后， 紧接着会以另外一个重复次数重新评估是否能使模式匹配。 当模式的作者明确知道执行上没有问题时， 通过改变匹配的行为或者使其更早的匹配失败以阻止这种行为是很有用的。
语法符号：(?>)_
如：(?>\d)bar

##条件子组
语法为： 
(?(condition)yes-pattern)
(?(condition)yes-pattern|no-pattern)
```
(?(?=[^a-z]*[a-z])
\d{2}-[a-z]{3}-\d{2}  |  \d{2}-\d{2}-\d{2} )
这个模式匹配两种格式的字符串：dd-aaa-dd 或 dd-dd-dd。aaa 代表小写字母， dd 是数字。
```

##注释 
(?# 注释内容)

##模式修饰符 
i       不区分大小写
m       多行匹配
s       .可以匹配任何字符，包括换行符，一个取反字符类[^a]总是可以匹配换行符

##PCRE函数
preg_filter() 执行一个正则表达式搜索和替换 
```
参数:preg_filter($pattern,$replacement,$subject[,int $limit  = -1  [, int &$count  ]] )
```
preg_grep(string $pattern  , array $input  [, int $flags  = 0  ] )返回给定数组 input 中与模式 pattern  匹配的元素组成的数组. 
```
flags:设置为 PREG_GREP_INVERT , 这个函数返回输入数组中与 给定模式 pattern  不匹配的元素组成的数组.
```

preg_last_error() 返回最后一次PCRE正则执行的错误代码
preg_match_all()
```
int preg_match_all(string $pattern,string $subject  [, array &$matches  [, int $flags  = PREG_PATTERN_ORDER    [, int $offset  = 0  ]]] )
搜索 subject 中所有匹配 pattern 给定正则表达式 的匹配结果并且将它们以 flag 指定顺序输出到 matches 中. 
flags  可以结合下面标记使用(注意不能同时使用 PREG_PATTERN_ORDER 和 PREG_SET_ORDER )： 
```
preg_match()
```
int preg_match  ( string $pattern  , string $subject  [, array &$matches  [, int $flags  = 0  [, int $offset  = 0  ]]] )
搜索 subject 与 pattern 给定的正则表达式的一个匹配，返回0或1，该函数匹配到一次就不会继续匹配了
```
preg_quote() 正则表达式字符 
```
string preg_quote  ( string $str  [, string $delimiter  = NULL    ] )
```
preg_replace_callback()
```
mixed  preg_replace_callback  ( mixed  $pattern  , callable  $callback  , mixed  $subject  [, int $limit  = -1  [, int &$count  ]] )
执行一个正则表达式搜索并且使用一个回调进行替换 
callback:一个回调函数，在每次需要替换时调用，调用时函数得到的参数是从 subject  中匹配到的结果。回调函数返回真正参与替换的字符串。
```
preg_split()通过一个正则表达式分隔字符串 
array preg_split  ( string $pattern  , string $subject  [, int $limit  = -1  [, int $flags  = 0  ]] )


###命名空间
在PHP中，命名空间用来解决在编写类库或应用程序时创建可重用的代码如类或函数时碰到的两类问题： 
1、用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。  
2.  为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高源代码的可读性。 

虽然任意合法的PHP代码都可以包含在命名空间中，但只有三种类型的代码受命名空间的影响，它们是：类，函数和常量。 

命名空间通过关键字namespace 来声明。如果一个文件中包含命名空间，它必须在其它所有代码之前声明命名空间。 

*定义子命名空间
与目录和文件的关系很象，PHP 命名空间也允许指定层次化的命名空间的名称。因此，命名空间的名字可以使用分层次的方式定义： 


*在同一个文件中定义多个命名空间

也可以在同一个文件中定义多个命名空间。在同一个文件中定义多个命名空间有两种语法形式。 



///////////////////////////////////////////////////////////////////////////////
//////////////////                cookie                  /////////////////////
///////////////////////////////////////////////////////////////////////////////

cookie和会话
浏览器会将对应的cookie编码进header和请求头一起发送到服务器，寻找cookie是靠域名或url来寻找的
cookie是http头的一部分，因此要在发送html之前调用`setcookie()`,当用户再次访问站点时，会自带cookie，服务器将此数据解码存储在全局变量`$_COOKIE`中，注意：当一个cookie被删除时，它的值在当前页仍然有效，如果把cookie设置成浏览器关闭后就失效，那么可以直接把时间设置成0或者不设置此值
注意事项：
```
1、setcookie()之前不能有任何html输出，就是空格都不行，必须在html文件的内容输出前设置
2、setcookie()后，在当前页还不能访问，必须刷新第二次进入时才能访问里面的变量
3、不同的浏览器对cookie处理不同，客户端可以禁用cookie，浏览器也会限制cookie数量，一个浏览器能创建的cookie数量最多为300个，并且每个不能超过4k,每个站点能设置的cookie总数不能超过20个
4、cookie是保存在客户端的，用户禁用了cookie,你的cookie也就没用了，避免过度依赖cookie，要想好如果cookie被禁用时的解决方案
```
setcookie()
```
语法：bool setcookie  ( string $name  [, string $value  [, int $expire  = 0  [, string $path  [, string $domain  [, bool $secure  = false  [, bool $httponly  = false  ]]]]]] )
一旦设置了cookie，就可以在另一个网页上获取$_COOKIE或$HTTP_COOKIE_VARS（老版本）数组，也可以通过$_REQUEST获取
参数：
 cookie名字
 cookie值
 cookie的生命周期
 cookie适用的路径，即在这些路径都可以访问
 cookie适用的域名空间
 返回布尔值，如果在之前有html输出，则设置失败返回false,否则返回true，即使客户端浏览器禁用了cookie也会返回true
eg.
<?php
$value  =  'something from somewhere' ;

 setcookie ( "TestCookie" ,  $value );
 setcookie ( "TestCookie" ,  $value ,  time ()+ 3600 );   /* expire in 1 hour */
 setcookie ( "TestCookie" ,  $value ,  time ()+ 3600 ,  "/~rasmus/" ,  "example.com" ,  1 );
 ?> 

删除cookie时只需要将cookie的有效期设置过去
```
setrawcookie()
```
发送一个原生的cookie到浏览器，即cookie的值不被编码(urlencoding),保留原有的格式，如逗号 句号 分号 
语法：同setcookie；
bool setrawcookie  ( string $name  [, string $value  [, int $expire  = 0  [, string $path  [, string $domain  [, bool $secure  = false  [, bool $httponly  = false  ]]]]]] )
```





/////////////////////////////////////////////////////////////////////////////////////////////               SESSION               ///////////////////////////
/////////////////////////////////////////////////////////////////////////////
会话支持
session-id  唯一，存储在cookie,也可以通过url传递
$_SESSION全局数组
配置保存路径：session.save_path 
运行时的配置：session.save_path 
              session.name 指定会话名以用作cookie存贮
              session.auto_start 请求开始是否自动启动一个会话
              session.serialize_handler 
              session.gc_probability 与 session.gc_divisor 垃圾回收gc_probability/gc_divisor 计算得来
              session.gc_maxlifetime session的生命周期
              session.referer_check  
              session.entropy_file 
              session.entropy_length 
              session.use_cookies 
              session.use_only_cookies 
              session.cookies_lifetime 
              session.cookie_path
              session.cookie_domain 
              session.cookie_secure 
              session.cookie_httponly 
            ? session.cache_limiter 
            ? session.cache_expore
            ? session.use_trans_sid  透明sid
            ？session.hash_function 
            ? session.hash_bits_per_character 
            ? url_rewroter.tags 
           ???? ? session.upload_progress.enabled 
            ? session.upload_progress.cleanup 
            ? session.upload_progress.prefix 
            ? session.upload_progress.name 
            ? session.upload_progress.freq 
            ? session.upload_progress.min-freq 

此扩展未定义资源类型

预定义常量：
        sid 
        PHP_SESSION_DISABLED
        PHP_SESSION_NONE
        PHP_SESSION_ACTIVE

Sessions follow a simple workflow. When a session is started, PHP will either retrieve an existing session using the ID passed (usually from a session cookie) or if no session is passed it will create a new session. 

If the session.auto_start directive is set to 1 , a session will automatically start on request startup. 
```
开启一个session并存入数据
<?php
session_start();
if(!isset($_SESSION["count"])){
    $_SESSION["count"]=0;
}else{
    $_SESSION["count"]++;
}
echo $_SESSION["count"];
?>

获取session文件中变量值
<?php
session_start();//获取session值必须开启
echo $_SESSION["count"];

?>
unset($_SESSION["count"]);//删除一个session中的变量，此时不可以访问

session文件锁：
当session在一个脚本里开启后，其他脚本在此脚本执行结束或
使用session_write_close()之前，都不能访问session文件，进而
不能读取数据
File based sessions (the default in PHP) lock the session file once a session is opened via session_start()  or implicitly via session.auto_start. Once locked, no other script can access the same session file until it has been closed by the first script terminating or calling session_write_close() . 
```
#基于此，session使用完后要及时关掉，session_write_close()
 The easiest way to deal with it is to call session_write_close()  as soon as any required changes to the session have been made, preferably early in the script. 

#传递SESSION-ID
两种方法：
    1、cookie
    2、url参数
sid是在第一次开启session时创建的，再次访问时就默认为空值
可以获得方法：echo $_COOKIE["PHPSESSID"];
SID  which is defined if the session started
如果禁用了cookie， it has the form session_name=session_id. Otherwise,此时就可以通过设置session.use_trans_sid来通过url传递，$_GET获取
```
<p>
To continue, <a href="nextpage.php?<?php  echo  htmlspecialchars ( SID );  ?>">click
here</a>.
</p> 
在另一文件：
$_GET["sid"];//这时sid即为地址
```
sesson生命周期：
    open-read-write-close[-destroy-gc]


session安全:
    session.use_only_cookies 

##session函数：
session_cache_expire()
```
读取或设置会话缓存的时间（分钟计）;要放在session_start()之前才生效
```
session_cache_limiter()
```
指定会话页面所使用的缓冲控制方法;用处是让表单history.go(-1)的时候，填写内容不丢失！就避免页面失效的警告;    这个会话与header('cache-control:private,must_revalidate');效果相同
但是要值得注意的是session_cache_limiter()方法要写在session_start()方法之前才有用;
```
session_commit()
```
session_write_close()的别名
```
session_destroy()
``` 
删除存储的某一session文件;但该sessionid还存在客户端的cookie中
```
unset()
```
删除session中的某一变量和值，但保留session文件；也可以使用$_SESSION=array()删除所有变量和值
```
setcookie()
```
删除通过更改sessionid的时间可以删除sessionid
setcookie(session_name(),"",time()-3600);          
```
session_name()
```
session-id存在cookie中的名字
```
session_encode()
```
将当前会话数据编码为一个字符串,返回当前会话编码后的内容,就是session文件里存储的内容格式，但使用$_SESSION取得变量时，会自动解码为PHP数组格式
```
session_get_cookie_params()
```
获得设置sessionid到cookie时的所有设置参数数组(不需要打开session即可获得)，其实就是对应cookie的后面几个参数，包括：lifetime-该cookie生命期，path-用于的路径，domain-用于的域名，secure-安全方面，httponpy-指定该cookie只可以通过http访问到
以上信息也可以在php.ini中设置默认值
```
ini_get(string参数)
```
可以通过ini_get()函数获得配置文件中的值
```
session_id()
```
获得或者设置session-id值(此时会替换原值存在cooke上的值，并在服务器上存有新的对应session文件)，设置要在session_start之前方才生效
```
session_is_registered()
```
5.3版本以废弃，5.4版本已移除
```
session_module_name()
```
获得或者设置当前session module ;默认情况下SESSION 数据是以文件方 式保存，想要使用数据库方式保存，就必 须重新定义SESSION 各个操作的处理函 数。PHP 提供了 session_set_save_handle() 函数，可以用此函数自定义SESSION 的处理过程，当然首先要先将 session.save_handler 改成user，可在 PHP 中进行设置：session_module_name('user');
```
session_name()
```
设置(在start之前)或者获取当脚本sessionid存储在cookie中的名字，如PHPSSID；在cookie他和session_id是一对键与值;设置为新的值后会对应生成一个新的sessionid，对应生成一个新的session文件在服务器
```
session_regenerate_id()
```
重新生成一个当前的sessionid，代替旧的，旧文件中的信息同步到新文件，(在start之后运行方生效)，但旧文件中的数据还保存，可以加上字符串参数"delete_old_session"删除旧的session文件;
```
session_register()
```
为session定义变量或赋值，完全可以通过$_SESSION[变量名]来设置
5.3版本以废弃，5.4已经移除
```
session_save_path()
```
获取或者设置session文件保存的目录，设置时需要在start之前
```
session_set_cookie_params()
```
设置session在cookie上的参数，没有返回值
语法：session_set_cookie_params  ( int $lifetime  [, string $path  [, string $domain  [, bool $secure  = false  [, bool $httponly  = false  ]]]] )
```
session_save_handler()
```
用户自定义session的操作方式
语法： session_set_save_handler  ( callable  $open  , callable  $close  , callable  $read  , callable  $write  , callable  $destroy  , callable  $gc  )
===================
<?php
 class  FileSessionHandler
 {
    private  $savePath ;

    function  open ( $savePath ,  $sessionName )
    {
         $this -> savePath  =  $savePath ;
        if (! is_dir ( $this -> savePath )) {
             mkdir ( $this -> savePath ,  0777 );
        }

        return  true ;
    }

    function  close ()
    {
        return  true ;
    }

    function  read ( $id )
    {
        return (string)@ file_get_contents ( " $this -> savePath /sess_ $id " );
    }

    function  write ( $id ,  $data )
    {
        return  file_put_contents ( " $this -> savePath /sess_ $id " ,  $data ) ===  false  ?  false  :  true ;
    }

    function  destroy ( $id )
    {
         $file  =  " $this -> savePath /sess_ $id " ;
        if ( file_exists ( $file )) {
             unlink ( $file );
        }

        return  true ;
    }

    function  gc ( $maxlifetime )
    {
        foreach ( glob ( " $this -> savePath /sess_*" ) as  $file ) {
            if ( filemtime ( $file ) +  $maxlifetime  <  time () &&  file_exists ( $file )) {
                 unlink ( $file );
            }
        }

        return  true ;
    }
}

 $handler  = new  FileSessionHandler ();
 session_set_save_handler (
    array( $handler ,  'open' ),
    array( $handler ,  'close' ),
    array( $handler ,  'read' ),
    array( $handler ,  'write' ),
    array( $handler ,  'destroy' ),
    array( $handler ,  'gc' )
    );

 // the following prevents unexpected effects when using objects as save handlers
 register_shutdown_function ( 'session_write_close' );

 session_start ();
 // proceed to set and retrieve values by key from $_SESSION 

```
session_start()
```
开始新的或者使用已存在的session,返回布尔值
```
session_status()
```
返回当前的session状态
值       说明
1         PHP_SESSION_DISABLED  if sessions are disabled.session被禁用，在session_start之前也会是1 
2         PHP_SESSION_NONE  if sessions are enabled, but none exists.
3         PHP_SESSION_ACTIVE  if sessions are enabled, and one exists. 
```
session_unset();
```
清除当前所有的session变量和值,等同于$_SESSION=array()
```
session_write_close()
```
结束当前session访问，并将数据保存到session文件
```


????????sesion_save_handeler
/////////////////////////////////////////////////////////


###？？？？？？？？安全 
平衡安全性和可用性

#文件系统安全

//////////////////////////文件处理////////////////////////////
文件系统和流配置选项
allow_url_fopen
```
可以打开网站代码
```
////////////////////Directory类//////////////////////////////////
Directory实例是通过dir()函数来创建的，而不是new操作符，即$dir=dir();而不是$dir=new dir();
类介绍：
```
Directory  {

/* 属性 */
public string $path   ;
public resource $handle   ;

/* 方法 */
public void close  ([ resource $dir_handle  ] )
public string read  ([ resource $dir_handle  ] )
public void rewind  ([ resource $dir_handle  ] )
}
说明：
path:被打开的目录地名字,与实例化时传入的文件名一样
handle:目录句柄
eg.
        $dir=dir('./test1');
        echo $dir->path."\n";
        echo $dir->handle."\n";
        while($v=readdir($dir->handle))
        {
            echo $v."\n";
        }
        $dir->close();
方法：
    close()释放目录句柄，与closedir()功能相同，只是默认为$this
    read()从目录句柄中读取条目，与readdir()功能相同，默认为$this
    rewind()倒回目录句柄，与rewinddir()功能相同，默认为$this

```

//////////////////////Directory目录处理函数////////////////////////
1. chdir
```
1. chdir — 改变目录，只接受一个参数，为目录名，将PHP的当前目录改为指定的目录
成功返回true,失败返回false
// current directory
echo  getcwd () .  "\n" ;
 chdir ( 'test1' );
 // current new directory
 echo  getcwd () .  "\n" ;
```
2. chroot
```
2. chroot — 改变根目录,只接受一个参数，将当前进程的根目录改为新的目录
成功返回true，失败返回false,win平台不能实现
```
3. closedir
```
3. closedir — 关闭目录句柄,只接受一个参数，为opendir()打开的目录句柄，没有返回值
closedir($dir);
```
4. dir
```
4. dir — 返回一个 Directory 类实例,只接受两个参数，第一个参数指定目录名名称，第二个参数指定上下文context
该函数以面向对象的方式范文m目录，
成功返回一个目录实例，参数错误返回null，其他返回false
print_r ( dir('test1') );//打印对象，返回数组，键值为path handle

$dir=dir('test1');
echo $dir->path."\n";
echo $dir->handle."\n";
while(false !== ($v=$dir->read()))
{
    echo $v."\n";
}
$dir->close();

```
5. getcwd
```
5. getcwd — 取得当前工作目录,不接受任何参数
成功返回当前工作目录，失败返回false,
echo getcwd();
```
6. opendir
```
6. opendir — 打开目录句柄,指接受两个参数，第一个参数为目录路径，第二个参数为可选，指定上下文context
成功返回目录句柄，失败(非法目录或没有权限)返回false和警告
opendir("test");
```
7. readdir
```
7. readdir — 从目录句柄中读取条目,接受一个可选的参数，指定目录句柄
返回目录中下一个文件的文件名。文件名以在文件系统中的排序返回，每次读取目录指针向下移动一步
成功返回文件名，失败返回false
$dir=opendir("test1");
while($v=readdir($dir)){
    echo $v."\n";
}
closedir($dir);
```
8. rewinddir
```
8. rewinddir — 倒回目录句柄,将目录指针指向目录开头，只接受一个参数，为目录句柄
没有返回值
$dir=opendir("test1");
while($v=readdir($dir)){
    echo $v."\n";
}
rewinddir($dir);//回到目录开头
echo readdir($dir);
closedir($dir);
```
9. scandir
```
9. scandir — 列出指定路径中的文件和目录只接受三个参数，第一个为必选参数，指定目录名称，第二个为可选参数指定排序，第三个为可选参数为上下文context
成功返回包含文件和目录的索引数组，失败返回false，如果指定的不是一个目录则产生false和错误
第二个参数默认安字母升序排列，如果指定为1，则按降序排列
print_r(scandir("test1"));

print_r(scandir("test1",1));//降序
```


///////////////////////////////文件处理函数///////////////////////
1. basename
```
1. basename — 返回路径中的文件名部分
echo basename("C:/WEEW/WEE/wee/w/.e/e.ph..p");//输出最后一个/后面的内容，由此可见它的原理就是取最后一个/之后的所有
当提供第二各参数时，会去掉与第二个参数内容完全相同的最后的字符串，否则不去除
echo basename("C:/WEEW/WEE/wee/w/.e/e.ph..p","..p");// e.ph 
echo basename("C:/WEEW/WEE/wee/w/.e/e.ph..p","t..p");// e.ph..p因为不匹配
该函数会忽略结尾的/字符，即
echo basename("C:/WEEW/WEE/wee/w/.e/e.ph..p/","t..p");// e.ph..p,不考虑最后的/
当找不到非最后的/时，就将整体字符串原样输出
注意：最好使用单引号，避免转义
```

```
2. chgrp — 改变文件所属的组
3. chmod — 改变文件模式
4. chown — 改变文件的所有者
5. clearstatcache — 清除文件状态缓存
```
6. copy
```
6. copy — 拷贝文件,将文件从原始地拷贝到目标地，会覆盖同名文件，成功返回true，失败返回false
// echo basename("C:WEEWWEEweew.e","t..p");
$sourse='D:\wamp\www\PHPstudy\test.txt';//相对绝对路径均可，包含文件名
$dest='D:\wamp\www\PHPstudy\test1\test.txt';//必须包括拷贝后的文件名,相对绝对路径均可
if(copy($sourse,$dest)){
    echo "拷贝成功";
}else{
    echo "拷贝失败";
}
```
7. unlink
```
7. unlink— 删除文件，成功返回true否则返回false
$dest='./test1/testt.txt';//相对绝对路径均可，包含文件名
if(unlink($dest)){
    echo "删除成功";
}else{
    echo "删除失败";
}
```
8. dirname
```
8. dirname — 返回路径中的目录部分
与basename操作正好相反，它截取之前的部分，注意不包含分开处的/符号，即两个函数都不包含这个/
$file='D:\wamp\www\PHPstudy\test1\t.txt';
echo dirname($file);// D:\wamp\www\PHPstudy\test1,使用单引号避免转义
```
9. disk_free_space
```
9. disk_free_space — 返回目录中或目录所在磁盘的可用空间,字节数
注意：是目录，即可以有dirname返回的，1k=1024字节
$file='D:\wamp\www\PHPstudy\test1\t.txt';
echo disk_free_space(dirname($file))/1024/1024/1024; // 打印出G级容量
```
10. disk_total_space
```
10. disk_total_space — 返回一个目录或目录所在磁盘的磁盘总大小
注意事项同上；
$file='D:\wamp\www\PHPstudy\test1\t.txt';
echo disk_total_space(dirname($file))/1024/1024/1024; 
```
11. diskfreespace — disk_free_space 的别名
12. fclose
```
12. fclose — 关闭一个已打开的文件指针，参数是文件通过fopen或fsockopen打开的句柄
成功返回true否则返回false
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"xb");
if($file){
    echo "文件打开成功";
}else{
    echo "文件打开失败";
}
fclose($file);
```
13. feof 
```
13. feof — 测试文件指针是否到了文件结束的位置,接受一个fopen和fsockopen打开的文件句柄
，在fclose()之前，到了返回true否则返回false
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"wb");
var_dump(feof($file));//即使清空源文件，会将指针指向开始，但这样不代表到了最后
fclose($file);
```
????14. fflush
```
????14. fflush — 将缓冲内容输出到文件，只接受一个文件资源参数，会将所有的缓冲输出都写入该资源指向的文件中(为fclose关闭)，成功返回true否则返回false

```
15. fgetc
```
15. fgetc — 从文件指针中读取一个字符，只接受一个文件资源句柄，返回该字符，碰到EOF则返回false或非false的布尔值
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"w+b");
$str=<<<str
haha本函数强制将所有缓冲的输出写入 handle  文件句柄所指向的资源。 成功时返回 TRUE ， 或者在失败时返回 FALSE 。 

文件指针必须是有效的，必须指向由 fopen()  或 fsockopen()  成功打开的文件(并还未由 fclose()  关闭)。
str;
$content=fwrite($file,$str);
rewind($file);//移动文件指针到开头
echo fgetc($file);//打印出 h
fclose($file);
```
16. fgetcsv
```
16. fgetcsv — 从文件指针中读入一行并解析 CSV 字段

```
17. fgets
```
17. fgets — 从文件指针中读取一行,接受两个参数，第一个参数为必需参数，为文件资源句柄，第二个参数为可选，指定返回长度为该参数-1的字符串，如果没有指定长度则默认为1k或1024字节，保留了html标记
返回读取的字符串，否则(没有可以读取的数据或出错)返回false
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"r+b");
$len=123;
$content=fgets($file,$len);
echo $content;
fclose($file);

不指定长度
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"r+b");
$len=123;
$content=fgets($file);
echo $content;
fclose($file);
```
18. fgetss
```
18. fgetss — 从文件指针中读取一行并过滤掉 HTML 标记，其他同fgets()
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"r+b");
$len=123;
$content=fgetss($file);
echo $content;
fclose($file);
```
19. file_exists
```
19. file_exists — 检查文件或目录是否存在,只接受一个参数，传入字符串表示的文件或目录，存在返回true，否则返回false
$file='D:\wamp\www\PHPstudy\test1\test.txt';//文件
var_dump(file_exists($file));

$file='D:\wamp\www\PHPstudy\test1';//目录
var_dump(file_exists($file));
```
20. file_get_contents
```
20. file_get_contents — 将整个文件读入一个字符串，接受5个参数，第一个为必须参数，指定要读取的文件名包含路径而非资源句柄，第二参数可选参数指定是否使用配置中的include_path,第三次个参数指定文章环境context，第四个参数指定读取文件开始的指针位置，第五个参数指定读取的最大长度
返回读取的内容，失败返回false
该函数不会过滤html标签，可用于二进制对象
$file='D:\wamp\www\PHPstudy\test1\test.txt';
$content=file_get_contents($file);//不能过滤html标签
echo $content;

从10位开始读起
$file='D:\wamp\www\PHPstudy\test1\test.txt';
$content=file_get_contents($file,false,null,10);
echo $content;

读取网络内容
$lines="http://www.baidu.com";
$content=file_get_contents($lines);
var_dump($content);
```
21. file_put_contents
```
21. file_put_contents — 将一个字符串写入文件,和依次调用fopen fwrite fclose功能一样，接收4个参数，2个必需参数，第一个为写入的文件名，第二个为要写入的数据（字符串或数组），第三个可选参数为写入时的模式，第四个可选参数为context资源
第三个参数可选值：FILE_USE_INCLUDE_PATH 指在include_path中搜索
                  FILE_APPEND 指文件已经存在时追加内容
                  LOCK_EX 指在文件写入操作时获得对文件的独占锁
如果文件不存在，则创建
该函数返回写入的字节数，否则返回false或等同于false的布尔值
$file='D:\wamp\www\PHPstudy\test1\tt.txt';
$str=<<<str
要写入的数据。类型可以是 string ， array  或者是 stream  资源（如上面所说的那样）。 

如果 data  指定为 stream 资源，这里 stream 中所保存的缓存数据将被写入到指定文件中，这种用法就相似于使用 stream_copy_to_stream()  函数。 

参数 data  可以是数组（但不能为多维数组），
str;
$len=file_put_contents($file,$str,FILE_APPEND);
echo $len;
```
22. file 
```
22. file — 把整个文件读入一个数组中,接受三个参数，第一个为必选参数文件名称包含路径而非文件句柄，第二个可选参数指定读入的模式，第三个为可选参数context资源
第二个参数可能值：FILE_USE_INCLUDE_PATH 
                  FILE_IGNORE_LINES  在数组每个元素的末尾不要添加换行符
                  FILE_SKIP_EMPTY_LINES 跳过空行
返回数组，数组中每一个元素对应一行(包括换行符除非设置第二个参数为FILE_IGNORE_NEW_LINES)，读取失败返回false
读取网络内容
$file=file("http://www.baidu.com");
var_dump(implode("",$file));
```
23. fileatime
```
23. fileatime — 取得文件的上次访问时间,仅接受一个参数，为文件名包含路径
返回时间戳，失败返回false
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
echo Date("Y-M-D h:i:s",fileatime($filename));
```
24. filectime
```
24. filectime — 取得文件的 inode 修改时间,仅接受一个参数，为文件名包含路径
返回时间戳，失败时返回false
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
echo Date("Y-M-D h:i:s",fileatime($filename));
```

```
???????25. filegroup — 取得文件的组的ID,仅接受一个参数，为文件名包含路径
返回所属组ID，失败时返回false


```

```
????????26. fileinode — 取得文件的 inode

```
27. filemtime
```
27. filemtime — 取得文件修改时间,仅接受一个参数，为文件名包含路径
返回时间戳，失败时返回false
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
echo Date("Y-M-D h:i:s",filemtime($filename));
```

```
??????28. fileowner — 取得文件的所有者,接受一个文件名包含路径的参数，放回所有的用户ID，否则返回false

```
29. fileperms
```
29. fileperms — 取得文件的权限

```
30. filesize
```
30. filesize — 取得文件大小,只接受一个参数，为文件的名称包含路径，返回文件大小(字节数)，如果出错返回false,并生成一条警告信息，不能操作目录
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
echo filesize($filename);
```
31. filetype
```
31. filetype — 取得文件类型,只接受一个参数，为文件的名字包含路径，返回文件的类型，包括fifo\char\dir\block\link\file和unknown，如果出错则返回false
$filename='D:\wamp\www\PHPstudy\test1';
echo filetype($filename);//dir

$filename='D:\wamp\www\PHPstudy\test1\test.txt';
echo filetype($filename);// file
```
32. flock
```
32. flock — 轻便的咨询文件锁定,接受三个参数，第一个为必须参数没文件资源句柄，第二个参数为可选参数，为操作模式，第三个为可选参数
第二个参数的可能值为：
        LOCK_SH 取得共享锁定-读取程序
        LOCK_EX 取得独占锁定-写入程序
        LOCK_UN 释放锁定-无论共享或独占
        LOCK_NB 

<?php 
public static function getContents($path, $waitIfLocked = true) { 
    if(!file_exists($path)) { 
        throw new Exception('File "'.$path.'" does not exists'); 
    } 
    else { 
        $fo = fopen($path, 'r'); 
        $locked = flock($fo, LOCK_SH, $waitIfLocked); 
         
        if(!$locked) { 
            return false; 
        } 
        else { 
            $cts = file_get_contents($path); 
             
            flock($fo, LOCK_UN); 
            fclose($fo); 
             
            return $cts; 
        } 
    } 
} 
?>

file1.php
header("Content-Type:text/html;charset=utf-8");
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+");
flock($file,LOCK_EX);
sleep(10);
flock($file,LOCK_UN);
fclose($file);

file2.php
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$content=file_get_contents($filename);//在锁定期内无法获得
echo $content;
```
33. fnmatch
```
？？？？？？？33. fnmatch — 用模式匹配文件名，移植性不好
```
34. fopen
```
34. fopen—打开文件或者URL,两个必须参数，第一个为文件名包含路径或url，第二个为打开的模式
主要模式分类：
r   r+   w   w+    a   a+  x   x+  c  c+   
注意：为移植性考虑，总是在模式中增加b标记，即 "rb"
该函数成功返回资源，失败返回false
以下为演示，不进行文件存在性判断
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"rb");//以只读方式
if($file){
    echo "文件打开成功";
}else{
    echo "文件打开失败";
}
fclose($file);//打开的资源资源要关闭，节省内存

$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"wb");//w方式打开，清除原内容，w+也如此
if($file){
    echo "文件打开成功";
}else{
    echo "文件打开失败";
}
fclose($file);

$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"xb");//文件存在，返回错误，不存在会创建
if($file){
    echo "文件打开成功";
}else{
    echo "文件打开失败";
}
fclose($file);
```
35. fpassthru
```
35. fpassthru — 输出文件指针处的所有剩余数据到输出缓冲区，只接受一个文件资源句柄参数，返回字符串及个数失败返回false
注意：已经向文件写入数据，文件指针就会在末尾，这时应该调用rewind来将文件指针指向开头
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
fpassthru($file);//自动将文件内容输出到屏幕
fclose($file);
```

```
?????????36. fputcsv — 将行格式化为 CSV 并写入文件指针
```
37. fputs
```
37. fputs — fwrite 的别名
```
38. fread
```
38. fread — 读取文件（可安全用于二进制文件，加上b模式标记）,接受两个参数，第一个参数是文件资源句柄，第二根资源是要读取的字符串最大长度（到文件末尾时自动停止读取）
成功返回读取的字符串，失败返回false
$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"r+b");
$len=12;
$content=fread($file,$len);
echo $content;
fclose($file);
```

```
??????????????39. fscanf — 从文件中格式化输入

```
40. fseek
```
40. fseek — 在文件指针中定位,设定文件指针的位置，接受三个参数，第一个为必选参数为文件资源句柄，第二个参数为可选参数指定长度，第三个可选参数指定第二个参数匹配的模式
第三个参数可选值：
            SEEK_SET 设定位置等于offset字节(第二个参数控制)
            SEEK_CUR 设定位置为当前位置加上offset
            SEEK_END 设定位置为文件尾加上offset

$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
fseek($file,10,SEEK_END);//结尾后10个字节
fpassthru($file);
flock($file,LOCK_UN);
fclose($file);

$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
fseek($file,10,SEEK_CUR);//当前位置后10个字节
fpassthru($file);
flock($file,LOCK_UN);
fclose($file);

$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
fseek($file,10,SEEK_SET);//开始位置后10个字节
fpassthru($file);
flock($file,LOCK_UN);
fclose($file);
```
41. fstat
```
41. fstat — 通过已打开的文件指针取得文件信息,只接受一个参数，为文件资源句柄，返回一个包含文件统计信息的数组(包括索引和关联)
echo "<pre>";
header("Content-Type:text/html;charset=utf-8");
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
print_r(fstat($file));
输出：Array( 
    以下关联的索引形式，
    [dev] => 0
    [ino] => 0
    [mode] => 33206
    [nlink] => 1
    [uid] => 0
    [gid] => 0
    [rdev] => 0
    [size] => 9
    [atime] => 1464429744
    [mtime] => 1464458190
    [ctime] => 1464429744
    [blksize] => -1
    [blocks] => -1
)
flock($file,LOCK_UN);
fclose($file);
```
42. ftell
```
42. ftell — 返回文件指针读/写的位置,只接受一个文件资源句柄参数，返回数字型，如果出错返回false
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"r+b");
flock($file,LOCK_EX);
fseek($file,10);
echo ftell($file);
flock($file,LOCK_UN);
fclose($file);
```
43. ftruncate
```
43. ftruncate — 将文件截断到给定的长度,接受两个必须参数，第一个参数为文件资源句柄，第二个参数为截取的长度，成功返回true失败返回false
如果给定长度大于文件大小，则以null值补充；
如果给定长度小于文件大小，则截取
该函数截取总是从文件头开始截取指定长度，删除剩余内容
$filename='D:\wamp\www\PHPstudy\test1\test.txt';
$file=fopen($filename,"a");
flock($file,LOCK_EX);
ftruncate($file,10);//截取10个字节，其余删除
flock($file,LOCK_UN);
fclose($file);
```
44. fwrite
```
44. fwrite — 写入文件（可安全用于二进制文件）,接受两个必须的参数，第一个为文件资源句柄，第二个为要写入的字符串，可选的第三个参数指定写入的长度或(如果长度大于第二字符串的长度)写完后停止
成功返回写入的字符数，否则false

$file=fopen('D:\wamp\www\PHPstudy\test1\test.txt',"wb");
$content=<<<str
If handle  was fopen() ed in append mode, fwrite() s are atomic (unless the size of string  exceeds the filesystem's block size, on some platforms, and as long as the file is on a local filesystem). That is, there is no need to flock()  a resource before calling fwrite() ; all of the data will be written without interruption. "
str;
echo $content."<br/>";
$len=fwrite($file,$content);
if(!$len==false){
    echo "文件写入成功";
}else{
    echo "文件写入失败";
}
fclose($file);
```


```
？？？？？45. glob — 寻找与模式匹配的文件路径
```
46. is_dir 
```
46. is_dir — 判断给定文件名是否是一个目录,只接受一个参数，为文件名称，如果文件存在并且是目录则返回true否则返回false
$filename='D:\wamp\www\PHPstudy\test1';
var_dump(is_dir($filename));// true

$filename='D:\wamp\www\PHPstudy\test1\test.txt';
var_dump(is_dir($filename));// false
```
47. is_executable
```
47. is_executable — 判断给定文件名是否可执行,只接受一个文件名参数，如果文件存在并且可以执行则返回true，否则返回false
$filename='D:\wamp\www\PHPstudy\test1\text.txt';
var_dump(is_executable($filename));//false
```
48. is_file
```
48. is_file — 判断给定文件名是否为一个正常的文件,只接受一个文件名参数，如果文件存在且正常则返回true，否则返回false
$filename='test1/test.txt';
var_dump(is_file($filename));// true
```

```
????????49. is_link — 判断给定文件名是否为一个符号连接,只接受一个文件名参数，如果文件存在并且是一个符号链接则返回true，否则返回false
$filename='test1/test.txt';
var_dump(is_link($filename));
```
50. is_readable
```
50. is_readable — 判断给定文件名是否可读,只接受一个文件名参数，如果文件\目录存在并且可读则返回true,否则返回false
$filename='test1/test.txt';
var_dump(is_readable($filename));//该文件存在且可读

$filename='test1';
var_dump(is_readable($filename));//该目录存在且可读
```
51. is_uploaded_file
```
51. is_uploaded_file — 判断文件是否是通过 HTTP POST 上传的,只接受一个参数为文件名，这种检查格外重要，多用于检查$_FILES["userfile"]["tmp_name"]是否为上传文件，成功返回true，失败返回false;
$filename='pdf.pdf';
var_dump(is_uploaded_file($filename));//检查一个本地文件，false

var_dump(is_uploaded_file($_FILES["pic"]["tmp_name"]));//判断上传的临时文件，此时为true
```
52. is_writable
```
52. is_writable — 判断给定的文件名是否可写,只接受一个文件名或目录名参数，如果文件或目录存在并且可写，则返回true,否则返回false
判断文件
$filename='pdf.pdf';
var_dump(is_writable($filename));

判断目录：
$filename='./test1/';
var_dump(is_writable($filename));


$filename='./test1';
var_dump(is_writable($filename));

```
53. is_writeable
```
53. is_writeable — is_writable 的别名
```

```
?????54. lchgrp — Changes group ownership of symlink,改变符号链接的所属组群关系，接受两个参数，第一个为要修改的符号链接文件名，第二个为要更改的组
```

```
?????????55. lchown — Changes user ownership of symlink,修改符号链接的所有者，接受两个参数，第一个为要修改的符号链接文件名，第二个为要更改所有者
```

```
?????????????56. link — 建立一个硬连接，接受两个参数，第一个为要连接的目标，第二个为该链接的名称，成功返回true,否则返回false
```

```
57. linkinfo — 获取一个连接的信息
58. lstat — 给出一个文件或符号连接的信息
```
59. mkdir
```
59. mkdir — 新建目录,接受4个参数，第一个为必选参数，为创建的目录名，第二个为可选参数，设定对该新目录的访问权（默认为0777,即最大权利访问权）,第三个也是可选参数指定是否允许递归创建目录（默认为false,即不允许递归创建），第四个为可选参数，指定上下文context
成功返回true，失败返回false
if(mkdir("test/a/",0777,true)){
    echo "创建成功";
}else{
    echo "创建失败";//
}
如果目录已经存在，则返回false
if(mkdir("test1/a/",0777,true)){
    echo "创建成功";
}else{
    echo "创建失败";
}
可以在已存在目录的基础上创建，并不会覆盖原目录文件
if(mkdir("test1/a/b/c/e/f",0777,false)){//不允许递归创建
    echo "创建成功";
}else{
    echo "创建失败";
}
```
60. move_uploaded_file
```
60. move_uploaded_file — 将上传的文件移动到新位置,只接受两个参数，第一个参数指定上传的文件名，第二个参数指定移动的目标位置（包括新的文件名），该方法只能移动通过HTTP上传的文件，成功返回true,失败返回false
注意：该方法会覆盖上传的文件
if(!empty($_FILES)){
    if(is_uploaded_file($_FILES["pic"]["tmp_name"])){
        if(file_exists("./test/a") && !file_exists("./test/a/1.png")){
            echo move_uploaded_file($_FILES["pic"]["tmp_name"],"./test/a/1.png")?"文件上传且移动成功":"文件上传或移动失败";
        }
    }
}
```
61. parse_ini_file
```
61. parse_ini_file — 解析一个配置文件,该函数接受三个参数，第一个为必选参数，指定载入的文件名，第二个为可选布尔类型参数，指定是否显示详细信息（默认为false），第三个为可选参数指定输出的模式；
第三个参数可能值：INI_SCANNER_NORMAL INI_SCANNER_RAW
载入成功是以关联数组返回该文件的配置信息，否则返回false
echo "<pre>";
$arr=@parse_ini_file("test.ini");//加入抑制符
print_r($arr);

$arr=@parse_ini_file("test.ini",true);//显示更详细的信息
print_r($arr);

$arr=@parse_ini_file("test.ini",true，INI_SCANNER_NORMAL);
print_r($arr);
```
62. parse_ini_string
```
62. parse_ini_string — Parse a configuration string,解析一个配置字符串，参数parse_ini_file相同，只是第一个参数为一个配置的字符串格式，以关联数组的形式返回配置信息，失败返回false
$ini=file_get_contents("test.ini",false,null,0,filesize("test.ini"));
echo $ini;
$arr=@parse_ini_string($ini,true,INI_SCANNER_NORMAL);
print_r($arr);
```
63. pathinfo
```
63. pathinfo — 返回文件路径的信息,接受两个参数，第一个参数为必选参数，指定文件路径，第二个参数为可选参数，指定需要显示路径的个别信息
返回数组或字符串（第二个参数影响）
操作文件
$filename="test.txt";
print_r(pathinfo($filename));
输出： 
Array
(
    [dirname] => .
    [basename] => test.txt
    [extension] => txt
    [filename] => test
)

操作目录：
$filename="test";
print_r(pathinfo($filename));
输出 ：
Array
(
    [dirname] => .
    [basename] => test
    [filename] => test
)
```

```
????????????64. pclose — 关闭进程文件指针，只接收一个文件资源句柄，关闭popen()打开的指向管道的文件指针
返回运行的进程的终止状态，错误时返回-1
```

```
????????65. popen — 打开进程文件指针
```
66. readfile
```
66. readfile — 输出一个文件,接收三个参数，第一个为必选参数，指定文件名，第二个布尔类型参数指定是否使用include_path，第三个参数指定上下文context
该函数读取文件并写入到输出缓冲
该函数返回从文件中读入的数据，出错返回false并有错误信息
$filename="test.txt";
echo readfile($filename);
```

```
??????67. readlink — 返回符号连接指向的目标

```
68. realpath_cache_get
```
68. realpath_cache_get — Get realpath cache entries,返回缓存的绝对路径信息数组，不接收任何参数
var_dump(realpath_cache_get());
```
69. realpath_cache_size
```
69. realpath_cache_size — Get realpath cache size,返回缓存的绝对路路径信息所用的内存大小，不接受任何参数
```
70. realpath
```
70. realpath — 返回规范化的绝对路径名,只接受一个参数，为路径名，包括文件名
返回绝对路径，失败返回false
$filename="test.txt";
echo realpath($filename);// D:\wamp\www\PHPstudy\test.txt
```
71. rename
```
71. rename — 重命名一个文件或目录,接受两个必选参数，第一个参数指定原文件名或目录名，第二个文件指定新的文件名后目录名，第三个可选参数为上下文context
成功返回true否则返回false
$filename="test.txt";
if(rename($filename,"./test/a/".$filename)){
    echo "重命名成功";
}else{
    echo "重命名失败";
}
该函数有移动文件的效果，原文件被删除

对目录
$filename="test";
if(rename($filename,"./test1/".$filename)){
    echo "重命名成功";
}else{
    echo "重命名失败";
}
原目录被删除
```
72. rewind
```
72. rewind — 倒回文件指针的位置到开头，只接受换一个文件资源句柄参数，成功返回true否则返回false
注意：如果将文件以附加（"a" 或者 "a+"）模式打开，写入文件的任何数据总是会被附加在原内容的后面，不管文件指针的位置。
rewind($file);//参数是一个文件资源句柄
```
73. rmdir
```
73. rmdir — 删除目录，接受两个参数，第一个为必选参数，指定要删除的目录，第二个参数为可选参数指定上下文context
注意：要删除的目录，该目录必须是空的，而且有相应的权限，
成功返回true,失败时返回false和提醒
if(is_dir("test2")){
    if(rmdir("test2")){//要保证目录是空的
        echo "删除目录成功";
    }else{
        echo "删除目录失败";
    }

}
```

```
???????74. set_file_buffer — stream_set_write_buffer 的别名
```
75. stat
```
75. stat — 给出文件的信息,只接受一个文件名参数，获取文件的统计信息，功能与fstat相同只是接受的参数不同，fstat接受文件或目录句柄
返回统计数组，失败返回false
print_r(stat("test.ini"));
输出： 
Array( 
    以下关联的索引形式，
    [dev] => 0
    [ino] => 0
    [mode] => 33206
    [nlink] => 1
    [uid] => 0
    [gid] => 0
    [rdev] => 0
    [size] => 9
    [atime] => 1464429744
    [mtime] => 1464458190
    [ctime] => 1464429744
    [blksize] => -1
    [blocks] => -1
)
也可以操作目录
print_r(stat("test1"));
```

```
??????76. symlink — 建立符号连接
```
77. tempnam
```
77. tempnam — 建立一个具有唯一文件名的文件,只接受两个参数，第一个参数指定；临时文件创建的目录，第二个参数指定创建文件时的前缀（只取前三个字符）
如果该目录不存在， tempnam()  会在系统临时目录中生成一个文件，并返回其文件名。
返回新的临时文件名，失败返回false
echo tempnam("test1","haha");//D:\wamp\www\PHPstudy\test1\hah258A.tmp
新建了的文件类型为tmp
```
78. tmpfile 
```
78. tmpfile — 建立一个临时文件,该函数不接受任何参数，以w+的方式建立一个具有唯一名的临时文件，返回文件句柄，文件会在关闭后（fclose()）或者脚本运行结束时自动被删除;
成功返回文件句柄，失败返回false
```
sys_get_temp_dir()
```
sys_get_temp_dir()，不接受任何参数，返回系统的临时文件目录
echo sys_get_temp_dir();
输出： 
C:\WINDOWS\TEMP
```
79. touch 
```
79. touch — 设定文件的访问和修改时间,只接受三个参数，第一个参数给出文件名，第二个可选参数给出要设定的修改时间，没有提供则为当前时间，第三个可选参数给出要设定的访问时间，没有提供则为当前时间
成功返回true,失败返回false
注意：访问时间总是会被修改
touch("text.txt",time()-312*600,time()-3600);
```

```
？？？？80. umask — 改变当前的 umask
改变文件的权限
```
81. unlink
```
81. unlink — 删除文件,只接受两个参数，第一个参数指定文件名，第二个参数为可选参数，指上下文context
成功返回true,失败返回false和提醒
unlink("a.txt");
if(unlink("tt.txt")){
    echo "文件删除成功";
}else{
    echo "文件删除失败";
}
```
parse_url()
```
parse_url()解析URL,以数组的形式返回各部分
print_r(parse_url("http://www.baidu.com"));
输出： 
Array
(
    [scheme] => http
    [host] => www.baidu.com
)
print_r(parse_url("http://weibo.com/u/1838861583/home?topnav=1&wvr=6"));
输出： 
Array
(
    [scheme] => http
    [host] => weibo.com
    [path] => /u/1838861583/home
    [query] => topnav=1&wvr=6
)
```

///////////////////////////////////////////////////////////////////////////////
///////////////////             文件上传                //////////////////////
///////////////////////////////////////////////////////////////////////////////

POST方法上传
```
可以上传文本和二进制文件
配置：
    file_uploads
    upload_max_filesize
    upload_tmp_dir
    post_max_size
    max_input_time
```

表单中设置：enctype="multipart/form-data"才能上传文件，即：
```
<form action="test.php" post="post" enctype="multipart/form-data"></form>
```
$_FILES
```
 <form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="userfile" />
    <input type="submit" name="" value="上传" />
 </form>
全局变量$_FILES保存上传文件的所有信息
该变量是一个多维数组，键值是表单中文件类型input的name，如userfile，输出：
Array
(
    [userfile] => Array
        (
            [name] => 0103.jpg
            [type] => image/jpeg
            [tmp_name] => D:\wamp\tmp\phpD17C.tmp
            [error] => 0
            [size] => 18900
        )

)
name:客户端机器上文件原名称
type:上传文件MIME类型，这个只是通过文件名称后缀判断的，并不能代表文件的真实类型
tmp_name：上传的文件在服务器端保存的临时地址
error：上传产生的差错代码（0 1 2 3 4 6 7）
size:已上传文件的大小，字节
```
is_uploaded_file()
```
判断文件是否是通过HTTP POST上传的
返回布尔类型
在上传后接受上传之前通过这个函数判断再操作较安全
```
move_uploaded_file()
```
检查上传文件是否合法（即是否是POST上传的），并将上传的临时文件移到指定目录并重命名，该函数仅作用域上传文件，会覆盖同名文件
语法:bool move_uploaded_file  ( string $filename  , string $destination  );
eg.
Array
(
    [userfile] => Array
        (
            [name] => Array
                (
                    [0] => 1.txt
                    [1] => 捕获.png
                )

            [type] => Array
                (
                    [0] => text/plain
                    [1] => image/png
                )

            [tmp_name] => Array
                (
                    [0] => D:\wamp\tmp\php8752.tmp
                    [1] => D:\wamp\tmp\php8763.tmp
                )

            [error] => Array
                (
                    [0] => 0
                    [1] => 0
                )

            [size] => Array
                (
                    [0] => 190159
                    [1] => 118726
                )

        )

)
可见当一次上传多个同名（表单中使用userfile[]）文件时，将上传文件的每一部分分别组成一个数组
```
rename()
```
重命名一个文件或目录
语法：bool rename  ( string $oldname  , string $newname  [, resource $context  ] )
成功返回true否则返回false
eg.
    <?php
    rename ( "/tmp/tmp_file.txt" ,  "/home/user/login/docs/my_file.txt" );
    ?> 
```
上传文件的检查：
```
    1、文件大小是否符合规范
    2、文件类型是否符合规范
    3、通过error来进行不同的操作
```
错误代码及一些文件上传的常量
```
error    描述
0           文件上传成功
1           文件上传超过了upload_max_filesize的设置
2           文件大小超过了表单 max_file_size 
3           文件仅部分上传
4           文件没有上传
6           找不到临时文件夹
7           文件写入失败
以上的值都可以通过常量访问
```
常见配置项
```
max_file_size
upload_max_filesize
memory_limit
max_execution_time
max_input_time
post_max_size
```
上传多个文件
```
如果表单中input的name值各不相同时，这时得到的文件信息组织形式有点不同：
Array
(
    [userfile] => Array
        (
            [name] => hostgator-chat.txt
            [type] => text/plain
            [tmp_name] => D:\wamp\tmp\phpF932.tmp
            [error] => 0
            [size] => 2893
        )

    [userfile1] => Array
        (
            [name] => hmtl-css.txt
            [type] => text/plain
            [tmp_name] => D:\wamp\tmp\phpF933.tmp
            [error] => 0
            [size] => 0
        )

)
```
/////////////////////////////////////////////////////////////////////////
///////////////////       PHP的 mysqli          ////////////////////
///////////////////////////////////////////////////////////////////

API
```
应用程序接口 Application Programming Interface，定义了类，方法，函数，变量等等一切你的应用程序中为了完成特定任务而需要调用的内容。
```
驱动：
```
设计用来执行某种服务的软件代码，这些软件代码库实现用于和mysql数据库服务交互的底层协议
```
扩展
```
类似于API,扩展一个典型的作用就是暴露一个API给PHP程序员,术语API和扩展描述的不是同一类事物，因为扩展可能并不需要暴露一个API接口给程序员。 
```
PHP中提供的mysql的API:
```
1、PHP的Mysql扩展
2、PHP的mysqli扩展
3、PHP数据库对象(PDO)
```
mysqli的持久化链接
mysqli类的属性和方法

#MySQLi类
```
面向对象接口               描述
////////////////(属性) ///////////////////////// 
$mysqli->affected_rows    获取前一个Mysql操作的受影响行数 
$mysqli->client_info      返回字符串类型的Mysql客户端版本信息 
$mysqli->client_version   返回整型的Mysql客户端版本信息 
$mysqli->connect_errno    返回最后一次连接调用的错误代码 
$mysqli->connect_error    返回一个字符串描述的最后一次连接调用的错误代码 
$mysqli->errno            返回最近的函数调用产生的错误代码 
$mysqli->error            返回字符串描述的最近一次函数调用产生的错误代码 
$mysqli->field_count      返回最近一次查询获取到的列的数目
```
$mysqli->host_info        返回一个能够代表使用的连接类型的字符串 
```
$mysqli=new mysqli("localhost","root","","blog");
echo $mysqli->host_info;// localhost via TCP/IP
```
$mysqli->protocol_version   返回使用的Mysql协议的版本信息
```
$mysqli=new mysqli("localhost","root","","blog");
echo $mysqli->protocol_version;//10
```
$mysqli->server_info    返回Mysql服务端版本的信息 
```
echo $mysqli->server_info;// 5.6.17
```
$mysqli->server_version  返回整型的Mysql服务端版本信息 
```
echo $mysqli->server_version;// 50617
```
$mysqli->info             最近一次执行的查询的检索信息 
$mysqli->insert_id        返回最后一次查询自动生成并使用的id 
$mysqli->sqlstate         返回前一个Mysql操作的SQLSTATE错误 
$mysqli->warning_count    返回给定链接最后一次查询的警告数量 
////////////////////////(方法)///////////////////////////  
mysqli->autocommit()    打开或关闭数据库的自动提交功能 
mysqli->change_user()     更改指定数据库连接的用户 
mysqli->character_set_name()    返回数据库连接的默认字符集 
```
echo $mysqli->character_set_name() ;// latin1
```
mysqli->close()         关闭先前打开的数据库连接 
mysqli->commit()        提交当前事务 
mysqli::__construct()   打开一个到Mysql服务端的新的连接［注意：静态方法］ 
mysqli->debug()         将调试信息转储到日志中 
mysqli->get_charset()      返回对象的字符集 
mysqli->get_connection_stats()  返回客户端连接的统计信息。 仅可用于 mysqlnd。 
mysqli->get_client_info()   返回字符串描述的Mysql客户端版本 
mysqli->get_client_stats()  返回每个客户端进程的统计信息。 仅可用于 mysqlnd。 
mysqli->get_cache_stats()    返回客户端的zval缓存统计信息。 仅可用于 mysqlnd。 
mysqli->get_server_info()     初始化mysqli并且返回一个由mysqli_real_connect使用的资源类型。［不是在对象上，是它返回的$mysqli对象］ 
mysqli->kill()    请求服务器杀死一个Mysql线程 
mysqli->more_results()    检查一个多语句查询是否还有其他查询结果集 
mysqli->multi_query()    在数据库上执行一个多语句查询 
mysqli->next_result()    从multi_query中准备下一个结果集 
mysqli->options()     设置选项 
mysqli->ping()    ping一个服务器连接，或者如果那个连接断了尝试重连 
mysqli->prepare()    准备一个用于执行的SQL语句 
mysqli->query()    在数据库上执行一个查询 
mysqli->real_connect()     打开一个到Mysql服务端的连接 
mysqli->real_escape_string()  转义字符串中用于SQL语句中的特殊字符，这个转换会考虑连接的当前字符集。 
mysqli->real_query()    执行一个SQL查询 
mysqli->rollback()     回滚当前事务 
mysqli->select_db()    为数据库查询选择默认数据库 
mysqli->set_charset()    设置默认的客户端字符集 
mysqli->set_local_infile_default()    清除用户为load data local infile命令定义的处理程序 
mysqli->set_local_infile_handler()   设置LOAD DATA LOCAL INFILE命令执行的回调函数 
mysqli->ssl_set()    使用SSL建立安装连接 
mysqli->stat()    获取当前系统状态 
mysqli->stmt_init()   初始化一个语句并且返回一个mysqli_stmt_prepare使用的对象 
mysqli->store_result()     传输最后一个查询的结果集 
mysqli->thread_id()    返回当前连接的线程ID 
mysqli->thread_safe()     返回是否设定了线程安全 
mysqli->use_result()     初始化一个结果集的取回 

#MySQL_STMT

面向对象接口    描述
//////////////////////(属性)  ////////////////////////////////////////
$mysqli_stmt->affected_rows   返回最后一条倍执行的语句改变，删除或插入的总行数 
$mysqli_stmt->errno   返回最近一次语句调用的错误代码 
$mysqli_stmt->error   返回最后一条语句错误的字符串描述 
$mysqli_stmt->field_count   返回给定语句得到的字段数量 
$mysqli_stmt->insert_id   获取前一个INSERT操作生成的ID 
$mysqli_stmt->num_rows   返回语句结果集中的行数 
$mysqli_stmt->param_count     返回给定语句中参数数量 
$mysqli_stmt->sqlstate    返回前一个语句操作的SQLSTATE错误代码

//////////////////////////(方法)  ////////////////////////
mysqli_stmt->attr_get()    用于获取语句属性的当前值 
mysqli_stmt->attr_set()     用于修改prepared语句的行为 
mysqli_stmt->bind_param()      将一个变量作为参数绑定到prepared语句上 
mysqli_stmt->bind_result()   将一个变量绑定到一个prepared语句上用于结果存储 
mysqli_stmt->close()     关闭一个prepared语句 
mysqli_stmt->data_seek()      查看语句结果集中的任意行 
mysqli_stmt->execute()       执行一个prepared查询 
mysqli_stmt->fetch()       从一个prepared语句中抓取结果到限定变量中 
mysqli_stmt->free_result()     释放给定语句处理存储的结果集所占内存 
$mysqli_stmt->get_result()   没有文档 仅可用于 mysqlnd。 
mysqli_stmt->get_warnings()     没有文档 
$mysqli_stmt->more_results()   没有文档 仅可用于 mysqlnd。 
$mysqli_stmt->next_result()   没有文档 仅可用于 mysqlnd。 
mysqli_stmt->num_rows()    查阅属性$mysqli_stmt->num_rows  
mysqli_stmt->prepare()    准备一个SQL语句用于执行 
mysqli_stmt->reset()     重置一个prepared语句 
mysqli_stmt->result_metadata()    从一个prepared语句返回结果集元数据 
mysqli_stmt->send_long_data()    发送数据块 
mysqli_stmt->store_result()    从一个prepared语句中传输一个结果集 


#MySQLi_RESULT类
面向对象接口      描述

///////////////////////(属性)  ///////////////////////////////
$mysqli_result->current_field   获取当前字段在结果集指针中的开始位置 
$mysqli_result->field_count   获取结果中字段数量 
$mysqli_result->lengths   返回结果集中功能当前行的列长度 
$mysqli_result->num_rows   获取结果中行的数量 

////////////////////////(方法)/////////////////////  
mysqli_result->data_seek()    将结果中的结果指针调整到任意行 
mysqli_result->fetch_all()    抓取所有的结果行并且以关联数据，数值索引数组，或者两者皆有的方式返回结果集。仅可用于 mysqlnd。 
mysqli_result->fetch_array()  以一个关联数组，数值索引数组，或者两者皆有的方式抓取一行结果 
mysqli_result->fetch_assoc()   以一个关联数组方式抓取一行结果 
mysqli_result->fetch_field_direct()   抓取一个单字段的元数据 
mysqli_result->fetch_field()   返回结果集中的下一个字段 
mysqli_result->fetch_fields()    返回一个代表结果集字段的对象数组 
mysqli_result->fetch_object()    以一个对象的方式返回一个结果集中的当前行 
mysqli_result->fetch_row()    以一个枚举数组方式返回一行结果 
mysqli_result->field_seek()   设置结果指针到特定的字段开始位置 
mysqli_result->free()     释放与一个结果集相关的内存 


#MySQL_Driver类

面向对象接口     描述

///////////////////(属性)  //////////////////////////
N/A 
//////////////////////////(方法)///////////////////  
mysqli_driver->embedded_server_end()   
mysqli_driver->embedded_server_start()  




###哈希HASH和md5
hash就相当于文章和固定字数的摘要，它总是将任意长度的字符串转换为固定长度的某一字符串
md5就是一种哈希函数，始终输出32个字符的字符串（当第二个参数设置为true时，将得到16个字符的散列值）
可能的问题
1、哈希碰撞
不同的内容得到了相同的哈希输出
*crc32()算法仅能产生32位的整数作为hash结果，造成碰撞的可能性更大；
*md5()可以产生128位的hash值，从而有340,282,366,920,938,463,463,374,607,431,768,211,456种可能的 输出
*sha1()是一个刚好的方案，它产生160位的hash值

2、彩虹表
“彩虹表通过计算常用的词及它们的组合的hash值建立起来的表。”
这个表可能存储了几百万甚至十亿条数据。现在存储已经非常的便宜，所以可以建立非常大的彩虹表。 
解决办法：添加其他不规则代码
```
$password = "easypassword"; 
// this may be found in a rainbow table 
// because the password contains 2 common words 
echo sha1($password); // 6c94d3b42518febd4ad747801d50a8972022f956 
// use bunch of random characters, and it can be longer than this  $salt = "f#@V)Hu^%Hgfds"; 
// this will NOT be found in any pre-built rainbow table 
echo sha1($salt . $password); // cd56a16759623378628c0d9336af69b74d9d71a5 
```

3、还是彩虹表
4、hash速度
//////////////////////////////////////////////////////



set_time_limit()
```
用来设置脚本最长的执行时间，可以在php.ini中设置max_execution_time,如果配置为0，表示不限定最久时间，如set_time_limit(0);
set_time_limit(30);表示脚本最长执行30秒
```



///////////////////////////////////////////////////////////////
//////////////      常用函数整理（包括返回值）       //////////
///////////////////////////////////////////////////////////////

#数组函数整理

1. array_change_key_case — 返回字符串键名全为小写或大写的数组
```
//更换键名大小写
echo "<pre>";
$arr2=array('key1'=>'后盾网','key2'=>'php视频','key3'=>'div视频');
print_r(array_change_key_case($arr2));//默认是小写
print_r(array_change_key_case($arr2,CASE_UPPER));//将键名变为大写
print_r($arr2);//以上修改并不影响原数组
```
2. array_chunk — 将一个数组分割成多个
```
//拆分数组为多个数组
$arr3=array('key1'=>'后盾网','key2'=>'php视频','key3'=>'div视频','key4'=>'mysql课程','key5'=>'后盾网','key6'=>'php视频','key7'=>'div视频','key8'=>'mysql课程');
print_r(array_chunk($arr3,3));//第二个参数指定拆分后数组单元中包含的元素个数，如果最后数目不够，那就直接将最后的作为一组
输出：
  Array
(
    [0] => Array
        (
            [0] => 后盾网
            [1] => php视频
            [2] => div视频
        )

    [1] => Array
        (
            [0] => mysql课程
            [1] => 后盾网
            [2] => php视频
        )

    [2] => Array
        (
            [0] => div视频
            [1] => mysql课程
        )

)
print_r(array_chunk($arr3,3));//3指拆分后数组中的元素个数,键名没有被保存，要保存键名需要添加第三个参数True
print_r(array_chunk($arr3,2,True));//保留了键名
```
3. array_column — 返回数组中指定的一列
```
array_column()  返回 input 数组中键值为 column_key 的列， 如果指定了可选参数 index_key ，那么 input 数组中的这一列的值将作为返回数组中对应值的键。一般用于多维数组取出指定列 
$records  = array(
    array(
         'id'  =>  2135 ,
         'first_name'  =>  'John' ,
         'last_name'  =>  'Doe' ,
    ),
    array(
         'id'  =>  3245 ,
         'first_name'  =>  'Sally' ,
         'last_name'  =>  'Smith' ,
    ),
    array(
         'id'  =>  5342 ,
         'first_name'  =>  'Jane' ,
         'last_name'  =>  'Jones' ,
    ),
    array(
         'id'  =>  5623 ,
         'first_name'  =>  'Peter' ,
         'last_name'  =>  'Doe' ,
    )
);
 
 $first_names  =  array_column ( $records ,  'first_name' );
 print_r ( $first_names );
输出： 
Array
(
    [0] => John
    [1] => Sally
    [2] => Jane
    [3] => Peter
)
$last_names  =  array_column ( $records ,  'last_name' ,  'id' );//指定了用id的值作为键名
 print_r ( $last_names );
 输出:
Array
(
    [2135] => Doe
    [3245] => Smith
    [5342] => Jones
    [5623] => Doe
)
```

4. array_combine — 创建一个数组，用一个数组的值作为其键名，另一个数组的值作为其值
```
$arrkey=array('key1','key2','key3','key4');//定义数组键名
$arrval=array('php视频','mysql课程','div视频','css课程');//定义数组键值
print_r(array_combine($arrkey,$arrval));
输出：
    Array
(
    [key1] => php视频
    [key2] => mysql课程
    [key3] => div视频
    [key4] => css课程
)
```
5. array_count_values — 统计数组中所有的值出现的次数
```
$arr3=array('新浪网','淘宝网','优酷土豆','京东网','新浪网','YAHOO','淘宝网');
print_r(array_count_values($arr3));
输出： 
Array
(
    [新浪网] => 2
    [淘宝网] => 2
    [优酷土豆] => 1
    [京东网] => 1
    [YAHOO] => 1
)
```
6. array_diff_assoc — 带索引检查计算数组的差集，arr_diff_assoc()同时比较键名和键值,查看array_diff_key 

7. array_diff_key — 使用键名比较计算数组的差集,寻找第一个数组键名为全集的后面数组键名的补集，返回不同的键在第一个数组中的键名和键值
```
//表较两个数组键名的不同，以第一个数组为准，返回第一个数组中不同的键名和对应的键值,不区分数组元素中的顺序
$arr5a=array('url'=>'bbs.houdunwang.com','name'=>'后盾网论坛');
$arr5b=array('weburl'=>'bbs.houdunwang.com','nsame'=>'后盾网论坛');
$arr5c=array('url'=>'bbs.houdunwang.com');
print_r(array_diff_key($arr5a,$arr5b,$arr5c));//返回数组 'name'=>'后盾网论坛'
```
8. array_diff_uassoc — 用用户提供的回调函数做索引检查来计算数组的差集
```
array_diff_uassoc()通过回掉函数的形式返回一个数组在其他数组中不存在键名的值和键值，键名和键值同时比较
```
9. array_diff_ukey — 用回调函数对键名比较计算数组的差集
```
array_diff_ukey()通过回掉函数的形式返回一个数组在其他数组中不存在键名的值
```
10. array_diff — 计算数组的差集,以第一个数组为全集，找其他所有数组的补集
```
//表较两个数组的不同，以第一个数组为准，返回第一个数组中不同的值,不区分数组元素中的顺序，仅比较值
$arr4a=array('houdunwang.com','web.houdunwang.com','bbs.houdunwang.com');
$arr4b=array('sina.com.cn','bbs.houdunwang.com','web.houdunwang.com');
$arr4c=array('houdunwang.com');
print_r(array_diff($arr4a,$arr4b,$arr4c));//相当于取以第一个数组为全集后面的数组的补集
```
11. array_fill_keys — 使用指定的键和值填充数组
```
$array1 = array( 
    "a" => "first", 
    "b" => "second", 
    "c" => "something", 
    "red" 
); 

$array2 = array( 
    "a" => "first", 
    "b" => "something", 
    "letsc" 
); 
print_r(array_fill_keys($array1, $array2)); //1个或多个键对应同一个值
输出： 
Array(
     [first] => Array(
         [a] => first,
         [b] => something,
         [0] => letsc
     ),
     [second] => Array(
         [a] => first,
         [b] => something,
         [0] => letsc
     ),
     [something] => Array(
         [a] => first,
         [b] => something,
         [0] => letsc
     ),
     [red] => Array(
         [a] => first,
         [b] => something,
         [0] => letsc
     )
 )
```
12. array_fill — 用给定的值填充数组
```
array_fill(开始索引下标，元素个数，元素内容)通过指定的索引顺序及个数生成数组
$arr0=array_fill(30,2,'后盾网');
print_r($arr0);//生成两个元素值都为后盾网
输出： 
Array
(
    [30] => 后盾网
    [31] => 后盾网
)
```
13. array_filter — 用回调函数过滤数组中的单元
```
array_filter()数组过滤函数，通过回调函数的方式返回新数组，如果回掉函数返回True,数组元素返回到新数组中
$arr1=array('class1'=>'PHP课程','class2'=>'mysql课程','webname'=>'后盾网','weburl'=>'houdunwang.com');
$arr0=array_filter($arr1,'a');//函数名用引号括起来
function a($v){
    if(strpos($v,'课程')){
      return true;
    }else{
      return false;
    }
}
print_r($arr0);
输出： 
Array
(
    [class1] => PHP课程
    [class2] => mysql课程
)
可以用来筛选数据:
//判断非法信息
echo "<pre>";
$user1=array('username'=>'李海枪支','msg'=>'购买联系xxx，很高兴见到大家');
if (array_filter($user1,'a')){
  echo '包含非法信息';
}else{
  echo '消息合法';
}
function a($v){
  if (strpos($v,'枪支')){
    return true;
  }
}
```
14. array_flip — 交换数组中的键和值
```
//array_flip()把数组中的键值和键名进行交换,原键值相同的项转换完后最后一个有效
$user1=array('class1'=>'PHP课程','class2'=>'mysql课程','webname'=>'mysql课程','weburl'=>'houdunwang.com');
$arr0=array_flip($user1);
print_r($arr0);
输出： 
Array
(
    [PHP课程] => class1
    [mysql课程] => webname
    [houdunwang.com] => weburl
)
```
15. array_intersect_assoc — 带索引检查计算数组的交集
```
array_intersect_assoc()在一个或多个数组中，返回各个数组都存在的数组元素(以第一个数组为准),同时比较键名和键值
echo "<pre>";
$arr1=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
$arr2=array('url'=>'b2bs.houdunwang.com','name'=>'后盾网');
$arr3=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
//同时比较键名和键值
print_r(array_intersect_assoc($arr1,$arr2,$arr3));
输出： 
    Array
(
    [name] => 后盾网
)
```
16. array_intersect_key — 使用键名比较计算数组的交集
```
array_intersect_key()数组差集，在一个或多个数组中，返回各个数组都存在的数组元素(返回的是第一个数组相应元素),仅比较键名
$arr1=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
$arr2=array('url'=>'b2bs.houdunwang.com','name'=>'后盾网');
$arr3=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
//比较键名找交集
print_r(array_intersect_key($arr1,$arr2,$arr3));
```
17. array_intersect_uassoc() — 数组差集，带索引检查计算数组的交集，用回调函数比较索引

18. array_intersect_ukey — 数组差集，用回调函数比较键名来计算数组的交集
```
通过回掉函数的方式寻找，在一个或多个数组中，返回各个数组都存在的数组元素(以第一个数组为准),仅比较键名
```
19. array_intersect — 计算数组的交集
```
array_intersect()在一个或多个数组中，返回各个数组都存在的数组元素(这里返回的 第是第一个数组的相应元素),仅比较键值
$arr1=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
$arr2=array('url'=>'b2bs.houdunwang.com','name'=>'后盾网');
$arr3=array('url'=>'bbs.houdunwang.com','name'=>'后盾网');
//比较键值找交集
print_r(array_intersect($arr1,$arr2,$arr3));
输出： 
    Array
(
    [name] => 后盾网
)
```
20. array_key_exists — 检查给定的键名或索引是否存在于数组中
```
//array_key_exists()判断内容是否是数组的键名
$arr2=array('class1'=>'php','class2'=>'php1','class3'=>'mysql');
if (array_key_exists('class1',$arr2)){
  echo "存在该键值";
}else{
  echo "不存在";
}
```
21. array_keys — 返回数组中所有的键名
```
//array_keys()返回数组中所有的键名
$arr2=array('class1'=>'php','class2'=>'php1','class3'=>'mysql');
print_r(array_keys($arr2));//所有键名
输出： 
Array
(
    [0] => class1
    [1] => class2
    [2] => class3
)
print_r(array_keys($arr2,'php'));//查找键值内容为php的键名
输出： 
Array
(
    [0] => class1
)
$arr3=array('class1'=>'1','class2'=>1,'class3'=>'mysql');
print_r(array_keys($arr3,'1',false));//查找键值内容为php的键名,false对数据类型不进行严格的匹配
输出： 
Array
(
    [0] => class1
    [1] => class2
)
```
22. array_map — 将回调函数作用到给定数组的单元上，相当于是筛选
```
//array_map()数组地图,对一个或多个数组每一个元素的键值都应用回调函数，返回新的数组，注意回调函数的参数
$houdunwang=array(12,33,43,1,23,5,27);
function func_map($v){
  echo $v."<br/>";
}
$compare=array_map('Compare',$houdunwang);
function Compare($v){
    if ($v>33){
      return $v;
    }
    return "";  
}
输出： 
Array
(
    [0] => 
    [1] => 
    [2] => 43
    [3] => 
    [4] => 
    [5] => 
    [6] => 
)
```
23. array_merge_recursive — 递归地合并一个或多个数组
```
$arr11=array('webname'=>'后盾网','weburl'=>'www.houdunwang.com');
$arr12=array('webname'=>'后盾网论坛','weburl'=>'bbs.houdunwang.com');
print_r(array_merge($arr11,$arr12));//键名相同时后边的会覆盖前面的
print_r(array_merge_recursive($arr11,$arr12));//当发现键名相同时，同名的生成二维数组
```
24. array_merge — 合并一个或多个数组
```
//array_merge()数组的合并
$arr1=array('webname'=>'后盾网','weburl'=>'bbs.houdunwang.com');
$arr2=array('db_hot'=>'localhost','db_user'=>'root','db_name'=>'hdw');
$arr=array_merge($arr1,$arr2);
print_r($arr);
$arr11=array('webname'=>'后盾网','weburl'=>'www.houdunwang.com');
$arr12=array('webname'=>'后盾网论坛','weburl'=>'bbs.houdunwang.com');
print_r(array_merge($arr11,$arr12));//键名相同时后边的会覆盖前面的
```
25. array_multisort — 对多个数组或多维数组进行排序
```
array_multisort()可以对多个数组进行排序，数组后的参数指明是升序还是降序
$arr1=array(1,2,34,23,23,45,65,65,23,87,34512,223,123);
$arr3=array(1,2,3,23,223,45,65,45,213,87,512,223,13);
array_multisort($arr1,SORT_DESC,$arr3);//第二个数组按第一个数组的索引变化进行更改
print_r($arr3);
array_multisort($arr1,SORT_DESC,$arr3,SORT_ASC);//SORT_ASC指在第一个数组存在相同的元素时，对第二个数组相应索引名对应的值进行升序排列
print_r($arr3);
```
26. array_pad — 用值将数组填补到指定长度
```
array_pad($arr5,10,3)，填充元素3，填充后新数组的长度为10，若第二个参数是负数则在数组的前面增加
$arr4=array(1,2,3);
$arr_pad=array_pad($arr4,5,'9');//在数组后面添加'9'到制定长度5
print_r($arr4);//原数组没变
print_r($arr_pad);
输出：
Array
(
    [0] => 1
    [1] => 2
    [2] => 3
    [3] => 9
    [4] => 9
)
$arr_pad=array_pad($arr4,-7,12);//在数组的前面开始添加12到制定长度7
print_r($arr_pad);
输出： 
Array
(
    [0] => 12
    [1] => 12
    [2] => 12
    [3] => 12
    [4] => 1
    [5] => 2
    [6] => 3
)

```
27. array_pop — 将数组最后一个单元弹出（出栈），查看array_shift()
```
array_pop()出栈，返回删除的数组末端元素，对原数组改变
```
28. array_product — 计算数组中所有值的乘积
```
$arr5=array(2,3,5);
echo array_product($arr5);
```
29. array_push — 将一个或多个单元压入数组的末尾（入栈）
```
array_push()数组的入栈,改变原数组,在数组末端添加，返回新数组的元素个数
```
30. array_rand — 从数组中随机取出一个或多个单元,第二个可选参数指定取出多少个元,返回随机抽取的元素的索引或者键名组成的数组（1个时为字符串）
```
$arr2=array('后盾网','新浪网','taobao','souhu'=>'souhu','yahoo','dangdang','amazon');
print_r(array_rand($arr2,2));
输出： 
Array
(
    [0] => 0
    [1] => 4
)
可以做随机出题
```
31. array_reduce — 用回调函数迭代地将数组简化为单一的值
```
array_reduce()通过回调函数的方式将数组转换成单一的值，并返回
回调函数有两个参数，第一个为最终的返回结果（也可以在函数内部参与运算），第二个参数代表数组的每一个单元
$arr1=array(1,2,3,4,5);
array_reduce($arr1,'func');//每次传入一个值连续调用遍历完数组
function func($c,$i){//$c为最终结果，$i为每次传入的数组单元
//  echo $i;//将传进来的数组的值输出
//  $c=2;
//  echo $c."<br/>";//$c相当于是汇总的意思，类似与次数
  $c+=$i;
  //echo $c;//$c并不会自增
  return $c;//添加return后才自增，开始时$c是一个空值
}
echo array_reduce($arr1,'func')."<br/>";
输出： 
15
```
32. array_replace_recursive — 使用传递的数组递归替换第一个数组的元素
```
array_replace_recursive()  使用后面数组元素的值替换第一个数组 array  的值。 如果一个键存在于第一个数组同时也存在于第二个数组，它的值将被第二个数组中的值替换。 如果一个键存在于第二个数组，但是不存在于第一个数组，则会在第一个数组中创建这个元素。 如果一个键仅存在于第一个数组，它将保持不变。 如果传递了多个替换数组，它们将被按顺序依次处理，后面的数组将覆盖之前的值。 
array_replace_recursive()  是递归的：它将遍历数组并将相同的处理应用到数组的内部值，对应多维数组
其他同array_replace
```
33. array_replace — 使用传递的数组替换第一个数组的元素
```
array_replace()  函数使用后面数组元素的值替换第一个 array  数组的值。如果一个键存在于第一个数组同时也存在于第二个数组，它的值将被第二个数组中的值替换。如果一个键存在于第二个数组，但是不存在于第一个数组，则会在第一个数组中创建这个元素。如果一个键仅存在于第一个数组，它将保持不变。如果传递了多个替换数组，它们将被按顺序依次处理，后面的数组将覆盖之前的值。
$base  = array( "orange" ,  "banana" ,  "apple" ,  "raspberry" );
 $replacements  = array( 0  =>  "pineapple" ,  4  =>  "cherry" );
 $replacements2  = array( 0  =>  "grape" );

 $basket  =  array_replace ( $base ,  $replacements ,  $replacements2 );
 print_r ( $basket );
 输出： 
 Array
(
    [0] => grape//替代而来
    [1] => banana//没有被替代
    [2] => apple
    [3] => raspberry
    [4] => cherry//新创建的
)

```
34. array_reverse — 返回一个单元顺序相反的数组
```
//array_reverse()反转数组,第二个参数为true时则原索引号不变，否则改变;当原数组是关联数组时则无影响
$arr=array('webname'=>'后盾网','weburl'=>'bbs.houdunwang.com');
$arr_r=array('a','b','c','d','e','f');
print_r($arr_r);
print_r(array_reverse($arr_r));//索引号改变
print_r(array_reverse($arr_r,true));//索引号不变
print_r($arr);//关联数组
print_r(array_reverse($arr));//关联数组不受影响
```
35. array_search — 在数组中搜索给定的值，如果成功则返回相应的键名(索引数组为索引)，失败返回false
```
//array_search()检索函数,返回匹配元素的索引值或键名(关联数组时),当数组中没有时返回布尔类型false
$arr2=array('后盾网','php视频','div视频');
$k=array_search('后盾网',$arr2);
echo $k;//输出：0
echo array_search("厚度",$arr2);//输出：false
```
36. array_shift — 将数组开头的单元移出数组
```
array_shift()删除数组第一位元素,返回被删除的元素，改变了原数组，如果删除失败返回null
echo "<pre>";
$arr1=array('苹果','梨','桃','苹果');
$arr1[]='葡萄';
print_r($arr1);
输出： 
Array
(
    [0] => 苹果
    [1] => 梨
    [2] => 桃
    [3] => 苹果
    [4] => 葡萄
)
array_unshift($arr1,'菠萝');
print_r($arr1);
输出： 
Array
(
    [0] => 菠萝
    [1] => 苹果
    [2] => 梨
    [3] => 桃
    [4] => 苹果
    [5] => 葡萄
)
print_r(array_shift($arr1));//输出：菠萝
print_r(array_pop($arr1));//输出：葡萄
print_r($arr1);
输出： 
葡萄Array
(
    [0] => 苹果
    [1] => 梨
    [2] => 桃
    [3] => 苹果
)
```
37. array_slice — 从数组中取出一段
```
array_slice(被截取的数组,开始位置,截取长度)截取数组元素,若第四个参数为true则保留索引(关联数组不受影响) 不改变原数组
$arr1=array(1,2,3,4,5);
$arr_new1=array_slice($arr1,2,2);//不保留索引
print_r($arr_new1);
输出： 
Array
(
    [0] => 3
    [1] => 4
)
$arr_new2=array_slice($arr1,2,2,true);//保留原索引
print_r($arr_new2);
输出： 
Array
(
    [2] => 3
    [3] => 4
)
print_r($arr1);//原数组并未改变
print_r(array_slice($arr1,-3,-1,true));//负数时从后面开始数起，向后取指定个数(第三个参数为正数时)的元素，直到数组末尾或者向后取到位置数(第三个参数为负数时)但不包括末位置数
输出： 
Array
(
    [2] => 3
    [3] => 4
)
print_r(array_slice($arr,-3,2,true));
```
38. array_splice — 把数组中的一部分去掉并用其它值取代
```
//array_splice(传入数组,开始位置，截取长度，在原数组中插入新的元素并去掉原数组元素(相当于替换))截取数组，改变原数组；返回截取的数组元素
$arr1=array(1,2,3,4,5);
print_r(array_splice($arr1,2,2,"houdunwang.com"));//返回原数组中该位置的元素,这一步返回值类似于array_slice
输出： 
Array
(
    [0] => 3
    [1] => 4
)
print_r($arr1);//实际数组改变了，将上一步返回值替换为指定的参数
输出:
Array
(
    [0] => 1
    [1] => 2
    [2] => houdunwang.com
    [3] => 5
)
```
39. array_sum — 计算数组中所有值的和

40. array_udiff_assoc — 带索引检查计算数组的差集，用回调函数比较数据
```
array_udiff_assoc($array1,$array2,$data_compare_func)通过一个回调函数比较两个或多个数组的相异键名或键值,以第一个为准(作为全集)，返回不同的元素，同时比较键名和键值
```
41. array_udiff_uassoc — 带索引检查计算数组的差集，用回调函数比较数据和索引
```
array_udiff_uassoc($array1,$array2,$data_compare_func)通过两个回调函数比较两个或多个数组的相异键名和键值,以第一个为准(作为全集)，返回不同的元素，同时比较键名和键值
```
42. array_udiff — 用回调函数比较数据来计算数组的差集
```
array_udiff($array1,$array2,$data_compare_func)通过回调函数比较两个或多个数组的相异键值,以第一个为准(作为全集)，返回不同的元素，仅比较键值
$arr1=array('a'=>'a','b'=>'b','c'=>'c');
$arr2=array('a'=>'a','b2'=>'c','c'=>'1b','d'=>'d');
$arr3=array('a'=>'a','d'=>'d');
$arr4=array_udiff($arr1,$arr2,$arr3,'func');//第一个为全集,寻找其他补集
function func($v1,$v2){
  if($v1===$v2){
    return 0;
  }elseif($v1>$v2){
    return 1;
  }else{
    return -1;
  }
}
echo "<pre>";
print_r($arr4);
print_r(array_udiff_assoc($arr1,$arr2,$arr3,'func'));//同时比较键名和键值,键名默认比较方法为内部函数
print_r(array_udiff_uassoc($arr1,$arr2,$arr3,'func','func'));
print_r(array_uintersect($arr1,$arr2,$arr3,'func'));
print_r(array_uintersect_assoc($arr1,$arr2,$arr3,'func'));//同时比较键名和键值,键名默认比较方法为内部函数
print_r(array_uintersect_uassoc($arr1,$arr2,$arr3,'func','func'));
```
43. array_uintersect_assoc — 带索引检查计算数组的交集，用回调函数比较数据
```
array_uintersect_assoc()通过一个回调函数求两个或多个数组的交集，返回交集（以第一个数组为准),同时比较键值和键名
```
44. array_uintersect_uassoc — 带索引检查计算数组的交集，用回调函数比较数据和索引
```
array_uintersect_uassoc()通过两个回调函数求两个或多个数组的交集，返回交集（以第一个数组为准),同时比较键值和键名
```
45. array_uintersect — 计算数组的交集，用回调函数比较数据
```
array_uintersect()通过回调函数求两个或多个数组的交集，返回交集（以第一个数组为准),仅比较键值
```
46. array_unique — 移除数组中重复的值
```
array_unique($array)删除数组中的重复项,保留第一次出现的索引
$arr1=array('苹果','梨','桃','苹果');
print_r(array_unique($arr1));
输出:
Array
(
    [0] => 苹果
    [1] => 梨
    [2] => 桃
)
```
47. array_unshift — 在数组开头插入一个或多个单元
```
$array[]='';
array_unshift($arr1,'菠萝');在数组第一位添加元素,返回添加后数组的元素个数，改变了原数组
```
48. array_values — 返回数组中所有的值
```

```
49. array_walk_recursive — 对数组中的每个成员递归地应用用户函数
```
//array_walk_recursive(input, funcname)操作二维数组里的数据
$arr5=array(
  array('cname'=>'语文','cscore'=>87),
  array('cname'=>'数学','cscore'=>97),
  array('cname'=>'英语','cscore'=>77),
  array('cname'=>'政治','cscore'=>57)
  );


array_walk_recursive($arr5, 'func5');
function func5(&$v,$k){
  if ($k=='cscore' && $v<60) {
    $v='不及格';
  }
}
print_r($arr5);
输出： 
Array
(
    [0] => Array
        (
            [cname] => 语文
            [cscore] => 87
        )

    [1] => Array
        (
            [cname] => 数学
            [cscore] => 97
        )

    [2] => Array
        (
            [cname] => 英语
            [cscore] => 77
        )

    [3] => Array
        (
            [cname] => 政治
            [cscore] => 不及格
        )

)
```
50. array_walk — 对数组中的每个成员应用用户函数
```
//array_walk(array, funcname)，array_walk()数组的漫游，将一个数组中的每一个元素都进行函数处理，处理成功返回true，否则返回 false,注意回调函数的参数,数组不能是多维数组
$arr3=array('money1'=>123,'money2'=>1223,'money3'=>323,'money4'=>523);
function func_walk(&$v,$k){
  if ($v<=1000) {
    $v+=500;
  }
}
if (array_walk($arr3,'func_walk')) {
  echo '加工资成功！'."<br/>";
}
print_r($arr3);
$arr5=array(
  array('cname'=>'语文','cscore'=>87),
  array('cname'=>'数学','cscore'=>97),
  array('cname'=>'英语','cscore'=>77),
  array('cname'=>'政治','cscore'=>57)
  );
  输出： 
加工资成功！
Array
(
    [money1] => 623
    [money2] => 1223
    [money3] => 823
    [money4] => 1023
)
```
51. array — 新建一个数组
52. arsort — 对数组进行逆向排序并保持索引关系
```
$arr4=array('bbs_url'=>'bbs.houdunwang.com','web_url'=>'www.houdunwang.com','bbs_name'=>'后盾网论坛','web_name'=>'后盾网免费视频教程');
arsort($arr4);//保留键名
print_r($arr4);
输出： 
Array
(
    [bbs_name] => 后盾网论坛
    [web_name] => 后盾网免费视频教程
    [web_url] => www.houdunwang.com
    [bbs_url] => bbs.houdunwang.com
)
```
53. asort — 对数组进行排序并保持索引关系
```
$arr=array('bbs_url'=>'bbs.houdunwang.com','web_url'=>'www.houdunwang.com','bbs_name'=>'后盾网论坛','web_name'=>'后盾网免费视频教程');
asort($arr1);//保留键名
print_r($arr1);
输出： 
Array
(
    [bbs_url] => bbs.houdunwang.com
    [web_url] => www.houdunwang.com
    [web_name] => 后盾网免费视频教程
    [bbs_name] => 后盾网论坛
)
```
54. compact — 建立一个数组，包括变量名和它们的值,参数可以是数组或字符串组合
```
$webname='后盾网';
$weburl='houdunwang.com';
$hdcms='cms.houdunwang.com';
$arr=compact('webname','weburl','hdcms');//函数寻找变量名并将名和值变为数组
print_r($arr);
$hdw_var=array('webname','weburl','hdcms');
$hdw=compact($hdw_var);//函数寻找数组中的变量名的值并将两者结合成数组
print_r($hdw);
```
55. count — 计算数组中的单元数目或对象中的属性个数
```
 $arr=array("houdunwang.com","后盾网php视频",array("php课程","CSS课程","THINKPAD课程"));
 echo count($arr);//输出3
 echo "<br/>---------------------------<br/>";
 echo count($arr,1);//输出6，第二个参数为1使得递归计算元素个数，可以计算多维数组，默认为0
```
56. current — 返回数组中的当前指针指向的单元，指针指向超过数组就返回false
```
echo "<pre>";
$arr3=array("houdunwang.com","后盾网php视频",array("php课程","CSS课程","THINKPAD课程"));
echo current($arr3);//输出：houdunwang.com,因为这是的指针在第一个
print_r(each($arr3));
var_dump(current($arr3));//输出：后盾网php视频，因为这时的指针在第二个
print_r(each($arr3));
print_r(each($arr3));
var_dump(current($arr3));//输出：false,到了最后超过数组大小，就返回false
```
57. each — 返回数组中当前指针所在位的键／值对并将数组指针向前移动一步
```
each()把数组中当前指针所在位的键名和键值生成新的数组,指针向下移动一位，如果指针结束返回bool值false
$arr1=array('class1'=>'php课程','class2'=>'mysql课程','class3'=>'div课程','webname'=>'houdunwang.com');
$arr_new=each($arr1);
print_r($arr_new);
输出： 
Array
(
    [1] => php课程
    [value] => php课程
    [0] => class1
    [key] => class1
)
```
58. end — 将数组的内部指针指向最后一个单元,并返回最后一个元素
```
$arr3=array("houdunwang.com",0,array("php课程","CSS课程","THINKPAD课程"));
var_dump(current($arr3));
print_r(end($arr3));//最后一个元素是数组
$arr_new=each($arr1);
print_r($arr_new);//输出下一个
$arr_new=each($arr1);
print_r($arr_new);
$arr_new=each($arr1);
print_r($arr_new);
$arr_new=each($arr1);
var_dump(($arr_new));//返回false,因为指针上一步已经已到了最后
```
59. extract — 将关联数组变为变量，通过第二个参数也可以是的索引数组分解为变量，返回值为转换成功的个数,不改变原数组
```
extract()将数组转换为变量，键名为变量名，键值为变量值，需要根据参数做更多的转换功能
$hdw=array('weburl'=>'bbs.houdunwang.com','webname'=>'后盾网','hdcms'=>'cms.houdunwang.com','后盾网论坛');
echo $hdw[0]."<br/>";//返回索引为0的元素：后盾网论坛
echo extract($hdw)."<br/>";//不加参数时，索引元素不能转换为变量，返回3
echo $webname;//输出：后盾网
extract($hdw,EXTR_PREFIX_ALL,'h');//为每个变量名加了前缀h_,使得最后一个索引元素也能够转换为变量
echo $h_0."<br/>";//输出：后盾网论坛
echo $h_webname;//输出：后盾网
```
60. in_array — 检查数组中是否存在某个值,一般用索引数组
```
$arr3=array('1','2','3');
var_dump(in_array(11,$arr3));//打印出false
$arr=array("PHP","MYSQL","HTML","CSS");
var_dump(in_array("PHP",$arr));//输出true
var_dump(in_array("PHP",$arr,true));//输出true，如果制定了第三个参数为true则为严格匹配，包括类型和值
```
61. key_exists — 别名 array_key_exists

62. key — 从关联数组中取得键名,返回当前指针位置的键名
```
$arr5=array("weburl"=>"houdunwang.com","cname"=>"后盾网视频教程");
echo key($arr5)."<br/>";//输出：weburl
next($arr5);
echo key($arr5)."<br/>";//输出：cname
```
63. krsort — 对数组按照键名逆向排序
```
$arr5=array('bbs_url'=>'bbs.houdunwang.com','web_url'=>'www.houdunwang.com','bbs_name'=>'后盾网论坛','web_name'=>'后盾网免费视频教程');
krsort($arr5);//依据键名反向排序
print_r($arr5);
输出： 
Array
(
    [web_url] => www.houdunwang.com
    [web_name] => 后盾网免费视频教程
    [bbs_url] => bbs.houdunwang.com
    [bbs_name] => 后盾网论坛
)
```
64. ksort — 对数组按照键名排序
```
$arr2=array('bbs_url'=>'bbs.houdunwang.com','web_url'=>'www.houdunwang.com','bbs_name'=>'后盾网论坛','web_name'=>'后盾网免费视频教程');
ksort($arr2);//按照键名进行排序
print_r($arr2);
输出： 
Array
(
    [bbs_name] => 后盾网论坛
    [bbs_url] => bbs.houdunwang.com
    [web_name] => 后盾网免费视频教程
    [web_url] => www.houdunwang.com
)
```
65. list — 把数组中的值赋给一些变量
```
list()将数组的值赋给变量，只能操作索引数组，指针操作，如果指针结束返回bool值false
$arr=array('PHP课程','HTML课程','JSP课程');
list($a,$b,$c)=$arr;
echo $a;//输出 PHP课程
//遍历数组，list和each组合
$arr4=array("houdunwang.com","后盾网php视频","php课程","CSS课程","THINKPAD课程");
while(list($k,$v)=each($arr4)){//这时数组的键名和键值分别赋给$k和$v
   echo $k."&nbsp;&nbsp;".$v."<br/>";
}
```
66. natcasesort — 用“自然排序”算法对数组进行不区分大小写字母的排序

67. natsort — 用“自然排序”算法对数组排序
```
natsort()通过自然顺序排序，区分大小写保留原索引名，排序成功返回布尔真，否则返回布尔假
$arr2=array('class1','class12','class3','class4','class21');
var_dump(natsort($arr2));//成功返回true
print_r($arr2);
输出： 
Array
(
    [0] => class1
    [2] => class3
    [3] => class4
    [1] => class12
    [4] => class21
)
```
68. next — 将数组中的内部指针向前移动一位并返回这时指向的值
```
 // next 把数组内部指针移动到下一个数组元素，并返回该指针，如果到结尾返回false
 $arr5=array("weburl"=>"houdunwang.com","cname"=>"后盾网视频教程");
 reset($arr5);
 echo key($arr5)."<br/>";
 next($arr5);//指针向下移动一步并返回这时指向的值
 echo key($arr5)."<br/>";
```
69. pos — current 的别名

70. prev — 将数组的内部指针倒回一位,并返回这一位的值
```
// prev 把数组内部指针移动到上一个数组元素，并返回该指针，如果到结尾返回false
$arr3=array("houdunwang.com",0,array("php课程","CSS课程","THINKPAD课程"));
print_r(each($arr3));
echo prev($arr3)."----prev<br/>";//输出：houdunwang,com
```
71. range — 建立一个包含指定范围单元的数组
```
range(1,10,2);//生成数组，1为第一个元素，每次递增2直到10
$tr=range(1,10);
$td=range(10,50,15);
print_r($tr);
输出： 
Array
(
    [0] => 1
    [1] => 2
    [2] => 3
    [3] => 4
    [4] => 5
    [5] => 6
    [6] => 7
    [7] => 8
    [8] => 9
    [9] => 10
)
print_r($td);
输出： 
Array
(
    [0] => 10
    [1] => 25
    [2] => 40
)
可以借此生成表格：
$tr=range(1,10);
$td=range(10,50,15);
echo "<table style='border:1px solid red'>";
foreach ($tr as $key1 => $value1) {
  echo "<tr>";
  foreach ($td as $key2=>$value2){
    echo "<td style='border:1px solid blue'>第$key1"."行第$key2"."个元素</td>";
  }
  echo "</tr>";
}
echo "</table>";
```
72. reset — 将数组的内部指针指向第一个单元,并返回第一个元素（以第一个元素的原有形式返回，字符串或或数组）
```
each的结果为数组，既包括素引又包括键名即关联数组
$arr2=array("houdunwang.com","后盾网php视频",array("php课程","CSS课程","THINKPAD课程"));
 print_r(each($arr2));//获得数组第一个值的数组（含有索引和键名），数组指针下移一位
 echo "<br/>---------------------------<br/>";
 print_r(each($arr2));//获得数组第二个值（含有索引和键名），数组指针下移一位
 echo "<br/>---------------------------<br/>";
 print_r(each($arr2));//获得数组第三个值（含有索引和键名），数组指针下移一位
 echo "<br/>---------------------------<br/>";
 var_dump(each($arr2));//数组没有第四个元素，不能获得值，返回,false
 reset($arr2);//重置指针的顺序，使得指针指向数组的头部
 echo reset($arr2);
```
73. rsort — 对数组逆向排序（最高到最低）

74. shuffle — 将数组打乱
```
shuffle()对数组元素随机排序,也可以说是打乱
$arr2=array('class1','class12','class3','class4','class21');;
print_r($arr2);
shuffle($arr2);//随机排序
print_r($arr2);
输出：每次输出的结果可能都不同
Array
(
    [0] => class21
    [1] => class1
    [2] => class3
    [3] => class4
    [4] => class12
)
```
75. sizeof — count 的别名

76. sort — 对数组排序
```
sort()数组的排序，递增,直接对原数组操作(即改变了原数组)，不保留原索引第二个参数指定按x进行排序
echo "<pre>";
$arr1=array(1,2,34,23,23,45,65,65,23,87,34512,223,123);
var_dump(sort($arr1));//返回布尔值，成功返回true
print_r($arr1);
输出： 
Array
(
    [0] => 1
    [1] => 2
    [2] => 23
    [3] => 23
    [4] => 23
    [5] => 34
    [6] => 45
    [7] => 65
    [8] => 65
    [9] => 87
    [10] => 123
    [11] => 223
    [12] => 34512
)
```
77. uasort — 使用用户自定义的比较函数对数组中的值进行排序并保持索引关联
```
排序方法同usort,只是会保留是索引
$arr1=array('5'=>5,'4'=>4,'2'=>2,'1'=>1,'6'=>6,'8'=>8,'3'=>3);
uasort($arr1,'func');//保留原数组索引
print_r($arr1);
$arr1=array('5'=>5,'4'=>4,'2'=>2,'1'=>1,'6'=>6,'8'=>8,'3'=>3);
uasort($arr1,'func');//保留原数组索引
print_r($arr1);
```
78. uksort — 使用用户自定义的比较函数对数组中的键名进行排序
```
uksort()按数组的键名来进行排序，保留键值,方法同usort
$arr2=array('6'=>5,'1'=>4,'2'=>2,'4'=>1);
uksort($arr2,'func');
print_r($arr2);
```
79. usort — 使用用户自定义的比较函数对数组中的值进行排序
```
usort()通过回调函数来排序数组，操作原数组,对索引重新添加0-x
$arr=array(5,4,2,1,6,8,3);
$result=usort($arr,'func');//不保留索引，排序成功返回true，否则返回false
function func($v1,$v2){
  if ($v1>$v2) {
    return 1;
  }elseif($v1==$v2){
    return 0;
  }else{
    return -1;
  }
}
var_dump($result);//函数返回true
print_r($arr);//原数组已经改变
输出： 
(
    [0] => 1
    [1] => 2
    [2] => 3
    [3] => 4
    [4] => 5
    [5] => 6
    [6] => 8
)
```




/////////////////字符串函数整理//////////////////////////
```
1. addcslashes — 以 C 语言风格使用反斜线转义字符串中的字符
```
2. addslashes — 使用反斜线引用字符串
```
 在预定义字符串前添加反斜杠(转义),包括单引号\'，双引号\",反斜线\\,与null字符
echo addslashes("ffaf“’adfa''adfa''\'nuklfd");
一般在使用前要先判别php是否已开启了自动转义，使用函数get_magic_quotes_gpc()
var_dump(get_magic_quotes_gpc());//返回false,说明没有开启
```
3. bin2hex — 将二进制数据转换成十六进制表示

4. chop — rtrim 的别名

5. chr — 返回指定的字符
```
返回相对应于 ascii  所指定的单个字符。与ord作用相反
echo chr(89);
```
6. chunk_split — 将字符串分割成指定个数字符组成的小块
```
$url="http://www.houdunwang.com?uname=zhangsan&age=33&sex=boy";
echo chunk_split($url,3);//每3个字符为一组默认以空字符串分开（最后一组可能不足3个），因此输出：htt p:/ /ww w.h oud unw ang .co m?u nam e=z han gsa n&a ge= 33& sex =bo y 
echo chunk_split($url,3,"分开");//第三个参数指定连接的字符串，此时以"分开"连接而不是空字符串，输出：htt分开p:/分开/ww分开w.h分开oud分开unw分开ang分开.co分开m?u分开nam分开e=z分开han分开gsa分开n&a分开ge=分开33&分开sex分开=bo分开y分开
```
7. convert_cyr_string — 将字符由一种 Cyrillic 字符转换成另一种
8. convert_uudecode — 解码一个 uuencode 编码的字符串
```
与convert_uuencode作用相反
$str=" CURRENT output";
echo convert_uudecode(convert_uuencode($str));
```
9. convert_uuencode — 使用 uuencode 编码一个字符串
```
uuencode 算法会将所有（含二进制）字符串转化为可输出的字符， 并且可以被安全的应用于网络传输。使用 uuencode 编码后的数据 将会比源数据大35%左右 
$str=" CURRENT output";
echo convert_uuencode($str);
输出： 
/($-54E)%3E0@;W5T<'5T
`
```
10. count_chars — 返回字符串所用字符的信息(个数)
```
统计 string  中每个字节值（0-255）出现的次数，使用多种模式返回结果。 第二个参数指定输出的模式,一定要指定第二个参数，否则会将0-255都输出出来再匹配字符个数
$str="echo convert_uudecode";
print_r(count_chars($str,1));
输出：
Array
(
    [32] => 1
    [95] => 1
    [99] => 3
    [100] => 2
    [101] => 4
    [104] => 1
    [110] => 1
    [111] => 3
    [114] => 1
    [116] => 1
    [117] => 2
    [118] => 1
)
```
11. crc32 — 计算一个字符串的 crc32 多项式，可以用作加密函数

12. crypt — 单向字符串散列，可用于加密字符串

13. echo — 输出一个或多个字符串

14. explode — 使用一个字符串分割另一个字符串为一个数组,去掉分割字符
```
$s="'PHP课程','HTML课程','JSP课程'";
var_dump(explode(",",$s));//输出数组，并去掉字符串中的,
var_dump(explode("课",$s));
第一参数为待分隔字符串中的字符
```
15. fprintf — 将格式化后的字符串写入到流
```
写入一个根据 format  格式化后的字符串到 由 handle  句柄打开的流中
if (!( $fp  =  fopen ( 'date.txt' ,  'w' ))) {
    return;
}
 fprintf ( $fp ,  "%04d-%02d-%02d" ,  $year ,  $month ,  $day );
 $fp为fopen打开的句柄，后面的为格式化字符串
 %04d为格式占位符，使用后面的变量依次替代
```
16. get_html_translation_table — 返回使用 htmlspecialchars 和 htmlentities 后的转换表
```
即返回在适应函数htmlspecialchars和htmlentities时相关字符是怎么转化的，以数组的形式返回
如：
array(1510) {
  ["
"]=>
  string(9) "&NewLine;"
  ["!"]=>
  string(6) "&excl;"
  ["""]=>
  string(6) "&quot;"
...}//可能很多
```

```
17. hebrev — 将逻辑顺序希伯来文（logical-Hebrew）转换为视觉顺序希伯来文（visual-Hebrew）
18. hebrevc — 将逻辑顺序希伯来文（logical-Hebrew）转换为视觉顺序希伯来文（visual-Hebrew），并且转换换行符
19. hex2bin — 转换十六进制字符串为二进制字符串
```
20. html_entity_decode — Convert all HTML entities to their applicable characters
```
将html实体转换为可用标签
$orig  =  "I'll \"walk\" the <b>dog</b> now" ;
 $a  =  htmlentities ( $orig );
 echo html_entity_decode($a);
```
21. htmlentities — Convert all applicable characters to HTML entities
```
$url="http://blog.csdn.net/beliefer/article/details/51473807";
echo htmlentities("<h1>$url</h1>");
echo "&lt;strong&gt;加粗&lt;/strong&gt;";
```
22. htmlspecialchars_decode — 将特殊的 HTML 实体转换回普通字符
```
$orig  =  "I'll \"walk\" the <b>dog</b> now" ;
 $a  =  htmlentities ( $orig );
 echo htmlspecialchars_decode($a);
```
23. htmlspecialchars — Convert special characters to HTML entities
```
$orig  =  "I'll \"walk\" the <b>dog</b> now" ;
 $a  =  htmlspecialchars( $orig );
 echo $a;
```
24. implode — 将一个一维数组的值转化为字符串
```
$arr=array('PHP课程','HTML课程','JSP课程');
echo implode(':',$arr);// 输出：PHP课程:HTML课程:JSP课程
```
25. join — 别名 implode,查看implode

26. lcfirst — 使一个字符串的第一个字符小写
```
$orig  =  "I'll  walk  The Dog now" ;
echo lcfirst($orig);
输出： 
i'll  walk  The Dog now
```
27. levenshtein — 计算两个字符串之间的编辑距离
```
编辑距离，是指两个字串之间，通过替换、插入、删除等操作将字符串 str1 转换成 str2 所需要操作的最少字符数量。
```
28. localeconv — Get numeric formatting information
```
获得本地数学字符信息
print_r(localeconv());
输出： 
Array
(
    [decimal_point] => .
    [thousands_sep] => 
    [int_curr_symbol] => 
    [currency_symbol] => 
    [mon_decimal_point] => 
    [mon_thousands_sep] => 
    [positive_sign] => 
    [negative_sign] => 
    [int_frac_digits] => 127
    ...
)
```
29. ltrim — 删除字符串开头的空白字符（或其他字符）

30. md5_file — 计算指定文件的 MD5 散列值
```
接受的参数为文件名包含路径
```
31. md5 — 计算字符串的 MD5 散列值

32. metaphone — Calculate the metaphone key of a string

33. money_format — Formats a number as a currency string
```
string money_format  ( string $format  , float $number  ),将数字转换为表示金钱格式的字符串
window上不可用
```
34. nl_langinfo — Query language and locale information
```在windows平台上不能实现```

35. nl2br — 在字符串所有新行之前插入 HTML 换行标记"<br/>"
```
echo  nl2br ( "foo isn't\n bar" );//将\n换为<br/>
```
36. number_format — 以千位分隔符方式格式化一个数字
```
echo  number_format(13413413413);
输出： 
13,413,413,413
```
37. ord — 返回字符串第一个字符的 ASCII 码值
```
与chr函数功能相反
echo  ord("document");
```
38. parse_str — 将字符串(类似url的get传递)解析成多个变量
```
$url="http://www.houdunwang.com?uname=zhangsan&age=33&sex=boy";
$u_msg=substr($url,(strpos($url,"?")+1));
echo $u_msg."<hr/>";//输出：uname=zhangsan&age=33&sex=boy
parse_str($u_msg);//该函数没有返回值
echo $uname."<br/>";//输出 zhangsan
echo $age."<br/>";//输出 33
echo $sex."<br/>";
如果设置了第二个变量arr，所有变量将会以数组元素的形式存入到这个数组 
```
39. print — 输出字符串

40. printf — 输出格式化字符串

41. quoted_printable_decode — Convert a quoted-printable string to an 8 bit string
```
quoted-printable一种编码方式，可见这个函数是两种编码之间的转换
```

42. quoted_printable_encode — Convert a 8 bit string to a quoted-printable string

43. quotemeta — Quote meta characters
```
为字符串中的这些字符：
. \ + * ? [ ^ ] ( $ )
之前添加反斜杠\
$str = "Hello world. (can you hear me?)";
echo quotemeta($str);
输出： 
Hello world\. \(can you hear me\?\)
```
44. rtrim — 删除字符串末端的空白字符（或者其他字符）

45. setlocale — Set locale information
```
设置某些本地格式信息
 setlocale ( LC_ALL ,  'nl_NL' );
 echo  strftime ( "%A %e %B %Y" ,  mktime ( 0 ,  0 ,  0 ,  12 ,  22 ,  1978 ));
```
46. sha1_file — 计算文件的 sha1 散列值

47. sha1 — 计算字符串的 sha1 散列值
48. 
48. similar_text — 计算两个字符串的相似度，比较时是每个字母的匹配，而不是看做整个字符串
```
规则老多了，下面说的不正确
echo similar_text('houdunwang','ho1du2wan3',$v);//比较相似度，返回相同字符的个数，输出7
echo "<br/>-----------------------------<br/>";
echo $v;//输出相似度的百分比,当求百分比时选择较长的字符串个数为除数，
```

```
49. soundex — Calculate the soundex key of a string
50. sprintf — Return a formatted string
51. sscanf — 根据指定格式解析输入的字符
52. str_getcsv — 解析 CSV 字符串为一个数组

53. str_ireplace — str_replace 的忽略大小写版本

54. str_pad — 使用另一个字符串填充字符串为指定长度

55. str_repeat — 重复一个字符串
```
56. str_replace — 子字符串替换
```
//str_replace()区分大小写,str_ireplace不区分大小写,也可以使用数组指定替换字符串
$hdw="后盾网www.houdunHwang.com,下载高清版请登录论坛";
$str=str_replace('h','后',$hdw);//将h换为后
echo $str;
echo "<br/>-----------------------------<br/>";
$stri=str_ireplace("h","后",$hdw);//不区分大小写,将h和H换为后
echo $stri;
echo "<br/>-----------------------------<br/>";
$arr1=array("h","d","w");
$arr2=array("H","D","W");
echo str_replace($arr1,$arr2,$hdw);//数组对应项为指定的替换，多个字符串替换
echo "<br/>-----------------------------<br/>";
echo str_replace($arr1,$arr2,$hdw,$k);//$k统计替换了多少次
echo "<br/>-----------------------------<br/>";
echo $k;
```


```
57. str_rot13 — 对字符串执行 ROT13 转换

58. str_shuffle — 随机打乱一个字符串

59. str_split — 将字符串转换为数组

60. str_word_count — 返回字符串中单词的使用情况
```
61. strcasecmp — 二进制安全比较字符串（不区分大小写）,查看strcmp

62. strchr — 别名 strstr
```
当查找到时，将被查找字符串及待查找字符串匹配位置后面的全部返回,没查找到返回false
$bbs="后盾网视频分享教程分享bbs.houdunwang.com,下载高清版请登录后盾网论坛";
$s1=strchr($bbs,"后盾网1")."查找的是后盾网1";//查找不到后盾网1因此返回false
var_dump($s);
$s1=strchr($bbs,"分享")."查找的是后盾网";//查找到返回字符串-分享bbs...论坛，而且查找到第一个就不在向后查找
$abc="adffadafa";
var_dump(strchr($abc,'f'));
var_dump(stristr($abc,'F'));//不区分大小写
var_dump(strrchr($abc,'f'));//从后面查找字符串
```

63. strcmp — 二进制安全字符串比较，返回-1、0或1
```
echo strcmp("houdunwang","Houdunwang");//比较字符串，区分大小写,返回 1，表示前边的大于后面的
echo "<br/>-----------------------------<br/>";
echo strcasecmp("houdunwang","HouDunwang");//比较字符串，不区分大小写，返回0
echo "<br/>-----------------------------<br/>";
echo strcmp("10","2");//比较字符串，不按照自然数大小比较，返回 -1
echo "<br/>-----------------------------<br/>";
echo strnatcmp("12","2");//比较字符串，按照自然数大小比较，返回 1
echo "<br/>-----------------------------<br/>";
echo strnatcasecmp("1h22","1H21");//比较字符串不区分大小写，按照自然数大小比较 返回 1
echo "<br/>-----------------------------<br/>";
echo strncmp("11112","111",3);//比较字符串，仅比较前3个字符，返回 0
```

```
64. strcoll — 基于区域设置的字符串比较
65. strcspn — 获取不匹配遮罩的起始子字符串的长度
```
66. strip_tags — 返回给定的字符串 str  去除空字符、HTML 和 PHP 标记后的结果
```
$str="<div style='background-color:blue;width:200px;height:50px'><span style='color:yellow'>后盾网</span>视频教程</div>";
echo $str;//带样式输出
echo strip_tags($str)."<br/>";//去除所有标签
//第二个参数指定要保留的标记
echo strip_tags($str,'<span><a>');//保留span标签（进而保留了格式）
```
67. stripcslashes — 反引用一个使用 addcslashes 转义的字符串
```
//相当于addslashses的反函数，将转义时增加的反斜线去掉
echo stripslashes(addslashes("afafdfd'as'\'a\'/aaf.\asdf'af"));//输出 afafdfd'as'\'a\'/aaf.\asdf'af
```
68. stripos — 查找字符串首次出现的位置（不区分大小写）,查看strpos

69. stripslashes — 反引用一个引用字符串

70. stristr — strstr 函数的忽略大小写版本,查看strchr

71. strlen — 获取字符串长度
```
72. strnatcasecmp — 使用“自然顺序”算法比较字符串（不区分大小写）,查看strcmp

73. strnatcmp — 使用自然排序算法比较字符串，查看strcmp

74. strncasecmp — 二进制安全比较字符串开头的若干个字符（不区分大小写）,查看strcmp
75. strncmp — 二进制安全比较字符串开头的若干个字符,查看strcmp

```
76. strpbrk — 在字符串中查找一组字符的任何一个字符

77. strpos — 查找字符串首次出现的位置
```
$abc="adffadadfa";
var_dump(strpos($abc,'f'));//区分大小写查找第一出现的下标，下标从0开始
var_dump(stripos($abc,'F'));//不区分大小写查找第一出现的下标，下标从0开始
var_dump(strrpos($abc,'f'));//区分大小写查找最后出现的下标，下标从0开始
var_dump(strripos($abc,'D'));//不区分大小写查找最后一次出现的下标，下标从0开始
```
78. strrchr — 区分大小写从最后向前查找最后一次出现的位置,查看strchr
```
79. strrev — 反转字符串
```
80. strripos — 计算指定字符串在目标字符串中最后一次出现的位置（不区分大小写）,查看strpos

81. strrpos — 计算指定字符串在目标字符串中最后一次出现的位置,查看strpos
```
82. strspn — 计算字符串中全部字符都存在于指定字符集合中的第一段子串的长度。
```
83. strstr — 查找字符串的首次出现，查看strchr

84. strtok — 标记分割字符串
```
$str="php课程,mysql课程,divcss课程,dreamweaver课程";
echo $str;
$s=strtok($str,',');//查找第一个, 将该“,”之前的部分字符串返回，查找不到则返回整个字符串
echo $s;//输出：php课程mysql课程divcss课程dreamweaver课程
ehco "<br/>";
echo strtok(',')."<br/>";//在之前的基础上继续查找，返回剩余字符串的相应部分，因此返回 mysql课程
echo strtok(',')."<br/>";//返回divcss课程
echo strtok(',')."<br/>";//返回dreamweaver课程
var_dump(strtok(','));//到字符串最后继续查找不到时返回false
```
85. strtolower — 将字符串转化为小写

86. strtoupper — 将字符串转化为大写

87. strtr — 转换指定字符
```
echo strtr('houdunwang.com','ham','HAM');//替换字符,也可以用数组指定替换
echo "<hr/>";
echo strtr('houdunwang.com',array("h"=>"H","a"=>"A","m"=>"M"));
```
88. substr_compare — 二进制安全比较字符串（从偏移位置比较指定长度）

89. substr_count — 计算字串出现的次数
```
echo substr_count('houdunwang.com 后盾网视频 houdunwang.com','houdunwang',20,20);//输出1，第一个20指从开头第20个字符（不是字节）开始找，第二个指从开始位找20个字符就停止查找
```
90. substr_replace — 替换字符串的子串

91. substr(字符串,数字,数字) — 返回字符串的子串
```
第二个参数指定开始截取的位置，第三个参数若为正则向后截取的是个数，若为负则向后截取到该位置

$houdunwang="bbs.houdunwang.com";
echo substr($houdunwang,4,10);//截取houdunwang,从第4索引开始向后截取10个
echo "<br/>--------------------------------<br/>";
echo substr($houdunwang,4)."<br/>";//不指定第二参数默认到字符串结束
echo substr($houdunwang,-5,2)."<br/>";//负数为从后向前数个数，第二个字符串是正数则向后截取第二个参数个，若是负数则截取到该负数指定位置
echo substr($houdunwang,-5,-2);//负数为从后向前数个数，第二个字符串是正数则向后截取第二个参数个，若是负数则截取到该负数指定位置
```
92. trim — 去除字符串首尾处的空白字符（或者其他字符）

93. ucfirst — 将字符串的首字母转换为大写
```
与lcfirst作用相反
```
94. ucwords — 将字符串中每个单词的首字母转换为大写

95. vfprintf — 将格式化字符串写入流
```
int vfprintf  ( resource $handle  , string $format  , array $args  )
作用与 fprintf()  函数类似，但是接收一个数组参数，而不是一系列可变数量的参数。 
if (!( $fp  =  fopen ( 'date.txt' ,  'w' )))
    return;
 vfprintf ( $fp ,  "%04d-%02d-%02d" , array( $year ,  $month ,  $day ));
```
96. vprintf — 输出格式化字符串
```
作用与 printf()  函数类似，但是接收一个数组参数，而不是一系列可变数量的参数
vprintf ( "%04d:%02d:%02d" ,  explode ( '-' ,  '1988-8-1' ));  // 1988-08-01
```
97. vsprintf — 返回格式化字符串
```
string vsprintf  ( string $format  , array $args  )
作用与 sprintf()  函数类似，但是接收一个数组参数，而不是一系列可变数量的参数。 

```

98. wordwrap — 打断字符串为指定数量的字串
```
$text  =  "The quick brown fox jumped over the lazy dog." ;
 $newtext  =  wordwrap ( $text ,  20 ,  "<br />" );
echo  $newtext ;
输出： 
The quick brown fox
jumped over the lazy
dog.
```


////////////////////////////////////////////////////////////////////////////
//////////////////////////     URL函数    /////////////////////////////
/////////////////////////////////////////////////////////////////////////

1. base64_decode — 对使用 MIME base64 编码的数据进行解码
2. base64_encode — 使用 MIME base64 对数据进行编码
3. get_headers — 取得服务器响应一个 HTTP 请求所发送的所有标头
4. get_meta_tags — 从一个文件中提取所有的 meta 标签 content 属性，返回一个数组
5. http_build_query — 生成 URL-encode 之后的请求字符串
6. parse_url — 解析 URL，返回其组成部分
```
$url="http://www.houdunwang.com/admin/index.php?m=channel&a=add";
$arr=parse_url($url);
echo "<pre>";
print_r($arr);//解析url
打印出：
      Array
(
    [scheme] => http
    [host] => www.houdunwang.com
    [path] => /admin/index.php
    [query] => m=channel&a=add
)
echo parse_url($url,PHP_URL_HOST);//取出主机名称
echo "<br/>";
echo parse_url($url,PHP_URL_PATH);//取出路径
```
7. rawurldecode — 对已编码的 URL 字符串进行解码
8. rawurlencode — 按照 RFC 1738 对 URL 进行编码
9. urldecode — 解码已编码的 URL 字符串
```
$str="后盾网视频教程php&div+css";
echo urldecode(urlencode($str));
```
10. urlencode — 编码 URL 字符串
```
$str="后盾网视频教程php&div+css";
echo "<a href='26.php?h=".urlencode($str)."'a>后盾网</a>";
echo "<br/>------------------------<br/>";
$str="后盾网视频教程";
echo urlencode($str);
```







/////////////////正则表达式函数/////////////////////////////
```
1. preg_filter — 执行一个正则表达式搜索和替换
2. preg_grep — 返回匹配模式的数组条目
3. preg_last_error — 返回最后一个PCRE正则执行产生的错误代码
4. preg_match_all — 执行一个全局正则表达式匹配
5. preg_match — 执行一个正则表达式匹配
6. preg_quote — 转义正则表达式字符
7. preg_replace_callback — 执行一个正则表达式搜索并且使用一个回调进行替换
8. preg_replace — 执行一个正则表达式的搜索和替换
9. preg_split — 通过一个正则表达式分隔字符串
```

```header输出图片
header("Content-type:image/png");//前面不能有任何输出，除非本来就是文本类型，这时输出后浏览器默认为文档类型
$filename='./1.png';
$file=fopen($filename,"r");
echo fread($file,filesize($filename));
fclose($file);
```

```
echo PHP_OS;//获取当前正在使用的PHP的操作系统简称
```





