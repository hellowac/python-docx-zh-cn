
段落格式
====================

Paragraph formatting

.. tab:: 中文

    WordprocessingML 支持多种段落格式属性来控制布局特征，例如对齐、缩进、行距、前后空格以及孤行控制。

.. tab:: 英文

    WordprocessingML supports a variety of paragraph formatting attributes to control layout characteristics such as justification, indentation, line spacing, space before and after, and widow/orphan control.


对齐（对齐）
-------------------------

Alignment (justification)

.. tab:: 中文

    在 Word 中，每个段落都有一个 `alignment` 属性，用于指定段落在页面上布局时如何对齐段落的行。常用值有左对齐、右对齐、居中和两端对齐。

.. tab:: 英文

    In Word, each paragraph has an `alignment` attribute that specifies how to justify the lines of the paragraph when the paragraph is laid out on the page. Common values are left, right, centered, and justified.

协议
~~~~~~~~

Protocol

.. tab:: 中文

    获取和设置段落对齐

.. tab:: 英文

    Getting and setting paragraph alignment

::

    >>> paragraph = body.add_paragraph()
    >>> paragraph.alignment
    None
    >>> paragraph.alignment = WD_ALIGN_PARAGRAPH.RIGHT
    >>> paragraph.alignment
    RIGHT (2)
    >>> paragraph.alignment = None
    >>> paragraph.alignment
    None

XML 语义
~~~~~~~~~~~~~

XML Semantics

.. tab:: 中文

    如果段落中不存在 ``<w:jc>`` 元素，则该段落的对齐方式将从其样式层次结构中继承。  
    如果该元素存在，其值将覆盖任何继承的值。  
    在 API 中，``Paragraph.alignment`` 属性的值为 |None| 时，表示该段落中不存在 ``<w:jc>`` 元素。  
    如果将 |None| 赋值给 ``Paragraph.alignment``，则 ``<w:jc>`` 元素将被移除。


.. tab:: 英文

    If the ``<w:jc>`` element is not present on a paragraph, the alignment value for that paragraph is inherited from its style hierarchy. If the element is present, its value overrides any inherited value. From the API, a value of |None| on the ``Paragraph.alignment`` property corresponds to no ``<w:jc>`` element being present. If |None| is assigned to ``Paragraph.alignment``, the ``<w:jc>`` element is removed.


段落间距
-----------------

Paragraph spacing

.. tab:: 中文

    相邻段落之间的间距由段落间距属性控制。  
    间距可以应用于段落之前、之后，或同时应用。  
    其概念类似于 CSS 中的 `padding` 或 `margin`。  

    WordprocessingML 支持以长度值或行高倍数指定段落间距；  
    然而，在 Word 用户界面中，仅支持使用长度值。  

    段落间距具有“重叠”特性，即两个段落之间的实际渲染间距为前一个段落的“段后间距”  
    和后一个段落的“段前间距”两者中的较大值。

.. tab:: 英文

    Spacing between subsequent paragraphs is controlled by the paragraph spacing attributes. Spacing can be applied either before the paragraph, after it, or both. The concept is similar to that of `padding` or `margin` in CSS. WordprocessingML supports paragraph spacing specified as either a length value or as a multiple of the line height; however only a length value is supported via the Word UI. Inter-paragraph spacing "overlaps", such that the rendered spacing between two paragraphs is the maximum of the space after the first paragraph and the space before the second.

协议
~~~~~~~~

Protocol

.. tab:: 中文

    获取和设置段落间距

.. tab:: 英文

    Getting and setting paragraph spacing

::

    >>> paragraph_format = document.styles['Normal'].paragraph_format
    >>> paragraph_format.space_before
    None
    >>> paragraph_format.space_before = Pt(12)
    >>> paragraph_format.space_before.pt
    12.0

XML 语义
~~~~~~~~~~~~~

XML Semantics

.. tab:: 中文

    * 段落间距由 `w:pPr/w:spacing` 元素指定，该元素同时控制行间距。间距以 twip（缇）为单位表示。  
    * 如果 `w:spacing` 元素不存在，则段落间距从其样式层次结构中继承。  
    * 如果样式层次结构中也未定义间距，则该段落不会应用任何间距。  
    * 如果 `w:spacing` 元素存在但某个具体属性（如 `w:before`）缺失，则该属性的值将被继承。  

