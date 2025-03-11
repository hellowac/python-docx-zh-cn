.. _WdCellVerticalAlignment:

``WD_CELL_VERTICAL_ALIGNMENT``
==============================

.. tab:: 中文

    别名: **WD_ALIGN_VERTICAL**

    指定表格中一个或多个单元格中的文本的垂直对齐方式。

    例子::

        from docx.enum.table import WD_ALIGN_VERTICAL

        table = document.add_table(3, 3)
        table.cell(0, 0).vertical_alignment = WD_ALIGN_VERTICAL.BOTTOM

    ----

    TOP
        文本与单元格的上边框对齐。

    CENTER
        文本与单元格中心对齐。

    BOTTOM
        文本与单元格的下边框对齐。

    BOTH
        这是 OpenXml 规范中的一个选项，但不是 Word 本身的选项。目前尚不清楚此设置会产生什么 Word 行为。如果您发现，请告诉我们，我们会更新此文档。否则，最好避免使用此选项。

.. tab:: 英文

    alias: **WD_ALIGN_VERTICAL**

    Specifies the vertical alignment of text in one or more cells of a table.

    Example::

        from docx.enum.table import WD_ALIGN_VERTICAL

        table = document.add_table(3, 3)
        table.cell(0, 0).vertical_alignment = WD_ALIGN_VERTICAL.BOTTOM

    ----

    TOP
        Text is aligned to the top border of the cell.

    CENTER
        Text is aligned to the center of the cell.

    BOTTOM
        Text is aligned to the bottom border of the cell.

    BOTH
        This is an option in the OpenXml spec, but not in Word itself. It's not
        clear what Word behavior this setting produces. If you find out please let
        us know and we'll update this documentation. Otherwise, probably best to
        avoid this option.
