
使用样式
===================

Working with Styles

.. tab:: 中文

    本页使用了上一页中开发的概念，但未作介绍。如果术语不熟悉，请参阅上一页 :ref:`understanding_styles` 以了解其定义。

.. tab:: 英文

    This page uses concepts developed in the prior page without introduction. If a term is unfamiliar, consult the prior page :ref:`understanding_styles` for a definition.


访问样式
--------------

Access a style

.. tab:: 中文

    使用 :attr:`.Document.styles` 属性访问样式::

        >>> document = Document()
        >>> styles = document.styles
        >>> styles
        <docx.styles.styles.Styles object at 0x10a7c4f50>

    |Styles| 对象提供按名称定义样式的字典式访问::

        >>> styles['Normal']
        <docx.styles.style._ParagraphStyle object at <0x10a7c4f6b>

    .. note:: 内置样式使用其英文名称（例如“Heading 1”）存储在 WordprocessingML 文件中，即使使用本地化版本的 Word 的用户将在 UI 中看到本地语言名称（例如“Kop 1”）。由于 |docx| 操作 WordprocessingML 文件，因此样式查找必须使用英文名称。此外部网站上提供的文档允许您创建本地语言名称和英文样式名称之间的映射：http://www.thedoctools.com/index.php?show=mt_create_style_name_list

    用户定义的样式（也称为 *自定义样式* ）未本地化，并且可以使用与 Word UI 中显示的名称完全相同的名称进行访问。

    |Styles| 对象也是可迭代的。通过使用 |BaseStyle| 上的标识属性，可以生成已定义样式的各种子集。例如，此代码将生成已定义段落样式的列表::

        >>> from docx.enum.style import WD_STYLE_TYPE
        >>> styles = document.styles
        >>> paragraph_styles = [
        ...     s for s in styles if s.type == WD_STYLE_TYPE.PARAGRAPH
        ... ]
        >>> for style in paragraph_styles:
        ...     print(style.name)
        ...
        Normal
        Body Text
        List Bullet

.. tab:: 英文

    Styles are accessed using the :attr:`.Document.styles` attribute::

        >>> document = Document()
        >>> styles = document.styles
        >>> styles
        <docx.styles.styles.Styles object at 0x10a7c4f50>

    The |Styles| object provides dictionary-style access to defined styles by
    name::

        >>> styles['Normal']
        <docx.styles.style._ParagraphStyle object at <0x10a7c4f6b>

    .. note:: Built-in styles are stored in a WordprocessingML file using their English name, e.g. 'Heading 1', even though users working on a localized version of Word will see native language names in the UI, e.g. 'Kop 1'. Because |docx| operates on the WordprocessingML file, style lookups must use the English name. A document available on this external site allows you to create a mapping between local language names and English style names: http://www.thedoctools.com/index.php?show=mt_create_style_name_list

    User-defined styles, also known as *custom styles*, are not localized and
    are accessed with the name exactly as it appears in the Word UI.

    The |Styles| object is also iterable. By using the identification properties
    on |BaseStyle|, various subsets of the defined styles can be generated. For
    example, this code will produce a list of the defined paragraph styles::

    >>> from docx.enum.style import WD_STYLE_TYPE
    >>> styles = document.styles
    >>> paragraph_styles = [
    ...     s for s in styles if s.type == WD_STYLE_TYPE.PARAGRAPH
    ... ]
    >>> for style in paragraph_styles:
    ...     print(style.name)
    ...
    Normal
    Body Text
    List Bullet


应用样式
-------------

Apply a style

.. tab:: 中文

    |Paragraph|、|Run| 和 |Table| 对象各自都有一个 :attr:`style` 属性。将样式对象分配给此属性将应用该样式::

        >>> document = Document()
        >>> paragraph = document.add_paragraph()
        >>> paragraph.style
        <docx.styles.style._ParagraphStyle object at <0x11a7c4c50>
        >>> paragraph.style.name
        'Normal'
        >>> paragraph.style = document.styles['Heading 1']
        >>> paragraph.style.name
        'Heading 1'

    也可以直接指定样式名称，在这种情况下 |docx| 将为您进行查找::

        >>> paragraph.style = 'List Bullet'
        >>> paragraph.style
        <docx.styles.style._ParagraphStyle object at <0x10a7c4f84>
        >>> paragraph.style.name
        'List Bullet'

    也可以在创建时使用样式对象或其名称来应用样式::

        >>> paragraph = document.add_paragraph(style='Body Text')
        >>> paragraph.style.name
        'Body Text'
        >>> body_text_style = document.styles['Body Text']
        >>> paragraph = document.add_paragraph(style=body_text_style)
        >>> paragraph.style.name
        'Body Text'

