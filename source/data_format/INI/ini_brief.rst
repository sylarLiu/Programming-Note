INI文件格式简介
===============

其实\ ``INI``\ 文件就是简单的文本文件, 只不过其遵循一定的\ ``INI``\ 文件格式.

``INI``\ 就是英文\ *initialization*\ 的头三个字母的缩写, ``INI``\ 文件的后缀名也不一定是\ *.ini*\ , 也可以是\ *.cfg*\, \ *.conf*\ 或\ *.txt*\ .

INI文件的格式
-------------

``INI``\ 文件的格式很简单, 最基本的三个要素是: ``section``, ``parameter``\ 和\ ``comment``.

``section``
^^^^^^^^^^^

``section``\ 的形式如下所示: 
      
    .. code-block:: text
        :emphasize-lines: 1

        [section]

    * 所有的\ ``parameter``\ 都是以\ ``section``\ 为单位结合在一起的;
    * 每个\ ``section``\ 名称独占一行, 并且\ ``section``\ 名字都被方括号包裹着;
    * 在一个\ ``section``\ 声明后的所有\ ``parameter``\ 都属于该\ ``section``\ ;
    * 对于一个\ ``section``\ , 没有显式的结束标识符, 一个\ ``section``\ 的开始就是上一个\ ``section``\ 的结束, 或到达文件结尾;
    * 在一般情况下, \ ``section``\ 不能嵌套.

``parameter``
^^^^^^^^^^^^^

``parameter``\ 的形式如下所示:

    .. code-block:: text
        :emphasize-lines: 1

        name = value

``INI``\ 所包含的最基本元素即使\ ``parameter``\ , 每一个\ ``parameter``\ 都有一个\ ``name``\ 和\ ``value``\ , 
``name``\ 和\ ``value``\ 由\ ``=``\ 隔开, ``name``\ 在等号的左边.

``comment``
^^^^^^^^^^^

注释的形式为:

    .. code-block:: text
        :emphasize-lines: 1

        ; comment text

在\ ``INI``\ 文件中的注释语句以\ ``;``\ 开头, 其后的文字直到本行结束都是注释.


总结
----

``INI``\ 这种文件格式, 一是易读, 二是易于修改, 三是前向兼容, 即兼容旧文件.

    * 若是配置内容有减少, 读取旧配置文件时, 只是不处理多出来的关键字即可;
    * 若是配置内容有增加, 读取旧配置文件会导致相应的关键字读不到值, 读取时可以判断出来, 提示版本不匹配, 或者使用默认值以保持系统运行.

