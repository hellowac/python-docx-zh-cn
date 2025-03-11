.. _tables:

使用表格
===================

Working with Tables

.. tab:: 中文

    Word 提供了创建表格的复杂功能。通常，这种功能也伴随着
    额外的概念复杂性。

    这种复杂性在 *阅读* 表格时最为明显，尤其是从
    随意获取的文档中，因为对于表格可能包含的内容或表格的结构，人们知之甚少或一无所知。

    这些是您需要了解的一些重要概念。

.. tab:: 英文

    Word provides sophisticated capabilities to create tables. As usual, this power comes with
    additional conceptual complexity.

    This complexity becomes most apparent when *reading* tables, in particular from documents drawn from
    the wild where there is limited or no prior knowledge as to what the tables might contain or how
    they might be structured.

    These are some of the important concepts you'll need to understand.


概念：简单（统一）表格
--------------------------------

Concept: Simple (uniform) tables

.. tab:: 中文

    ::

        +---+---+---+
        | a | b | c |
        +---+---+---+
        | d | e | f |
        +---+---+---+
        | g | h | i |
        +---+---+---+

    表格的基本概念非常直观。您有 *行* 和 *列* ，并且每个（行、列）位置都有不同的 *单元格* 。它可以被描述为 *网格* 或 *矩阵* 。我们将此概念称为 *统一表* 。关系数据库表和 Pandas 数据框都是统一表的示例。

    以下不变量适用于统一表：

    * 每行具有相同数量的单元格，每列一个。
    * 每列具有相同数量的单元格，每行一个。

.. tab:: 英文

    ::

        +---+---+---+
        | a | b | c |
        +---+---+---+
        | d | e | f |
        +---+---+---+
        | g | h | i |
        +---+---+---+

    The basic concept of a table is intuitive enough. You have *rows* and *columns*, and at each (row,
    column) position is a different *cell*. It can be described as a *grid* or a *matrix*. Let's call
    this concept a *uniform table*. A relational database table and a Pandas dataframe are both examples
    of a uniform table.

    The following invariants apply to uniform tables:

    * Each row has the same number of cells, one for each column.
    * Each column has the same number of cells, one for each row.


问题 1：合并单元格
----------------------------

Complication 1: Merged Cells

::

    +---+---+---+   +---+---+---+
    |   a   | b |   |   | b | c |
    +---+---+---+   + a +---+---+
    | c | d | e |   |   | d | e |
    +---+---+---+   +---+---+---+
    | f | g | h |   | f | g | h |
    +---+---+---+   +---+---+---+

.. tab:: 中文

    虽然统一表格非常适合数据处理，但它缺乏供人类阅读的表格所需的表达能力。

    统一表格所缺乏的最重要的特性可能是 *合并单元格* 。将多个单元格组合成一个单元格是很常见的，例如形成列组标题或为一系列单元格提供相同的值，而不是为每个单元格重复该值。通过减少人类读者的认知负担，这些方法使呈现的表格更具可读性，并使某些关系变得明确，否则这些关系可能很容易被忽略。

    不幸的是，容纳合并的单元格会破坏统一表格的两个不变量：

    * 每行可以有不同数量的单元格。

    * 每列可以有不同数量的单元格。

    这对以编程方式读取表格内容提出了挑战。人们可能自然而然地想将表格读入统一的矩阵数据结构，如 3 x 3 “2D 数组” （可能是列表列表），但当表格不是统一的时，这不可能直接实现。

.. tab:: 英文

    While very suitable for data processing, a uniform table lacks expressive power desireable for
    tables intended for a human reader.

    Perhaps the most important characteristic a uniform table lacks is *merged cells*. It is very common
    to want to group multiple cells into one, for example to form a column-group heading or provide the
    same value for a sequence of cells rather than repeat it for each cell. These make a rendered table
    more *readable* by reducing the cognitive load on the human reader and make certain relationships
    explicit that might easily be missed otherwise.

    Unfortunately, accommodating merged cells breaks both the invariants of a uniform table:

    * Each row can have a different number of cells.
    * Each column can have a different number of cells.

    This challenges reading table contents programatically. One might naturally want to read the table
    into a uniform matrix data structure like a 3 x 3 "2D array" (list of lists perhaps), but this is
    not directly possible when the table is not known to be uniform.


