YAML简介
========

`JS-YAML在线解析器 <http://nodeca.github.io/js-yaml/>`_

`维基百科-YAML <https://zh.wikipedia.org/zh-cn/YAML>`_

编程免不了要写配置文件, 怎么写配置文件也是一门学问.
``YAML``\ 是专门用来写配置文件的语言, 简洁和强大.

``YAML``\ (/ˈjæməl/), 是\ **YAML Ain't a Markup Language**\ (``YAML``\ 不是一种标记语言)的递归缩写.

在开发这种语言时, ``YAML``\ 的意思起始是: **Yet Another Markup Language**\ (仍是一种标记语言), 
但为了强调这种语言以数据为中心, 而不是以标记语言为重点, 而用反向缩略语重命名.


简介
----

YAML的基本语法规则:

    + 大小写敏感;
    + 使用缩进表示层级关系;
    + **缩进时不允许使用Tab键, 只允许使用空格(否则会导致解析错误);**
    + 缩进的空格数目不重要(通常使用两个或四个空格), 但相同的层级要使用相同的缩进;
    + 以\ ``#``\ 开头的行表示注释, 只支持单行注释.

YAML支持三种数据结构:

    + 键值对
    + 数组
    + 常量


键值对
------

* 键值对, 使用\ ``:``\ 结构表示, 格式为: ``key: value``, 冒号后面要加一个空格

    .. code-block:: text

        key: value

* value可以是其它的数据结构, 用缩进表示层级关系

    .. code-block:: text

        key:
            # value是一个键值对
            child_key_1: value1
            child_key_2: value2

* 在YAML中, 键值对还可以使用花括号\ ``{}``\ 义, 项之间用逗号分隔, 这样可以将key和value写在一行

    .. code-block:: text

        {key: value}
        {key: {child_key_1: value1, child_key_2: value2}}


数组
-----

* 使用一个\ ``-``\ 加一个空格表示一个数组元素, 所有的数组元素构成一个数组

    .. code-block:: text

        hobby:
            - Java
            - LOL

* 对于数组，也可以将数组元素写在一行内(用\ ``[]``\ 包裹数组元素, 数组元素之间用逗号分隔)

.. code-block:: text

    hobby: [Java, LOL]


复合结构
---------

键值对和数组可以组合使用，构成复合结构(使用缩进表示层次关系).

示例:

    .. code-block:: text

        languages:
            - Ruby
            - Perl
            - Python

        Websites:
            YAML: yaml.org
            Ruby: ruby-lang.org
            Python: python.org
            Perl: use.perl.org


常量
----

YAML中提供了多种常量类型:

    + 字符串
    + 布尔值
    + 整数
    + 浮点数
    + Null
    + 时间
    + 日期


* 数值直接以字面量的形式表示

    示例:

    .. code-block:: text

        float:
            - 3.14
            - 6.8523015e+5 # 可以使用科学计数法

        int:
            - 123
            - 0b1010_0111_0100_1010_1110 # 二进制表示


* 布尔值用\ ``TRUE`` / ``True`` / ``true`` 和\ ``FALSE`` / ``False`` / ``false``\ 表示

    示例:

    .. code-block:: text

        boolean:
            - True
            - False

* ``Null``\ 用\ ``~``\ 表示
 
    示例:

    .. code-block:: text

        Null:
            nodeName: 'node'
            parent: ~

* 日期采用ISO8601格式(``YYYY-MM-DD``)

    示例:

    .. code-block:: text

        # 年月日, 用-分隔
        date: 1976-07-31 

* 时间

    示例:

    .. code-block:: text
    
        datetime: 2018-12-3T15:30:30+08:00 
        # 时分秒之间用 : 分隔
        # 年月日之间用 - 分隔
        # 日期和时间之间用T连接, 最后使用+代表时区


字符串
------

字符串是最常见的, 也是最复杂的一种数据类型.

* 字符串默认不使用引号表示

    示例:

    .. code-block:: text

        str: This is a string

* 如果字符串中包含特殊字符, 需要用引号包裹

    示例:

    .. code-block:: text

        str: 'content: string'

    .. note::

        用引号包裹, 显式的表示引号内的部分是一个字符串.

* 单引号和双引号都可以使用, 双引号不会对特殊字符转义

    示例:

    .. code-block:: text

        s1: 'content\n字符串'
        s2: "content\n字符串"


    .. note::

        双引号内的特殊字符, 保持特殊字符的意义;

        单引号内的特殊字符会被转义, 表示其字面意义(所见即所得).

* 单引号之中如果还有单引号, 必须连续使用两个单引号转义

    示例:

    .. code-block:: text

        str: 'labor''s day'


引用
----

重复的内容在YAML中可以使用\ ``&``\ 定义锚点, 使用\ ``*``\ 引用锚点;
定义锚点的格式为: ``&锚点名``, 引用锚点的格式为: ``*锚点名``.

* 可以在定义数据的同时定义锚点

    .. code-block:: text

        hr:
            - Mark McGwire
            - &SS Samy Sosa # 定义一个名为SS的锚点, 其代表的值为Samy Sosa
        rbi:
            - *SS # 引用锚点
            - Ken Griffey

* 可以将锚点作为一个单独的键值对定义(定义一个专门用作锚点的键值对)

    .. code-block:: text

        SS: &SS Samy Sosa
        hr:
            - Mark McGwire
            - *SS
        rbi:
            - *SS
            - Ken Griffey

    .. note::

        * 不能单独的定义锚点, 比如不能直接写: &SS Sammy Sosa.
          必须先定义一个对象, 然后把这个对象定义为一个锚点, 锚点表示其定义位置后的对象.
          锚点有点类似于C语言中的取地址，要取地址，被取地址的对象必须要已定义.

        * 对一个键值对定义锚点时, 注意锚点定义的位置: 在\ ``:``\ 之后, \ ``value``\ 之前.

* 锚点能够定义更复杂的内容

    .. code-block:: text

        default: &default
            - Mark McGwire
            - Samy Sosa
        hr: *default


合并内容
--------

合并内容主要和锚点配合使用, 将一个锚点内容抽取合并到一个对象中, 作为当前对象的一部分.

* 使用\ ``<<``\ 合并内容

    示例:

    .. code-block:: text

        merge:
            - &CENTER {x: 1, y: 2}
            - &LEFT {x: 0, y: 2}
            - &BIG {r: 10}
            - &SMALL {r: 1}
    
        sample1:
            <<: *CENTER
            r: 10
       
        sample2:
            <<: [ *CENTER, *BIG ]
            other: haha

        sample3:
            <<: [ *CENTER, *BIG ]
            r: 100

    .. note::
    
        使用锚点和合并功能时, 可以将一个锚点的内容合并到一个对象中;
    
        如果锚点中的某一个项在对象中已经存在, 则忽略锚点中的该项目.

* 有了合并, 就可以在配置中, 把相同的基础配置抽取出来, 在不同的子配置中合并引用即可.

