
表格 - 合并单元格
===================

Table - Merge Cells

.. tab:: 中文

    Word 允许合并相邻的表格单元格，使两个或多个单元格看起来像一个单元格。单元格可以水平合并（跨多个列）或垂直合并（跨多行）。单元格还可以同时水平和垂直合并，从而形成一个同时跨行和跨列的单元格。只能合并矩形范围内的单元格。

.. tab:: 英文

    Word allows contiguous table cells to be merged, such that two or more cells appear to be a single cell. Cells can be merged horizontally (spanning multple columns) or vertically (spanning multiple rows). Cells can also be merged both horizontally and vertically at the same time, producing a cell that spans both rows and columns. Only rectangular ranges of cells can be merged.


表格图
--------------

Table diagrams

.. tab:: 中文

    在本分析中，类似下图的示意图用于描述表格结构。  

    - **水平合并** 以连续的水平单元格表示，合并范围内没有垂直分隔线。  
    - **垂直合并** 以一系列具有相同宽度的垂直单元格表示，其中续接单元格的顶部边框为虚线，并包含插入符号 (`^`)，表示它们是上方单元格的延续。  
    - **单元格“地址”** 显示在列和行的网格线上。这种表示方法在概念上很方便，因为它复用了列表索引（和切片）的概念，使某些操作的指定更加直观。  

    例如，合并单元格 `A` 在下图中，其 **顶部、左侧、底部和右侧** 的索引值分别为 **0、0、2 和 2**。

.. tab:: 英文

    Diagrams like the one below are used to depict tables in this analysis.
    Horizontal spans are depicted as a continuous horizontal cell without
    vertical dividers within the span. Vertical spans are depicted as a vertical
    sequence of cells of the same width where continuation cells are separated by
    a dashed top border and contain a caret ('^') to symbolize the continuation
    of the cell above. Cell 'addresses' are depicted at the column and row grid
    lines. This is conceptually convenient as it reuses the notion of list
    indices (and slices) and makes certain operations more intuitive to specify.
    The merged cell `A` below has top, left, bottom, and right values of 0, 0, 2,
    and 2 respectively

::

  \ 0   1   2   3
  0 +---+---+---+
    | A     |   |
  1 + - - - +---+
    | ^     |   |
  2 +---+---+---+
    |   |   |   |
  3 +---+---+---+


基本单元格访问协议
--------------------------

Basic cell access protocol

.. tab:: 中文

    有三种方法可以访问表格单元格:

    * ``Table.cell(row_idx, col_idx)``
    * ``Row.cells[col_idx]``
    * ``Column.cells[col_idx]``


    访问 3 x 3 表格的中间单元格::

        >>> table = document.add_table(3, 3)
        >>> middle_cell = table.cell(1, 1)
        >>> table.rows[1].cells[1] == middle_cell
        True
        >>> table.columns[1].cells[1] == middle_cell
        True

.. tab:: 英文

    There are three ways to access a table cell:

    * ``Table.cell(row_idx, col_idx)``
    * ``Row.cells[col_idx]``
    * ``Column.cells[col_idx]``


    Accessing the middle cell of a 3 x 3 table::

        >>> table = document.add_table(3, 3)
        >>> middle_cell = table.cell(1, 1)
        >>> table.rows[1].cells[1] == middle_cell
        True
        >>> table.columns[1].cells[1] == middle_cell
        True


基本合并协议
--------------------

Basic merge protocol

.. tab:: 中文

    使用两个对角单元格指定合并

.. tab:: 英文

    A merge is specified using two diagonal cells

::

    >>> table = document.add_table(3, 3)
    >>> a = table.cell(0, 0)
    >>> b = table.cell(1, 1)
    >>> A = a.merge(b)

::

    \ 0   1   2   3
    0 +---+---+---+        +---+---+---+
      | a |   |   |        | A     |   |
    1 +---+---+---+        + - - - +---+
      |   | b |   |  -->   | ^     |   |
    2 +---+---+---+        +---+---+---+
      |   |   |   |        |   |   |   |
    3 +---+---+---+        +---+---+---+


访问已合并单元格
-----------------------