.. tab:: 英文

    The |Paragraph|, |Run|, and |Table| objects each have a :attr:`style`
    attribute. Assigning a style object to this attribute applies that style::

        >>> document = Document()
        >>> paragraph = document.add_paragraph()
        >>> paragraph.style
        <docx.styles.style._ParagraphStyle object at <0x11a7c4c50>
        >>> paragraph.style.name
        'Normal'
        >>> paragraph.style = document.styles['Heading 1']
        >>> paragraph.style.name
        'Heading 1'

    A style name can also be assigned directly, in which case |docx| will do the
    lookup for you::

        >>> paragraph.style = 'List Bullet'
        >>> paragraph.style
        <docx.styles.style._ParagraphStyle object at <0x10a7c4f84>
        >>> paragraph.style.name
        'List Bullet'

    A style can also be applied at creation time using either the style object or
    its name::

        >>> paragraph = document.add_paragraph(style='Body Text')
        >>> paragraph.style.name
        'Body Text'
        >>> body_text_style = document.styles['Body Text']
        >>> paragraph = document.add_paragraph(style=body_text_style)
        >>> paragraph.style.name
        'Body Text'


添加或删除样式
---------------------

Add or delete a style

.. tab:: 中文

    可以通过指定唯一的名称和样式类型将新样式添加到文档中::

        >>> from docx.enum.style import WD_STYLE_TYPE
        >>> styles = document.styles
        >>> style = styles.add_style('Citation', WD_STYLE_TYPE.PARAGRAPH)
        >>> style.name
        'Citation'
        >>> style.type
        PARAGRAPH (1)

    使用 :attr:`~.BaseStyle.base_style` 属性指定新样式应从中继承格式设置的样式::

        >>> style.base_style
        None
        >>> style.base_style = styles['Normal']
        >>> style.base_style
        <docx.styles.style._ParagraphStyle object at 0x10a7a9550>
        >>> style.base_style.name
        'Normal'

    只需调用其 :meth:`~.BaseStyle.delete` 方法即可从文档中删除样式::

        >>> styles = document.styles
        >>> len(styles)
        10
        >>> styles['Citation'].delete()
        >>> len(styles)
        9

    .. note:: The :meth:`.Style.delete` method removes the style's definition from the document. It does not affect content in the document to which that style is applied. Content having a style not defined in the document is rendered using the default style for that content object, e.g. 'Normal' in the case of a paragraph.

.. tab:: 英文

    A new style can be added to the document by specifying a unique name and a style type::

        >>> from docx.enum.style import WD_STYLE_TYPE
        >>> styles = document.styles
        >>> style = styles.add_style('Citation', WD_STYLE_TYPE.PARAGRAPH)
        >>> style.name
        'Citation'
        >>> style.type
        PARAGRAPH (1)

    Use the :attr:`~.BaseStyle.base_style` property to specify a style the new style should inherit formatting settings from::

        >>> style.base_style
        None
        >>> style.base_style = styles['Normal']
        >>> style.base_style
        <docx.styles.style._ParagraphStyle object at 0x10a7a9550>
        >>> style.base_style.name
        'Normal'

    A style can be removed from the document simply by calling its :meth:`~.BaseStyle.delete` method::

        >>> styles = document.styles
        >>> len(styles)
        10
        >>> styles['Citation'].delete()
        >>> len(styles)
        9

    .. note:: The :meth:`.Style.delete` method removes the style's definition from the document. It does not affect content in the document to which that style is applied. Content having a style not defined in the document is rendered using the default style for that content object, e.g. 'Normal' in the case of a paragraph.


定义字符格式
---------------------------

Define character formatting

