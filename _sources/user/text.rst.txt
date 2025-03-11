
使用文本
=================

Working with Text

.. tab:: 中文

    为了有效地处理文本，首先需要了解一些块级元素（例如段落）和行内级对象（例如运行(runs)）。

.. tab:: 英文

    To work effectively with text, it's important to first understand a little
    about block-level elements like paragraphs and inline-level objects like
    runs.


块级文本对象与内联文本对象
-----------------------------------

Block-level vs. inline text objects

.. tab:: 中文

    段落是 Word 中的主要块级对象。

    块级项目将其包含的文本流动在其左边缘和右边缘之间，每次文本超出其右边界时都会添加一条额外的行。对于段落，边界通常是页边距，但如果页面按列布局，它们也可以是列边界，如果段落出现在表格单元格内，它们也可以是单元格边界。

    表格也是块级对象。

    内联对象是块级项目内出现的内容的一部分。例如，以粗体显示的单词或全大写的句子。最常见的内联对象是“运行”。块容器内的所有内容都在内联对象内。通常，段落包含一个或多个运行，每个运行都包含段落文本的某些部分。

    块级项目的属性指定其在页面上的位置，例如段落前后的缩进和空格。内联项目的属性
    通常指定内容显示的字体，
    例如字体、字体大小、粗体和斜体。

.. tab:: 英文

    The paragraph is the primary block-level object in Word.

    A block-level item flows the text it contains between its left and right
    edges, adding an additional line each time the text extends beyond its right
    boundary. For a paragraph, the boundaries are generally the page margins, but
    they can also be column boundaries if the page is laid out in columns, or
    cell boundaries if the paragraph occurs inside a table cell.

    A table is also a block-level object.

    An inline object is a portion of the content that occurs inside a block-level
    item. An example would be a word that appears in bold or a sentence in
    all-caps. The most common inline object is a `run`. All content within
    a block container is inside of an inline object. Typically, a paragraph
    contains one or more runs, each of which contain some part of the paragraph's
    text.

    The attributes of a block-level item specify its placement on the page, such
    items as indentation and space before and after a paragraph. The attributes
    of an inline item generally specify the font in which the content appears,
    things like typeface, font size, bold, and italic.


段落属性
--------------------

Paragraph properties

.. tab:: 中文

    段落具有多种属性，这些属性指定了段落在容器（通常是页面）中的位置以及将内容划分为单独行的方式。

    通常，最好定义一个 *段落样式* ，将这些属性收集到一个有意义的组中，并将适当的样式应用于每个段落，而不是重复地将这些属性直接应用于每个段落。这类似于层叠样式表 (CSS) 与 HTML 的配合使用方式。此处描述的所有段落属性都可以使用样式进行设置，也可以直接应用于段落。

    段落的格式属性可通过段落的
    :attr:`~.Paragraph.paragraph_format` 属性提供的
    |ParagraphFormat| 对象进行访问。

.. tab:: 英文

    A paragraph has a variety of properties that specify its placement within its
    container (typically a page) and the way it divides its content into separate
    lines.

    In general, it's best to define a *paragraph style* collecting these
    attributes into a meaningful group and apply the appropriate style to each
    paragraph, rather than repeatedly apply those properties directly to each
    paragraph. This is analogous to how Cascading Style Sheets (CSS) work with
    HTML. All the paragraph properties described here can be set using a style as
    well as applied directly to a paragraph.

    The formatting properties of a paragraph are accessed using the
    |ParagraphFormat| object available using the paragraph's
    :attr:`~.Paragraph.paragraph_format` property.


水平对齐（对齐）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Horizontal alignment (justification)

