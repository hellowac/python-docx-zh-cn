.. _MsoColorType:

``MSO_COLOR_TYPE``
==================

.. tab:: 中文

    指定颜色规范方案

    例子::

        from docx.enum.dml import MSO_COLOR_TYPE

        assert font.color.type == MSO_COLOR_TYPE.THEME

    ----

    RGB
        颜色由 |RGBColor| 值指定。

    THEME
        颜色是预设的主题颜色之一。

    AUTO
        颜色由应用程序自动确定。

.. tab:: 英文

    Specifies the color specification scheme

    Example::

        from docx.enum.dml import MSO_COLOR_TYPE

        assert font.color.type == MSO_COLOR_TYPE.THEME

    ----

    RGB
        Color is specified by an |RGBColor| value.

    THEME
        Color is one of the preset theme colors.

    AUTO
        Color is determined automatically be the application.