.. tab:: 英文

    * Paragraph spacing is specified using the `w:pPr/w:spacing` element, which also controls line spacing. Spacing is specified in twips.
    * If the `w:spacing` element is not present, paragraph spacing is inherited from the style hierarchy.
    * If not present in the style hierarchy, the paragraph will have no spacing.
    * If the `w:spacing` element is present but the specific attribute (e.g. `w:before`) is not, its value is inherited.

样本 XML
~~~~~~~~~~~~

Specimen XML

.. tab:: 中文

    前间距为 12 pt，后间距为 0

.. tab:: 英文

    12 pt space before, 0 after

.. highlight:: xml

::

  <w:pPr>
    <w:spacing w:before="240" w:after="0"/>
  </w:pPr>


行间距
------------

Line spacing

.. tab:: 中文

    行间距可以指定为特定长度或是行高（字体大小）的倍数。行间距由 `w:spacing/@w:line` 和 `w:spacing/@w:lineRule` 的组合值决定。  
    :attr:`.ParagraphFormat.line_spacing` 属性根据赋值是否为 |Length| 实例来确定使用哪种方法。  

.. tab:: 英文

    Line spacing can be specified either as a specific length or as a multiple of the line height (font size). Line spacing is specified by the combination of values in `w:spacing/@w:line` and `w:spacing/@w:lineRule`. The :attr:`.ParagraphFormat.line_spacing` property determines which method to use based on whether the assigned value is an instance of |Length|.

协议
~~~~~~~~

Protocol

.. tab:: 中文

    获取和设置行距

.. tab:: 英文

    Getting and setting line spacing

.. highlight:: python

::

    >>> paragraph_format.line_spacing, paragraph_format.line_spacing_rule
    (None, None)

    >>> paragraph_format.line_spacing = Pt(18)
    >>> paragraph_format.line_spacing, paragraph_format.line_spacing_rule
    (228600, WD_LINE_SPACING.EXACTLY (4))

    >>> paragraph_format.line_spacing = 1
    >>> paragraph_format.line_spacing, paragraph_format.line_spacing_rule
    (152400, WD_LINE_SPACING.SINGLE (0))

    >>> paragraph_format.line_spacing = 0.9
    >>> paragraph_format.line_spacing, paragraph_format.line_spacing_rule
    (137160, WD_LINE_SPACING.MULTIPLE (5))

XML 语义
~~~~~~~~~~~~~

XML Semantics

.. tab:: 中文

    * 行间距由 `w:spacing/@w:line` 和 `w:spacing/@w:lineRule` 的组合值决定。  
    * `w:spacing/@w:line` 以 twip 为单位指定。如果 `@w:lineRule` 的值为 'auto'（或缺失），则 `@w:line` 被解释为 240 分之一行的倍数。对于 `@w:lineRule` 的其他所有值，`@w:line` 直接被解释为具体的 twip 长度。  
    * 如果 `w:spacing` 元素不存在，则行间距从样式层次结构中继承。  
    * 如果 `@w:line` 不存在，则行间距从样式层次结构中继承。  
    * 如果 `@w:lineRule` 不存在，则默认为 'auto'。  
    * 如果在样式层次结构中未指定行间距，则默认使用单倍行距。  
    * `@w:lineRule` 取 'atLeast' 值时，行间距将取 `@w:line` 指定的 twip 长度或单倍行距中较大的值。  

.. tab:: 英文

    * Line spacing is specified by the combination of the values in `w:spacing/@w:line` and `w:spacing/@w:lineRule`.
    * `w:spacing/@w:line` is specified in twips. If `@w:lineRule` is 'auto' (or missing), `@w:line` is interpreted as 240ths of a line. For all other values of `@w:lineRule`, the value of `@w:line` is interpreted as a specific length in twips.
    * If the `w:spacing` element is not present, line spacing is inherited.
    * If `@w:line` is not present, line spacing is inherited.
    * If not present, `@w:lineRule` defaults to 'auto'.
    * If not present in the style hierarchy, line spacing defaults to single spaced.
    * The 'atLeast' value for `@w:lineRule` indicates the line spacing will be `@w:line` twips or single spaced, whichever is greater.

样本 XML
~~~~~~~~~~~~

Specimen XML

.. highlight:: xml

14 points::

  <w:pPr>
    <w:spacing w:line="280"/>
  </w:pPr>

double-spaced::

  <w:pPr>
    <w:spacing w:line="480" w:lineRule="exact"/>
  </w:pPr>


缩进
-----------

Indentation

