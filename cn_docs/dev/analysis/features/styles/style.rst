
样式对象
=============

Style objects

.. tab:: 中文

    样式有四种类型：字符、段落、表格或编号。

    所有样式对象都具有行为属性和格式属性。格式属性集因样式类型而异。一般来说，格式属性会沿着以下层次结构继承：字符 -> 段落 -> 表格。编号样式没有格式属性，也不会继承。

.. tab:: 英文

    A style is one of four types; character, paragraph, table, or numbering. All
    style objects have behavioral properties and formatting properties. The set of
    formatting properties varies depending on the style type. In general,
    formatting properties are inherited along this hierarchy: character ->
    paragraph -> table. A numbering style has no formatting properties and does
    not inherit.

行为协议
---------------------

Behavioral properties

.. tab:: 中文

    有六种行为属性：

    hidden
        样式用于分配格式属性，但在任何情况下都不会出现在 UI 中。用于由应用程序分配的“内部”样式，这些样式不应受最终用户的控制。

    priority
        确定样式在 UI 呈现的序列中的排序顺序。

    semi-hidden
        样式在所谓的“主”用户界面中隐藏。在 Word 中，这意味着 *推荐列表* 和样式库。样式仍然出现在 *所有样式* 列表中。

    unhide_when_used
        标记应用程序在下次使用样式时将 semi-hidden 设置为 False。

    quick_style
        当样式未隐藏时，在样式库中显示样式。

    closed
        文档格式保护处于活动状态时，样式被隐藏且无法应用。

.. tab:: 英文

    There are six behavior properties:

    hidden
        Style operates to assign formatting properties, but does not appear in
        the UI under any circumstances. Used for `internal` styles assigned by an
        application that should not be under the control of an end-user.

    priority
        Determines the sort order of the style in sequences presented by the UI.

    semi-hidden
        The style is hidden from the so-called "main" user interface. In Word
        this means the *recommended list* and the style gallery. The style still
        appears in the *all styles* list.

    unhide_when_used
        Flag to the application to set semi-hidden False when the style is next
        used.

    quick_style
        Show the style in the style gallery when it is not hidden.

    locked
        Style is hidden and cannot be applied when document formatting protection
        is active.


隐藏
------

hidden

.. tab:: 中文

    `hidden` 属性不适用于内置样式，其在自定义样式上的行为也不稳定。暂时跳过此属性。如果有人要求并提供具体用例，我会重新考虑。

.. tab:: 英文

    The `hidden` attribute doesn't work on built-in styles and its behavior on
    custom styles is spotty. Skipping this attribute for now. Will reconsider if
    someone requests it and can provide a specific use case.

行为
~~~~~~~~

Behavior

.. tab:: 中文

    **范围。** `hidden` 在“普通”或“标题 1”样式上根本不起作用。

    它也不适用于称呼。 `w:latentStyles` 上没有 `w:defHidden` 属性，这证实了它未对内置样式启用的假设。*假设：*不适用于内置样式。

    **UI 行为。** 将 `w:hidden` 设置为 |True| 的自定义样式在库和所有样式窗格列表中隐藏。但是，当光标位于该样式的段落上时，它会出现在样式窗格中的“所选文本的当前样式”框中。用户可以从此当前样式 UI 元素修改样式。用户可以为具有隐藏样式的段落分配新样式。

.. tab:: 英文

    **Scope.** `hidden` doesn't work at all on 'Normal' or 'Heading 1' style. It
    doesn't work on Salutation either. There is no `w:defHidden` attribute on
    `w:latentStyles`, lending credence to the hypothesis it is not enabled for
    built-in styles. *Hypothesis:* Doesn't work on built-in styles.

    **UI behavior.** A custom style having `w:hidden` set |True| is hidden from
    the gallery and all styles pane lists. It does however appear in the "Current
    style of selected text" box in the styles pane when the cursor is on
    a paragraph of that style. The style can be modified by the user from this
    current style UI element. The user can assign a new style to a paragraph
    having a hidden style.


权重
--------

priority

.. tab:: 中文

    `priority` 属性是整数主排序键，用于确定样式在 UI 列表中的位置。次要排序按名称字母顺序进行。 负值有效，但不是 Word 本身分配的，并且似乎被视为 0。

