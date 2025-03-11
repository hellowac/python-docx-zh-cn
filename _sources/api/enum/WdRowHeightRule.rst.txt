.. _WdRowHeightRule:

``WD_ROW_HEIGHT_RULE``
======================

.. tab:: 中文

    别名: **WD_ROW_HEIGHT**

    规定确定表格行高规则

    Example::

        from docx.enum.table import WD_ROW_HEIGHT_RULE

        table = document.add_table(3, 3)
        table.rows[0].height_rule = WD_ROW_HEIGHT_RULE.EXACTLY

    ----

    AUTO
        行高会进行调整以适应行中的最高值。

    AT_LEAST
        行高至少为指定的最小值。

    EXACTLY
        行高是一个精确值。

.. tab:: 英文

    alias: **WD_ROW_HEIGHT**

    Specifies the rule for determining the height of a table row

    Example::

        from docx.enum.table import WD_ROW_HEIGHT_RULE

        table = document.add_table(3, 3)
        table.rows[0].height_rule = WD_ROW_HEIGHT_RULE.EXACTLY

    ----

    AUTO
        The row height is adjusted to accommodate the tallest value in the row.

    AT_LEAST
        The row height is at least a minimum specified value.

    EXACTLY
        The row height is an exact value.