.. tab:: 中文

    也称为“对齐” (`justification`)，可以使用枚举中的值将段落的水平对齐设置为左对齐、居中对齐、右对齐或完全对齐（左右两侧对齐）:ref:`WdParagraphAlignment`::

        >>> from docx.enum.text import WD_ALIGN_PARAGRAPH
        >>> document = Document()
        >>> paragraph = document.add_paragraph()
        >>> paragraph_format = paragraph.paragraph_format

        >>> paragraph_format.alignment
        None  # indicating alignment is inherited from the style hierarchy
        >>> paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER
        >>> paragraph_format.alignment
        CENTER (1)

.. tab:: 英文

    Also known as `justification`, the horizontal alignment of a paragraph can be
    set to left, centered, right, or fully justified (aligned on both the left
    and right sides) using values from the enumeration
    :ref:`WdParagraphAlignment`::

        >>> from docx.enum.text import WD_ALIGN_PARAGRAPH
        >>> document = Document()
        >>> paragraph = document.add_paragraph()
        >>> paragraph_format = paragraph.paragraph_format

        >>> paragraph_format.alignment
        None  # indicating alignment is inherited from the style hierarchy
        >>> paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER
        >>> paragraph_format.alignment
        CENTER (1)


缩进
~~~~~~~~~~~

Indentation

.. tab:: 中文

    缩进是段落与其容器边缘之间的水平空间，通常是页边距。段落的左侧和右侧可以分别缩进。第一行的缩进也可以与段落的其余部分不同。第一行的缩进比段落的其余部分更远，则为*首行缩进*。第一行的缩进较少，则为*悬挂缩进*。

    缩进使用 |Length| 值指定，例如 |Inches|、|Pt| 或
    |Cm|。负值有效，可使段落与边距重叠指定的量。值 |None| 表示缩进值是从样式层次结构继承的。分配 |None|缩进
    属性会删除任何直接应用的缩进设置并恢复
    样式层次结构的继承::

        >>> from docx.shared import Inches
        >>> passage = document.add_paragraph()
        >>> passage_format = passage.paragraph_format

        >>> passage_format.left_indent
        None # 表示缩进从样式层次结构继承
        >>> passage_format.left_indent = Inches(0.5)
        >>> passage_format.left_indent
        457200
        >>> passage_format.left_indent.inches
        0.5

    右侧缩进的工作方式类似::

        >>> from docx.shared import Pt
        >>> passage_format.right_indent
        None
        >>> passage_format.right_indent = Pt(24)
        >>> passage_format.right_indent
        304800
        >>> paragraph_format.right_indent.pt
        24.0

    首行缩进使用
    :attr:`~.ParagraphFormat.first_line_indent` 属性指定，并
    相对于左缩进进行解释。负值表示悬挂缩进::

        >>> passage_format.first_line_indent
        None
        >>> passage_format.first_line_indent = Inches(-0.25)
        >>> passage_format.first_line_indent
        -228600
        >>> passage_format.first_line_indent.inches
        -0.25

.. tab:: 英文

    Indentation is the horizontal space between a paragraph and edge of its
    container, typically the page margin. A paragraph can be indented separately
    on the left and right side. The first line can also have a different
    indentation than the rest of the paragraph. A first line indented further
    than the rest of the paragraph has *first line indent*. A first line indented
    less has a *hanging indent*.

    Indentation is specified using a |Length| value, such as |Inches|, |Pt|, or
    |Cm|. Negative values are valid and cause the paragraph to overlap the margin
    by the specified amount. A value of |None| indicates the indentation value is
    inherited from the style hierarchy. Assigning |None| to an indentation
    property removes any directly-applied indentation setting and restores
    inheritance from the style hierarchy::

        >>> from docx.shared import Inches
        >>> paragraph = document.add_paragraph()
        >>> paragraph_format = paragraph.paragraph_format

        >>> paragraph_format.left_indent
        None  # indicating indentation is inherited from the style hierarchy
        >>> paragraph_format.left_indent = Inches(0.5)
        >>> paragraph_format.left_indent
        457200
        >>> paragraph_format.left_indent.inches
        0.5


    Right-side indent works in a similar way::

        >>> from docx.shared import Pt
        >>> paragraph_format.right_indent
        None
        >>> paragraph_format.right_indent = Pt(24)
        >>> paragraph_format.right_indent
        304800
        >>> paragraph_format.right_indent.pt
        24.0

    First-line indent is specified using the
    :attr:`~.ParagraphFormat.first_line_indent` property and is interpreted
    relative to the left indent. A negative value indicates a hanging indent::

        >>> paragraph_format.first_line_indent
        None
        >>> paragraph_format.first_line_indent = Inches(-0.25)
        >>> paragraph_format.first_line_indent
        -228600
        >>> paragraph_format.first_line_indent.inches
        -0.25


