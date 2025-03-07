
制表位
=========

Tab Stops

.. tab:: 中文

    WordprocessingML 允许在段落级别自定义制表符停止位置。制表符停止位置的间距是该系统中段落格式化的一部分，因此将在 `docx.text.parfmt.ParagraphFormatting` 对象中实现。制表符停止位置将作为类似列表的 `TabStops` 对象来处理，该对象由 `TabStop` 对象组成。

    `TabStop` 对象有三个属性：对齐方式、前导符和位置。对齐方式是一个 `WD_TAB_ALIGNMENT` 成员，位置是一个 `Length()` 对象。

    制表符停止位置总是按位置顺序排序。对齐方式默认为 `WD_TAB_ALIGNMENT.LEFT`，前导符默认为 `WD_TAB_LEADER.SPACES`。

    制表符停止位置指定了段落中的制表符字符是如何呈现的。制表符字符的插入是通过使用 `Run` 对象来实现的。

.. tab:: 英文

    WordprocessingML allows for custom specification of tab stops at the paragraph level.  Tab stop spacing is a subset of paragraph formatting in this system, so will be implemented within the docx.text.parfmt.ParagraphFormatting object.  Tab stops will be handled as a List-like TabStops object made up of TabStop objects.

    A TabStop object has three properties, alignment, leader, and position. Alignment is a WD_TAB_ALIGNMENT member and position is a Length() object.

    Tab stops are always sorted in position order.  Alignment defaults to WD_TAB_ALIGNMENT.LEFT, and leader defaults to WD_TAB_LEADER.SPACES.

    Tab stops specify how tab characters in a paragraph are rendered. Insertion of tab characters is accomplished using the Run object.


协议
--------

Protocol

.. highlight:: python

.. tab:: 中文

    获取和设置制表符停止位置::

        >>> tab_stops = paragraph.paragraph_format.tab_stops
        >>> tab_stops
        <docx.text.parfmt.TabStops object at 0x104ea8c30>

        >>> tab_stop = tab_stops.add_tab_stop(Inches(2), WD_TAB_ALIGNMENT.LEFT, WD_TAB_LEADER.DOTS)

        # add_tab_stop 默认为 WD_TAB_ALIGNMENT.LEFT, WD_TAB_LEADER.SPACES

        >>> tab_stop = tab_stops.add_tab_stop(Inches(0.5))
        >>> tab_stop.alignment
        WD_TAB_ALIGNMENT.LEFT
        >>> tab_stop.leader
        WD_TAB_LEADER.SPACES

        # TabStop 属性是可读写的

        >>> tab_stop.position = Inches(2.5)
        >>> tab_stop.alignment = WD_TAB_ALIGNMENT.CENTER
        >>> tab_stop.leader = WD_TAB_LEADER.DASHES

        # 制表符停止位置按创建或修改时的位置顺序排序

        >>> [(t.position, t.alignment) for t in tab_stops]
        [(914400, WD_TAB_ALIGNMENT.LEFT), (2286000, WD_TAB_ALIGNMENT.CENTER)]

        # 使用 del 语句删除制表符停止位置

        >>> len(tab_stops)
        2
        >>> del tab_stops[1]
        >>> len(tab_stops)
        1

        # 恢复默认的制表符停止位置

        >>> tab_stops.clear()


.. tab:: 英文

    Getting and setting tab stops::

        >>> tab_stops = paragraph.paragraph_format.tab_stops
        >>> tab_stops
        <docx.text.parfmt.TabStops object at 0x104ea8c30>

        >>> tab_stop = tab_stops.add_tab_stop(Inches(2), WD_TAB_ALIGNMENT.LEFT, WD_TAB_LEADER.DOTS)

        # add_tab_stop defaults to WD_TAB_ALIGNMENT.LEFT, WD_TAB_LEADER.SPACES

        >>> tab_stop = tab_stops.add_tab_stop(Inches(0.5))
        >>> tab_stop.alignment
        WD_TAB_ALIGNMENT.LEFT
        >>> tab_stop.leader
        WD_TAB_LEADER.SPACES

        # TabStop properties are read/write

        >>> tab_stop.position = Inches(2.5)
        >>> tab_stop.alignment = WD_TAB_ALIGNMENT.CENTER
        >>> tab_stop.leader = WD_TAB_LEADER.DASHES

        # Tab stops are sorted into position order as created or modified

        >>> [(t.position, t.alignment) for t in tab_stops]
        [(914400, WD_TAB_ALIGNMENT.LEFT), (2286000, WD_TAB_ALIGNMENT.CENTER)]

        # A tab stop is deleted using del statement

        >>> len(tab_stops)
        2
        >>> del tab_stops[1]
        >>> len(tab_stops)
        1

        # Restore default tabs

        >>> tab_stops.clear()