.. tab:: 中文

    字符、段落和表格样式都可以指定要应用于具有该样式的内容的字符格式。所有可以直接应用于文本的字符格式都可以在样式中指定。示例包括字体字体和大小、粗体、斜体和下划线。

    这三种样式类型中的每一种都有一个 :attr:`~._CharacterStyle.font` 属性，用于访问 |Font| 对象。样式的 |Font| 对象提供用于获取和设置该样式的字符格式的属性。

    这里提供了几个示例。有关可用属性的完整集合，请参阅 |Font| API 文档。

    可以像这样访问样式的字体::

        >>> from docx import Document
        >>> document = Document()
        >>> style = document.styles['Normal']
        >>> font = style.font

    字体和大小设置如下::

        >>> from docx.shared import Pt
        >>> font.name = 'Calibri'
        >>> font.size = Pt(12)

    许多字体属性都是 *三态* 的，这意味着它们可以取值 |True|、|False| 和 |None|。|True| 表示属性处于“开启”状态，|False| 表示属性处于“关闭”状态。从概念上讲，|None| 值表示“继承”。由于样式存在于继承层次结构中，因此能够在层次结构的正确位置指定属性非常重要，通常尽可能地位于层次结构的上层。例如，如果所有标题都应采用 Arial 字体，则更有意义的做法是将该属性设置为 `Heading 1` 样式，并让 `Heading 2` 从 `Heading 1` 继承。

    粗体和斜体是三态属性，全大写、删除线、上标和许多其他属性也是如此。请参阅 |Font| API 文档以获取完整列表::

        >>> font.bold, font.italic
        (None, None)
        >>> font.italic = True
        >>> font.italic
        True
        >>> font.italic = False
        >>> font.italic
        False
        >>> font.italic = None
        >>> font.italic
        None

    下划线有点特殊。它是三态属性和枚举值属性的混合体。|True| 表示单下划线，这是最常见的。|False| 表示无下划线，但如果不需要下划线，则更常见的是 |None| 是正确的选择，因为很少从基本样式继承下划线。其他形式的下划线，例如双下划线或虚线，由 :ref:`WdUnderline` 枚举的成员指定::

        >>> font.underline
        None
        >>> font.underline = True
        >>> # or perhaps
        >>> font.underline = WD_UNDERLINE.DOT_DASH

.. tab:: 英文

    Character, paragraph, and table styles can all specify character formatting to be applied to content with that style. All the character formatting that can be applied directly to text can be specified in a style. Examples include font typeface and size, bold, italic, and underline.

    Each of these three style types have a :attr:`~._CharacterStyle.font` attribute providing access to a |Font| object. A style's |Font| object provides properties for getting and setting the character formatting for that style.

    Several examples are provided here. For a complete set of the available properties, see the |Font| API documentation.

    The font for a style can be accessed like this::

        >>> from docx import Document
        >>> document = Document()
        >>> style = document.styles['Normal']
        >>> font = style.font

    Typeface and size are set like this::

        >>> from docx.shared import Pt
        >>> font.name = 'Calibri'
        >>> font.size = Pt(12)

    Many font properties are *tri-state*, meaning they can take the values |True|, |False|, and |None|. |True| means the property is "on", |False| means it is "off". Conceptually, the |None| value means "inherit". Because a style exists in an inheritance hierarchy, it is important to have the ability to specify a property at the right place in the hierarchy, generally as far up the hierarchy as possible. For example, if all headings should be in the Arial typeface, it makes more sense to set that property on the `Heading 1` style and have `Heading 2` inherit from `Heading 1`.

    Bold and italic are tri-state properties, as are all-caps, strikethrough, superscript, and many others. See the |Font| API documentation for a full list::

        >>> font.bold, font.italic
        (None, None)
        >>> font.italic = True
        >>> font.italic
        True
        >>> font.italic = False
        >>> font.italic
        False
        >>> font.italic = None
        >>> font.italic
        None

    Underline is a bit of a special case. It is a hybrid of a tri-state property and an enumerated value property. |True| means single underline, by far the most common. |False| means no underline, but more often |None| is the right choice if no underlining is wanted since it is rare to inherit it from a base style. The other forms of underlining, such as double or dashed, are specified with a member of the :ref:`WdUnderline` enumeration::

        >>> font.underline
        None
        >>> font.underline = True
        >>> # or perhaps
        >>> font.underline = WD_UNDERLINE.DOT_DASH


定义段落格式
---------------------------