制表位
~~~~~~~~~

Tab stops

.. tab:: 中文

    制表位决定了段落文本中制表符的呈现方式。具体来说，它指定了制表符后面的文本的起始位置、文本与该位置的对齐方式，以及填充制表符横跨的水平空间的可选前导符。

    段落或样式的制表位包含在 |TabStops| 中对象
    使用 :attr:`~.ParagraphFormat.tab_stops` 属性访问
    |ParagraphFormat|::

        >>> tab_stops = passage_format.tab_stops
        >>> tab_stops
        <docx.text.tabstops.TabStops 对象位于 0x106b802d8>

    使用 :meth:`~.TabStops.add_tab_stop` 方法添加新的制表位::

        >>> tab_stop = tab_stops.add_tab_stop(Inches(1.5))
        >>> tab_stop.position
        1371600
        >>> tab_stop.position.inches
        1.5

    对齐方式默认为左对齐，但可以通过提供
    :ref:`WdTabAlignment` 枚举的成员来指定。前导字符默认为空格，
    但可以通过提供 :ref:`WdTabLeader`
    枚举的成员来指定::

        >>> from docx.enum.text import WD_TAB_ALIGNMENT, WD_TAB_LEADER
        >>> tab_stop = tab_stops.add_tab_stop(Inches(1.5), WD_TAB_ALIGNMENT.RIGHT, WD_TAB_LEADER.DOTS)
        >>> print(tab_stop.alignment)
        RIGHT (2)
        >>> print(tab_stop.leader)
        DOTS (1)

    使用 |TabStops| 上的序列语义访问现有制表位::

        >>> tab_stops[0]
        <docx.text.tabstops.TabStop object at 0x1105427e8>

    更多详细信息请参阅 |TabStops|和 |TabStop| API 文档

.. tab:: 英文

    A tab stop determines the rendering of a tab character in the text of
    a paragraph. In particular, it specifies the position where the text
    following the tab character will start, how it will be aligned to that
    position, and an optional leader character that will fill the horizontal
    space spanned by the tab.

    The tab stops for a paragraph or style are contained in a |TabStops| object
    accessed using the :attr:`~.ParagraphFormat.tab_stops` property on
    |ParagraphFormat|::

        >>> tab_stops = paragraph_format.tab_stops
        >>> tab_stops
        <docx.text.tabstops.TabStops object at 0x106b802d8>

    A new tab stop is added using the :meth:`~.TabStops.add_tab_stop` method::

        >>> tab_stop = tab_stops.add_tab_stop(Inches(1.5))
        >>> tab_stop.position
        1371600
        >>> tab_stop.position.inches
        1.5

    Alignment defaults to left, but may be specified by providing a member of the
    :ref:`WdTabAlignment` enumeration. The leader character defaults to spaces,
    but may be specified by providing a member of the :ref:`WdTabLeader`
    enumeration::

        >>> from docx.enum.text import WD_TAB_ALIGNMENT, WD_TAB_LEADER
        >>> tab_stop = tab_stops.add_tab_stop(Inches(1.5), WD_TAB_ALIGNMENT.RIGHT, WD_TAB_LEADER.DOTS)
        >>> print(tab_stop.alignment)
        RIGHT (2)
        >>> print(tab_stop.leader)
        DOTS (1)

    Existing tab stops are accessed using sequence semantics on |TabStops|::

        >>> tab_stops[0]
        <docx.text.tabstops.TabStop object at 0x1105427e8>

    More details are available in the |TabStops| and |TabStop| API documentation