.. tab:: 中文

    段落缩进由 `w:pPr/w:ind` 元素指定。可以设置左缩进、右缩进、首行缩进和悬挂缩进。缩进可以使用长度值或字符宽度的百分之一指定。但 |docx| 仅支持长度值。首行缩进和悬挂缩进均通过 :attr:`.ParagraphFormat.first_line_indent` 属性指定。赋值为正数时，产生首行缩进；赋值为负数时，产生悬挂缩进。

.. tab:: 英文

    Paragraph indentation is specified using the `w:pPr/w:ind` element. Left, right, first line, and hanging indent can be specified. Indentation can be specified as a length or in hundredths of a character width. Only length is supported by |docx|. Both first line indent and hanging indent are specified using the :attr:`.ParagraphFormat.first_line_indent` property. Assigning a positive value produces an indented first line. A negative value produces a hanging indent.

协议
~~~~~~~~

Protocol

.. tab:: 中文

    获取和设置缩进

.. tab:: 英文

    Getting and setting indentation

.. highlight:: python

::

    >>> paragraph_format.left_indent
    None
    >>> paragraph_format.right_indent
    None
    >>> paragraph_format.first_line_indent
    None

    >>> paragraph_format.left_indent = Pt(36)
    >>> paragraph_format.left_indent.pt
    36.0

    >>> paragraph_format.right_indent = Inches(0.25)
    >>> paragraph_format.right_indent.pt
    18.0

    >>> paragraph_format.first_line_indent = Pt(-18)
    >>> paragraph_format.first_line_indent.pt
    -18.0

XML 语义
~~~~~~~~~~~~~

XML Semantics

.. tab:: 中文

    * 缩进由 `w:ind/@w:start`、`w:ind/@w:end`、`w:ind/@w:firstLine` 和 `w:ind/@w:hanging` 指定。

    * `w:firstLine` 和 `w:hanging` 互斥，如果两者都被指定，则 `w:firstLine` 将被忽略。

    * 以上四个属性的值均以 twips 为单位。

    * `w:start` 控制从左到右（LTR）段落的左缩进，或从右到左（RTL）段落的右缩进，而 `w:end` 控制另一侧的缩进。如果指定了 `mirrorIndents`，则 `w:start` 控制内侧边距，`w:end` 控制外侧边距。允许使用负值，这将导致文本超出文本边距。

    * 如果 `w:ind` 元素不存在，则缩进值将从样式层级继承。

    * 任何缺失的属性都会从样式层级继承。

    * 如果样式层级中未定义缩进值，则默认值为零。


.. tab:: 英文

    * Indentation is specified by `w:ind/@w:start`, `w:ind/@w:end`, `w:ind/@w:firstLine`, and `w:ind/@w:hanging`.

    * `w:firstLine` and `w:hanging` are mutually exclusive, if both are specified, `w:firstLine` is ignored.

    * All four attributes are specified in twips.

    * `w:start` controls left indent for a left-to-right paragraph or right indent for a right-to-left paragraph. `w:end` controls the other side. If mirrorIndents is specified, `w:start` controls the inside margin and `w:end` the outside. Negative values are permitted and cause the text to move past the text margin.

    * If `w:ind` is not present, indentation is inherited.

    * Any omitted attributes are inherited.

    * If not present in the style hierarchy, indentation values default to zero.

样本 XML
~~~~~~~~~~~~

Specimen XML

.. highlight:: xml

.. tab:: 中文

    1 英寸左缩进，0.5 英寸（额外）首行缩进，0.5 英寸右缩进::  

          <w:pPr>
            <w:ind w:start="1440" w:end="720" w:firstLine="720"/>
          </w:pPr>

    0.5 英寸左缩进，0.5 英寸悬挂缩进::  

          <w:pPr>
            <w:ind w:start="720" w:hanging="720"/>
          </w:pPr>


.. tab:: 英文

    1 inch left, 0.5 inch (additional) first line, 0.5 inch right::

      <w:pPr>
        <w:ind w:start="1440" w:end="720" w:firstLine="720"/>
      </w:pPr>

    0.5 inch left, 0.5 inch hanging indent::

      <w:pPr>
        <w:ind w:start="720" w:hanging="720"/>
      </w:pPr>


页面位置
--------------

Page placement

.. tab:: 中文

    有一些页面布局属性用于控制诸如将段落的所有行保持在同一页上、使段落（如标题）与后续段落保持在同一页上，以及将段落放置在新页顶部等行为。这些属性都是三态布尔值，其中 |None| 表示“继承”。

.. tab:: 英文

    There are a handful of page placement properties that control such things as keeping the lines of a paragraph together on the same page, keeing a paragraph (such as a heading) on the same page as the subsequent paragraph, and placing the paragraph at the top of a new page. Each of these are tri-state boolean properties where |None| indicates "inherit".