Define paragraph formatting

.. tab:: 中文

    段落样式和表格样式都允许指定段落格式。这些样式通过其 :attr:`~._ParagraphStyle.paragraph_format` 属性提供对 |ParagraphFormat| 对象的访问。

    段落格式包括布局行为，例如对齐、缩进、前后空格、分页符和孤行控制。有关可用属性的完整列表，请参阅 |ParagraphFormat| 对象的 API 文档页面。

    以下是如何创建具有 1/4 英寸悬挂缩进、12 点上方间距和孤行控制的段落样式的示例::

        >>> from docx.enum.style import WD_STYLE_TYPE
        >>> from docx.shared import Inches, Pt
        >>> document = Document()
        >>> style = document.styles.add_style('Indent', WD_STYLE_TYPE.PARAGRAPH)
        >>> paragraph_format = style.paragraph_format
        >>> paragraph_format.left_indent = Inches(0.25)
        >>> paragraph_format.first_line_indent = Inches(-0.25)
        >>> paragraph_format.space_before = Pt(12)
        >>> paragraph_format.widow_control = True

.. tab:: 英文

    Both a paragraph style and a table style allow paragraph formatting to be specified. These styles provide access to a |ParagraphFormat| object via their :attr:`~._ParagraphStyle.paragraph_format` property.

    Paragraph formatting includes layout behaviors such as justification, indentation, space before and after, page break before, and widow/orphan control. For a complete list of the available properties, consult the API documentation page for the |ParagraphFormat| object.

    Here's an example of how you would create a paragraph style having hanging indentation of 1/4 inch, 12 points spacing above, and widow/orphan control::

        >>> from docx.enum.style import WD_STYLE_TYPE
        >>> from docx.shared import Inches, Pt
        >>> document = Document()
        >>> style = document.styles.add_style('Indent', WD_STYLE_TYPE.PARAGRAPH)
        >>> paragraph_format = style.paragraph_format
        >>> paragraph_format.left_indent = Inches(0.25)
        >>> paragraph_format.first_line_indent = Inches(-0.25)
        >>> paragraph_format.space_before = Pt(12)
        >>> paragraph_format.widow_control = True


使用特定于段落的样式属性
---------------------------------------

Use paragraph-specific style properties

.. tab:: 中文

    段落样式具有 :attr:`~._ParagraphStyle.next_paragraph_style` 属性，该属性指定要应用于插入到该样式段落后的新段落的样式。当样式通常只在序列中出现一次（例如标题）时，这非常有用。在这种情况下，完成标题后，段落样式可以自动设置回正文样式。

    在最常见的情况下（正文段落），后续段落应采用与当前段落相同的样式。如果未指定下一个段落样式，则默认通过应用相同样式来很好地处理这种情况。

    以下是如何将 *Heading 1* 样式的下一个段落样式更改为 *Body Text* 的示例::

        >>> from docx import Document
        >>> document = Document()
        >>> styles = document.styles

        >>> styles['Heading 1'].next_paragraph_style = styles['Body Text']

    可以通过指定 |None| 或样式本身来恢复默认行为::

        >>> heading_1_style = styles['Heading 1']
        >>> heading_1_style.next_paragraph_style.name
        'Body Text'

        >>> heading_1_style.next_paragraph_style = heading_1_style
        >>> heading_1_style.next_paragraph_style.name
        'Heading 1'

        >>> heading_1_style.next_paragraph_style = None
        >>> heading_1_style.next_paragraph_style.name
        'Heading 1'

.. tab:: 英文

    A paragraph style has a :attr:`~._ParagraphStyle.next_paragraph_style` property that specifies the style to be applied to new paragraphs inserted after a paragraph of that style. This is most useful when the style would normally appear only once in a sequence, such as a heading. In that case, the paragraph style can automatically be set back to a body style after completing the heading.

    In the most common case (body paragraphs), subsequent paragraphs should receive the same style as the current paragraph. The default handles this case well by applying the same style if a next paragraph style is not specified.

    Here's an example of how you would change the next paragraph style of the *Heading 1* style to *Body Text*::

        >>> from docx import Document
        >>> document = Document()
        >>> styles = document.styles

        >>> styles['Heading 1'].next_paragraph_style = styles['Body Text']

    The default behavior can be restored by assigning |None| or the style itself::

        >>> heading_1_style = styles['Heading 1']
        >>> heading_1_style.next_paragraph_style.name
        'Body Text'

        >>> heading_1_style.next_paragraph_style = heading_1_style
        >>> heading_1_style.next_paragraph_style.name
        'Heading 1'

        >>> heading_1_style.next_paragraph_style = None
        >>> heading_1_style.next_paragraph_style.name
        'Heading 1'