Accessing a merged cell

.. tab:: 中文

    单元格的访问方式基于其 **“布局网格” (layout grid)** 位置，而不受合并单元格的影响。  

    - **如果网格地址落在合并区域内**，则返回该合并区域 **左上角的单元格**。  
    - **合并单元格拥有多个地址**，对应其在网格中所覆盖的所有单元格。例如，合并单元格 `A` 可以通过 `(0, 0)`、 `(0, 1)`、 `(1, 0)` 或 `(1, 1)` 访问。  
    - **这种寻址方式** 在表格存在合并单元格时仍然能保持直观的访问行为。  

    此外：  

    - `Row.cells` 的长度始终等于 **网格列数**，不受合并影响。  
    - `Column.cells` 的长度始终等于 **表格行数**，也不受合并影响。

.. tab:: 英文

    A cell is accessed by its "layout grid" position regardless of any spans that
    may be present. A grid address that falls in a span returns the top-leftmost
    cell in that span. This means a span has as many addresses as layout grid
    cells it spans. For example, the merged cell `A` above can be addressed as
    (0, 0), (0, 1), (1, 0), or (1, 1). This addressing scheme leads to desirable
    access behaviors when spans are present in the table.

    The length of Row.cells is always equal to the number of grid columns,
    regardless of any spans that are present. Likewise, the length of
    Column.cells is always equal to the number of table rows, regardless of any
    spans.

::

    >>> table = document.add_table(2, 3)
    >>> row = table.rows[0]
    >>> len(row.cells)
    3
    >>> row.cells[0] == row.cells[1]
    False

    >>> a, b = row.cells[:2]
    >>> a.merge(b)

    >>> len(row.cells)
    3
    >>> row.cells[0] == row.cells[1]
    True

::

    \ 0   1   2   3
    0 +---+---+---+        +---+---+---+
      | a | b |   |        | A     |   |
    1 +---+---+---+  -->   +---+---+---+
      |   |   |   |        |   |   |   |
    2 +---+---+---+        +---+---+---+


合并时的单元格内容行为
------------------------------

Cell content behavior on merge

.. tab:: 中文

    当两个或多个单元格合并时，所有现有内容都会被拼接，并放置到合并后的单元格中。  

    - 每个原始单元格的内容 **之间** 由 **段落标记** (`\n`) 分隔。  
    - **空单元格不会出现在拼接结果中**，即如果原单元格内容为空，则在合并时会被跳过。  

    在 Python 中，该过程可以大致表示如下::

        merged_cell_text = '\n'.join(
            cell.text for cell in original_cells if cell.text
        )

    例如，将四个单元格（内容分别为 `'a'`、 `'b'`、 `''` （空）、 `'d'` ）合并后，  
    **合并单元格的文本内容将变为** ::

        'a\nb\nd'

.. tab:: 英文

    When two or more cells are merged, any existing content is concatenated and
    placed in the resulting merged cell. Content from each original cell is
    separated from that in the prior original cell by a paragraph mark. An
    original cell having no content is skipped in the contatenation process. In
    Python, the procedure would look roughly like this::

      merged_cell_text = '\n'.join(
          cell.text for cell in original_cells if cell.text
      )

    Merging four cells with content ``'a'``, ``'b'``, ``''``, and ``'d'``
    respectively results in a merged cell having text ``'a\nb\nd'``.


合并时的单元格大小行为
---------------------------

Cell size behavior on merge

.. tab:: 中文

    单元格宽度和高度（如果存在）在单元格合并时添加

.. tab:: 英文

    Cell width and height, if present, are added when cells are merged

::

    >>> a, b = row.cells[:2]
    >>> a.width.inches, b.width.inches
    (1.0, 1.0)
    >>> A = a.merge(b)
    >>> A.width.inches
    2.0


删除多余的行或列
----------------------------------

Removing a redundant row or column

.. tab:: 中文

    **折叠列（Collapsing a column）。**   当网格中的 **所有单元格** 在同一列中 **共享相同的** `w:gridSpan` **属性** 时，   可以通过 **移除** `w:gridSpan` **属性**，将这些跨列的单元格 **合并为单个列**。

