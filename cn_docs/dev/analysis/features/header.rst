.. _header:

页眉和页脚
=================

Header and Footer

.. tab:: 中文

    在 WordprocessingML 文档中，页眉是与正文分开的文本，出现在打印页面的顶部。文档中的页眉通常在各个页面之间相同，内容只有细微的差异，例如章节标题或页码。这种页眉也称为页眉。

    页脚在各个方面都与页眉类似，只是它出现在页面的底部。不要将其与脚注混淆，因为脚注在各个页面之间并不统一。为简洁起见，术语`页眉(header)` 通常在这里用于指代页眉或页脚对象，相信读者能够理解它对这两种对象类型的适用性。

    在书本印刷的文档中，页面双面打印，打开时，每页的正面或“正面(recto)”出现在装订边缘的右侧，而每页的背面或“反面(verso)”出现在左侧。第一个打印页面的页码为“1”，并且始终是正面页。由于页面是连续编号的，因此每个正面页面都会收到一个“奇数(odd)”页码，而每个反面页面都会收到一个“偶数(even)”页码。

    正面页面的页眉通常与反面页面的页眉不同。支持这种差异会导致出现一个选项，即在文档中使用与默认奇数页页眉不同的偶数页页眉。此“奇偶页眉”选项应用于文档级别，并影响文档的所有部分。

    出现在某一部分（例如章节）第一页上的页眉可能与出现在后续页面上的页眉不同。支持这种差异会导致出现一个选项，即设置不同的首页页眉。此“不同的首页页眉”选项应用于部分级别，并且可能因文档中各部分而异。

    在 WordprocessingML 中，页眉或页脚出现在页面的边距区域内。除少数例外情况外，页眉或页脚可能包含正文中可以显示的所有类型的内容，包括文本和图像。每个页眉和页脚都可以访问 ``/word/styles.xml`` 中定义的样式。

    每个部分都有自己的一组页眉和页脚，但可以将某个部分配置为从前一节“继承”页眉和页脚。每个部分可以有三个页眉定义，即默认页眉、偶数页眉和首页页眉。当未启用不同的偶数/奇数页眉时，默认页眉会出现在偶数页和奇数页上。如果启用了偶数/奇数页眉，则默认页眉用于奇数页。也可以使用相应的三个页脚定义。所有页眉/页脚定义都是可选的。

.. tab:: 英文

    In a WordprocessingML document, a page header is text that is separated from the main body of text and appears at the top of a printed page. The page headers in a document are often the same from page to page, with only small differences in content, such as a section title or page number. Such a header is also known as a running head.

    A page footer is analogous in every way to a page header except that it appears at the bottom of a page. It should not be confused with a footnote, which is not uniform between pages. For brevity's sake, the term `header` is often used here to refer to what may be either a header or footer object, trusting the reader to understand its applicability to both object types.

    In book-printed documents, where pages are printed on both sides, when opened, the front or `recto` side of each page appears to the right of the bound edge and the back or `verso` side of each page appears on the left. The first printed page receives the page-number "1", and is always a recto page. Because pages are numbered consecutively, each recto page receives an `odd` page number and each verso page receives an `even` page number.

    The header appearing on a recto page often differs from that on a verso page. Supporting this difference gives rise to the option to have an even-page header that differs from the default odd-page header in a document. This "both odd-and-even headers" option is applied at the document level and affects all sections of the document.

    The header appearing on the first page of a section (e.g. a chapter) may differ from that appearing on subsequent pages. Supporting this difference gives rise to the option to set a distinct first-page header. This "different first-page-header" option is applied at the section level and may differ from section-to-section in the document.

    In WordprocessingML, a header or footer appears within the margin area of a page. With a few exceptions, a header or footer may contain all the types of content that can appear in the main body, including text and images. Each header and footer has access to the styles defined in ``/word/styles.xml``.

    Each section has its own set of headers and footers, although a section can be configured to "inherit" headers and footers from the prior section. Each section can have three header definitions, the default header, even header, and first page header. When different even/odd headers are not enabled, the default header appears on both even and odd numbered pages. If even/odd headers are enabled, the default header is used for odd pages. A corresponding set of three footer definitions are also possible. All header/footer definitions are optional.


未解决的问题
--------------

Open Questions

.. tab:: 中文

  * 连续分节符是怎样的？那里的页眉/页脚行为是什么？

.. tab:: 英文

  * What about a continuous section break? What is the header/footer behavior there?


候选协议
------------------

Candidate Protocol