Word 行为
-------------

Word Behavior

.. tab:: 中文

    当 w:tabs 元素为空或不存在时，Word 使用默认的制表符停止位置（通常是每半英寸一个）。

    在最后一个指定的制表符停止位置后，Word 会恢复使用默认的制表符停止位置。

    TabStops 必须在 XML 中按位置顺序排列。如果它们不是按顺序排列的，顺序错误的制表符停止位置将在标尺和属性对话框中显示，但实际上不会被 Word 使用。

.. tab:: 英文

    When the w:tabs element is empty or not present, Word uses default tab stops (typically every half inch).

    Word resumes using default tab stops following the last specified tab stop.

    TabStops must be in position order within the XML.  If they are not, the out- of-order tab stop will appear in the ruler and in the properties dialog, but will not actually be used by Word.


XML 语义
-------------

XML Semantics

.. tab:: 中文

    * "num" 和 "list" 对齐方式是早期版本的 Word 中遗留下来的，它们是在挂缩进不可用时使用的。两者都已弃用。

    * "start" 对齐方式相当于 "left"，而 "end" 对齐方式相当于 "right"。（通过手动编辑的 XML 确认。）

    * "clear" 制表符停止位置不会显示在 Word 的制表符条中，文档中将遵循默认的制表符行为。也就是说，Word 完全忽略该制表符停止位置，表现得像它根本不存在。这允许忽略从样式继承的制表符停止位置，例如。

    * w:pos 属性使用 twips，而不是 EMU。

    * 当 w:tabs 元素为空时，必须将其移除。如果存在，它必须包含至少一个 w:tab 元素。

.. tab:: 英文

    * Both "num" and "list" alignment are a legacy from early versions of Word before hanging indents were available. Both are deprecated.

    * "start" alignment is equivalent to "left", and "end" alignment are equivalent to "right". (Confirmed with manually edited XML.)

    * A "clear" tab stop is not shown in Word's tab bar and default tab behavior is followed in the document.  That is, Word ignores that tab stop specification completely, acting as if it were not there at all.  This allows a tab stop inherited from a style, for example, to be ignored.

    * The w:pos attribute uses twips rather than EMU.

    * The w:tabs element must be removed when empty. If present, it must contain at least one w:tab element.


样本 XML
------------

Specimen XML

.. highlight:: xml

::

  <w:pPr>
    <w:tabs>
      <w:tab w:val="left" w:leader="dot" w:pos="2880"/>
      <w:tab w:val="decimal" w:pos="6480"/>
    </w:tabs>
  </w:pPr>


枚举
------------

Enumerations

.. tab:: 中文

    * `MSDN 上的 WdTabAlignment 枚举`_

    =================   ========  =====
    Name                XML       Value
    =================   ========  =====
    wdAlignTabBar       bar         4
    wdAlignTabCenter    center      1
    wdAlignTabDecimal   decimal     3
    wdAlignTabLeft      left        0
    wdAlignTabList      list        6
    wdAlignTabRight     right       2
    =================   ========  =====

    WdTabAlignment 中未出现的其他枚举值:

    ===============   ========  =====
    Name              XML       Value
    ===============   ========  =====
    wdAlignTabClear   clear      101
    wdAlignTabEnd     end        102
    wdAlignTabNum     num        103
    wdAlignTabStart   start      104
    ===============   ========  =====


    * `MSDN 上的 WdTabLeader 枚举`_

    ====================   ==========  =====
    Name                   XML         Value
    ====================   ==========  =====
    wdTabLeaderDashes      hyphen        2
    wdTabLeaderDots        dot           1
    wdTabLeaderHeavy       heavy         4
    wdTabLeaderLines       underscore    3
    wdTabLeaderMiddleDot   middleDot     5
    wdTabLeaderSpaces      none          0
    ====================   ==========  =====