.. tab:: 英文

    **Collapsing a column.** When all cells in a grid column share the same ``w:gridSpan`` specification, the spanned columns can be collapsed into a single column by removing the ``w:gridSpan`` attributes.


单词行为
-------------

Word behavior

.. tab:: 中文

    * **MS API 中的行（Row）和列（Column）访问在非均匀表格中会失效。**  
      当表格 **包含垂直合并单元格** 时，调用 `Table.Rows(n)` 或 `Cell.Row` 会引发 `EnvironmentError`。  
      当表格 **包含水平合并单元格** 时，调用 `Table.Columns(n)` 或 `Cell.Column` **始终** 会引发 `EnvironmentError`。  
      我们可以做得更好。

    * `Table.Cell(n, m)` **可以在任何非均匀表格上正常工作**，  
      但它基于 **视觉网格（visual grid）**，这会 **极大增加访问的复杂性**。  
      如果 `n` 或 `m` 超出视觉范围，它会引发错误，  
      并且 **无法通过** `Row.Count` 或 `Column.Count` **来确定视觉范围**，  
      **只能使用 try/except 进行错误捕获**。

    * **在合并单元格时**， **续接单元格的文本** 会作为 **单独的段落** **追加** 到 **原始单元格** 中。

    * **如果合并范围包含** **已经合并的单元格**，  
      则 **必须完全包围** 这些已合并的单元格，才能进行合并操作。

    * **Word 允许访问超出行索引范围的单元格**，  
      此时 **会自动增加行数** 以适应新的单元格。  
      但是，如果 **列索引超出范围**，则会引发异常。  
      **这一行为不会在 |docx| 中实现。**

.. tab:: 英文

    * Row and Column access in the MS API just plain breaks when the table is not uniform. `Table.Rows(n)` and `Cell.Row` raise `EnvironmentError` when a table contains a vertical span, and `Table.Columns(n)` and `Cell.Column` unconditionally raise `EnvironmentError` when the table contains a horizontal span. We can do better.

    * `Table.Cell(n, m)` works on any non-uniform table, although it uses a *visual grid* that greatly complicates access. It raises an error for `n` or `m` out of visual range, and provides no way other than try/except to determine what that visual range is, since `Row.Count` and `Column.Count` are unavailable.

    * In a merge operation, the text of the continuation cells is appended to that of the origin cell as separate paragraph(s).

    * If a merge range contains previously merged cells, the range must completely enclose the merged cells.

    * Word resizes a table (adds rows) when a cell is referenced by an out-of-bounds row index. If the column identifier is out of bounds, an exception is raised. This behavior will not be implemented in |docx|.


词汇表
--------

Glossary

.. tab:: 中文

    **布局网格（layout grid）**  
        表格的 **规则二维矩阵**，由 **行和列** 组成，决定了单元格的布局。  
        **主要由 `w:gridCol` 元素定义**，用于指定表格的 **布局列**。  
        每一行 **基本上复制** 这些布局列，但行高可以不同。  
        **表格中的每个单元格**（无论是否合并）**必须始于和终止于布局网格的“线”**。

    **合并单元格（span）**  
        由多个合并单元格 **组合而成的单个单元格**。

    **跳过单元格（skipped cell）**  
        WordprocessingML（WML） **允许** **“跳过”** 某些单元格位置，使其不包含实际单元格。  
        但 **Word UI 似乎无法创建这样的表格**，目前尚未测试 Word 是否能加载手动构造的 XML 版本。

    **均匀表格（uniform table）**  
        一个 **每个单元格都完全对应一个布局单元格** 的表格。  
        **均匀表格** **不包含** **合并单元格** 或 **跳过的单元格**。

    **非均匀表格（non-uniform table）**  
        一个 **包含一个或多个合并单元格** 的表格，  
        **并非所有单元格都对应单个布局单元格**。  
        虽然 **跳过单元格** 也可能导致非均匀表格，但本分析仅用于指代 **包含合并单元格** 的情况。

    **均匀单元格（uniform cell）**  
        **不属于任何合并单元格**，仅占据 **一个布局单元格** 的单元格。

    **原始单元格（origin cell）**  
        **合并单元格的左上角单元格**。  
        可与 **续接单元格（continuation cell）** 进行对比。

    **续接单元格（continuation cell）**  
        **被合并单元格包含的布局单元格**。  
        续接单元格 **主要是一个抽象概念**，但在 **垂直合并** 的情况下，  
        **每个续接单元格在 XML 中都会有对应的 `w:tc` 元素**。

