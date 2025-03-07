.. _understanding_styles:

了解样式
====================

Understanding Styles

.. tab:: 中文

    **Grasshopper：**
        *“大师，为什么我的段落没有按照我指定的样式显示？”*

    **大师：**
        *“Grasshopper，您来对地方了；请继续阅读...”*

.. tab:: 英文

    **Grasshopper:**
        *"Master, why doesn't my paragraph appear with the style I specified?"*

    **Master:**
        *"You have come to the right page Grasshopper; read on ..."*


Word 中的样式是什么？
------------------------

What is a style in Word?

.. tab:: 中文

    当类似元素的格式一致时，文档可以更好地传达信息。为了实现这种一致性，专业文档设计人员开发了一个 *样式表* ，它定义了文档元素类型并指定了每个元素的格式。例如，也许正文段落应该设置为 9 pt Times Roman，行高为 11 pt，左对齐，右对齐。当将这些规范应用于文档的每个元素时，就会实现一致且精致的外观。

    Word 中的样式就是这样一组可以同时应用于文档元素的规范。Word 具有段落样式、字符样式、表格样式和编号定义。它们分别应用于段落、文本范围、表格和列表。

    经验丰富的程序员会将样式视为一种间接级别。这些的优点在于它允许您定义一次，然后多次应用该定义。这节省了一遍又一遍定义相同内容的工作；但更重要的是，它允许你改变定义，并且
    让这种改变反映在你应用它的所有地方。

.. tab:: 英文

    Documents communicate better when like elements are formatted consistently. To
    achieve that consistency, professional document designers develop a *style
    sheet* which defines the document element types and specifies how each should
    be formatted. For example, perhaps body paragraphs are to be set in 9 pt Times
    Roman with a line height of 11 pt, justified flush left, ragged right. When
    these specifications are applied to each of the elements of the document,
    a consistent and polished look is achieved.

    A style in Word is such a set of specifications that may be applied, all at
    once, to a document element. Word has paragraph styles, character styles, table
    styles, and numbering definitions. These are applied to a paragraph, a span of
    text, a table, and a list, respectively.

    Experienced programmers will recognize styles as a level of indirection. The
    great thing about those is it allows you to define something once, then apply
    that definition many times. This saves the work of defining the same thing
    over an over; but more importantly it allows you to change the definition and
    have that change reflected in all the places you have applied it.


为什么我应用的样式没有显示？
----------------------------------------

Why doesn't the style I applied show up?

.. tab:: 中文

    在我添加一些更高级的功能来解决这个问题之前，这个问题可能会经常出现，所以这里将其放在最上面。

    #. 在 Word 中工作时，您可以将所有这些样式应用于事物，这些样式看起来非常漂亮，而且看起来更好，因为您不必自己制作它们。大多数人只关注内置的样式。

    #. 虽然这些样式显示在 UI 中，但它们实际上并不在您正在创建的 文档中，至少在您第一次使用它之前不是。 这是一件好事。它们占用空间，而且数量很多。 如果文件包含您可以使用但尚未使用的所有样式定义，则文件会变得有点臃肿。

    #. 如果您使用 |docx| 应用未在文件中定义的样式（如果您好奇，在 styles.xml 部分中），Word 会忽略它。它不会抱怨，只是不会改变格式。我确信 这有充分的理由。但是，如果您不了解 Word 的工作原理，这可能会让您感到有些困惑。

    #. 当您使用样式时，Word 会将其添加到文件中。一旦添加到文件中，它就会保留下来。 我想有一种方法可以摆脱它，但您必须努力。如果 您应用样式，删除您应用它的内容，然后保存 文档；样式定义将保留在保存的文件中。

    所有这些加起来就是以下内容：如果您想在使用 |docx| 创建的文档中使用样式，您开始使用的文档必须包含样式
    定义。否则它就无法工作。它不会引发异常，只是
    无法工作。

    如果您使用“默认”模板文档，它包含下面列出的样式，如果您不设计自己的样式，则大部分样式都是您可能需要的。
    如果您使用自己的起始文档，则需要在其中使用您想要的每种样式至少一次。您不必保留内容，但在保存文档之前，您需要将样式至少应用于某项内容一次。创建一个单词段落，连续应用五种样式，然后删除该段落，效果很好。这就是我将下面的样式放入默认模板的方法:)。

