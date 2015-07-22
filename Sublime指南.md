# Sublime插件安装 #
#### 1. Package Control,必装.是装其他插件的插件.....####

**按``ctrl+` ``打开sublime命令行或者View > Show Console**     
       
>如果是sublime3,输入：

    import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

>如果是sublime2,输入：

    import urllib2,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')

**重启sublime,完成安装**

 


#### 2. PHP CodeSniffer,比较强大的代码嗅探工具.####

**使用sublime的package control安装PHPCS.**

`Ctrl+shift+P`,输入install package再搜索phpcs安装

**安装PEAR:**

    sudo apt-get install php-pear

**安装php code sniffer:**

    sudo pear install PHP_CodeSniffer
    which phpcs` 查看是否安装成功  

**安装php md**

    sudo pear channel-discover pear.phpmd.org
    sudo pear channel-discover pear.pdepend.org
    sudo pear install pdepend/PHP_Depend
    sudo pear install --alldeps phpmd/PHP_PMD
    which phpmd 查看是否安装成功

**安装php-cs-fixer**

    sudo wget http://get.sensiolabs.org/php-cs-fixer.phar -O /usr/local/bin/php-cs-fixer
    sudo chmod a+x /usr/local/bin/php-cs-fixer

**安装scheck,这个可以不用装,这个是facabook提供的一个代码检查工具.**

    cd /opt/
    git clone --depth=1 https://github.com/facebook/pfff.git
    ./configure
    make depend
    make
    make opt

Note:这个插件真没必要装,phpcs和phpmd的代码检查已经够先进了.
如果权限不够,请用sudo.最后一步编译可能会有问题,问题很多,自己解决吧.大多数可以通过apt-get install 解决.
我自己在64位 Ubuntu 14.04 下编译好了一个scheck,[Sublime附件][]

**最后一步修改插件PHP Codesniffer的配置**
配置文件在Preferences->Package Settings->PHP Code Sniffer->Settings-User
添加:

    {
        "phpmd_run": true,
        "phpmd_additional_args": {
            "codesize,controversial,design,naming,unusedcode": ""
        },
        "php_cs_fixer_executable_path":"/usr/local/bin/php-cs-fixer",
        "scheck_executable_path":"/opt/pfff/scheck"
    }