.. tab:: 英文

    layout grid 
        The regular two-dimensional matrix of rows and columns that determines the layout of cells in the table. The grid is primarily defined by the `w:gridCol` elements that define the layout columns for the table. Each row essentially duplicates that layout for an additional row, although its height can differ from other rows. Every actual cell in the table must begin and end on a layout grid "line", whether the cell is merged or not.

    span
        The single "combined" cell occupying the area of a set of merged cells.

    skipped cell
        The WordprocessingML (WML) spec allows for 'skipped' cells, where
        a layout cell location contains no actual cell. I can't find a way to
        make a table like this using the Word UI and haven't experimented yet to
        see whether Word will load one constructed by hand in the XML.

    uniform table
        A table in which each cell corresponds exactly to a layout cell.
        A uniform table contains no spans or skipped cells.

    non-uniform table
        A table that contains one or more spans, such that not every cell
        corresponds to a single layout cell. I suppose it would apply when there
        was one or more skipped cells too, but in this analysis the term is only
        used to indicate a table with one or more spans.

    uniform cell
        A cell not part of a span, occupying a single cell in the layout grid.

    origin cell
        The top-leftmost cell in a span. Contrast with *continuation cell*.

    continuation cell
        A layout cell that has been subsumed into a span. A continuation cell is
        mostly an abstract concept, although a actual `w:tc` element will always
        exist in the XML for each continuation cell in a vertical span.


直观地理解合并 XML
-----------------------------------

Understanding merge XML intuitively

.. tab:: 中文

    一个关键的见解是，合并的单元格总是如下图所示。
    水平跨度通过每行中的单个 `w:tc` 元素实现，
    使用 `gridSpan` 属性跨度额外的网格列。垂直跨度通过每个连续行中的相同单元格实现，
    具有相同的 `gridSpan` 值，并将 vMerge 设置为 `continue`（默认）。这些垂直连续单元格在下图中用虚线顶部边框和最左侧网格列中的插入符号（“^”）表示，
    以表示上方单元格的连续性。::

      \ 0   1   2   3
      0 +---+---+---+
        | A     |   |
      1 + - - - +---+
        | ^     |   |
      2 +---+---+---+
        |   |   |   |
      3 +---+---+---+

    上表与此 XML 相对应（为清晰起见已最小化）

.. tab:: 英文

    A key insight is that merged cells always look like the diagram below.
    Horizontal spans are accomplished with a single `w:tc` element in each row,
    using the `gridSpan` attribute to span additional grid columns. Vertical
    spans are accomplished with an identical cell in each continuation row,
    having the same `gridSpan` value, and having vMerge set to `continue` (the
    default). These vertical continuation cells are depicted in the diagrams
    below with a dashed top border and a caret ('^') in the left-most grid column
    to symbolize the continuation of the cell above.::

      \ 0   1   2   3
      0 +---+---+---+
        | A     |   |
      1 + - - - +---+
        | ^     |   |
      2 +---+---+---+
        |   |   |   |
      3 +---+---+---+

    The table depicted above corresponds to this XML (minimized for clarity)

.. highlight:: xml

::

  <w:tbl>
    <w:tblGrid>
       <w:gridCol/>
       <w:gridCol/>
       <w:gridCol/>
    </w:tblGrid>
    <w:tr>
       <w:tc>
          <w:tcPr>
             <w:gridSpan w:val="2"/>
             <w:vMerge w:val="restart"/>
          </w:tcPr>
       </w:tc>
       <w:tc/>
    </w:tr>
    <w:tr>
       <w:tc>
          <w:tcPr>
             <w:gridSpan w:val="2"/>
             <w:vMerge/>
          </w:tcPr>
       </w:tc>
       <w:tc/>
    </w:tr>
    <w:tr>
       <w:tc/>
       <w:tc/>
       <w:tc/>
    </w:tr>
  </w:tbl>