.. tab:: 中文

    每个节都有一个页眉；它永远不会是 None::

        >>> header = section.header
        >>> header
        <docx.hdrftr.Header object at 0x02468ACE>

    |Section| 具有三个页眉属性：`.header`、`.even_page_header` 和 `.first_page_header`。  
    所有页眉对象共享相同的属性和方法。此外，页脚也有三个对应的属性。

    `Header` 是 |BlockItemContainer| 的子类，继承了 |Document| 的内容编辑能力，  
    如 `.add_paragraph()` 方法。

    如果页眉没有 `w:headerReference` 元素，则该节的页眉定义会“继承”前一个节的页眉定义。  
    这种继承是递归的，例如，第一节的页眉定义可以应用到第三节。  
    继承页眉定义的页眉称为“链接到前一个”。  
    有趣的是，即使第一节没有前一个节，它的页眉仍然可以是“链接到前一个”。  
    `.is_linked_to_previous` 仅用于判断当前节是否具有页眉定义::

        >>> header.is_linked_to_previous
        True

    编辑操作会自动作用于来源页眉，即当前节缺少该类型页眉时，  
    会编辑最近的上一个节的同类型页眉。  
    如果没有任何前面的节定义了页眉，  
    那么在第一次有效编辑操作时，会在文档的第一节创建一个新的页眉::

        >>> header = document.sections[0].header
        >>> header.is_linked_to_previous
        True
        >>> header.text = 'foobar'
        >>> header.is_linked_to_previous
        False

    将 `.is_linked_to_previous` 赋值为 `False`，可以在当前节创建一个空白页眉（如果尚未存在）::

        >>> header.is_linked_to_previous
        True
        >>> header.is_linked_to_previous = False
        >>> header.is_linked_to_previous
        False

    相反，将 `.is_linked_to_previous` 赋值为 `True`，可以删除当前节的现有页眉::

        >>> header.is_linked_to_previous
        False
        >>> header.is_linked_to_previous = True
        >>> header.is_linked_to_previous
        True

    文档的 `settings` 对象具有可读写的 `.odd_and_even_pages_header_footer` 属性，  
    指示正反页（verso 和 recto）是否具有不同的页眉。  
    如果 `.odd_and_even_pages_header_footer` 为 `False`，  
    任何已存在的偶数页页眉仍然会被保留，但 Word 不会显示它们。  
    将 `.odd_and_even_pages_header_footer` 设为 `True` 并不会自动创建新的偶数页页眉::

        >>> document.settings.odd_and_even_pages_header_footer
        False
        >>> document.settings.odd_and_even_pages_header_footer = True
        >>> section.even_page_header.is_linked_to_previous
        True

    |Section| 具有可读写的 `.different_first_page_header_footer` 属性，  
    用于指示当前节的第一页是否应具有不同的页眉。  
    将 `.different_first_page_header_footer` 设为 `True` 并不会自动创建新的首页页眉::

        >>> section.different_first_page_header_footer
        False
        >>> section.different_first_page_header_footer = True
        >>> section.different_first_page_header_footer
        True
        >>> section.first_page_header.is_linked_to_previous
        True


.. tab:: 英文

    Every section has a header; it is never None::

        >>> header = section.header
        >>> header
        <docx.hdrftr.Header object at 0x02468ACE>


    There are three header properties on |Section|: `.header`, `.even_page_header`, and `.first_page_header`. All header objects share the same properties and methods. There are three corresponding properties for the footers.

    Header is a subclass of |BlockItemContainer|, from which it inherits the same content editing capabilities as |Document|, such as `.add_paragraph()`.

    If the `w:headerReference` element for a header is not present, the definition for that header is "inherited" from the prior section. This action is recursive, such that, for example, the header definition from the first section could be applied to the third section. A header that inherits its definition is said to be "linked to previous". Perhaps counterintuitively, a header for the first section can be "linked to previous", even though no previous section exists. The `.is_linked_to_previous` property is simply a test for the existence of a header definition in the current section::

        >>> header.is_linked_to_previous
        True

    Editing operations transparently operate on the source header, the one in the first prior section having a header of that type (when one is not present in the current section). If no prior sections have a header, one is created in the first section of the document on the first constructive edit call::

        >>> header = document.sections[0].header
        >>> header.is_linked_to_previous
        True
        >>> header.text = 'foobar'
        >>> header.is_linked_to_previous
        False

    Assigning False to `.is_linked_to_previous` creates a blank header for that section when one does not already exist::

        >>> header.is_linked_to_previous
        True
        >>> header.is_linked_to_previous = False
        >>> header.is_linked_to_previous
        False

    Conversely, an existing header is deleted from a section by assigning True to `.is_linked_to_previous`::

        >>> header.is_linked_to_previous
        False
        >>> header.is_linked_to_previous = True
        >>> header.is_linked_to_previous
        True

    The document settings object has a read/write `.odd_and_even_pages_header_footer` property that indicates verso and recto pages will have a different header. Any existing even page header definitions are preserved when `.odd_and_even_pages_header_footer` is False; they are simply not rendered by Word. Assigning `True` to `.odd_and_even_pages_header_footer` does not automatically create new even header definitions::

        >>> document.settings.odd_and_even_pages_header_footer
        False
        >>> document.settings.odd_and_even_pages_header_footer = True
        >>> section.even_page_header.is_linked_to_previous
        True

    `Section` has a read/write `.different_first_page_header_footer` property that indicates whether the first page of the section should have a distinct header. Assigning `True` to `.different_first_page_header_footer` does not automatically create a new first page header definition::

        >>> section.different_first_page_header_footer
        False
        >>> section.different_first_page_header_footer = True
        >>> section.different_first_page_header_footer
        True
        >>> section.first_page_header.is_linked_to_previous
        True