控制样式在 Word UI 中的显示方式
------------------------------------------

Control how a style appears in the Word UI

.. tab:: 中文

    样式的属性分为两类： *行为属性* 和 *格式属性* 。其行为属性控制样式在 Word UI 中出现的时间和位置。其格式属性决定应用样式的内容的格式，例如字体大小和段落缩进。

    样式有五种行为属性:

    * :attr:`~.BaseStyle.hidden`
    * :attr:`~.BaseStyle.unhide_when_used`
    * :attr:`~.BaseStyle.priority`
    * :attr:`~.BaseStyle.quick_style`
    * :attr:`~.BaseStyle.locked`

    有关这些行为属性如何相互作用以确定样式在 Word UI 中出现的时间和位置的描述，请参阅 :ref:`understanding_styles` 中的 :ref:`style_behavior` 部分.

    :attr:`priority` 属性采用整数值。其他四个样式行为属性是 *三态*，这意味着它们可以采用值 |True|（开启）、|False|（关闭）或 |None|（继承）。

.. tab:: 英文

    The properties of a style fall into two categories, *behavioral properties* and *formatting properties*. Its behavioral properties control when and where the style appears in the Word UI. Its formatting properties determine the formatting of content to which the style is applied, such as the size of the font and its paragraph indentation.

    There are five behavioral properties of a style:

    * :attr:`~.BaseStyle.hidden`
    * :attr:`~.BaseStyle.unhide_when_used`
    * :attr:`~.BaseStyle.priority`
    * :attr:`~.BaseStyle.quick_style`
    * :attr:`~.BaseStyle.locked`

    See the :ref:`style_behavior` section in :ref:`understanding_styles` for a description of how these behavioral properties interact to determine when and where a style appears in the Word UI.

    The :attr:`priority` property takes an integer value. The other four style behavior properties are *tri-state*, meaning they can take the value |True| (on), |False| (off), or |None| (inherit).

在样式库中显示样式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Display a style in the style gallery

.. tab:: 中文

    以下代码将使 'Body Text' 段落样式首先出现在样式库中::

        >>> from docx import Document
        >>> document = Document()
        >>> style = document.styles['Body Text']

        >>> style.hidden = False
        >>> style.quick_style = True
        >>> style.priorty = 1

.. tab:: 英文

    The following code will cause the 'Body Text' paragraph style to appear first in the style gallery::

        >>> from docx import Document
        >>> document = Document()
        >>> style = document.styles['Body Text']

        >>> style.hidden = False
        >>> style.quick_style = True
        >>> style.priorty = 1

从样式库中删除样式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Remove a style from the style gallery

.. tab:: 中文

    此代码将从样式库中删除 'Normal' 段落样式，但允许其保留在推荐列表中::

        >>> style = document.styles['Normal']

        >>> style.hidden = False
        >>> style.quick_style = False

.. tab:: 英文

    This code will remove the 'Normal' paragraph style from the style gallery, but allow it to remain in the recommended list::

        >>> style = document.styles['Normal']

        >>> style.hidden = False
        >>> style.quick_style = False


使用潜在样式
--------------------------

Working with Latent Styles

.. tab:: 中文

    请参阅 :ref:`understanding_styles` 中的 :ref:`builtin_styles` 和 :ref:`latent_styles` 部分，了解潜在样式如何定义 .docx 文件的 `styles.xml` 部分中尚未定义的内置样式的行为属性。

.. tab:: 英文

    See the :ref:`builtin_styles` and :ref:`latent_styles` sections in :ref:`understanding_styles` for a description of how latent styles define the behavioral properties of built-in styles that are not yet defined in the `styles.xml` part of a .docx file.

访问文档中的潜在样式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Access the latent styles in a document

