.. _WdOrientation:

``WD_ORIENTATION``
==================

.. tab:: 中文

    别名: **WD_ORIENT**

    指定页面布局方向。

    Example::

        from docx.enum.section import WD_ORIENT

        section = document.sections[-1]
        section.orientation = WD_ORIENT.LANDSCAPE

    ----

    PORTRAIT
        纵向。

    LANDSCAPE
        横向。

.. tab:: 英文

    alias: **WD_ORIENT**

    Specifies the page layout orientation.

    Example::

        from docx.enum.section import WD_ORIENT

        section = document.sections[-1]
        section.orientation = WD_ORIENT.LANDSCAPE

    ----

    PORTRAIT
        Portrait orientation.

    LANDSCAPE
        Landscape orientation.
