.. _WdRowAlignment:

``WD_TABLE_ALIGNMENT``
======================

.. tab:: 中文

    指定表格对齐类型。

    例子::

        from docx.enum.table import WD_TABLE_ALIGNMENT

        table = document.add_table(3, 3)
        table.alignment = WD_TABLE_ALIGNMENT.CENTER

    ----

    LEFT
        左对齐

    CENTER
        中间对齐

    RIGHT
        右对齐

.. tab:: 英文

    Specifies table justification type.

    Example::

        from docx.enum.table import WD_TABLE_ALIGNMENT

        table = document.add_table(3, 3)
        table.alignment = WD_TABLE_ALIGNMENT.CENTER

    ----

    LEFT
        Left-aligned

    CENTER
        Center-aligned.

    RIGHT
        Right-aligned.