概念：布局网格
------------------------

Concept: The layout grid

::

  + - + - + - +
  |   |   |   |
  + - + - + - +
  |   |   |   |
  + - + - + - +
  |   |   |   |
  + - + - + - +

.. tab:: 中文

  在 Word 中，每个表格都有一个 *布局网格*。

  - 布局网格是 *统一的*。每个（布局行、布局列）对都有一个布局位置。
  - 布局网格本身不可见。但是，它由表格 XML 中的某些元素和属性表示和引用
  - 每个表格单元格都位于一个布局网格位置；即每个单元格的左上角是布局网格单元格的左上角。
  - 每个表格单元格占据一个或多个整个布局网格单元格。合并的单元格将占据多个布局网格单元格。没有表格单元格可以占据部分布局网格单元格。
  - 另一种说法是，单元格的每个垂直边界（左和右）都与布局网格垂直边界对齐，水平边界也是如此。但并非所有布局网格边界都需要被表格的单元格边界占据。

.. tab:: 英文

    In Word, each table has a *layout grid*.

    - The layout grid is *uniform*. There is a layout position for every (layout-row, layout-column) pair.
    - The layout grid itself is not visible. However it is represented and referenced by certain elements and attributes within the table XML
    - Each table cell is located at a layout-grid position; i.e. the top-left corner of each cell is the top-left corner of a layout-grid cell.
    - Each table cell occupies one or more whole layout-grid cells. A merged cell will occupy multiple layout-grid cells. No table cell can occupy a partial layout-grid cell.
    - Another way of saying this is that every vertical boundary (left and right) of a cell aligns with a layout-grid vertical boundary, likewise for horizontal boundaries. But not all layout-grid boundaries need be occupied by a cell boundary of the table.


问题 2：省略单元格
-----------------------------

Complication 2: Omitted Cells

::

      +---+---+   +---+---+---+
      | a | b |   | a | b | c |
  +---+---+---+   +---+---+---+
  | c | d |           | d |
  +---+---+       +---+---+---+
      | e |       | e | f | g |
      +---+       +---+---+---+

.. tab:: 中文

    Word 的一个不同寻常之处在于它允许从行的开头或结尾（但不能从中间）省略单元格。一个典型的实际示例是具有一行列标题和一列行标题的表格，但没有左上角单元格（位置 0, 0），例如此 XOR 真值表。

    ::

            +---+---+
            | T | F |
        +---+---+---+
        | T | F | T |
        +---+---+---+
        | F | T | F |
        +---+---+---+

    在 `python-docx` 中，|_Row| 对象中省略的单元格由 ``.grid_cols_before`` 和
    ``.grid_cols_after`` 属性表示。在上面的例子中，对于第一行，``.grid_cols_before`` 等于 ``1``，而 ``.grid_cols_after`` 等于 ``0``。

    请注意，省略的单元格不仅仅是“空”单元格。它们表示未被单元格占用的布局网格位置，并且不能由 |_Cell| 对象表示。当尝试为任意 Word 表生成统一表示（例如 2D 数组）时，这种区别变得非常重要。

.. tab:: 英文

    Word is unusual in that it allows cells to be omitted from the beginning or end (but not the middle)
    of a row. A typical practical example is a table with both a row of column headings and a column of
    row headings, but no top-left cell (position 0, 0), such as this XOR truth table.

    ::

          +---+---+
          | T | F |
      +---+---+---+
      | T | F | T |
      +---+---+---+
      | F | T | F |
      +---+---+---+

    In `python-docx`, omitted cells in a |_Row| object are represented by the ``.grid_cols_before`` and
    ``.grid_cols_after`` properties. In the example above, for the first row, ``.grid_cols_before``
    would equal ``1`` and ``.grid_cols_after`` would equal ``0``.

    Note that omitted cells are not just "empty" cells. They represent layout-grid positions that are
    unoccupied by a cell and they cannot be represented by a |_Cell| object. This distinction becomes
    important when trying to produce a uniform representation (e.g. a 2D array) for an arbitrary Word
    table.


概念：`python-docx` 默认近似统一表格
-------------------------------------------------------------

Concept: `python-docx` approximates uniform tables by default