样本 XML
------------

Specimen XML

.. tab:: 中文

    .. highlight:: xml

    共有七种不同的页眉组合方式：

    **整篇文档使用相同的页眉**::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          ...
      </w:sectPr>

    **仅使用奇数页页眉**  
    该节的结构与上面相同，但 `settings.xml` 中包含 `<w:evenAndOddHeaders>` 属性::

      <w:settings xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
          ...
          <w:evenAndOddHeaders w:val="1"/>
          ...
      </w:settings>

    **奇偶页使用不同的页眉**::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="even" r:id="rId4"/>
          ...
      </w:sectPr>

    **首页使用不同的页眉，后续页面使用相同的页眉**::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="first" r:id="rId4"/>
          <w:titlePg/>
          ...
      </w:sectPr>

    **首页、奇数页和偶数页均使用不同的页眉**::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="first" r:id="rId4"/>
          <w:headerReference w:type="even" r:id="rId5"/>
          <w:titlePg/>
          ...
      </w:sectPr>

    **页眉部分**::

      <w:hdr>
        <w:p>
          <w:pPr>
            <w:pStyle w:val="Header"/>
          </w:pPr>
          <w:r>
            <w:t>Header for section-1</w:t>
          </w:r>
        </w:p>
      </w:hdr>

.. tab:: 英文

    .. highlight:: xml

    There are seven different permutations of headers:

    The same header on all pages of the document::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          ...
      </w:sectPr>


    Only an odd header. The section is exactly the same as above but
    `settings.xml` has the the `<w:evenAndOddHeaders>` property::

      <w:settings xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
          ...
          <w:evenAndOddHeaders w:val="1"/>
          ...
      </w:settings>

    Different even and odd headers::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="even" r:id="rId4"/>
          ...
      </w:sectPr>

    Distinct first page header, subsequent pages all have the same header::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="first" r:id="rId4"/>
          <w:titlePg/>
          ...
      </w:sectPr>

    Distinct first, even, and odd page headers::

      <w:sectPr>
          <w:headerReference w:type="default" r:id="rId3"/>
          <w:headerReference w:type="first" r:id="rId4"/>
          <w:headerReference w:type="even" r:id="rId5"/>
          <w:titlePg/>
          ...
      </w:sectPr>

    A header part::

      <w:hdr>
        <w:p>
          <w:pPr>
            <w:pStyle w:val="Header"/>
          </w:pPr>
          <w:r>
            <w:t>Header for section-1</w:t>
          </w:r>
        </w:p>
      </w:hdr>


Word 行为
-------------

Word Behavior

.. tab:: 中文

    * 当你关闭奇偶页页眉时，Word 会将 `w:evenAndOddHeaders` 的值设为 0，但不会实际删除偶数页页眉。

    * 当你关闭首页页眉时，Word 会将 `w:titlePg` 的值设为 0，但不会实际删除偶数页页眉。

    * Word 可以加载仅包含偶数页页眉但没有奇数页页眉的文件。

.. tab:: 英文

    * When you turn off even/odd headers, Word sets the value of `w:evenAndOddHeaders` to 0, but does not actually remove the even header.

    * When you turn off first page header, Word sets the value of `w:titlePg` to 0, but does not actually remove the even header.

    * Word will load a file with an even page header but no odd page header.


微软 API
----------

MS API