XML 语义
-------------

XML Semantics

.. tab:: 中文

    在水平合并中， ``<w:tc w:gridSpan="?">`` 属性指示单元格应跨越的列数。仅保留最左侧的单元格；合并中的其余单元格将被删除。

    对于垂直合并，列最上部单元格的 ``w:vMerge`` 表格单元格属性设置为 ``w:ST_Merge`` 类型的值“restart”。垂直合并中包含的以下较低单元格必须在其单元格属性 (``w:TcPr``) 元素中存在 ``w:vMerge`` 元素。其值应设置为“continue”，尽管没有必要明确定义它，因为它是默认值。只要单元格 ``w:TcPr`` 元素缺少 ``w:vMerge`` 元素，垂直合并就会结束。与 ``w:gridSpan`` 元素类似，只有当表格的布局在各个列之间不一致时，才需要 ``w:vMerge`` 元素。在这种情况下，只保留最顶部的单元格；合并区域中其他较低的单元格连同它们的 ``w:vMerge`` 元素一起被删除，并且 ``w:trHeight`` 表行属性用于指定合并单元格的组合高度。

.. tab:: 英文

    In a horizontal merge, the ``<w:tc w:gridSpan="?">`` attribute indicates the
    number of columns the cell should span. Only the leftmost cell is preserved;
    the remaining cells in the merge are deleted.

    For merging vertically, the ``w:vMerge`` table cell property of the uppermost
    cell of the column is set to the value "restart" of type ``w:ST_Merge``. The
    following, lower cells included in the vertical merge must have the
    ``w:vMerge`` element present in their cell property (``w:TcPr``) element. Its
    value should be set to "continue", although it is not necessary to
    explicitely define it, as it is the default value. A vertical merge ends as
    soon as a cell ``w:TcPr`` element lacks the ``w:vMerge`` element. Similarly
    to the ``w:gridSpan`` element, the ``w:vMerge`` elements are only required
    when the table's layout is not uniform across its different columns. In the
    case it is, only the topmost cell is kept; the other lower cells in the
    merged area are deleted along with their ``w:vMerge`` elements and the
    ``w:trHeight`` table row property is used to specify the combined height of
    the merged cells.


Row.cells 和 Column.cells 的 len() 实现
---------------------------------------------------

len() implementation for Row.cells and Column.cells

.. tab:: 中文

    每个 ``Row`` 和 ``Column`` 对象都提供对其所包含的单元格集合的访问。这些单元格集合的长度不受合并单元格存在的影响。

    ``len()`` 始终以布局网格为基础进行计数，就好像没有合并单元格一样。

    * ``len(Table.columns)`` 是 `w:gridCol` 元素的数量，表示网格列的数量，而不考虑表中是否存在合并单元格。

    * ``len(Table.rows)`` 是 `w:tr` 元素的数量，无论表中是否存在合并单元格。

    * ``len(Row.cells)`` 是网格列的数量，无论行中是否有单元格合并。

    * ``len(Column.cells)`` 是表中的行数，无论列中是否有单元格合并。

.. tab:: 英文

    Each ``Row`` and ``Column`` object provides access to the collection of cells it contains. The length of these cell collections is unaffected by the presence of merged cells.

    `len()` always bases its count on the layout grid, as though there were no merged cells.

    * ``len(Table.columns)`` is the number of `w:gridCol` elements, representing the number of grid columns, without regard to the presence of merged cells in the table.

    * ``len(Table.rows)`` is the number of `w:tr` elements, regardless of any merged cells that may be present in the table.

    * ``len(Row.cells)`` is the number of grid columns, regardless of whether any cells in the row are merged.

    * ``len(Column.cells)`` is the number of rows in the table, regardless of whether any cells in the column are merged.


合并已包含跨度的单元格
----------------------------------------

Merging a cell already containing a span