段落间距
~~~~~~~~~~~~~~~~~

Paragraph spacing

.. tab:: 中文

    :attr:`~.ParagraphFormat.space_before` 和 :attr:`~.ParagraphFormat.space_after` 属性控制后续段落之间的间距，分别控制段落前后的间距。段落间间距在页面布局期间是“折叠”的，这意味着两个段落之间的间距是第一个段落的 `space_after` 和第二个段落的 `space_before` 中的最大值。段落间距指定为 |Length| 值，通常使用 |Pt|::

        >>> paragraph_format.space_before, paragraph_format.space_after
        (None, None)  # inherited by default

        >>> paragraph_format.space_before = Pt(18)
        >>> paragraph_format.space_before.pt
        18.0

        >>> paragraph_format.space_after = Pt(12)
        >>> paragraph_format.space_after.pt
        12.0

.. tab:: 英文

    The :attr:`~.ParagraphFormat.space_before` and
    :attr:`~.ParagraphFormat.space_after` properties control the spacing between
    subsequent paragraphs, controlling the spacing before and after a paragraph,
    respectively. Inter-paragraph spacing is `collapsed` during page layout,
    meaning the spacing between two paragraphs is the maximum of the
    `space_after` for the first paragraph and the `space_before` of the second
    paragraph. Paragraph spacing is specified as a |Length| value, often using
    |Pt|::

        >>> paragraph_format.space_before, paragraph_format.space_after
        (None, None)  # inherited by default

        >>> paragraph_format.space_before = Pt(18)
        >>> paragraph_format.space_before.pt
        18.0

        >>> paragraph_format.space_after = Pt(12)
        >>> paragraph_format.space_after.pt
        12.0


行间距
~~~~~~~~~~~~

Line spacing

.. tab:: 中文

    行距是段落行中后续基线之间的距离。行距可以指定为绝对距离或相对于行高（本质上是所用字体的点大小）的距离。

    典型的绝对测量值为 18 点。典型的相对测量值为双倍行距（2.0 行高）。默认行距为单倍行距（1.0 行高）。

    行距由 :attr:`~.ParagraphFormat.line_spacing` 和 :attr:`~.ParagraphFormat.line_spacing_rule` 属性的交互控制。

    :attr:`~.ParagraphFormat.line_spacing` 可以是 |Length| 值、（较小的）|float| 或 None。|Length| 值表示绝对距离。|float| 表示行高数。|None| 表示行距是继承的。 :attr:`~.ParagraphFormat.line_spacing_rule` 是 :ref:`WdLineSpacing` 枚举的成员
    或 |None|::

        >>> from docx.shared import Length
        >>> paragraph_format.line_spacing
        None
        >>> paragraph_format.line_spacing_rule
        None

        >>> paragraph_format.line_spacing = Pt(18)
        >>> isinstance(paragraph_format.line_spacing, Length)
        True
        >>> paragraph_format.line_spacing.pt
        18.0
        >>> paragraph_format.line_spacing_rule
        EXACTLY (4)

        >>> paragraph_format.line_spacing = 1.75
        >>> paragraph_format.line_spacing
        1.75
        >>> paragraph_format.line_spacing_rule
        MULTIPLE (5)

