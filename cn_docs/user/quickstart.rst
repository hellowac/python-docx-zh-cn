.. _quickstart:

快速入门
==========

Quickstart

.. tab:: 中文

    开始使用 |docx| 非常简单。让我们来了解一下基础知识。

.. tab:: 英文

    Getting started with |docx| is easy. Let's walk through the basics.


打开文档
------------------

Opening a document

.. tab:: 中文

    您首先需要的是一份要处理的文档。最简单的方法是::

        from docx import Document

        document = Document()

    这将打开一个基于默认“模板”的空白文档，这与使用内置默认值在 Word 中启动新文档时所获得的内容非常相似。您可以使用 |docx| 打开并处理现有的 Word 文档，但目前我们先简单介绍一下。

.. tab:: 英文

    First thing you'll need is a document to work on. The easiest way is this::

        from docx import Document

        document = Document()

    This opens up a blank document based on the default "template", pretty much what you get when you start a new document in Word using the built-in defaults. You can open and work on an existing Word document using |docx|, but we'll keep things simple for the moment.


添加段落
------------------

Adding a paragraph

.. tab:: 中文

    段落是 Word 中的基础。它们用于正文，也用于标题和列表项（如项目符号）。

    这是添加段落的最简单方法::

        paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')

    此方法返回对段落的引用，即文档末尾新添加的段落。在本例中，新段落引用被分配给“paragraph”，但除非我需要，否则我将在以下示例中省略它。在您的代码中，通常您在添加项目后不会对其进行任何操作，因此保留对它的引用没有多大意义。

    还可以将一个段落用作“光标”，并在其上方直接插入一个新段落::

        prior_paragraph = paragraph.insert_paragraph_before('Lorem ipsum')

    这样可以将一个段落插入到文档中间，这在修改现有文档而不是从头生成文档时通常很重要。

.. tab:: 英文

    Paragraphs are fundamental in Word. They're used for body text, but also for headings and list items like bullets.

    Here's the simplest way to add one::

        paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')

    This method returns a reference to a paragraph, newly added paragraph at the end of the document. The new paragraph reference is assigned to ``paragraph`` in this case, but I'll be leaving that out in the following examples unless I have a need for it. In your code, often times you won't be doing anything with the item after you've added it, so there's not a lot of sense in keep a reference to it hanging around.

    It's also possible to use one paragraph as a "cursor" and insert a new paragraph directly above it::

        prior_paragraph = paragraph.insert_paragraph_before('Lorem ipsum')

    This allows a paragraph to be inserted in the middle of a document, something that's often important when modifying an existing document rather than generating one from scratch.


添加标题
----------------

Adding a heading

.. tab:: 中文

    除了最短的文档外，正文还会被分成几个部分，每个部分都以标题开头。添加标题的方法如下::

        document.add_heading('宇宙的真正意义')

    默认情况下，这会添加一个顶级标题，在 Word 中显示为“标题 1”。当您想要为子部分添加标题时，只需将所需的级别指定为 1 到 9 之间的整数::

        document.add_heading('海豚的作用', level=2)

    如果您将级别指定为 0，则会添加“标题”段落。这对于开始一个没有单独标题页的相对较短的文档非常方便。

.. tab:: 英文

    In anything but the shortest document, body text is divided into sections, each of which starts with a heading. Here's how to add one::

        document.add_heading('The REAL meaning of the universe')

    By default, this adds a top-level heading, what appears in Word as 'Heading 1'. When you want a heading for a sub-section, just specify the level you want as an integer between 1 and 9::

        document.add_heading('The role of dolphins', level=2)

    If you specify a level of 0, a "Title" paragraph is added. This can be handy to start a relatively short document that doesn't have a separate title page.


添加分页符
-------------------

Adding a page break

.. tab:: 中文

    有时，即使当前页面未满，您也希望将后面的文本放在单独的页面上。“硬”分页符可以实现此目的::

        document.add_page_break()

    如果您发现自己经常使用此功能，则可能表明您可以通过更好地了解段落样式受益。您可以设置的一个段落样式属性是在每个具有该样式的段落之前立即分页。因此，您可以将特定级别的标题设置为始终开始新页面。稍后将详细介绍样式。事实证明，它们对于真正充分利用 Word 至关重要。

