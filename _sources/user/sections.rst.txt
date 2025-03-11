.. _sections:

使用节
=====================

Working with Sections

.. tab:: 中文

    Word 支持“节”（ `section` ）的概念，即文档中具有相同页面布局设置（如页边距和页面方向）的节。例如，文档中某些页面可以采用纵向布局，而另一些页面采用横向布局。每个节还定义了适用于该节页面的页眉和页脚。

    大多数 Word 文档只有一个默认节，而且大多数节没有理由更改默认页边距或其他页面布局。但是，当您确实需要更改页面布局时，您需要了解节才能完成。

.. tab:: 英文

    Word supports the notion of a `section`, a division of a document having the same page
    layout settings, such as margins and page orientation. This is how, for example, a
    document can contain some pages in portrait layout and others in landscape. Each section
    also defines the headers and footers that apply to the pages of that section.

    Most Word documents have only the single section that comes by default and further, most
    of those have no reason to change the default margins or other page layout. But when you
    `do` need to change the page layout, you'll need to understand sections to get it done.


访问节
------------------

Accessing sections

.. tab:: 中文

    通过 |Document| 对象上的 ``sections`` 属性可以访问文档节::

        >>> document = Document()
        >>> sections = document.sections
        >>> sections
        <docx.parts.document.Sections object at 0x1deadbeef>
        >>> len(sections)
        3
        >>> section = sections[0]
        >>> section
        <docx.section.Section object at 0x1deadbeef>
        >>> for section in sections:
        ...     print(section.start_type)
        ...
        NEW_PAGE (2)
        EVEN_PAGE (3)
        ODD_PAGE (4)

    理论上，文档可以没有任何明确的节，
    尽管我还没有看到这种情况在实际中发生。如果您正在访问
    不可预测的 .docx 文件数量，您可能希望使用 ``len()`` 检查或 ``try`` 块来应对这种可能性，以避免未捕获的
    ``IndexError`` 异常停止您的程序。

.. tab:: 英文

    Access to document sections is provided by the ``sections`` property on the
    |Document| object::

        >>> document = Document()
        >>> sections = document.sections
        >>> sections
        <docx.parts.document.Sections object at 0x1deadbeef>
        >>> len(sections)
        3
        >>> section = sections[0]
        >>> section
        <docx.section.Section object at 0x1deadbeef>
        >>> for section in sections:
        ...     print(section.start_type)
        ...
        NEW_PAGE (2)
        EVEN_PAGE (3)
        ODD_PAGE (4)

    It's theoretically possible for a document not to have any explicit sections,
    although I've yet to see this occur in the wild. If you're accessing an
    unpredictable population of .docx files you may want to provide for that
    possibility using a ``len()`` check or ``try`` block to avoid an uncaught
    ``IndexError`` exception stopping your program.


添加新节
--------------------

Adding a new section

.. currentmodule:: docx.api

.. tab:: 中文

    :meth:`Document.add_section` 方法允许在文档末尾开始新的节。调用此方法后添加的段落和表格将出现在新节中::

        >>> current_section = document.sections[-1] # 文档中的最后一节
        >>> current_section.start_type
        NEW_PAGE (2)
        >>> new_section = document.add_section(WD_SECTION.ODD_PAGE)
        >>> new_section.start_type
        ODD_PAGE (4)

.. tab:: 英文

    The :meth:`Document.add_section` method allows a new section to be started at
    the end of the document. Paragraphs and tables added after calling this method
    will appear in the new section::

        >>> current_section = document.sections[-1]  # last section in document
        >>> current_section.start_type
        NEW_PAGE (2)
        >>> new_section = document.add_section(WD_SECTION.ODD_PAGE)
        >>> new_section.start_type
        ODD_PAGE (4)


节属性
------------------

Section properties

.. currentmodule:: docx.section

.. tab:: 中文

    |Section| 对象有 11 个属性，允许发现和指定页面布局设置。

.. tab:: 英文

    The |Section| object has eleven properties that allow page layout settings to
    be discovered and specified.


节开始类型
~~~~~~~~~~~~~~~~~~

Section start type

.. tab:: 中文

    :attr:`Section.start_type` 描述了在 section::

        >>> section.start_type
        NEW_PAGE (2)
        >>> section.start_type = WD_SECTION.ODD_PAGE
        >>> section.start_type
        ODD_PAGE (4)

    ``start_type`` 的值是 :ref:`WdSectionStart` 枚举的成员。

.. tab:: 英文

    :attr:`Section.start_type` describes the type of break that precedes the
    section::

        >>> section.start_type
        NEW_PAGE (2)
        >>> section.start_type = WD_SECTION.ODD_PAGE
        >>> section.start_type
        ODD_PAGE (4)

    Values of ``start_type`` are members of the :ref:`WdSectionStart` enumeration.


页面尺寸和方向
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Page dimensions and orientation

.. tab:: 中文

    |Section| 上的三个属性描述了页面尺寸和方向。 这些属性可以一起使用，例如将节的​​方向从纵向更改为横向::

        >>> section.orientation, section.page_width, section.page_height
        (PORTRAIT (0), 7772400, 10058400)  # (Inches(8.5), Inches(11))
        >>> new_width, new_height = section.page_height, section.page_width
        >>> section.orientation = WD_ORIENT.LANDSCAPE
        >>> section.page_width = new_width
        >>> section.page_height = new_height
        >>> section.orientation, section.page_width, section.page_height
        (LANDSCAPE (1), 10058400, 7772400)

.. tab:: 英文

    Three properties on |Section| describe page dimensions and orientation.
    Together these can be used, for example, to change the orientation of a section
    from portrait to landscape::

        >>> section.orientation, section.page_width, section.page_height
        (PORTRAIT (0), 7772400, 10058400)  # (Inches(8.5), Inches(11))
        >>> new_width, new_height = section.page_height, section.page_width
        >>> section.orientation = WD_ORIENT.LANDSCAPE
        >>> section.page_width = new_width
        >>> section.page_height = new_height
        >>> section.orientation, section.page_width, section.page_height
        (LANDSCAPE (1), 10058400, 7772400)


页边距
~~~~~~~~~~~~

Page margins

.. tab:: 中文

    |Section| 上的七个属性共同指定了各种边缘间距，这些间距决定了文本在页面上的显示位置：

        >>> from docx.shared import Inches
        >>> section.left_margin, section.right_margin
        (1143000, 1143000)  # (Inches(1.25), Inches(1.25))
        >>> section.top_margin, section.bottom_margin
        (914400, 914400)  # (Inches(1), Inches(1))
        >>> section.gutter
        0
        >>> section.header_distance, section.footer_distance
        (457200, 457200)  # (Inches(0.5), Inches(0.5))
        >>> section.left_margin = Inches(1.5)
        >>> section.right_margin = Inches(1)
        >>> section.left_margin, section.right_margin
        (1371600, 914400)

.. tab:: 英文

    Seven properties on |Section| together specify the various edge spacings that
    determine where text appears on the page::

        >>> from docx.shared import Inches
        >>> section.left_margin, section.right_margin
        (1143000, 1143000)  # (Inches(1.25), Inches(1.25))
        >>> section.top_margin, section.bottom_margin
        (914400, 914400)  # (Inches(1), Inches(1))
        >>> section.gutter
        0
        >>> section.header_distance, section.footer_distance
        (457200, 457200)  # (Inches(0.5), Inches(0.5))
        >>> section.left_margin = Inches(1.5)
        >>> section.right_margin = Inches(1)
        >>> section.left_margin, section.right_margin
        (1371600, 914400)