Note:phpmd去掉了cleancode规则,这个规则比较严格,在我们项目中不能在方法里直接创建类使用,所以我禁用了.
phpmd规则:[http://phpmd.org/rules/index.html](http://phpmd.org/rules/index.html)

#### 3. sidebarEnhancements  文件夹选项扩展 只有**sublime 3**有.####

`Ctrl+shift+P`,输入install package,再搜索sidebarEnhancements 安装

#### 4. Git Sublime集成git的插件,这个最好也装下.####

`Ctrl+shift+P`,输入install package,再搜索Git安装

#### 5. WordHighlight 顾名思义,高亮相同与你选择的字符串.####

`Ctrl+shift+P`,输入install package,再搜索WordHighlight安装

#### 6. GotoDocumentation  有点弱的插件....可以让浏览器打开指定的PHP方法文档.####

`Ctrl+shift+P`,输入install package,再搜索GotoDocumentation安装
默认`Ctrl+shift+P`与系统快捷键冲突,需要在Preference->Key Bindings - User设置.

#### 7. PHPnamespace 快速插入namespace或者use.####

`Ctrl+shift+P`,输入install package,再搜索PHPnamespace安装
默认快捷键与系统快捷键冲突,需要在Preference->Key Bindings - User设置.

#### 8. JavaScriptNext  JS语法高亮,支持ES6语法.####
`Ctrl+shift+P`,输入install package,再搜索JavaScriptNext安装
默认快捷键`Ctrl+shift+F`与系统快捷键冲突,需要在Preference->Key Bindings - User设置.

#### 9. JSHint  最好的语法检查工具.####
先用npm安装jshint.不知道什么是npm自行google.

    npm install -g jshint
　　
再用package control安装JSHint.
使用`alt+J`或者`F7`使用.

#### 10. JsFormat   Javascript格式化插件####
直接用package control 安装.
`Ctrl+shift+F`格式化,快捷键会冲突,自己定义快捷键吧.
也可以用`Ctrl+shift+P` 然后输入format:javasctipt

#### 11. emmet 用于html和twig文件的快速编写 ####
直接用package control 安装.
具体用法看[http://blog.csdn.net/lmmilove/article/details/9181323](http://blog.csdn.net/lmmilove/article/details/9181323)

#### 12. Twig Twig语法高亮和自动提示 ####
直接用package control 安装.

#### 13. less less语法高亮 ####
直接用package control 安装.

#### 14. jQuery  在编写jQuery的时候，给出语法提示 ####
直接用package control 安装.

#### 15. less2css 将less编辑成css
具体配置请看：
http://www.qianduan.net/sublime-text-2-less2css-plugin-introduction.html

---------------------------

# 其他 #

#### 1.Sublime的Snippet使用. ####
创建一个snippet, Tools->new Snippet.
具体的语法就不介绍了,可以看[http://sublimetext.info/docs/en/extensibility/snippets.html](http://sublimetext.info/docs/en/extensibility/snippets.html)

这里有我自己写的4个snipet.分别是dao daoImpl service serviceImpl,
把它们放到~/.config/sublime-text-3/Packages/User下面.
`Ctrl+shift+P`,打开命令窗口,然后输入`Dao` `DaoImpl` `Service` `Service Impl`
就可以快速生成代码...[Sublime附件][]

#### 2.　Sublime 保存一个项目 ####
Project->Save Project As..
保存之后,再Edit Project,将配置修改为以下.注意,path为你的项目的跟目录

    {
        "folders":
        [
            {
                "follow_symlinks": true,
                "folder_exclude_patterns":
                [
                        "web/bundles/",
                        "app/cache/",
                        "build"
                ],
                "path": "/var/www/project"
            }
        ]
    }

#### 3. Sublime 中文输入解决方案 ####
需要用到2个文件,分别是ibsublime-imfix.so和sublime_text.desktop,[Sublime附件][]

    sudo cp libsublime-imfix.so /opt/sublime_text/
    sudo cp sublime_text.desktop  /usr/share/applications/

如果还不行的话,请自行编译libsublime-imfix.so编译方法,源文件sublime_imfix.c,可以在[Sublime附件][]找到:
    
    sudo apt-get install pkg-config
    sudo apt-get install build-essential
    sudo apt-get install libgtk2.0-dev
    gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
    sudo cp libsublime-imfix.so /opt/sublime_text/

还不行的话,自求多福!


#### 4. 一些常用的快捷键 ####

**编辑**

Ctrl+C    copy current line (if no selection)

Ctrl+X    cut current line (if no selection)

Ctrl+Shift+K  delete line

Ctrl+↩    insert line after

Ctrl+Shift+↩  insert line before

Ctrl+Shift+↑  move line (or selection) up

Ctrl+L    select line (repeat to select next lines)

Ctrl+D    select word (repeat select others occurrences in context for multiple editing)

Ctrl+M    jump to closing bracket for current code, repeat to jump to opening bracket

Ctrl+Shift+M  select all contents of the current brackets (curly brackets, square brackets, parentheses)

Ctrl+KK   delete from cursor to end of line

Ctrl+K+⌫  delete from cursor to start of line

Ctrl+]    indent current line(s)

Ctrl+[    un-indent current line(s)

Ctrl+Shift+D  duplicate line(s)

Ctrl+J    join line below to the end of the current line

Ctrl+ /   comment/un-comment current line

Ctrl+Shift+/  block comment current selection

Ctrl+Y    redo, or repeat last keyboard shortcut command

Ctrl+Shift+V  paste and indent correctly

Ctrl+Space    select next auto-complete suggestion

Ctrl+U    soft undo (somehow undoes your movements; it jumps to your last change before undoing it when you repeat this command)

**导航**

Ctrl+P    quick-open files by name in your project (doesn’t seem to need an actual project set up, it just searches in the directories around the currently-opened file

Ctrl+R    goto symbol (functions and classes) in the file. Same as Ctrl+P, then type @

Ctrl+;    goto word in current file. Same as Ctrl+P, then type #

Ctrl+G    goto line in current file. Same as Ctrl+P, then type :

F12       goto definition 这个很有用,可以导航到方法或者类定义的地方.  

**常用**

Ctrl+Shift+P  command prompt

Ctrl+KB   toggle side bar

**查看替换**

Ctrl+F    find

Ctrl+H    replace

Ctrl+Shift+F  find in files

**Tabs**

Ctrl+Shift+t  open last closed tab (just like in your browser)

Ctrl+PgDn cycle down through open tabs, cycle up with Ctrl+PgUp

Ctrl+⇆    cycle through last tabs (repeat to go back further in history)

**拆分窗口**

Alt+Shift+2   split into two columns

Alt+Shift+1   revert to single column

Alt+Shift+5   grid (4 groups)

Ctrl+[1,2,3,4]    jump to “group” (pane)

Ctrl+Shift+[1,2,3,4]  move file to specified group

**书签**

Ctrl+F2   toggle bookmark

F2    next bookmark

Shift+F2  previous bookmark

Ctrl+Shift+F2 clear bookmarks

**大写小写**

Ctrl+KU   upper case

Ctrl+KL   lower case

[Sublime附件]:https://github.com/wenqinruan/sublime-attchment