.. tab:: 英文

    The `priority` attribute is the integer primary sort key determining the
    position of a style in a UI list. The secondary sort is alphabetical by name.
    Negative values are valid, although not assigned by Word itself and appear to
    be treated as 0.

行为
~~~~~~~~

Behavior

.. tab:: 中文
    
    **默认。** Word behavior 似乎将自定义样式的优先级默认为 0。规范表明，有效默认值在概念上是无穷大，因此样式出现在样式列表的末尾，大概是按字母顺序排列在其他未分配优先级的样式中。

.. tab:: 英文

    **Default.** Word behavior appears to default priority to 0 for custom
    styles. The spec indicates the effective default value is conceptually
    infinity, such that the style appears at the end of the styles list,
    presumably alphabetically among other styles having no priority assigned.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

::

    >>> style = document.styles['Foobar']
    >>> style.priority
    None
    >>> style.priority = 7
    >>> style.priority
    7
    >>> style.priority = -42
    >>> style.priority
    0


semi-hidden
-----------

semi-hidden

.. tab:: 中文

    `w:semiHidden` 元素指定样式在所谓的 `main` 用户界面中的可见性。对于 Word，这意味着样式库和
    推荐的、正在使用的样式和当前文档中的列表。样式窗格中的全部样式 列表和当前样式下拉列表将被视为 `advanced` 用户界面的一部分。

.. tab:: 英文

    The `w:semiHidden` element specifies visibility of the style in the so-called
    `main` user interface. For Word, this means the style gallery and the
    recommended, styles-in-use, and in-current-document lists. The all-styles
    list and current-style dropdown in the styles pane would then be considered
    part of an `advanced` user interface.

行为
~~~~~~~~

Behavior

.. tab:: 中文

    **Default.** 如果省略 `w:semiHidden` 元素，则其有效值为 |False|。此值没有继承。

    **Scope.** 适用于内置样式和自定义样式。

    **Word 行为。** Word 不使用 `@w:val` 属性。它为 |True| 写入 `<w:semiHidden/>`，并为 |False| 省略元素。

.. tab:: 英文

    **Default.** If the `w:semiHidden` element is omitted, its effective value is |False|. There is no inheritance of this value.

    **Scope.** Works on both built-in and custom styles.

    **Word behavior.** Word does not use the `@w:val` attribute. It writes `<w:semiHidden/>` for |True| and omits the element for |False|.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

::

    >>> style = document.styles['Foo']
    >>> style.hidden
    False
    >>> style.hidden = True
    >>> style.hidden
    True

XML 例子
~~~~~~~~~~~

Example XML

.. highlight:: xml

style.hidden = True::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:semiHidden/>
  </w:style>

style.hidden = False::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
  </w:style>

Alternate constructions should also report the proper value but not be
used when writing XML::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:semiHidden w:val="0"/>  <!-- style.hidden is False -->
  </w:style>

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:semiHidden w:val="1"/>  <!-- style.hidden is True -->
  </w:style>


使用未隐藏样式
----------------

unhide-when-used

.. tab:: 中文

    `w:unhideWhenUsed` 元素向应用程序发出信号，表示下次使用时该样式应该可见。

.. tab:: 英文

    The `w:unhideWhenUsed` element signals an application that this style should be made visibile the next time it is used.

行为
~~~~~~~~

Behavior
.. tab:: 中文

    **Default.** 如果省略 `w:unhideWhenUsed` 元素，则其有效值为 |False|。此值不继承。

    **Word 行为。** 下次使用样式时， `w:unhideWhenUsed` 元素不会更改或删除。只有 `w:semiHidden` 元素（如果存在）会受到影响。据推测，这样样式就可以重新隐藏，并在后续使用时取消隐藏。

    请注意，Word 中的此行为仅由用户实际应用样式触发。仅加载在其内容中某处应用了样式的文档不会导致 `w:semiHidden` 元素被删除。