.. tab:: 英文

    This is likely to show up quite a bit until I can add some fancier features to
    work around it, so here it is up top.

    #. When you're working in Word, there are all these styles you can apply to things, pretty good looking ones that look all the better because you don't have to make them yourself. Most folks never look further than the built-in styles.

    #. Although those styles show up in the UI, they're not actually in the document you're creating, at least not until you use it for the first time. That's kind of a good thing. They take up room and there's a lot of them. The file would get a little bloated if it contained all the style definitions you could use but haven't.

    #. If you apply a style using |docx| that's not defined in your file (in the styles.xml part if you're curious), Word just ignores it. It doesn't complain, it just doesn't change how things are formatted. I'm sure there's a good reason for this. But it can present as a bit of a puzzle if you don't understand how Word works that way.
    
    #. When you use a style, Word adds it to the file. Once there, it stays. I imagine there's a way to get rid of it, but you have to work at it. If you apply a style, delete the content you applied it to, and then save the document; the style definition stays in the saved file.

    All this adds up to the following: If you want to use a style in a document you
    create with |docx|, the document you start with must contain the style
    definition. Otherwise it just won't work. It won't raise an exception, it just
    won't work.

    If you use the "default" template document, it contains the styles listed
    below, most of the ones you're likely to want if you're not designing your own.
    If you're using your own starting document, you need to use each of the styles
    you want at least once in it. You don't have to keep the content, but you need
    to apply the style to something at least once before saving the document.
    Creating a one-word paragraph, applying five styles to it in succession and
    then deleting the paragraph works fine. That's how I got the ones below into
    the default template :).


词汇表
--------

Glossary

.. tab:: 中文

    样式定义
        文档样式部分中的 ``<w:style>`` 元素，用于明确定义样式的属性。

    已定义样式
        文档中明确定义的样式。与 *潜在样式* 相对。

    内置样式
        Word 内置的 276 种预设样式之一，例如“标题 1”。内置样式可以是已定义的，也可以是潜在的。尚未定义的内置样式称为 *潜在样式*。已定义和潜在的内置样式都可能作为选项出现在 Word 的样式面板和样式库中。

    自定义样式
        也称为 *用户定义样式*，Word 文档中定义的任何样式，但不是内置样式。请注意，自定义样式不能是潜在样式。

    潜在样式
        在特定文档中没有定义的内置样式在该文档中称为 *潜在样式*。潜在样式可以作为 Word UI 中的选项出现，具体取决于文档的 |LatentStyles| 对象中的设置。

    推荐样式列表
        当从 “列表：” 下拉框中选择 “推荐” 时，样式工具箱或面板中显示的样式列表。

    样式库
        Word UI 功能区中显示的示例样式的选择，可通过单击其中一个来应用。

.. tab:: 英文

    style definition
        A ``<w:style>`` element in the styles part of a document that explicitly
        defines the attributes of a style.

    defined style
        A style that is explicitly defined in a document. Contrast with *latent
        style*.

    built-in style
        One of the set of 276 pre-set styles built into Word, such as "Heading
        1". A built-in style can be either defined or latent. A built-in style
        that is not yet defined is known as a *latent style*. Both defined and
        latent built-in styles may appear as options in Word's style panel and
        style gallery.

    custom style
        Also known as a *user defined style*, any style defined in a Word
        document that is not a built-in style. Note that a custom style cannot be
        a latent style.

    latent style
        A built-in style having no definition in a particular document is known
        as a *latent style* in that document. A latent style can appear as an
        option in the Word UI depending on the settings in the |LatentStyles|
        object for the document.

    recommended style list
        A list of styles that appears in the styles toolbox or panel when
        "Recommended" is selected from the "List:" dropdown box.

    Style Gallery
        The selection of example styles that appear in the ribbon of the Word UI
        and which may be applied by clicking on one of them.