.. tab:: 中文

    合并操作中的一个或两个“对角（diagonal corner）”单元格本身可以是合并单元格，只要指定的区域是矩形即可.

    例如::

      \   0   1   2   3
        +---+---+---+---+       +---+---+---+---+
      0 | a     | b |   |       | a\nb\nC   |   |
        + - - - +---+---+       + - - - - - +---+
      1 | ^     | C |   |       | ^         |   |
        +---+---+---+---+  -->  +---+---+---+---+
      2 |   |   |   |   |       |   |   |   |   |
        +---+---+---+---+       +---+---+---+---+
      3 |   |   |   |   |       |   |   |   |   |
        +---+---+---+---+       +---+---+---+---+

        cell(0, 0).merge(cell(1, 2))

    或::

          0   1   2   3   4
        +---+---+---+---+---+       +---+---+---+---+---+
      0 | a     | b | c |   |       | abcD          |   |
        + - - - +---+---+---+       + - - - - - - - +---+
      1 | ^     | D     |   |       | ^             |   |
        +---+---+---+---+---+  -->  +---+---+---+---+---+
      2 |   |   |   |   |   |       |   |   |   |   |   |
        +---+ - - - +---+---+       +---+---+---+---+---+
      3 |   |   |   |   |   |       |   |   |   |   |   |
        +---+---+---+---+---+       +---+---+---+---+---+

        cell(0, 0).merge(cell(1, 2))


    相反，这两种合并操作都是非法的::

        \ 0   1   2   3   4      0   1   2   3   4
        0 +---+---+---+---+    0 +---+---+---+---+
          |   |   | b |   |      |   |   |   |   |
        1 +---+---+ - +---+    1 +---+---+---+---+
          |   | a | ^ |   |      |   | a |   |   |
        2 +---+---+ - +---+    2 +---+---+---+---+
          |   |   | ^ |   |      | b         |   |
        3 +---+---+---+---+    3 +---+---+---+---+
          |   |   |   |   |      |   |   |   |   |
        4 +---+---+---+---+    4 +---+---+---+---+

          a.merge(b)

.. tab:: 英文

    One or both of the "diagonal corner" cells in a merge operation may itself be a merged cell, as long as the specified region is rectangular.

    For example::

      \   0   1   2   3
        +---+---+---+---+       +---+---+---+---+
      0 | a     | b |   |       | a\nb\nC   |   |
        + - - - +---+---+       + - - - - - +---+
      1 | ^     | C |   |       | ^         |   |
        +---+---+---+---+  -->  +---+---+---+---+
      2 |   |   |   |   |       |   |   |   |   |
        +---+---+---+---+       +---+---+---+---+
      3 |   |   |   |   |       |   |   |   |   |
        +---+---+---+---+       +---+---+---+---+

        cell(0, 0).merge(cell(1, 2))

    or::

          0   1   2   3   4
        +---+---+---+---+---+       +---+---+---+---+---+
      0 | a     | b | c |   |       | abcD          |   |
        + - - - +---+---+---+       + - - - - - - - +---+
      1 | ^     | D     |   |       | ^             |   |
        +---+---+---+---+---+  -->  +---+---+---+---+---+
      2 |   |   |   |   |   |       |   |   |   |   |   |
        +---+ - - - +---+---+       +---+---+---+---+---+
      3 |   |   |   |   |   |       |   |   |   |   |   |
        +---+---+---+---+---+       +---+---+---+---+---+

        cell(0, 0).merge(cell(1, 2))


    Conversely, either of these two merge operations would be illegal::

        \ 0   1   2   3   4      0   1   2   3   4
        0 +---+---+---+---+    0 +---+---+---+---+
          |   |   | b |   |      |   |   |   |   |
        1 +---+---+ - +---+    1 +---+---+---+---+
          |   | a | ^ |   |      |   | a |   |   |
        2 +---+---+ - +---+    2 +---+---+---+---+
          |   |   | ^ |   |      | b         |   |
        3 +---+---+---+---+    3 +---+---+---+---+
          |   |   |   |   |      |   |   |   |   |
        4 +---+---+---+---+    4 +---+---+---+---+

          a.merge(b)


通用算法
~~~~~~~~~~~~~~~~~

General algorithm