.. tab:: 中文

    要准确表示任意表格，需要复杂的图形数据结构。浏览此数据结构至少与浏览表格的 `python-docx` 对象图一样复杂。从任意 Word 文件集合中提取内容（例如为文档编制索引）时，通常选择更简单的数据结构并*近似*该结构中的表格。

    反思关系表或数据框如何表示表格信息，一个简单的近似方法是简单地重复合并单元格占用的每个布局网格单元格的合并单元格值::


      +---+---+---+      +---+---+---+
      |   a   | b |  ->  | a | a | b |
      +---+---+---+      +---+---+---+
      |   | d | e |  ->  | c | d | e |
      + c +---+---+      +---+---+---+
      |   | f | g |  ->  | c | f | g |
      +---+---+---+      +---+---+---+

    这是 ``_Row.cells`` 默认执行的操作。概念上::

      >>> [tuple(c.text for c in r.cells) for r in table.rows]
      [
      (a, a, b),
      (c, d, e),
      (c, f, g),
      ]

    请注意，当没有省略单元格时，这只会生成一个统一的单元格“矩阵”。当需要保持列完整性时，处理省略的单元格需要更复杂的方法::

      #     +---+---+
      #     | a | b |
      # +---+---+---+
      # | c | d |
      # +---+---+
      #     | e |
      #     +---+

      def iter_row_cell_texts(row: _Row) -> Iterator[str]:
          for _ in range(row.grid_cols_before):
              yield ""
          for c in row.cells:
              yield c.text
          for _ in range(row.grid_cols_after):
              yield ""

      >>> [tuple(iter_row_cell_texts(r)) for r in table.rows]
      [
        ("",  "a", "b"),
        ("c", "d", ""),
        ("",  "e", ""),
      ]

.. tab:: 英文

    To accurately represent an arbitrary table would require a complex graph data structure. Navigating
    this data structure would be at least as complex as navigating the `python-docx` object graph for a
    table. When extracting content from a collection of arbitrary Word files, such as for indexing the
    document, it is common to choose a simpler data structure and *approximate* the table in that
    structure.

    Reflecting on how a relational table or dataframe represents tabular information, a straightforward
    approximation would simply repeat merged-cell values for each layout-grid cell occupied by the
    merged cell::


      +---+---+---+      +---+---+---+
      |   a   | b |  ->  | a | a | b |
      +---+---+---+      +---+---+---+
      |   | d | e |  ->  | c | d | e |
      + c +---+---+      +---+---+---+
      |   | f | g |  ->  | c | f | g |
      +---+---+---+      +---+---+---+

    This is what ``_Row.cells`` does by default. Conceptually::

      >>> [tuple(c.text for c in r.cells) for r in table.rows]
      [
        (a, a, b),
        (c, d, e),
        (c, f, g),
      ]

    Note this only produces a uniform "matrix" of cells when there are no omitted cells. Dealing with
    omitted cells requires a more sophisticated approach when maintaining column integrity is required::

      #     +---+---+
      #     | a | b |
      # +---+---+---+
      # | c | d |
      # +---+---+
      #     | e |
      #     +---+

      def iter_row_cell_texts(row: _Row) -> Iterator[str]:
          for _ in range(row.grid_cols_before):
              yield ""
          for c in row.cells:
              yield c.text
          for _ in range(row.grid_cols_after):
              yield ""

      >>> [tuple(iter_row_cell_texts(r)) for r in table.rows]
      [
        ("",  "a", "b"),
        ("c", "d", ""),
        ("",  "e", ""),
      ]


问题 3：表格是递归的
------------------------------------

Complication 3: Tables are Recursive

.. tab:: 中文

    使表格处理更加复杂的是它们的递归性质。在 Word 中，与在 HTML 中一样，表格单元格本身可以包含一个或多个表格。

    可以使用 ``_Cell.tables`` 或 ``_Cell.iter_inner_content()`` 检测这些表格。后者还保留了表格相对于单元格中段落的文档顺序。

.. tab:: 英文

    Further complicating table processing is their recursive nature. In Word, as in HTML, a table cell
    can itself include one or more tables.

    These can be detected using ``_Cell.tables`` or ``_Cell.iter_inner_content()``. The latter preserves
    the document order of the table with respect to paragraphs also in the cell.
