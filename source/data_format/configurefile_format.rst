配置文件格式的选择
==================

配置文件通常有以下几种选择:

-  二进制文件

   二进制文件的好处是程序读写非常方便, 但是因为可读性和其他一些问题, 通常不会使用二进制文件作为配置文件.

-  文本文件

   因为可读性好, 文本文件非常适合用作配置文件.

   当然, 文本文件是个大概念, 通常用作配置文件的文本文件格式有:

   -  ``INI文件``

   -  ``XML文件``

   -  ``JSON文件``

   -  ``YAML文件``


   ``INI``\ 文件对于比较简单的配置是很方便的, 但是对于复杂的情况就不太适用了.
   对于比较复杂的配置, 可以使用\ ``JSON``, ``YAML``\ 或\ ``XML``\ 格式的文件; 相比较而言, ``XML``\ 更加复杂.

-  数据库

   数据库也可以存储配置参数, 不过这有些大材小用了.

   数据库通常的使用是用来存储结构相同的记录, 对于记录的插入, 查询等操作,
   有独特的优势.