.. tab:: 中文

    * 找到左上角和目标宽度、高度
    * 对于目标高度中的每个 tr，tc.grow_right(target_width)

.. tab:: 英文

    * find top-left and target width, height
    * for each tr in target height, tc.grow_right(target_width)


样本 XML
------------

Specimen XML

.. tab:: 中文

    一个 3 x 3 的表格，其中由 2 x 2 左上角单元格定义的区域已合并，展示了 Word 生成的 ``w:gridSpan`` 和 ``w:vMerge`` 元素的组合使用

.. tab:: 英文

.. highlight:: xml

    A 3 x 3 table where an area defined by the 2 x 2 topleft cells has been merged, demonstrating the combined use of the ``w:gridSpan`` as well as the ``w:vMerge`` elements, as produced by Word

::

  <w:tbl>
    <w:tblPr>
       <w:tblW w:w="0" w:type="auto" />
    </w:tblPr>
    <w:tblGrid>
       <w:gridCol w:w="3192" />
       <w:gridCol w:w="3192" />
       <w:gridCol w:w="3192" />
    </w:tblGrid>
    <w:tr>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="6384" w:type="dxa" />
             <w:gridSpan w:val="2" />
             <w:vMerge w:val="restart" />
          </w:tcPr>
       </w:tc>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="3192" w:type="dxa" />
          </w:tcPr>
       </w:tc>
    </w:tr>
    <w:tr>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="6384" w:type="dxa" />
             <w:gridSpan w:val="2" />
             <w:vMerge />
          </w:tcPr>
       </w:tc>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="3192" w:type="dxa" />
          </w:tcPr>
       </w:tc>
    </w:tr>
    <w:tr>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="3192" w:type="dxa" />
          </w:tcPr>
       </w:tc>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="3192" w:type="dxa" />
          </w:tcPr>
       </w:tc>
       <w:tc>
          <w:tcPr>
             <w:tcW w:w="3192" w:type="dxa" />
          </w:tcPr>
       </w:tc>
    </w:tr>
  </w:tbl>


架构摘录
--------------

Schema excerpt

.. highlight:: xml