.. tab:: 英文

    Every once in a while you want the text that comes next to go on a separate page, even if the one you're on isn't full. A "hard" page break gets this done::

        document.add_page_break()

    If you find yourself using this very often, it's probably a sign you could benefit by better understanding paragraph styles. One paragraph style property you can set is to break a page immediately before each paragraph having that style. So you might set your headings of a certain level to always start a new page. More on styles later. They turn out to be critically important for really getting the most out of Word.


添加表格
--------------

Adding a table

.. tab:: 中文

    我们经常会遇到适合以表格形式呈现的内容，整齐地排列在行和列中。Word 在这方面做得相当不错。以下是添加表格的方法::

        table = document.add_table(rows=2, cols=2)

    要填充表格，你需要了解表格的一些属性和方法。首先，最好从访问单个单元格开始。作为基础操作，你可以通过行和列的索引来访问单元格::

        cell = table.cell(0, 1)

    这将获取我们刚刚创建的表格顶部行的右侧单元格。请注意，行和列的索引是从零开始的，就像列表索引一样。

    一旦你有了一个单元格，就可以在其中填入内容::

        cell.text = 'parrot, possibly dead'

    通常情况下，一次访问一行单元格会更方便，例如从数据源填充长度可变的表格时。表格的 `.rows` 属性可以让你访问单独的行，每一行都有一个 `.cells` 属性。`Row` 和 `Column` 上的 `.cells` 属性支持像列表一样的索引访问::

        row = table.rows[1]
        row.cells[0].text = 'Foo bar to you.'
        row.cells[1].text = 'And a hearty foo bar to you too sir!'

    表格上的 `.rows` 和 `.columns` 集合是可迭代的，因此你可以直接在 `for` 循环中使用它们。行或列上的 `.cells` 序列也是如此::

        for row in table.rows:
            for cell in row.cells:
                print(cell.text)

    如果你想获取表格中的行数或列数，只需对序列使用 `len()` 函数::

        row_count = len(table.rows)
        col_count = len(table.columns)

    你也可以像下面这样逐步向表格中添加行::

        row = table.add_row()

    对于我们上面提到的可变长度表格场景，这非常有用::

        # 获取表格数据 -------------
        items = (
            (7, '1024', 'Plush kittens'),
            (3, '2042', 'Furbees'),
            (1, '1288', 'French Poodle Collars, Deluxe'),
        )

        # 添加表格 ------------------
        table = document.add_table(1, 3)

        # 填充表头行 --------
        heading_cells = table.rows[0].cells
        heading_cells[0].text = '数量'
        heading_cells[1].text = 'SKU'
        heading_cells[2].text = '描述'

        # 为每个项目添加一行数据
        for item in items:
            cells = table.add_row().cells
            cells[0].text = str(item.qty)
            cells[1].text = item.sku
            cells[2].text = item.desc

    对于列也可以这样做，不过我还没有遇到过这样的使用场景。

    Word 提供了一系列预格式化的表格样式，你可以从其表格样式库中进行选择。你可以像下面这样将其中一种样式应用到表格上::

        table.style = 'LightShading-Accent1'

    样式名称是通过删除表格样式名称中的所有空格形成的。你可以在 Word 的表格样式库中将鼠标悬停在缩略图上查看表格样式名称 。