.. tab:: 中文

    .. highlight:: python

    WdHeaderFooterIndex 枚举::

      EVEN_PAGES = 3
      FIRST_PAGE = 2
      PRIMARY    = 1

    在 MS API 中创建页脚::

      section = Document.Sections(1)
      footers = section.Footers  # HeadersFooters 集合对象
      default_footer = footers(wdHeaderFooterPrimary)
      default_footer.Range.Text = "Footer text"

    PageSetup 对象::

      DifferentFirstPageHeaderFooter: Read/write {True, False, WD_UNDEFINED}
      OddAndEvenPagesHeaderFooter: Read/write {True, False, WD_UNDEFINED}

.. tab:: 英文

    .. highlight:: python

    WdHeaderFooterIndex Enumeration::

      EVEN_PAGES = 3
      FIRST_PAGE = 2
      PRIMARY    = 1

    Create footer in MS API::

      section = Document.Sections(1)
      footers = section.Footers  # a HeadersFooters collection object
      default_footer = footers(wdHeaderFooterPrimary)
      default_footer.Range.Text = "Footer text"

    PageSetup object::

      DifferentFirstPageHeaderFooter: Read/write {True, False, WD_UNDEFINED}
      OddAndEvenPagesHeaderFooter: Read/write {True, False, WD_UNDEFINED}


Schema 摘录
--------------

Schema Excerpt

.. code-block:: xml

    <xsd:complexType name="CT_SectPr">  <!-- denormalized -->
      <xsd:sequence>
        <xsd:choice minOccurs="0" maxOccurs="6"/>
          <xsd:element name="headerReference" type="CT_HdrFtrRef"/>
          <xsd:element name="footerReference" type="CT_HdrFtrRef"/>
        </xsd:choice>
        <xsd:element name="footnotePr"      type="CT_FtnProps"      minOccurs="0"/>
        <xsd:element name="endnotePr"       type="CT_EdnProps"      minOccurs="0"/>
        <xsd:element name="type"            type="CT_SectType"      minOccurs="0"/>
        <xsd:element name="pgSz"            type="CT_PageSz"        minOccurs="0"/>
        <xsd:element name="pgMar"           type="CT_PageMar"       minOccurs="0"/>
        <xsd:element name="paperSrc"        type="CT_PaperSource"   minOccurs="0"/>
        <xsd:element name="pgBorders"       type="CT_PageBorders"   minOccurs="0"/>
        <xsd:element name="lnNumType"       type="CT_LineNumber"    minOccurs="0"/>
        <xsd:element name="pgNumType"       type="CT_PageNumber"    minOccurs="0"/>
        <xsd:element name="cols"            type="CT_Columns"       minOccurs="0"/>
        <xsd:element name="formProt"        type="CT_OnOff"         minOccurs="0"/>
        <xsd:element name="vAlign"          type="CT_VerticalJc"    minOccurs="0"/>
        <xsd:element name="noEndnote"       type="CT_OnOff"         minOccurs="0"/>
        <xsd:element name="titlePg"         type="CT_OnOff"         minOccurs="0"/>
        <xsd:element name="textDirection"   type="CT_TextDirection" minOccurs="0"/>
        <xsd:element name="bidi"            type="CT_OnOff"         minOccurs="0"/>
        <xsd:element name="rtlGutter"       type="CT_OnOff"         minOccurs="0"/>
        <xsd:element name="docGrid"         type="CT_DocGrid"       minOccurs="0"/>
        <xsd:element name="printerSettings" type="CT_Rel"           minOccurs="0"/>
        <xsd:element name="sectPrChange"    type="CT_SectPrChange"  minOccurs="0"/>
      </xsd:sequence>
      <xsd:attribute name="rsidRPr"  type="ST_LongHexNumber"/>
      <xsd:attribute name="rsidDel"  type="ST_LongHexNumber"/>
      <xsd:attribute name="rsidR"    type="ST_LongHexNumber"/>
      <xsd:attribute name="rsidSect" type="ST_LongHexNumber"/>
    </xsd:complexType>

    <xsd:complexType name="CT_HdrFtrRef">
      <xsd:attribute ref="r:id" use="required"/>
      <xsd:attribute name="type" type="ST_HdrFtr" use="required"/>
    </xsd:complexType>

    <xsd:simpleType name="ST_HdrFtr">
      <xsd:restriction base="xsd:string">
        <xsd:enumeration value="even"/>
        <xsd:enumeration value="default"/>
        <xsd:enumeration value="first"/>
      </xsd:restriction>
    </xsd:simpleType>