识别样式
-------------------

Identifying a style

.. tab:: 中文

    样式有三个标识属性，即 `name`、 `style_id` 和 `type`。

    每种样式的 :attr:`name` 属性是其稳定、唯一的标识符，用于访问目的。

    样式的 :attr:`style_id` 在内部用于将内容对象（例如段落）键入其样式。但是，此值由 Word 自动生成，并且不能保证在保存时保持稳定。通常，样式 id 只需从 `localized` 样式名称中删除空格即可形成，但也有例外。|docx| 的用户通常应避免使用 样式 id，除非他们对所涉及的内部结构有信心。

    样式的 :attr:`type` 在创建时设置，无法更改。

.. tab:: 英文

    A style has three identifying properties, `name`, `style_id`, and `type`.

    Each style's :attr:`name` property is its stable, unique identifier for
    access purposes.

    A style's :attr:`style_id` is used internally to key a content object such as
    a paragraph to its style. However this value is generated automatically by
    Word and is not guaranteed to be stable across saves. In general, the style
    id is formed simply by removing spaces from the `localized` style name,
    however there are exceptions. Users of |docx| should generally avoid using
    the style id unless they are confident with the internals involved.

    A style's :attr:`type` is set at creation time and cannot be changed.


.. _builtin_styles:

内置样式
---------------

Built-in styles

.. tab:: 中文

    Word 附带了近 300 种所谓的 *内置* 样式，如 `Normal`、
    `Heading 1` 和 `List Bullet`。样式定义存储在 .docx 包的
    `styles.xml` 部分中，但内置样式定义存储在 Word 应用程序本身中，在实际使用之前不会写入 `styles.xml`。这是一个明智的策略，因为它们占用了相当大的空间，否则在每个 .docx 文件中都会成为大量冗余和无用的开销。

    内置样式在使用之前不会写入 .docx 包，这一事实导致了对 *潜在样式* 定义的需求，如下所述。

.. tab:: 英文

    Word comes with almost 300 so-called *built-in* styles like `Normal`,
    `Heading 1`, and `List Bullet`. Style definitions are stored in the
    `styles.xml` part of a .docx package, but built-in style definitions are
    stored in the Word application itself and are not written to `styles.xml`
    until they are actually used. This is a sensible strategy because they take
    up considerable room and would be largely redundant and useless overhead in
    every .docx file otherwise.

    The fact that built-in styles are not written to the .docx package until used
    gives rise to the need for *latent style* definitions, explained below.


.. _style_behavior:

样式行为
--------------

Style Behavior

.. tab:: 中文

    除了收集一组格式属性之外，样式还有五个
    属性来指定其“行为”。此行为相对简单，
    基本上相当于样式在 Word 或 LibreOffice UI 中出现的时间和位置。

    理解样式行为的关键概念是推荐列表。在 Word 的
    样式窗格中，用户可以选择他们想要查看的样式列表。其中一个名为“推荐”，称为*推荐
    列表*。所有五个行为属性都会影响样式在此列表和样式库中的某些方面。

    简而言之，如果样式的 :attr:`hidden`
    属性为 |False|（默认值），则样式会出现在推荐列表中。如果样式未隐藏且其
    :attr:`quick_style` 属性为 |True|，则它也会出现在样式库中。
    如果隐藏样式的 :attr:`unhide_when_used` 属性为 |True|，则其隐藏
    属性在第一次使用时设置为 |False|。样式列表
    和样式库中的样式按 :attr:`priority` 顺序排序，然后按字母顺序对优先级相同的样式进行排序。如果样式的 :attr:`locked` 属性为
    |True|，并且为文档启用了格式限制，则样式
    将不会出现在任何列表或样式库中，也无法应用于
    内容。