.. tab:: 英文

    One frequently encounters content that lends itself to tabular presentation, lined up in neat rows and columns. Word does a pretty good job at this. Here's how to add a table::

        table = document.add_table(rows=2, cols=2)

    Tables have several properties and methods you'll need in order to populate them. Accessing individual cells is probably a good place to start. As a baseline, you can always access a cell by its row and column indicies::

        cell = table.cell(0, 1)

    This gives you the right-hand cell in the top row of the table we just created. Note that row and column indicies are zero-based, just like in list access.

    Once you have a cell, you can put something in it::

        cell.text = 'parrot, possibly dead'

    Frequently it's easier to access a row of cells at a time, for example when populating a table of variable length from a data source. The ``.rows`` property of a table provides access to individual rows, each of which has a ``.cells`` property.  The ``.cells`` property on both ``Row`` and ``Column`` supports indexed access, like a list::

        row = table.rows[1]
        row.cells[0].text = 'Foo bar to you.'
        row.cells[1].text = 'And a hearty foo bar to you too sir!'

    The ``.rows`` and ``.columns`` collections on a table are iterable, so you can use them directly in a ``for`` loop. Same with the ``.cells`` sequences on a row or column::

        for row in table.rows:
            for cell in row.cells:
                print(cell.text)

    If you want a count of the rows or columns in the table, just use ``len()`` on the sequence::

        row_count = len(table.rows)
        col_count = len(table.columns)

    You can also add rows to a table incrementally like so::

        row = table.add_row()

    This can be very handy for the variable length table scenario we mentioned above::

        # get table data -------------
        items = (
            (7, '1024', 'Plush kittens'),
            (3, '2042', 'Furbees'),
            (1, '1288', 'French Poodle Collars, Deluxe'),
        )

        # add table ------------------
        table = document.add_table(1, 3)

        # populate header row --------
        heading_cells = table.rows[0].cells
        heading_cells[0].text = 'Qty'
        heading_cells[1].text = 'SKU'
        heading_cells[2].text = 'Description'

        # add a data row for each item
        for item in items:
            cells = table.add_row().cells
            cells[0].text = str(item.qty)
            cells[1].text = item.sku
            cells[2].text = item.desc


    The same works for columns, although I've yet to see a use case for it.

    Word has a set of pre-formatted table styles you can pick from its table style gallery. You can apply one of those to the table like this::

        table.style = 'LightShading-Accent1'

    The style name is formed by removing all the spaces from the table style name. You can find the table style name by hovering your mouse over its thumbnail in Word's table style gallery.


添加图片
----------------

Adding a picture

.. tab:: 中文

    Word 允许您使用 ``插入 > 照片 > 来自文件的图片...`` 菜单项将图像放入文档中。以下是在 |docx| 中执行此操作的方法::

        document.add_picture('image-filename.png')

    此示例使用路径，从本地文件系统加载图像文件。您还可以使用 *类文件对象*，本质上是任何像打开文件一样的对象。如果您从数据库或通过网络检索图像并且不想让文件系统参与其中，这可能会很方便。

.. tab:: 英文

    Word lets you place an image in a document using the ``Insert > Photo > Picture from file...`` menu item. Here's how to do it in |docx|::

        document.add_picture('image-filename.png')

    This example uses a path, which loads the image file from the local filesystem. You can also use a *file-like object*, essentially any object that acts like an open file. This might be handy if you're retrieving your image from a database or over a network and don't want to get the filesystem involved.


图像大小
~~~~~~~~~~

Image size

.. tab:: 中文

    默认情况下，添加的图片会以“原始”尺寸显示。这通常比你期望的要大。原始尺寸是根据“像素数 / 每英寸点数（dpi）”计算得出的。因此，一张分辨率为 300 dpi、像素尺寸为 300×300 的图片会在文档中显示为一个边长为一英寸的正方形。问题是，大多数图片并不包含 dpi 属性，其默认值为 72 dpi。这样一来，同一张图片的边长就会显示为 4.167 英寸，大约占了页面的一半。

    要使图片达到你期望的大小，你可以使用英寸或厘米等便捷单位来指定图片的宽度或高度::

        from docx.shared import Inches

        document.add_picture('image-filename.png', width=Inches(1.0))

    你可以同时指定宽度和高度，但通常没必要这么做。如果你只指定了其中一个参数，|docx| 会根据它自动计算出另一个参数的适当缩放值。这样就能保持图片的“纵横比”，避免图片看起来被拉伸变形。

    `Inches` 和 `Cm` 类可用于让你以便捷的单位指定尺寸。在 |docx| 内部，使用的是英制公制单位（English Metric Units），1 英寸对应 914400 个单位。所以，如果你忘了这一点，只是简单地写 `width=2` ，那么得到的图片会极小 :)。你需要从 `docx.shared` 子包中导入这些类。在使用时，你可以像处理整数一样对它们进行算术运算，实际上它们在内部就是以整数形式存储的。因此，像 `width = Inches(3) / thing_count` 这样的表达式完全可以正常工作 。