.. tab:: 英文

    **Default.** If the `w:unhideWhenUsed` element is omitted, its effective value is |False|. There is no inheritance of this value.

    **Word behavior.** The `w:unhideWhenUsed` element is not changed or removed when the style is next used. Only the `w:semiHidden` element is affected, if present. Presumably this is so a style can be re-hidden, to be unhidden on the subsequent use.

    Note that this behavior in Word is only triggered by a user actually applying a style. Merely loading a document having the style applied somewhere in its contents does not cause the `w:semiHidden` element to be removed.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

.. highlight:: python

::

    >>> style = document.styles['Foo']
    >>> style.unhide_when_used
    False
    >>> style.unhide_when_used = True
    >>> style.unhide_when_used
    True

XML 例子
~~~~~~~~~~~

Example XML

.. highlight:: xml

style.unhide_when_used = True::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:semiHidden/>
    <w:unhideWhenUsed/>
  </w:style>

style.unhide_when_used = False::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
  </w:style>

Alternate constructions should also report the proper value but not be
used when writing XML::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:unhideWhenUsed w:val="0"/>  <!-- style.unhide_when_used is False -->
  </w:style>

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:unhideWhenUsed w:val="1"/>  <!-- style.unhide_when_used is True -->
  </w:style>


快速样式
-----------

quick-style

.. tab:: 中文

    `w:qFormat` 元素指定 Word 是否应在样式库中显示此样式。为了显示在样式库中，此属性必须为 |True|，并且 `hidden` 必须为 |False|。

.. tab:: 英文

    The `w:qFormat` element specifies whether Word should display this style in the style gallery. In order to appear in the gallery, this attribute must be |True| and `hidden` must be |False|.

行为
~~~~~~~~

Behavior

.. tab:: 中文

    **默认。** 如果省略 `w:qFormat` 元素，则其有效值为 |False|。此值没有继承。

    **Word 行为。** 如果 `w:qFormat` 为 |True| 且样式未隐藏，则它将按照 `w:uiPriority` 指定的顺序出现在图库中。

.. tab:: 英文

    **Default.** If the `w:qFormat` element is omitted, its effective value is |False|. There is no inheritance of this value.

    **Word behavior.** If `w:qFormat` is |True| and the style is not hidden, it will appear in the gallery in the order specified by `w:uiPriority`.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

.. highlight:: python

::

    >>> style = document.styles['Foo']
    >>> style.quick_style
    False
    >>> style.quick_style = True
    >>> style.quick_style
    True

XML 例子
~~~~~~~~~~~

Example XML

.. highlight:: xml

style.quick_style = True::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:qFormat/>
  </w:style>

style.quick_style = False::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
  </w:style>

Alternate constructions should also report the proper value but not be
used when writing XML::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:qFormat w:val="0"/>  <!-- style.quick_style is False -->
  </w:style>

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:qFormat w:val="1"/>  <!-- style.quick_style is True -->
  </w:style>


锁定
------

locked

.. tab:: 中文

    `w:locked` 元素指定 Word 是否应阻止将此样式应用于内容。此行为仅在打开格式保护时才会激活。

.. tab:: 英文

    The `w:locked` element specifies whether Word should prevent this style from being applied to content. This behavior is only active if formatting protection is turned on.

行为
~~~~~~~~

Behavior

.. tab:: 中文

    **默认。** 如果省略 `w:locked` 元素，其有效值为 |False|。此值没有继承。

.. tab:: 英文

    **Default.** If the `w:locked` element is omitted, its effective value is |False|. There is no inheritance of this value.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

.. highlight:: python

::

    >>> style = document.styles['Foo']
    >>> style.locked
    False
    >>> style.locked = True
    >>> style.locked
    True

XML 例子
~~~~~~~~~~~

Example XML

.. highlight:: xml

style.locked = True::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:locked/>
  </w:style>

style.locked = False::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
  </w:style>

Alternate constructions should also report the proper value but not be
used when writing XML::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:locked w:val="0"/>  <!-- style.locked is False -->
  </w:style>

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:locked w:val="1"/>  <!-- style.locked is True -->
  </w:style>


候选协议
-------------------

Candidate protocols

.. highlight:: python

Identification::

    >>> style = document.styles['Body Text']
    >>> style.name
    'Body Text'
    >>> style.style_id
    'BodyText'
    >>> style.type
    WD_STYLE_TYPE.PARAGRAPH (1)

