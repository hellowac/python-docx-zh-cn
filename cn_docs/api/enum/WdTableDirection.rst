.. _WdTableDirection:

``WD_TABLE_DIRECTION``
======================

.. tab:: 中文

    指定应用程序在指定表格或行中排列单元格的方向。

    示例::

        from docx.enum.table import WD_TABLE_DIRECTION

        table = document.add_table(3, 3)
        table.direction = WD_TABLE_DIRECTION.RTL

    ----

    LTR
        表格或行的排列方式为第一列位于最左侧。

    RTL
        表格或行的排列方式为第一列位于最右侧。

.. tab:: 英文

    Specifies the direction in which an application orders cells in the specified table or row.

    Example::

        from docx.enum.table import WD_TABLE_DIRECTION

        table = document.add_table(3, 3)
        table.direction = WD_TABLE_DIRECTION.RTL

    ----

    LTR
        The table or row is arranged with the first column in the leftmost position.

    RTL
        The table or row is arranged with the first column in the rightmost position.