.. tab:: 英文

    In addition to collecting a set of formatting properties, a style has five
    properties that specify its `behavior`. This behavior is relatively simple,
    basically amounting to when and where the style appears in the Word or
    LibreOffice UI.

    The key notion to understanding style behavior is the recommended list. In
    the style pane in Word, the user can select which list of styles they want to
    see. One of these is named `Recommended` and is known as the *recommended
    list*. All five behavior properties affect some aspect of the style’s
    appearance in this list and in the style gallery.

    In brief, a style appears in the recommended list if its :attr:`hidden`
    property is |False| (the default). If a style is not hidden and its
    :attr:`quick_style` property is |True|, it also appears in the style gallery.
    If a hidden style's :attr:`unhide_when_used` property is |True|, its hidden
    property is set |False| the first time it is used. Styles in the style lists
    and style gallery are sorted in :attr:`priority` order, then alphabetically
    for styles of the same priority. If a style's :attr:`locked` property is
    |True| and formatting restrictions are turned on for the document, the style
    will not appear in any list or the style gallery and cannot be applied to
    content.


.. _latent_styles:

潜在样式
-------------

Latent styles

.. tab:: 中文

    由于需要指定未在 `styles.xml` 中定义的内置样式的 UI 行为，因此需要 *潜在样式* 定义。潜在样式定义基本上是一个存根样式定义，除了样式名称外，最多还包含五个行为属性。通过为每个行为属性定义默认值，可以节省额外的空间，因此只需要定义与默认值不同的属性，并且与所有默认值匹配的样式不需要潜在样式定义。

    使用 `styles.xml` 中出现的 `w:latentStyles` 和 `w:lsdException` 元素指定潜在样式定义。

    仅内置样式需要潜在样式定义，因为只有内置样式才能在 UI 中出现，而无需在 `styles.xml` 中定义样式。

.. tab:: 英文

    The need to specify the UI behavior of built-in styles not defined in
    `styles.xml` gives rise to the need for *latent style* definitions. A latent
    style definition is basically a stub style definition that has at most the
    five behavior attributes in addition to the style name. Additional space is
    saved by defining defaults for each of the behavior attributes, so only those
    that differ from the default need be defined and styles that match all
    defaults need no latent style definition.

    Latent style definitions are specified using the `w:latentStyles` and
    `w:lsdException` elements appearing in `styles.xml`.

    A latent style definition is only required for a built-in style because only
    a built-in style can appear in the UI without a style definition in
    `styles.xml`.


样式继承
-----------------

Style inheritance

.. tab:: 中文

    一种样式可以继承另一种样式的属性，这有点类似于
    层叠样式表 (CSS) 的工作方式。使用
    :attr:`~.BaseStyle.base_style` 属性指定继承。通过将一种样式建立在另一种样式的基础上，可以形成任意深度的
    继承层次结构。没有
    基本样式的样式会从文档默认值继承属性。

.. tab:: 英文

    A style can inherit properties from another style, somewhat similarly to how
    Cascading Style Sheets (CSS) works. Inheritance is specified using the
    :attr:`~.BaseStyle.base_style` attribute. By basing one style on another, an
    inheritance hierarchy of arbitrary depth can be formed. A style having no
    base style inherits properties from the document defaults.


默认模板中的段落样式
------------------------------------

Paragraph styles in default template

* Normal
* Body Text
* Body Text 2
* Body Text 3
* Caption
* Heading 1
* Heading 2
* Heading 3
* Heading 4
* Heading 5
* Heading 6
* Heading 7
* Heading 8
* Heading 9
* Intense Quote
* List
* List 2
* List 3
* List Bullet
* List Bullet 2
* List Bullet 3
* List Continue
* List Continue 2
* List Continue 3
* List Number
* List Number 2
* List Number 3
* List Paragraph
* Macro Text
* No Spacing
* Quote
* Subtitle
* TOCHeading
* Title