`delete()`::

    >>> len(styles)
    6
    >>> style.delete()
    >>> len(styles)
    5
    >>> styles['Citation']
    KeyError: no style with id or name 'Citation'

Style.base_style::

    >>> style = styles.add_style('Citation', WD_STYLE_TYPE.PARAGRAPH)
    >>> style.base_style
    None
    >>> style.base_style = styles['Normal']
    >>> style.base_style
    <docx.styles.style._ParagraphStyle object at 0x10a7a9550>
    >>> style.base_style.name
    'Normal'


XML 例子
-----------

Example XML

.. highlight:: xml

::

  <w:styles>

    <!-- ... -->

    <w:style w:type="paragraph" w:default="1" w:styleId="Normal">
      <w:name w:val="Normal"/>
      <w:qFormat/>
    </w:style>
    <w:style w:type="character" w:default="1" w:styleId="DefaultParagraphFont">
      <w:name w:val="Default Paragraph Font"/>
      <w:uiPriority w:val="1"/>
      <w:semiHidden/>
      <w:unhideWhenUsed/>
    </w:style>
    <w:style w:type="table" w:default="1" w:styleId="TableNormal">
      <w:name w:val="Normal Table"/>
      <w:uiPriority w:val="99"/>
      <w:semiHidden/>
      <w:unhideWhenUsed/>
      <w:tblPr>
        <w:tblInd w:w="0" w:type="dxa"/>
        <w:tblCellMar>
          <w:top w:w="0" w:type="dxa"/>
          <w:left w:w="108" w:type="dxa"/>
          <w:bottom w:w="0" w:type="dxa"/>
          <w:right w:w="108" w:type="dxa"/>
        </w:tblCellMar>
      </w:tblPr>
    </w:style>
    <w:style w:type="numbering" w:default="1" w:styleId="NoList">
      <w:name w:val="No List"/>
      <w:uiPriority w:val="99"/>
      <w:semiHidden/>
      <w:unhideWhenUsed/>
    </w:style>

    <w:style w:type="paragraph" w:customStyle="1" w:styleId="Foobar">
      <w:name w:val="Foobar"/>
      <w:basedOn w:val="Normal"/>
      <w:qFormat/>
    </w:style>

  </w:styles>


Schema 摘录
--------------

Schema excerpt

::

  <xsd:complexType name="CT_Style">
    <xsd:sequence>
      <xsd:element name="name"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="aliases"         type="CT_String"        minOccurs="0"/>
      <xsd:element name="basedOn"         type="CT_String"        minOccurs="0"/>
      <xsd:element name="next"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="link"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="autoRedefine"    type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="hidden"          type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="uiPriority"      type="CT_DecimalNumber" minOccurs="0"/>
      <xsd:element name="semiHidden"      type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="unhideWhenUsed"  type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="qFormat"         type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="locked"          type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personal"        type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personalCompose" type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personalReply"   type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="rsid"            type="CT_LongHexNumber" minOccurs="0"/>
      <xsd:element name="pPr"             type="CT_PPrGeneral"    minOccurs="0"/>
      <xsd:element name="rPr"             type="CT_RPr"           minOccurs="0"/>
      <xsd:element name="tblPr"           type="CT_TblPrBase"     minOccurs="0"/>
      <xsd:element name="trPr"            type="CT_TrPr"          minOccurs="0"/>
      <xsd:element name="tcPr"            type="CT_TcPr"          minOccurs="0"/>
      <xsd:element name="tblStylePr"      type="CT_TblStylePr"    minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="type"        type="ST_StyleType"/>
    <xsd:attribute name="styleId"     type="s:ST_String"/>
    <xsd:attribute name="default"     type="s:ST_OnOff"/>
    <xsd:attribute name="customStyle" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_OnOff">
    <xsd:attribute name="val" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_String">
    <xsd:attribute name="val" type="s:ST_String" use="required"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_OnOff">
    <xsd:union memberTypes="xsd:boolean ST_OnOff1"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff1">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="on"/>
      <xsd:enumeration value="off"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_StyleType">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="paragraph"/>
      <xsd:enumeration value="character"/>
      <xsd:enumeration value="table"/>
      <xsd:enumeration value="numbering"/>
    </xsd:restriction>
  </xsd:simpleType>