.. tab:: 英文

    Line spacing is the distance between subsequent baselines in the lines of
    a paragraph. Line spacing can be specified either as an absolute distance or
    relative to the line height (essentially the point size of the font used).
    A typical absolute measure would be 18 points. A typical relative measure
    would be double-spaced (2.0 line heights). The default line spacing is
    single-spaced (1.0 line heights).

    Line spacing is controlled by the interaction of the
    :attr:`~.ParagraphFormat.line_spacing` and
    :attr:`~.ParagraphFormat.line_spacing_rule` properties.
    :attr:`~.ParagraphFormat.line_spacing` is either a |Length| value,
    a (small-ish) |float|, or None. A |Length| value indicates an absolute
    distance. A |float| indicates a number of line heights. |None| indicates line
    spacing is inherited. :attr:`~.ParagraphFormat.line_spacing_rule` is a member
    of the :ref:`WdLineSpacing` enumeration or |None|::

        >>> from docx.shared import Length
        >>> paragraph_format.line_spacing
        None
        >>> paragraph_format.line_spacing_rule
        None

        >>> paragraph_format.line_spacing = Pt(18)
        >>> isinstance(paragraph_format.line_spacing, Length)
        True
        >>> paragraph_format.line_spacing.pt
        18.0
        >>> paragraph_format.line_spacing_rule
        EXACTLY (4)

        >>> paragraph_format.line_spacing = 1.75
        >>> paragraph_format.line_spacing
        1.75
        >>> paragraph_format.line_spacing_rule
        MULTIPLE (5)


分页属性
~~~~~~~~~~~~~~~~~~~~~

Pagination properties

.. tab:: 中文

    四个段落属性：:attr:`~.ParagraphFormat.keep_together`、
    :attr:`~.ParagraphFormat.keep_with_next`、
    :attr:`~.ParagraphFormat.page_break_before` 和
    :attr:`~.ParagraphFormat.widow_control` 控制段落在页面边界附近的行为方式。

    :attr:`~.ParagraphFormat.keep_together` 使整个段落显示在同一页上，如果段落要跨两页，则在段落前发出分页符。

    :attr:`~.ParagraphFormat.keep_with_next` 将段落与后续段落保持在同一页上。例如，这可用于将节标题与节的第一段保持在同一页上。

    :attr:`~.ParagraphFormat.page_break_before` 使段落放置在新页面的顶部。这可用于章节标题，以确保章节从新页面开始。

    :attr:`~.ParagraphFormat.widow_control` 分隔页面，以避免将段落的第一行或最后一行放置在与段落其余部分不同的页面上。

    所有这四个属性都是 *三态*，这意味着它们可以采用值 |True|、|False| 或 |None|。|None| 表示属性值从样式层次结构继承。|True| 表示“开启”，|False|表示“关闭”::

        >>> paragraph_format.keep_together
        None  # all four inherit by default
        >>> paragraph_format.keep_with_next = True
        >>> paragraph_format.keep_with_next
        True
        >>> paragraph_format.page_break_before = False
        >>> paragraph_format.page_break_before
        False

.. tab:: 英文

    Four paragraph properties, :attr:`~.ParagraphFormat.keep_together`,
    :attr:`~.ParagraphFormat.keep_with_next`,
    :attr:`~.ParagraphFormat.page_break_before`, and
    :attr:`~.ParagraphFormat.widow_control` control aspects of how the paragraph
    behaves near page boundaries.

    :attr:`~.ParagraphFormat.keep_together` causes the entire paragraph to appear
    on the same page, issuing a page break before the paragraph if it would
    otherwise be broken across two pages.

    :attr:`~.ParagraphFormat.keep_with_next` keeps a paragraph on the same page
    as the subsequent paragraph. This can be used, for example, to keep a section
    heading on the same page as the first paragraph of the section.

    :attr:`~.ParagraphFormat.page_break_before` causes a paragraph to be placed
    at the top of a new page. This could be used on a chapter heading to ensure
    chapters start on a new page.

    :attr:`~.ParagraphFormat.widow_control` breaks a page to avoid placing the
    first or last line of the paragraph on a separate page from the rest of the
    paragraph.

    All four of these properties are *tri-state*, meaning they can take the value
    |True|, |False|, or |None|. |None| indicates the property value is inherited
    from the style hierarchy. |True| means "on" and |False| means "off"::

        >>> paragraph_format.keep_together
        None  # all four inherit by default
        >>> paragraph_format.keep_with_next = True
        >>> paragraph_format.keep_with_next
        True
        >>> paragraph_format.page_break_before = False
        >>> paragraph_format.page_break_before
        False


