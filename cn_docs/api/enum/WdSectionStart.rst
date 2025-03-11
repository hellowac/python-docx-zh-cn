.. _WdSectionStart:

``WD_SECTION_START``
====================

.. tab:: 中文

    别名: **WD_SECTION**

    指定分节符的开始类型。

    例子::

        from docx.enum.section import WD_SECTION

        section = document.sections[0]
        section.start_type = WD_SECTION.NEW_PAGE

    ----

    CONTINUOUS
        连续分节符。

    NEW_COLUMN
        新的列分节符。

    NEW_PAGE
        新的页面分节符。

    EVEN_PAGE
        偶数页分节符。

    ODD_PAGE
        章节从下一个奇数页开始。

.. tab:: 英文

    alias: **WD_SECTION**

    Specifies the start type of a section break.

    Example::

        from docx.enum.section import WD_SECTION

        section = document.sections[0]
        section.start_type = WD_SECTION.NEW_PAGE

    ----

    CONTINUOUS
        Continuous section break.

    NEW_COLUMN
        New column section break.

    NEW_PAGE
        New page section break.

    EVEN_PAGE
        Even pages section break.

    ODD_PAGE
        Section begins on next odd page.