协议
~~~~~~~~

Protocol

.. tab:: 中文

    获取和设置缩进

.. tab:: 英文

    Getting and setting indentation

.. highlight:: python

::

    >>> paragraph_format.keep_with_next
    None
    >>> paragraph_format.keep_together
    None
    >>> paragraph_format.page_break_before
    None
    >>> paragraph_format.widow_control
    None

    >>> paragraph_format.keep_with_next = True
    >>> paragraph_format.keep_with_next
    True

    >>> paragraph_format.keep_together = False
    >>> paragraph_format.keep_together
    False

    >>> paragraph_format.page_break_before = True
    >>> paragraph_format.widow_control = None


XML 语义
~~~~~~~~~~~~~

XML Semantics

.. tab:: 中文

    * 所有四个元素都具有“开/关”语义。

    * 如果不存在，则它们的值将被继承。

    * 如果在样式层次结构中不存在，则值默认为 False。

.. tab:: 英文

    * All four elements have "On/Off" semantics.

    * If not present, their value is inherited.

    * If not present in the style hierarchy, values default to False.

样本 XML
~~~~~~~~~~~~

Specimen XML

.. tab:: 中文

    与下页保持同步、保持在一起、前页无分页符以及孤行控制

.. tab:: 英文

    keep with next, keep together, no page break before, and widow/orphan control

.. highlight:: xml

::

  <w:pPr>
    <w:keepNext/>
    <w:keepLines/>
    <w:pageBreakBefore w:val="0"/>
    <w:widowControl/>
  </w:pPr>


枚举
------------

Enumerations

.. tab:: 中文

.. tab:: 英文

* :ref:`WdLineSpacing`
* :ref:`WdParagraphAlignment`


样本 XML
------------

Specimen XML

.. highlight:: xml

.. tab:: 中文

  一个继承了对齐方式的段落::

      <w:p>
        <w:r>
          <w:t>继承的段落对齐方式。</w:t>
        </w:r>
      </w:p>

  一个右对齐的段落::

    <w:p>
      <w:pPr>
        <w:jc w:val="right"/>
      </w:pPr>
      <w:r>
        <w:t>右对齐的段落。</w:t>
        </w:r>
      </w:p>

.. tab:: 英文

    A paragraph with inherited alignment::

      <w:p>
        <w:r>
          <w:t>Inherited paragraph alignment.</w:t>
        </w:r>
      </w:p>

    A right-aligned paragraph::

      <w:p>
        <w:pPr>
          <w:jc w:val="right"/>
        </w:pPr>
        <w:r>
          <w:t>Right-aligned paragraph.</w:t>
        </w:r>
      </w:p>



架构摘录
--------------

Schema excerpt

.. tab:: 中文

.. tab:: 英文