.. tab:: 英文

    By default, the added image appears at `native` size. This is often bigger than
    you want. Native size is calculated as ``pixels / dpi``. So a 300x300 pixel
    image having 300 dpi resolution appears in a one inch square. The problem is
    most images don't contain a dpi property and it defaults to 72 dpi. This would
    make the same image appear 4.167 inches on a side, somewhere around half the
    page.

    To get the image the size you want, you can specify either its width or height
    in convenient units, like inches or centimeters::

        from docx.shared import Inches

        document.add_picture('image-filename.png', width=Inches(1.0))

    You're free to specify both width and height, but usually you wouldn't want to.
    If you specify only one, |docx| uses it to calculate the properly scaled value
    of the other. This way the *aspect ratio* is preserved and your picture doesn't
    look stretched.

    The ``Inches`` and ``Cm`` classes are provided to let you specify measurements
    in handy units. Internally, |docx| uses English Metric Units, 914400 to the
    inch. So if you forget and just put something like ``width=2`` you'll get an
    extremely small image :). You'll need to import them from the ``docx.shared``
    sub-package. You can use them in arithmetic just like they were an integer,
    which in fact they are. So an expression like ``width = Inches(3)
    / thing_count`` works just fine.


应用段落样式
--------------------------

Applying a paragraph style

.. tab:: 中文

    如果你不了解 Word 段落样式是什么，那绝对应该去了解一下。基本上，它能让你一次性为段落应用一整套格式设置选项。如果你了解 CSS 样式的话，段落样式与之非常相似。

    你可以在创建段落时就应用段落样式::

        document.add_paragraph('Lorem ipsum dolor sit amet.', style='ListBullet')

    这种特定的样式会使段落显示为带有项目符号的形式，这非常方便。你也可以在创建段落后再应用样式。下面这两行代码与上面的代码效果相同::

        paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')
        paragraph.style = 'List Bullet'

    样式的指定是通过其样式名称来完成的，在这个例子中样式名称为 'List Bullet' 。通常情况下，样式名称与 Word 用户界面（UI）中显示的名称完全一致 。

.. tab:: 英文

    If you don't know what a Word paragraph style is you should definitely check it
    out. Basically it allows you to apply a whole set of formatting options to
    a paragraph at once. It's a lot like CSS styles if you know what those are.

    You can apply a paragraph style right when you create a paragraph::

        document.add_paragraph('Lorem ipsum dolor sit amet.', style='ListBullet')

    This particular style causes the paragraph to appear as a bullet, a very handy
    thing. You can also apply a style afterward. These two lines are equivalent to
    the one above::

        paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')
        paragraph.style = 'List Bullet'

    The style is specified using its style name, 'List Bullet' in this example.
    Generally, the style name is exactly as it appears in the Word user interface
    (UI).


应用粗体和斜体
------------------------

Applying bold and italic

.. tab:: 中文

    为了理解加粗和倾斜是如何实现的，你需要对段落内部的情况有一些了解。简单来说如下：

    #. 段落包含所有 *块级* 格式设置，例如缩进、行高、制表符等。

    #. 字符级格式设置（如加粗和倾斜）是在 `run` （文本运行块）级别应用的。段落中的所有内容必须位于某个 `run` 中，但一个段落可以包含多个 `run` 。因此，如果一个段落的中间有一个加粗的单词，那么这个段落就需要三个 `run` ：一个是普通文本 `run` ，一个包含加粗单词的 `run` ，以及另一个用于后续文本的普通 `run` 。

    当你通过向 `.add_paragraph()` 方法提供文本来添加段落时，该文本会被放入一个单独的 `run` 中。你可以使用段落的 `.add_run()` 方法添加更多的 `run` ::

        paragraph = document.add_paragraph('Lorem ipsum ')
        paragraph.add_run('dolor sit amet.')

    这样生成的段落在外观上与从单个字符串创建的段落完全一样。除非查看 XML 代码，否则你无法看出段落文本是如何划分成多个 `run` 的。注意第一个字符串末尾的空格。你需要明确指定每个 `run` 开头和结尾处的空格位置，因为 `run` 之间不会自动插入空格。你可能会因此犯几次错 :).

    `Run` 对象有 `.bold` 和 `.italic` 属性，你可以用它们来设置某个 `run` 的加粗或倾斜效果::

        paragraph = document.add_paragraph('Lorem ipsum ')
        run = paragraph.add_run('dolor')
        run.bold = True
        paragraph.add_run(' sit amet.')

    这样生成的文本看起来是这样的：'Lorem ipsum **dolor** sit amet.'

    注意，如果你不需要对 `.add_run()` 的结果做其他用途，也可以直接在其结果上设置加粗或倾斜::

        paragraph.add_run('dolor').bold = True

        # 等同于：

        run = paragraph.add_run('dolor')
        run.bold = True

        # 只不过之后你就没有对 run 对象的引用了


    向 `.add_paragraph()` 方法提供文本并不是必需的。如果你打算从 `run` 开始构建段落，这样做可以让代码更简洁::

        paragraph = document.add_paragraph()
        paragraph.add_run('Lorem ipsum ')
        paragraph.add_run('dolor').bold = True
        paragraph.add_run(' sit amet.')

