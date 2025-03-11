
中断
======

Breaks

.. tab:: 中文

    Word 支持多种中断文档中文本流动的分隔符：

    * 换行符
    * 分页符
    * 列分隔符
    * 节分隔符（新页面、偶数页、奇数页）

    此外，可以通过将段落设置为“分页前”来强制分页。

    本分析仅限于换行符、分页符和列分隔符。节分隔符使用完全不同的一组元素实现，单独进行说明。

.. tab:: 英文

    Word supports a variety of breaks that interrupt the flow of text in the
    document:

    * line break
    * page break
    * column break
    * section break (new page, even page, odd page)

    In addition, a page break can be forced by formatting a paragraph with the
    "page break before" setting.

    This analysis is limited to line, page, and column breaks. A section break is
    implemented using a completely different set of elements and is covered
    separately.


候选协议 -- run.add_break()
-------------------------------------

Candidate protocol -- run.add_break()

.. tab:: 中文

    以下交互式会话演示了添加分页符的协议

.. tab:: 英文

    The following interactive session demonstrates the protocol for adding a page break

::

    >>> run = p.add_run()
    >>> run.breaks
    []

    >>> run.add_break()  # by default adds WD_BREAK.LINE
    >>> run.breaks
    [<docx.text.Break object at 0x10a7c4f50>]
    >>> run.breaks[0].type.__name__
    WD_BREAK.LINE

    >>> run.add_break(WD_BREAK.LINE)
    >>> run.breaks
    [<docx.text.Break object at 0x10a7c4f50>, <docx.text.Break object at 0x10a7c4f58>]

    >>> run.add_break(WD_BREAK.PAGE)
    >>> run.add_break(WD_BREAK.COLUMN)
    >>> run.add_break(WD_BREAK.LINE_CLEAR_LEFT)
    >>> run.add_break(WD_BREAK.LINE_CLEAR_RIGHT)
    >>> run.add_break(WD_BREAK.TEXT_WRAPPING)


枚举 -- WD_BREAK_TYPE
----------------------------

Enumeration -- WD_BREAK_TYPE

* WD_BREAK.LINE
* WD_BREAK.LINE_CLEAR_LEFT
* WD_BREAK.LINE_CLEAR_RIGHT
* WD_BREAK.TEXT_WRAPPING (e.g. LINE_CLEAR_ALL)

* WD_BREAK.PAGE

* WD_BREAK.COLUMN

* WD_BREAK.SECTION_NEXT_PAGE
* WD_BREAK.SECTION_CONTINUOUS
* WD_BREAK.SECTION_EVEN_PAGE
* WD_BREAK.SECTION_ODD_PAGE


样本 XML
------------

Specimen XML

.. highlight:: xml


换行符
~~~~~~~~~~

Line break

.. tab:: 中文

    以下 XML 是 Word 在使用 Shift-Enter 插入换行符后生成的::

      <w:p>
        <w:r>
          <w:t>Text before</w:t>
        </w:r>
        <w:r>
          <w:br/>
          <w:t>and after line break</w:t>
        </w:r>
      </w:p>

    Word 可以正常加载这种更直接的生成方式，尽管它在下次保存时会将其更改。我不确定创建一个新的 run，使得 ``<w:br/>`` 元素成为第一个子元素的优势何在::

      <w:p>
        <w:r>
          <w:t>Text before</w:t>
          <w:br/>
          <w:t>and after line break</w:t>
        </w:r>
      </w:p>

.. tab:: 英文

    This XML is produced by Word after inserting a line feed with Shift-Enter::

        <w:p>
          <w:r>
            <w:t>Text before</w:t>
          </w:r>
          <w:r>
            <w:br/>
            <w:t>and after line break</w:t>
          </w:r>
        </w:p>

    Word loads this more straightforward generation just fine, although it changes
    it back on next save. I'm not sure of the advantage in creating a fresh run
    such that the ``<w:br/>`` element is the first child::

        <w:p>
          <w:r>
            <w:t>Text before</w:t>
            <w:br/>
            <w:t>and after line break</w:t>
          </w:r>
        </w:p>


分页符
~~~~~~~~~~

Page break

.. tab:: 中文

    从这个 XML 开始... ::

        <w:p>
          <w:r>
            <w:t>Before inserting a page break, the cursor was here }</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>This was the following paragraph, the last in the document</w:t>
          </w:r>
        </w:p>

    ... 这是 Word 在插入硬分页时生成的 XML::

        <w:p>
          <w:r>
            <w:t>Before inserting a page break, the cursor was here }</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:br w:type="page"/>
          </w:r>
        </w:p>
        <w:p>
          <w:bookmarkStart w:id="0" w:name="_GoBack"/>
          <w:bookmarkEnd w:id="0"/>
        </w:p>
        <w:p>
          <w:r>
            <w:t>This was the following paragraph, the last in the document</w:t>
          </w:r>
        </w:p>

    Word 可以正常加载以下简化形式... ::

        <w:p>
          <w:r>
            <w:t>Text before an intra-run page break</w:t>
            <w:br w:type="page"/>
            <w:t>Text after an intra-run page break</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>following paragraph</w:t>
          </w:r>
        </w:p>

    ... 然而在保存时，它会将其转换为以下形式::

        <w:p>
          <w:r>
            <w:t>Text before an intra-run page break</w:t>
          </w:r>
          <w:r>
            <w:br w:type="page"/>
          </w:r>
          <w:r>
            <w:lastRenderedPageBreak/>
            <w:t>Text after an intra-run page break</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>following paragraph</w:t>
          </w:r>
        </w:p>