::

  <xsd:complexType name="CT_PPr">  <!-- denormalized -->
    <xsd:sequence>
      <xsd:element name="pStyle"              type="CT_String"           minOccurs="0"/>
      <xsd:element name="keepNext"            type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="keepLines"           type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="pageBreakBefore"     type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="framePr"             type="CT_FramePr"          minOccurs="0"/>
      <xsd:element name="widowControl"        type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="numPr"               type="CT_NumPr"            minOccurs="0"/>
      <xsd:element name="suppressLineNumbers" type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="pBdr"                type="CT_PBdr"             minOccurs="0"/>
      <xsd:element name="shd"                 type="CT_Shd"              minOccurs="0"/>
      <xsd:element name="tabs"                type="CT_Tabs"             minOccurs="0"/>
      <xsd:element name="suppressAutoHyphens" type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="kinsoku"             type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="wordWrap"            type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="overflowPunct"       type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="topLinePunct"        type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="autoSpaceDE"         type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="autoSpaceDN"         type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="bidi"                type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="adjustRightInd"      type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="snapToGrid"          type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="spacing"             type="CT_Spacing"          minOccurs="0"/>
      <xsd:element name="ind"                 type="CT_Ind"              minOccurs="0"/>
      <xsd:element name="contextualSpacing"   type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="mirrorIndents"       type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="suppressOverlap"     type="CT_OnOff"            minOccurs="0"/>
      <xsd:element name="jc"                  type="CT_Jc"               minOccurs="0"/>
      <xsd:element name="textDirection"       type="CT_TextDirection"    minOccurs="0"/>
      <xsd:element name="textAlignment"       type="CT_TextAlignment"    minOccurs="0"/>
      <xsd:element name="textboxTightWrap"    type="CT_TextboxTightWrap" minOccurs="0"/>
      <xsd:element name="outlineLvl"          type="CT_DecimalNumber"    minOccurs="0"/>
      <xsd:element name="divId"               type="CT_DecimalNumber"    minOccurs="0"/>
      <xsd:element name="cnfStyle"            type="CT_Cnf"              minOccurs="0"/>
      <xsd:element name="rPr"                 type="CT_ParaRPr"          minOccurs="0"/>
      <xsd:element name="sectPr"              type="CT_SectPr"           minOccurs="0"/>
      <xsd:element name="pPrChange"           type="CT_PPrChange"        minOccurs="0"/>
    </xsd:sequence>
  </xsd:complexType>

  <xsd:complexType name="CT_FramePr">
    <xsd:attribute name="dropCap"    type="ST_DropCap"/>
    <xsd:attribute name="lines"      type="ST_DecimalNumber"/>
    <xsd:attribute name="w"          type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="h"          type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="vSpace"     type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="hSpace"     type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="wrap"       type="ST_Wrap"/>
    <xsd:attribute name="hAnchor"    type="ST_HAnchor"/>
    <xsd:attribute name="vAnchor"    type="ST_VAnchor"/>
    <xsd:attribute name="x"          type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="xAlign"     type="s:ST_XAlign"/>
    <xsd:attribute name="y"          type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="yAlign"     type="s:ST_YAlign"/>
    <xsd:attribute name="hRule"      type="ST_HeightRule"/>
    <xsd:attribute name="anchorLock" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_Ind">
    <xsd:attribute name="start"          type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="startChars"     type="ST_DecimalNumber"/>
    <xsd:attribute name="end"            type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="endChars"       type="ST_DecimalNumber"/>
    <xsd:attribute name="left"           type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="leftChars"      type="ST_DecimalNumber"/>
    <xsd:attribute name="right"          type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="rightChars"     type="ST_DecimalNumber"/>
    <xsd:attribute name="hanging"        type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="hangingChars"   type="ST_DecimalNumber"/>
    <xsd:attribute name="firstLine"      type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="firstLineChars" type="ST_DecimalNumber"/>
  </xsd:complexType>

  <xsd:complexType name="CT_Jc">
    <xsd:attribute name="val" type="ST_Jc" use="required"/>
  </xsd:complexType>

  <xsd:complexType name="CT_OnOff">
    <xsd:attribute name="val" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_Spacing">
    <xsd:attribute name="before"            type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="beforeLines"       type="ST_DecimalNumber"/>
    <xsd:attribute name="beforeAutospacing" type="s:ST_OnOff"/>
    <xsd:attribute name="after"             type="s:ST_TwipsMeasure"/>
    <xsd:attribute name="afterLines"        type="ST_DecimalNumber"/>
    <xsd:attribute name="afterAutospacing"  type="s:ST_OnOff"/>
    <xsd:attribute name="line"              type="ST_SignedTwipsMeasure"/>
    <xsd:attribute name="lineRule"          type="ST_LineSpacingRule"/>
  </xsd:complexType>

  <xsd:complexType name="CT_String">
    <xsd:attribute name="val" type="s:ST_String" use="required"/>
  </xsd:complexType>

  <xsd:complexType name="CT_Tabs">
    <xsd:sequence>
      <xsd:element name="tab" type="CT_TabStop" maxOccurs="unbounded"/>
    </xsd:sequence>
  </xsd:complexType>

  <!-- simple types -->

  <xsd:simpleType name="ST_Jc">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="start"/>
      <xsd:enumeration value="center"/>
      <xsd:enumeration value="end"/>
      <xsd:enumeration value="both"/>
      <xsd:enumeration value="mediumKashida"/>
      <xsd:enumeration value="distribute"/>
      <xsd:enumeration value="numTab"/>
      <xsd:enumeration value="highKashida"/>
      <xsd:enumeration value="lowKashida"/>
      <xsd:enumeration value="thaiDistribute"/>
      <xsd:enumeration value="left"/>
      <xsd:enumeration value="right"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_LineSpacingRule">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="auto"/>  <!-- default -->
      <xsd:enumeration value="exact"/>
      <xsd:enumeration value="atLeast"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff">
    <xsd:union memberTypes="xsd:boolean ST_OnOff1"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff1">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="on"/>
      <xsd:enumeration value="off"/>
    </xsd:restriction>
  </xsd:simpleType>
