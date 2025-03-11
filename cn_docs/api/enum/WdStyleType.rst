.. _WdStyleType:

``WD_STYLE_TYPE``
=================

.. tab:: 中文

    指定四种样式类型之一：段落、字符、列表或表格。

    例子::

        from docx import Document
        from docx.enum.style import WD_STYLE_TYPE

        styles = Document().styles
        assert styles[0].type == WD_STYLE_TYPE.PARAGRAPH

    ----

    CHARACTER
        字符样式

    LIST
        列表样式

    PARAGRAPH
        段落样式

    TABLE
        表格样式

.. tab:: 英文

    Specifies one of the four style types: paragraph, character, list, or table.

    Example::

        from docx import Document
        from docx.enum.style import WD_STYLE_TYPE

        styles = Document().styles
        assert styles[0].type == WD_STYLE_TYPE.PARAGRAPH

    ----

    CHARACTER
        Character style.

    LIST
        List style.

    PARAGRAPH
        Paragraph style.

    TABLE
        Table style.