应用字符格式
--------------------------

Apply character formatting

.. tab:: 中文

    字符格式应用于 Run 级别。示例包括字体
    字型和大小、粗体、斜体和下划线。

    |Run| 对象具有只读 :attr:`~.Run.font` 属性，用于访问
    |Font| 对象。运行的 |Font| 对象提供用于获取
    和设置该运行的字符格式的属性。

    这里提供了几个示例。有关可用
    属性的完整集合，请参阅 |Font| API 文档。

    可以像这样访问运行的字体::

        >>> from docx import Document
        >>> document = Document()
        >>> run = document.add_paragraph().add_run()
        >>> font = run.font

    字体和大小设置如下::

        >>> from docx.shared import Pt
        >>> font.name = 'Calibri'
        >>> font.size = Pt(12)

    许多字体属性都是 *三态*，这意味着它们可以采用值
    |True|、|False| 和 |None|。|True| 表示属性为“开”，|False| 表示属性为“关”。从概念上讲，|None| 值表示“继承”。运行存在于样式继承层次结构中，默认情况下从该层次结构继承其字符格式。使用 |Font| 对象直接应用的任何字符格式都会覆盖继承的值。

    粗体和斜体是三态属性，全大写、删除线、
    上标和许多其他属性也是如此。请参阅 |Font| API 文档以获取完整
    列表::

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

    下划线有点特殊。它是三态属性
    和枚举值属性的混合体。|True| 表示单下划线，是最常见的。|False| 表示无下划线，但如果不需要下划线，则更常见的是 |None| 是正确的
    选择。其他形式的下划线，例如
    双下划线或虚线下划线，由 :ref:`WdUnderline`
    枚举的成员指定::

        >>> font.underline
        None
        >>> font.underline = True
        >>> # 或者可能
        >>> font.underline = WD_UNDERLINE.DOT_DASH

.. tab:: 英文

    Character formatting is applied at the Run level. Examples include font
    typeface and size, bold, italic, and underline.

    A |Run| object has a read-only :attr:`~.Run.font` property providing access
    to a |Font| object. A run's |Font| object provides properties for getting
    and setting the character formatting for that run.

    Several examples are provided here. For a complete set of the available
    properties, see the |Font| API documentation.

    The font for a run can be accessed like this::

        >>> from docx import Document
        >>> document = Document()
        >>> run = document.add_paragraph().add_run()
        >>> font = run.font

    Typeface and size are set like this::

        >>> from docx.shared import Pt
        >>> font.name = 'Calibri'
        >>> font.size = Pt(12)

    Many font properties are *tri-state*, meaning they can take the values
    |True|, |False|, and |None|. |True| means the property is "on", |False| means
    it is "off". Conceptually, the |None| value means "inherit". A run exists in
    the style inheritance hierarchy and by default inherits its character
    formatting from that hierarchy. Any character formatting directly applied
    using the |Font| object overrides the inherited values.

    Bold and italic are tri-state properties, as are all-caps, strikethrough,
    superscript, and many others. See the |Font| API documentation for a full
    list::

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

    Underline is a bit of a special case. It is a hybrid of a tri-state property
    and an enumerated value property. |True| means single underline, by far the
    most common. |False| means no underline, but more often |None| is the right
    choice if no underlining is wanted. The other forms of underlining, such as
    double or dashed, are specified with a member of the :ref:`WdUnderline`
    enumeration::

        >>> font.underline
        None
        >>> font.underline = True
        >>> # or perhaps
        >>> font.underline = WD_UNDERLINE.DOT_DASH

字体颜色
~~~~~~~~~~

Font color

