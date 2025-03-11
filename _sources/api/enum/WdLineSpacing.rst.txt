.. _WdLineSpacing:

``WD_LINE_SPACING``
===================

.. tab:: 中文

    指定应用于段落的行距格式。

    例子::

        from docx.enum.text import WD_LINE_SPACING

        paragraph = document.add_paragraph()
        paragraph.paragraph_format.line_spacing_rule = WD_LINE_SPACING.EXACTLY

    ----

    ONE_POINT_FIVE
        一个半空格的行距。

    AT_LEAST
        行距始终至少为指定量。该量单独指定。

    DOUBLE
        双倍行距。

    EXACTLY
        行距正好是指定量。该量另行指定。

    MULTIPLE
        行距被指定为行高的倍数。更改字体大小将按比例更改行距。

    SINGLE
        单倍行距 (default).

.. tab:: 英文

    Specifies a line spacing format to be applied to a paragraph.

    Example::

        from docx.enum.text import WD_LINE_SPACING

        paragraph = document.add_paragraph()
        paragraph.paragraph_format.line_spacing_rule = WD_LINE_SPACING.EXACTLY

    ----

    ONE_POINT_FIVE
        Space-and-a-half line spacing.

    AT_LEAST
        Line spacing is always at least the specified amount. The amount is
        specified separately.

    DOUBLE
        Double spaced.

    EXACTLY
        Line spacing is exactly the specified amount. The amount is specified
        separately.

    MULTIPLE
        Line spacing is specified as a multiple of line heights. Changing the font
        size will change the line spacing proportionately.

    SINGLE
        Single spaced (default).
