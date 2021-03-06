﻿.. currentmodule:: module-compiler

使用说明
=========================================================

该工具为一个 jar 包, 推荐嵌入到 ant 中, 作为项目构建的一个阶段.

.. note::

    ant 以及相关压缩工具可直接使用 `kissy-tools <https://github.com/kissyteam/kissy-tools>`_ 中的文件,
    建议直接下载整个 kissy-tools 作为项目工具一部分.
    
    
使用前请先下载 kissy 源码到本地硬盘 ``x:/kissy/`` , kissy-tools 源码到硬盘 ``x:/kissy-tools/`` , 假设项目源码在 ``x:/code/`` , 如上一节包括两个模块文件: ``x:/code/package/x.js`` 以及 ``x:/code/package/y.js`` , 则 ant 的调用为：

.. code-block:: xml

    <java classname="com.taobao.f2e.Main">

        <arg value="-requires"/>
        <arg value="package/y"/>
        <arg value="-baseUrls"/>
        <arg value="x:/kissy/,x:/code/"/>
        <arg value="-encodings"/>
        <arg value="utf-8,gbk"/>
        <arg value="-outputEncoding"/>
        <arg value="utf-8"/>
        <arg value="-excludes"/>
        <arg value="core"/>
        <arg value="-output"/>
        <arg value="x:/code/package/y.combine.js"/>

        <classpath>
            <pathelement path="x:/kissy-tools/module-compiler/module-compiler.jar"/>
            <pathelement path="${java.class.path}"/>
        </classpath>
                
    </java>    
    
如上所示该工具需要一些参数, 包括 ``requires``  , ``baseUrls`` , ``encodings`` , ``outputEncoding`` , ``excludes`` , ``output`` , 具体格式如下：

requires
----------------------------------------------------

需要打包的模块名集合, 该模块以及其递归依赖都会被一并打包. 多个模块名用 ``,`` 分隔. 如以上示例： ``package/y`` .


baseUrls
----------------------------------------------------------   

模块文件查找目录集合, 一般存在两个： ``kissy`` 内置模块目录以及业务模块源码目录, 目录间以 ``,`` 分隔.
如以上示例 ``x:/kissy/,x:/code/`` .


encodings
-----------------------------------------------------------

指明模块目录中文件的编码, 顺序对应于 ``baseUrls`` , 多个编码以 ``,`` 分隔. 如以上示例： ``utf-8,gbk`` ,
表示 ``kissy`` 内置模块为 ``utf-8`` 编码, 业务模块为 ``gbk`` 编码.


outputEncoding
---------------------------------------
指明最后合并打包文件的编码格式. 如以上示例 ``utf-8`` .


excludes
-------------------------------------

指明 ``requires`` 递归依赖模块中不需要打包的模块名称集合, 该集合内的模块是单独动态加载或静态引入的, 多个模块以 ``,`` 分隔.
如以上示例 ``core`` 表示 ``kissy`` 的 ``core`` 模块不需要合并打包, 是通过 ``kissy.js`` 静态引入到页面中的.

output
--------------------------------------------

指明最终合并打包后的文件路径以及名称. 如以上示例： ``x:/code/package/y.combine.js`` ,
表示该工具产生的合并后文件为 ``x:/code/package/y.combine.js`` .