.. tab:: 中文

    每个 |Font| 对象都有一个 |ColorFormat| 对象，可通过其只读 :attr:`~.Font.color` 属性访问其 颜色。

    将特定的 RGB 颜色应用于字体::

        >>> from docx.shared import RGBColor
        >>> font.color.rgb = RGBColor(0x42, 0x24, 0xE9)

    还可以通过分配 :ref:`MsoThemeColorIndex` 枚举的成员将字体设置为主题颜色::

        >>> from docx.enum.dml import MSO_THEME_COLOR
        >>> font.color.theme_color = MSO_THEME_COLOR.ACCENT_1

    可以通过分配
    |None| 将字体的颜色恢复为其默认（继承）值到 |ColorFormat| 的 :attr:`~.ColorFormat.rgb` 或
    :attr:`~.ColorFormat.theme_color` 属性::

        >>> font.color.rgb = None

    确定字体的颜色首先要确定其颜色类型::

        >>> font.color.type
        RGB (1)

    :attr:`~.ColorFormat.type` 属性的值可以是
    :ref:`MsoColorType` 枚举的成员或 None。`MSO_COLOR_TYPE.RGB` 表示它是
    RGB 颜色。`MSO_COLOR_TYPE.THEME` 表示主题颜色。

    `MSO_COLOR_TYPE.AUTO` 表示其值由应用程序自动确定，通常设置为黑色。（此值相对罕见。）|None|
    表示未应用任何颜色，颜色从样式层次结构继承；这是最常见的情况。

    当颜色类型为 `MSO_COLOR_TYPE.RGB` 时，:attr:`~.ColorFormat.rgb`
    属性将为表示 RGB 颜色的 |RGBColor| 值::

        >>> font.color.rgb
        RGBColor(0x42, 0x24, 0xe9)

    当颜色类型为 `MSO_COLOR_TYPE.THEME` 时，
    :attr:`~.ColorFormat.theme_color` 属性将为
    :ref:`MsoThemeColorIndex` 的成员，表示主题颜色::

        >>> font.color.theme_color
        ACCENT_1 (5)

.. tab:: 英文

    Each |Font| object has a |ColorFormat| object that provides access to its
    color, accessed via its read-only :attr:`~.Font.color` property.

    Apply a specific RGB color to a font::

        >>> from docx.shared import RGBColor
        >>> font.color.rgb = RGBColor(0x42, 0x24, 0xE9)

    A font can also be set to a theme color by assigning a member of the
    :ref:`MsoThemeColorIndex` enumeration::

        >>> from docx.enum.dml import MSO_THEME_COLOR
        >>> font.color.theme_color = MSO_THEME_COLOR.ACCENT_1

    A font's color can be restored to its default (inherited) value by assigning
    |None| to either the :attr:`~.ColorFormat.rgb` or
    :attr:`~.ColorFormat.theme_color` attribute of |ColorFormat|::

        >>> font.color.rgb = None

    Determining the color of a font begins with determining its color type::

        >>> font.color.type
        RGB (1)

    The value of the :attr:`~.ColorFormat.type` property can be a member of the
    :ref:`MsoColorType` enumeration or None. `MSO_COLOR_TYPE.RGB` indicates it is
    an RGB color. `MSO_COLOR_TYPE.THEME` indicates a theme color.
    `MSO_COLOR_TYPE.AUTO` indicates its value is determined automatically by the
    application, usually set to black. (This value is relatively rare.) |None|
    indicates no color is applied and the color is inherited from the style
    hierarchy; this is the most common case.

    When the color type is `MSO_COLOR_TYPE.RGB`, the :attr:`~.ColorFormat.rgb`
    property will be an |RGBColor| value indicating the RGB color::

        >>> font.color.rgb
        RGBColor(0x42, 0x24, 0xe9)

    When the color type is `MSO_COLOR_TYPE.THEME`, the
    :attr:`~.ColorFormat.theme_color` property will be a member of
    :ref:`MsoThemeColorIndex` indicating the theme color::

        >>> font.color.theme_color
        ACCENT_1 (5)