.. tab:: 中文

    文档中的潜在样式可以通过样式对象访问::

        >>> document = Document()
        >>> latent_styles = document.styles.latent_styles

    |LatentStyles| 对象支持 :meth:`len`、迭代和通过样式名称进行字典样式访问::

        >>> len(latent_styles)
        161

        >>> latent_style_names = [ls.name for ls in latent_styles]
        >>> latent_style_names
        ['Normal', 'Heading 1', 'Heading 2', ... 'TOC Heading']

        >>> latent_quote = latent_styles['Quote']
        >>> latent_quote
        <docx.styles.latent.LatentStyle object at 0x10a7c4f50>
        >>> latent_quote.priority
        29

.. tab:: 英文

    The latent styles in a document are accessed from the styles object::

        >>> document = Document()
        >>> latent_styles = document.styles.latent_styles

    A |LatentStyles| object supports :meth:`len`, iteration, and dictionary-style access by style name::

        >>> len(latent_styles)
        161

        >>> latent_style_names = [ls.name for ls in latent_styles]
        >>> latent_style_names
        ['Normal', 'Heading 1', 'Heading 2', ... 'TOC Heading']

        >>> latent_quote = latent_styles['Quote']
        >>> latent_quote
        <docx.styles.latent.LatentStyle object at 0x10a7c4f50>
        >>> latent_quote.priority
        29

更改潜在样式默认值
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Change latent style defaults

.. tab:: 中文

    |LatentStyles| 对象还提供对当前文档中内置样式的默认行为属性的访问。这些默认值为 |_LatentStyle| 定义中任何未定义的属性以及没有明确潜在样式定义的内置样式的所有行为属性提供值。有关可用属性的完整集合，请参阅 |LatentStyles| 对象的 API 文档::

        >>> latent_styles.default_to_locked
        False
        >>> latent_styles.default_to_locked = True
        >>> latent_styles.default_to_locked
        True

.. tab:: 英文

    The |LatentStyles| object also provides access to the default behavioral properties for built-in styles in the current document. These defaults provide the value for any undefined attributes of the |_LatentStyle| definitions and to all behavioral properties of built-in styles having no explicit latent style definition. See the API documentation for the |LatentStyles| object for the complete set of available properties::

        >>> latent_styles.default_to_locked
        False
        >>> latent_styles.default_to_locked = True
        >>> latent_styles.default_to_locked
        True

添加潜在样式定义
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a latent style definition

.. tab:: 中文

    可以使用 |LatentStyles| 上的 :meth:`~.LatentStyles.add_latent_style` 方法添加新的潜在样式。此代码为内置样式'List Bullet' 添加了新的潜在样式，并将其设置为显示在样式库中::

        >>> latent_style = latent_styles['List Bullet']
        KeyError: no latent style with name 'List Bullet'
        >>> latent_style = latent_styles.add_latent_style('List Bullet')
        >>> latent_style.hidden = False
        >>> latent_style.priority = 2
        >>> latent_style.quick_style = True

.. tab:: 英文

    A new latent style can be added using the :meth:`~.LatentStyles.add_latent_style` method on |LatentStyles|. This code adds a new latent style for the builtin style 'List Bullet', setting it to appear in the style gallery::

        >>> latent_style = latent_styles['List Bullet']
        KeyError: no latent style with name 'List Bullet'
        >>> latent_style = latent_styles.add_latent_style('List Bullet')
        >>> latent_style.hidden = False
        >>> latent_style.priority = 2
        >>> latent_style.quick_style = True

删除潜在样式定义
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Delete a latent style definition

.. tab:: 中文

    可以通过调用其 :meth:`~.LatentStyle.delete` 方法来删​​除潜在样式定义::

        >>> latent_styles['Light Grid']
        <docx.styles.latent.LatentStyle object at 0x10a7c4f50>
        >>> latent_styles['Light Grid'].delete()
        >>> latent_styles['Light Grid']
        KeyError: no latent style with name 'Light Grid'

.. tab:: 英文

    A latent style definition can be deleted by calling its :meth:`~.LatentStyle.delete` method::

        >>> latent_styles['Light Grid']
        <docx.styles.latent.LatentStyle object at 0x10a7c4f50>
        >>> latent_styles['Light Grid'].delete()
        >>> latent_styles['Light Grid']
        KeyError: no latent style with name 'Light Grid'
