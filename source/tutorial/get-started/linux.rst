GMT初探: Linux篇
================

启动终端
--------

GMT是一个纯命令行软件，没有任何的图形界面。所有的绘图操作都需要通过
在终端和脚本中执行命令来完成。
终端是Linux系统的标配，通常你可以在系统的“应用程序”中找到并启动它。

运行GMT
-------

启动终端后，敲入 ``gmt`` 以执行GMT命令。你将看到GMT的欢迎界面信息，类似于::

        GMT - The Generic Mapping Tools, Version 6.0.0 [64-bit] [8 cores]
        (c) 1991-2019 The GMT Team (https://www.generic-mapping-tools.org/team.html).

    Supported in part by the US National Science Foundation (http://www.nsf.gov/)
    and volunteers from around the world.

    GMT is distributed under the GNU LGP License (http://www.gnu.org/licenses/lgpl.html).

    usage: gmt [options]
        gmt <module name> [<module-options>]

    options:
    --help            List descriptions of available GMT modules.
    --new-script      Write GMT modern mode script template to stdout.
    --show-bindir     Show directory with GMT executables.
    --show-citation   Show the most recent citation for GMT.
    --show-cores      Show number of available cores.
    --show-datadir    Show directory/ies with user data.
    --show-dataserver Show URL of the remote GMT data server.
    --show-doi        Show the DOI for the current release.
    --show-modules    Show all module names.
    --show-library    Show path of the shared GMT library.
    --show-plugindir  Show directory for plug-ins.
    --show-sharedir   Show directory for shared GMT resources.
    --version         Print GMT version number.

    if <module-options> is '=' we call exit (0) if module exist and non-zero otherwise.

生成脚本模板
------------

继续在终端中敲入::

    gmt --new-script > myplot.sh

该命令会生成一个GMT模板脚本，并保存到Bash脚本文件 :file:`myplot.sh` 中。

.. note::

    本手册中所有示例均使用Bash脚本，要求读者对Bash脚本及Unix命令行有最基本的了解。
    不了解的用户请阅读网络上Bash相关教程，或本手册中 :doc:`/tutorial/scripting` 一节。

查看并编辑脚本文件
------------------

Bash脚本文件是一个纯文本文件，可以直接用文本编辑器打开。比如，可以使用大多数
Linux都自带了的文本编辑器 **gedit** 打开该脚本文件::

    gedit myplot.sh

打开脚本文件后会看到如下内容::

    #!/usr/bin/env bash
    # GMT modern mode bash template
    # Date:    2019-09-10T00:44:39
    # User:    seisman
    # Purpose: Purpose of this script
    export GMT_SESSION_NAME=$$	# Set a unique session name
    gmt begin figurename
        # Place modern session commands here
    gmt end show

其中，以 **#** 开头的行尾注释行，\ **export GMT_SESSION_NAME=$$** 这一行属于
高级用法，可以忽略。因而核心内容只有两行，即 **gmt begin** 和 **gmt end** 这两行。

编辑脚本，在 **gmt begin** 和 **gmt end** 中间添加GMT命令，将脚本修改如下::

    #!/usr/bin/env -S bash -e
    # GMT modern mode bash template
    # Date:    2019-09-10T00:44:39
    # User:    seisman
    # Purpose: Purpose of this script
    export GMT_SESSION_NAME=$$	# Set a unique session name
    gmt begin figurename
        gmt coast -Rg -JH15c -Gpurple -Baf -B+t"My First Plot"
    gmt end show

编辑完成后记得保存文件。

执行脚本以绘图
--------------

回到终端，运行Bash脚本::

    bash myplot.sh

待脚本执行完成后，会自动用阅读器（通常是evince）打开生成的PDF格式的图片文件。
你将看到如下图所示的图片。

.. gmtplot::
    :width: 75%
    :show-code: false

    #!/usr/bin/env bash
    # GMT modern mode bash template
    # Date:    2019-09-10T00:44:39
    # User:    seisman
    # Purpose: Purpose of this script
    export GMT_SESSION_NAME=$$	# Set a unique session name
    gmt begin figurename png,pdf
        gmt coast -Rg -JH15c -Gpurple -Baf -B+t"My First Plot"
    gmt end

这基本上就是运行GMT脚本的基本流程，即：

- 生成脚本模板
- 编辑脚本，添加GMT绘图命令
- 运行脚本并查看绘图效果