.. tab:: 英文

    * `WdTabAlignment Enumeration on MSDN`_

    =================   ========  =====
    Name                XML       Value
    =================   ========  =====
    wdAlignTabBar       bar         4
    wdAlignTabCenter    center      1
    wdAlignTabDecimal   decimal     3
    wdAlignTabLeft      left        0
    wdAlignTabList      list        6
    wdAlignTabRight     right       2
    =================   ========  =====

    Additional Enumeration values not appearing in WdTabAlignment

    ===============   ========  =====
    Name              XML       Value
    ===============   ========  =====
    wdAlignTabClear   clear      101
    wdAlignTabEnd     end        102
    wdAlignTabNum     num        103
    wdAlignTabStart   start      104
    ===============   ========  =====


    * `WdTabLeader Enumeration on MSDN`_

    ====================   ==========  =====
    Name                   XML         Value
    ====================   ==========  =====
    wdTabLeaderDashes      hyphen        2
    wdTabLeaderDots        dot           1
    wdTabLeaderHeavy       heavy         4
    wdTabLeaderLines       underscore    3
    wdTabLeaderMiddleDot   middleDot     5
    wdTabLeaderSpaces      none          0
    ====================   ==========  =====


.. _MSDN 上的 WdTabAlignment 枚举:
   https://msdn.microsoft.com/EN-US/library/office/ff195609.aspx

.. _MSDN 上的 WdTabLeader 枚举:
   https://msdn.microsoft.com/en-us/library/office/ff845050.aspx

.. _WdTabAlignment Enumeration on MSDN:
   https://msdn.microsoft.com/EN-US/library/office/ff195609.aspx

.. _WdTabLeader Enumeration on MSDN:
   https://msdn.microsoft.com/en-us/library/office/ff845050.aspx

MS API 协议
---------------

MS API Protocol

.. tab:: 中文

    MS API 定义了一个 `TabStops 对象`_，它是 `TabStop 对象`_ 的集合。

.. tab:: 英文

    The MS API defines a `TabStops object`_ which is a collection of `TabStop objects`_.

.. _TabStops object:
  https://msdn.microsoft.com/EN-US/library/office/ff192806.aspx

.. _TabStop objects:
   https://msdn.microsoft.com/EN-US/library/office/ff195736.aspx

.. _TabStops 对象:
  https://msdn.microsoft.com/EN-US/library/office/ff192806.aspx

.. _TabStop 对象:
   https://msdn.microsoft.com/EN-US/library/office/ff195736.aspx

Schema 摘录
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

  <xsd:complexType name="CT_Tabs">
    <xsd:sequence>
      <xsd:element name="tab" type="CT_TabStop" maxOccurs="unbounded"/>
    </xsd:sequence>
  </xsd:complexType>

  <xsd:complexType name="CT_TabStop">
    <xsd:attribute name="val"    type="ST_TabJc"              use="required"/>
    <xsd:attribute name="leader" type="ST_TabTlc"             use="optional"/>
    <xsd:attribute name="pos"    type="ST_SignedTwipsMeasure" use="required"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_TabJc">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="clear"/>
      <xsd:enumeration value="start"/>
      <xsd:enumeration value="center"/>
      <xsd:enumeration value="end"/>
      <xsd:enumeration value="decimal"/>
      <xsd:enumeration value="bar"/>
      <xsd:enumeration value="num"/>
      <xsd:enumeration value="left"/>
      <xsd:enumeration value="right"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_TabTlc">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="none"/>
      <xsd:enumeration value="dot"/>
      <xsd:enumeration value="hyphen"/>
      <xsd:enumeration value="underscore"/>
      <xsd:enumeration value="heavy"/>
      <xsd:enumeration value="middleDot"/>
    </xsd:restriction>
  </xsd:simpleType>