::

  <xsd:complexType name="CT_Tc">  <!-- denormalized -->
    <xsd:sequence>
      <xsd:element name="tcPr" type="CT_TcPr" minOccurs="0"/>
      <xsd:choice minOccurs="1" maxOccurs="unbounded">
        <xsd:element name="p"                           type="CT_P"/>
        <xsd:element name="tbl"                         type="CT_Tbl"/>
        <xsd:element name="customXml"                   type="CT_CustomXmlBlock"/>
        <xsd:element name="sdt"                         type="CT_SdtBlock"/>
        <xsd:element name="proofErr"                    type="CT_ProofErr"/>
        <xsd:element name="permStart"                   type="CT_PermStart"/>
        <xsd:element name="permEnd"                     type="CT_Perm"/>
        <xsd:element name="ins"                         type="CT_RunTrackChange"/>
        <xsd:element name="del"                         type="CT_RunTrackChange"/>
        <xsd:element name="moveFrom"                    type="CT_RunTrackChange"/>
        <xsd:element name="moveTo"                      type="CT_RunTrackChange"/>
        <xsd:element  ref="m:oMathPara"                 type="CT_OMathPara"/>
        <xsd:element  ref="m:oMath"                     type="CT_OMath"/>
        <xsd:element name="bookmarkStart"               type="CT_Bookmark"/>
        <xsd:element name="bookmarkEnd"                 type="CT_MarkupRange"/>
        <xsd:element name="moveFromRangeStart"          type="CT_MoveBookmark"/>
        <xsd:element name="moveFromRangeEnd"            type="CT_MarkupRange"/>
        <xsd:element name="moveToRangeStart"            type="CT_MoveBookmark"/>
        <xsd:element name="moveToRangeEnd"              type="CT_MarkupRange"/>
        <xsd:element name="commentRangeStart"           type="CT_MarkupRange"/>
        <xsd:element name="commentRangeEnd"             type="CT_MarkupRange"/>
        <xsd:element name="customXmlInsRangeStart"      type="CT_TrackChange"/>
        <xsd:element name="customXmlInsRangeEnd"        type="CT_Markup"/>
        <xsd:element name="customXmlDelRangeStart"      type="CT_TrackChange"/>
        <xsd:element name="customXmlDelRangeEnd"        type="CT_Markup"/>
        <xsd:element name="customXmlMoveFromRangeStart" type="CT_TrackChange"/>
        <xsd:element name="customXmlMoveFromRangeEnd"   type="CT_Markup"/>
        <xsd:element name="customXmlMoveToRangeStart"   type="CT_TrackChange"/>
        <xsd:element name="customXmlMoveToRangeEnd"     type="CT_Markup"/>
        <xsd:element name="altChunk"                    type="CT_AltChunk"/>
      </xsd:choice>
    </xsd:sequence>
    <xsd:attribute name="id" type="s:ST_String" use="optional"/>
  </xsd:complexType>

  <xsd:complexType name="CT_TcPr">  <!-- denormalized -->
    <xsd:sequence>
      <xsd:element name="cnfStyle"             type="CT_Cnf"           minOccurs="0"/>
      <xsd:element name="tcW"                  type="CT_TblWidth"      minOccurs="0"/>
      <xsd:element name="gridSpan"             type="CT_DecimalNumber" minOccurs="0"/>
      <xsd:element name="hMerge"               type="CT_HMerge"        minOccurs="0"/>
      <xsd:element name="vMerge"               type="CT_VMerge"        minOccurs="0"/>
      <xsd:element name="tcBorders"            type="CT_TcBorders"     minOccurs="0"/>
      <xsd:element name="shd"                  type="CT_Shd"           minOccurs="0"/>
      <xsd:element name="noWrap"               type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="tcMar"                type="CT_TcMar"         minOccurs="0"/>
      <xsd:element name="textDirection"        type="CT_TextDirection" minOccurs="0"/>
      <xsd:element name="tcFitText"            type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="vAlign"               type="CT_VerticalJc"    minOccurs="0"/>
      <xsd:element name="hideMark"             type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="headers"              type="CT_Headers"       minOccurs="0"/>
      <xsd:choice  minOccurs="0">
        <xsd:element name="cellIns"            type="CT_TrackChange"/>
        <xsd:element name="cellDel"            type="CT_TrackChange"/>
        <xsd:element name="cellMerge"          type="CT_CellMergeTrackChange"/>
      </xsd:choice>
      <xsd:element name="tcPrChange"           type="CT_TcPrChange"    minOccurs="0"/>
    </xsd:sequence>
  </xsd:complexType>

  <xsd:complexType name="CT_DecimalNumber">
    <xsd:attribute name="val" type="ST_DecimalNumber" use="required"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_DecimalNumber">
     <xsd:restriction base="xsd:integer"/>
  </xsd:simpleType>

  <xsd:complexType name="CT_VMerge">
    <xsd:attribute name="val" type="ST_Merge"/>
  </xsd:complexType>

  <xsd:complexType name="CT_HMerge">
    <xsd:attribute name="val" type="ST_Merge"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_Merge">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="continue"/>
      <xsd:enumeration value="restart"/>
    </xsd:restriction>
  </xsd:simpleType>


未解决的问题
-----------

Open Issues

.. tab:: 中文

    * Word 是否允许在行首“跳过”单元格（ `w:gridBefore` 元素）？规范中描述了这些，但我没有在 Word UI 中看到创建此类表格的方法。

.. tab:: 英文

    * Does Word allow "skipped" cells at the beginning of a row (`w:gridBefore` element)? These are described in the spec, but I don't see a way in the Word UI to create such a table.


资源
----------

Ressources

* `Cell.Merge Method on MSDN`_

.. _`Cell.Merge Method on MSDN`:
   http://msdn.microsoft.com/en-us/library/office/ff821310%28v=office.15%29.aspx

ISO 规范中的相关章节
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Relevant sections in the ISO Spec

* 17.4.17 gridSpan (Grid Columns Spanned by Current Table Cell)
* 17.4.84 vMerge (Vertically Merged Cell)
* 17.18.57 ST_Merge (Merged Cell Type)
