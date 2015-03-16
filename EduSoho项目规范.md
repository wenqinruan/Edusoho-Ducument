#EduSoho项目规范

####代码规范####

**基本**

* 代码必须遵循PSR [PSR-1].
* PHP,JS代码使用4个空格作为缩进,html和css使用2个空格作为缩进。
* 一行代码长度要限制,通常情况应该是80字符以内,特殊情况,最大不能超过120个字符。
* namespace申明之后必须要有一个空行,use申明块之后必须要有一个空行.
* 类的左花括号必须放到下一行，右花括号必须放在类主体的下一行。
* 方法的左花括号必须放在下一行，右花括号必须放在方法主体下面。
* 所有的属性和方法必须有可见性(译者注：Public, Protect, Private)声明；abstract和final声明必须在可见性之前；static声明必须在可见性之后。
* 控制结构的关键词必须在后面有一个空格； 方法和函数不可有。
* 控制结构的左花括号必须放在同一行，右花括号必须放在控制主体的下一行。
* 控制结构的左括号后面不可有空格，右括号之前不可有空格。
* 只能有`if`判断,不能有`else`和`elseif`。

示例代码:

    <?php
    namespace Vendor\Package;

    use FooInterface;
    use BarClass as Bar;
    use OtherVendor\OtherPackage\BazClass;

    class Foo extends Bar implements FooInterface
    {
        public function sampleFunction($a, $b = null)
        {
            if ($a === $b) {
                bar();
            } elseif ($a > $b) {
                $foo->bar($arg1);
            } else {
                BazClass::bar($arg2, $arg3);
            }
        }

        final public static function bar()
        {
            // method body
        }
    }

**命名要有意义的**

不能起$a、$arr、$tmp这样的变量

**要考虑命名的长度**

    $consecutivePasswordErrorTimes //不要起这么长的名字:
    $filedsWithUserIdAndQuestionNumAndQuestionAndHashedAnswerAndAnswerSalt 

**命名要遵守规范**

    const MAX_NUM = 10; //常量要大写,变量中只能出现下划线(_)

    private $_name; //私有变量要以下划线_,私有方法也是一样
    private function _call()


    public $userCount; //所有变量和方法名遵循陀峰规则
    public function getCourse($id);

    class CourseService;//类命名,首字母大写,驼峰规则

**一个概念不要用多个词来表示，一个词也不要表示多种概念**

* 使用领域背景中、上下文(Context)中有意义的名字
* 不要太技术化
* 不要只看表面含义


**Service / Dao 方法的命名**

* 取单行数据，方法名以get开头
* 取多行数据，方法名以find开头，名词需复数
* 方法的参数顺序，跟方法名中的查询条件要对应

####数据库命名规范####

* 表名为单数，多个单词以下划线分割
* 字段名遵循鸵峰命名
* 表名、字段名避免使用关键词比如order、group...
* 正整数的字段，要标记为：UNSIGNED
* 通常每个表要有id字段，自增, 主键
* 表的引擎为Innodb
* 每个表名、字段名要有注释
* 字段通常要有默认值，不为空；Text类型比较特殊，要为空、默认NULL。
* 表示开关的字段(0/1），用Tinyint
* 字符集使用utf8_general_ci
* 数据库设计、字段的增加/删除，需严格评审
* 数据库的变更，需写migration脚本，一旦脚本已push，就不能修改。如需修改，请新增migration脚本。

####插件开发规范####

* 插件名称，尽量使用１~2个单词，１个单词最佳
* 插件的数据库表名，以插件名称开头, plugin__couponxxxx

####客户定制开发规范####

* 客户定制新增功能，需增加数据库的，尽量通过加表的方式；如需加字段，请加字段前缀
* 客户定制新功能的，通常在src/Custom目录下新增功能

####GIT 规范####

**规范１：**

* 所有特性开发，均开分支feature/{id}-feature-short-name，{id}为特性的redmine任务号；
* 所有bug修复，均开分支bugfix/{id}-bug-short-name，{id}为bug的redmine号。

**规范２：**

* master为稳定分支，进入此分支的代码都必须经过review；
* develop为下一个即将发布的版本开发分支，一旦版本开发完毕，转到release/{version}分支，进行最后的完善以及bug修复。

**规范３：**

* 所有bugix分支,feature分支开发完成后，需merge到developer分支时，都需在提交Gitlab中提交Merge Request进行Code Review；
* release分支，需merge到master分支时，也需在Gitlab中提交Merge Requst，进行Code Review；
* 首先由各组组长Code Review，再由Wellming Review；
* Wellming的代码，由各组组长Review。

**规范４：**

* 新增的Service方法及类，需写单元测试；
* 单元测试也纳入Code Review；
* 需单元测试跑通后才能提交代码；
* 测试集成一旦BUILD失败，请立即修复。

**规范５：**

* GIT COMMIT 日志，需写清楚本次提交的内容；
* 一次COMMIT只做一件事情。

单元测试文档：edusoho主目录/doc/test-unit.md
持续集成地址：http://gitlab-ci.topxia.com/ ，使用Giltlab帐号可登录

####TWIG####

* 减少重复代码，使用extend, include, render, embeded
* 缩进2个空格
* twig中尽量使用sysmfony的内置对象app.user, app.request
* [http://symfony.com/doc/current/book/templating.html](http://symfony.com/doc/current/book/templating.html)
* [http://twig.sensiolabs.org/](http://twig.sensiolabs.org/)

####路由的命名####

* 请遵循Restful API的设计原则
* [文档](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)

####开发环境####

* PHP 5.3.x
* 设置MySQL数据库SQL严格模式

    /etc/mysql/my.cnf
    
    在[mysqld]配置下新增：sql-mode="STRICT_TRANS_TABLES"

* Ubuntu
* Sublime Text 3 [文档](https://gist.github.com/wenqinruan/07522eda0e2f2af9e00b)

####其他####

* 废弃代码要及时清理，特别是功能需求变更后。不清理，会带来额外的维护成本。
* 变量声明，要靠近使用。
* 我们项目遵循PSR2规范

[更加详细的代码规范文档](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)