.. tab:: 英文

    In order to understand how bold and italic work, you need to understand
    a little about what goes on inside a paragraph. The short version is this:

    #. A paragraph holds all the *block-level* formatting, like indentation, line
    height, tabs, and so forth.

    #. Character-level formatting, such as bold and italic, are applied at the
    `run` level. All content within a paragraph must be within a run, but there
    can be more than one. So a paragraph with a bold word in the middle would
    need three runs, a normal one, a bold one containing the word, and another
    normal one for the text after.

    When you add a paragraph by providing text to the ``.add_paragraph()`` method,
    it gets put into a single run. You can add more using the ``.add_run()`` method
    on the paragraph::

        paragraph = document.add_paragraph('Lorem ipsum ')
        paragraph.add_run('dolor sit amet.')

    This produces a paragraph that looks just like one created from a single
    string. It's not apparent where paragraph text is broken into runs unless you
    look at the XML. Note the trailing space at the end of the first string. You
    need to be explicit about where spaces appear at the beginning and end of
    a run. They're not automatically inserted between runs. Expect to be caught by
    that one a few times :).

    |Run| objects have both a ``.bold`` and ``.italic`` property that allows you to
    set their value for a run::

        paragraph = document.add_paragraph('Lorem ipsum ')
        run = paragraph.add_run('dolor')
        run.bold = True
        paragraph.add_run(' sit amet.')

    which produces text that looks like this: 'Lorem ipsum **dolor** sit amet.'

    Note that you can set bold or italic right on the result of ``.add_run()`` if
    you don't need it for anything else::

        paragraph.add_run('dolor').bold = True

        # is equivalent to:

        run = paragraph.add_run('dolor')
        run.bold = True

        # except you don't have a reference to `run` afterward


    It's not necessary to provide text to the ``.add_paragraph()`` method. This can
    make your code simpler if you're building the paragraph up from runs anyway::

        paragraph = document.add_paragraph()
        paragraph.add_run('Lorem ipsum ')
        paragraph.add_run('dolor').bold = True
        paragraph.add_run(' sit amet.')


应用字符样式
--------------------------

Applying a character style

.. tab:: 中文

    除了段落样式（用于指定一组段落级别的设置）之外，Word 还有 *字符样式* ，用于指定一组文本运行块（run）级别的设置。一般来说，你可以将字符样式理解为指定一种字体，包括字体类型、字号、颜色、加粗、倾斜等属性。

    与段落样式一样，字符样式必须在你使用 `Document()` 调用打开的文档中已经定义好（`参见` :ref:`understanding_styles`）。

    在添加新的文本运行块（run）时可以指定字符样式::

        paragraph = document.add_paragraph('Normal text, ')
        paragraph.add_run('text with emphasis.', 'Emphasis')

    你也可以在创建文本运行块（run）后为其应用样式。下面的代码与上面的代码效果相同::

        paragraph = document.add_paragraph('Normal text, ')
        run = paragraph.add_run('text with emphasis.')
        run.style = 'Emphasis'

    与段落样式一样，样式名称与 Word 用户界面（UI）中显示的名称完全一致 。

.. tab:: 英文

    In addition to paragraph styles, which specify a group of paragraph-level
    settings, Word has *character styles* which specify a group of run-level
    settings. In general you can think of a character style as specifying a font,
    including its typeface, size, color, bold, italic, etc.

    Like paragraph styles, a character style must already be defined in the
    document you open with the ``Document()`` call (`see`
    :ref:`understanding_styles`).

    A character style can be specified when adding a new run::

        paragraph = document.add_paragraph('Normal text, ')
        paragraph.add_run('text with emphasis.', 'Emphasis')

    You can also apply a style to a run after it is created. This code produces
    the same result as the lines above::

        paragraph = document.add_paragraph('Normal text, ')
        run = paragraph.add_run('text with emphasis.')
        run.style = 'Emphasis'

    As with a paragraph style, the style name is as it appears in the Word UI.