.. tab:: 英文

    Starting with this XML ... ::

        <w:p>
          <w:r>
            <w:t>Before inserting a page break, the cursor was here }</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>This was the following paragraph, the last in the document</w:t>
          </w:r>
        </w:p>


    ... this XML is produced by Word on inserting a hard page::

        <w:p>
          <w:r>
            <w:t>Before inserting a page break, the cursor was here }</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:br w:type="page"/>
          </w:r>
        </w:p>
        <w:p>
          <w:bookmarkStart w:id="0" w:name="_GoBack"/>
          <w:bookmarkEnd w:id="0"/>
        </w:p>
        <w:p>
          <w:r>
            <w:t>This was the following paragraph, the last in the document</w:t>
          </w:r>
        </w:p>

    Word loads the following simplified form fine ... ::

        <w:p>
          <w:r>
            <w:t>Text before an intra-run page break</w:t>
            <w:br w:type="page"/>
            <w:t>Text after an intra-run page break</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>following paragraph</w:t>
          </w:r>
        </w:p>

    ... although on saving it converts it to this::

        <w:p>
          <w:r>
            <w:t>Text before an intra-run page break</w:t>
          </w:r>
          <w:r>
            <w:br w:type="page"/>
          </w:r>
          <w:r>
            <w:lastRenderedPageBreak/>
            <w:t>Text after an intra-run page break</w:t>
          </w:r>
        </w:p>
        <w:p>
          <w:r>
            <w:t>following paragraph</w:t>
          </w:r>
        </w:p>


架构摘录
--------------

Schema excerpt

.. highlight:: xml

::

  <xsd:complexType name="CT_R">
    <xsd:sequence>
      <xsd:group ref="EG_RPr"             minOccurs="0"/>
      <xsd:group ref="EG_RunInnerContent" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="rsidRPr" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidDel" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidR"   type="ST_LongHexNumber"/>
  </xsd:complexType>

  <xsd:group name="EG_RunInnerContent">
    <xsd:choice>
      <xsd:element name="br"                    type="CT_Br"/>
      <xsd:element name="t"                     type="CT_Text"/>
      <xsd:element name="contentPart"           type="CT_Rel"/>
      <xsd:element name="delText"               type="CT_Text"/>
      <xsd:element name="instrText"             type="CT_Text"/>
      <xsd:element name="delInstrText"          type="CT_Text"/>
      <xsd:element name="noBreakHyphen"         type="CT_Empty"/>
      <xsd:element name="softHyphen"            type="CT_Empty"/>
      <xsd:element name="dayShort"              type="CT_Empty"/>
      <xsd:element name="monthShort"            type="CT_Empty"/>
      <xsd:element name="yearShort"             type="CT_Empty"/>
      <xsd:element name="dayLong"               type="CT_Empty"/>
      <xsd:element name="monthLong"             type="CT_Empty"/>
      <xsd:element name="yearLong"              type="CT_Empty"/>
      <xsd:element name="annotationRef"         type="CT_Empty"/>
      <xsd:element name="footnoteRef"           type="CT_Empty"/>
      <xsd:element name="endnoteRef"            type="CT_Empty"/>
      <xsd:element name="separator"             type="CT_Empty"/>
      <xsd:element name="continuationSeparator" type="CT_Empty"/>
      <xsd:element name="sym"                   type="CT_Sym"/>
      <xsd:element name="pgNum"                 type="CT_Empty"/>
      <xsd:element name="cr"                    type="CT_Empty"/>
      <xsd:element name="tab"                   type="CT_Empty"/>
      <xsd:element name="object"                type="CT_Object"/>
      <xsd:element name="pict"                  type="CT_Picture"/>
      <xsd:element name="fldChar"               type="CT_FldChar"/>
      <xsd:element name="ruby"                  type="CT_Ruby"/>
      <xsd:element name="footnoteReference"     type="CT_FtnEdnRef"/>
      <xsd:element name="endnoteReference"      type="CT_FtnEdnRef"/>
      <xsd:element name="commentReference"      type="CT_Markup"/>
      <xsd:element name="drawing"               type="CT_Drawing"/>
      <xsd:element name="ptab"                  type="CT_PTab"/>
      <xsd:element name="lastRenderedPageBreak" type="CT_Empty"/>
    </xsd:choice>
  </xsd:group>

  <xsd:complexType name="CT_Br">
    <xsd:attribute name="type"  type="ST_BrType"/>
    <xsd:attribute name="clear" type="ST_BrClear"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_BrType">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="page"/>
      <xsd:enumeration value="column"/>
      <xsd:enumeration value="textWrapping"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_BrClear">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="none"/>
      <xsd:enumeration value="left"/>
      <xsd:enumeration value="right"/>
      <xsd:enumeration value="all"/>
    </xsd:restriction>
  </xsd:simpleType>


资源
---------

Resources

* `WdBreakType Enumeration on MSDN`_
* `Range.InsertBreak Method (Word) on MSDN`_

.. _WdBreakType Enumeration on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff195905.aspx

.. _Range.InsertBreak Method (Word) on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff835132.aspx


ISO 规范中的相关部分
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Relevant sections in the ISO Spec

* 17.18.3 ST_BrClear (Line Break Text Wrapping Restart Location)