默认模板中的字符样式
------------------------------------

Character styles in default template

* Body Text Char
* Body Text 2 Char
* Body Text 3 Char
* Book Title
* Default Paragraph Font
* Emphasis
* Heading 1 Char
* Heading 2 Char
* Heading 3 Char
* Heading 4 Char
* Heading 5 Char
* Heading 6 Char
* Heading 7 Char
* Heading 8 Char
* Heading 9 Char
* Intense Emphasis
* Intense Quote Char
* Intense Reference
* Macro Text Char
* Quote Char
* Strong
* Subtitle Char
* Subtle Emphasis
* Subtle Reference
* Title Char


默认模板中的表格样式
--------------------------------

Table styles in default template

* Table Normal
* Colorful Grid
* Colorful Grid Accent 1
* Colorful Grid Accent 2
* Colorful Grid Accent 3
* Colorful Grid Accent 4
* Colorful Grid Accent 5
* Colorful Grid Accent 6
* Colorful List
* Colorful List Accent 1
* Colorful List Accent 2
* Colorful List Accent 3
* Colorful List Accent 4
* Colorful List Accent 5
* Colorful List Accent 6
* Colorful Shading
* Colorful Shading Accent 1
* Colorful Shading Accent 2
* Colorful Shading Accent 3
* Colorful Shading Accent 4
* Colorful Shading Accent 5
* Colorful Shading Accent 6
* Dark List
* Dark List Accent 1
* Dark List Accent 2
* Dark List Accent 3
* Dark List Accent 4
* Dark List Accent 5
* Dark List Accent 6
* Light Grid
* Light Grid Accent 1
* Light Grid Accent 2
* Light Grid Accent 3
* Light Grid Accent 4
* Light Grid Accent 5
* Light Grid Accent 6
* Light List
* Light List Accent 1
* Light List Accent 2
* Light List Accent 3
* Light List Accent 4
* Light List Accent 5
* Light List Accent 6
* Light Shading
* Light Shading Accent 1
* Light Shading Accent 2
* Light Shading Accent 3
* Light Shading Accent 4
* Light Shading Accent 5
* Light Shading Accent 6
* Medium Grid 1
* Medium Grid 1 Accent 1
* Medium Grid 1 Accent 2
* Medium Grid 1 Accent 3
* Medium Grid 1 Accent 4
* Medium Grid 1 Accent 5
* Medium Grid 1 Accent 6
* Medium Grid 2
* Medium Grid 2 Accent 1
* Medium Grid 2 Accent 2
* Medium Grid 2 Accent 3
* Medium Grid 2 Accent 4
* Medium Grid 2 Accent 5
* Medium Grid 2 Accent 6
* Medium Grid 3
* Medium Grid 3 Accent 1
* Medium Grid 3 Accent 2
* Medium Grid 3 Accent 3
* Medium Grid 3 Accent 4
* Medium Grid 3 Accent 5
* Medium Grid 3 Accent 6
* Medium List 1
* Medium List 1 Accent 1
* Medium List 1 Accent 2
* Medium List 1 Accent 3
* Medium List 1 Accent 4
* Medium List 1 Accent 5
* Medium List 1 Accent 6
* Medium List 2
* Medium List 2 Accent 1
* Medium List 2 Accent 2
* Medium List 2 Accent 3
* Medium List 2 Accent 4
* Medium List 2 Accent 5
* Medium List 2 Accent 6
* Medium Shading 1
* Medium Shading 1 Accent 1
* Medium Shading 1 Accent 2
* Medium Shading 1 Accent 3
* Medium Shading 1 Accent 4
* Medium Shading 1 Accent 5
* Medium Shading 1 Accent 6
* Medium Shading 2
* Medium Shading 2 Accent 1
* Medium Shading 2 Accent 2
* Medium Shading 2 Accent 3
* Medium Shading 2 Accent 4
* Medium Shading 2 Accent 5
* Medium Shading 2 Accent 6
* Table Grid
