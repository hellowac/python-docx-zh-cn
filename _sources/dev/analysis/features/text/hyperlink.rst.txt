
超链接
=========

Hyperlink

.. tab:: 中文

    Word 允许在文档中任何段落可以出现的地方插入超链接。  
    实际的超链接元素与 |Run| 处于同一级别。

    超链接可以指向外部资源（例如网站），  
    也可以是内部链接，指向文档中的另一个位置。  
    此外，超链接还可以是 `mailto:` URI，  
    或者指向可访问的本地文件或网络文件系统中的文件。

    超链接的可见文本存储在一个或多个 `run` 中。  
    从技术上讲，超链接可以包含零个 `run`，  
    但这种情况仅在特定构造的案例中才会发生  
    （否则将没有可点击的内容）。  
    与普通文本一样，每个 `run` 可以有自己独立的文本格式（字体）。  
    例如，超链接中的某个单词可以加粗等。  
    默认情况下，Word 会对新插入的超链接应用内置的 `Hyperlink` 字符样式。  
    与其他文本一样，由于在不同的“修订保存”编辑会话  
    （即多次执行 "Save" 命令）中进行的修改，  
    超链接文本可能会被拆分成多个 `run`。

    请注意，超链接中间可能会出现分页符。

    |Hyperlink| 是 |Paragraph| 的子元素，与 |Run| 处于同一级别。

    TODO: 需要确认 URL 编码/解码（如 %20）在超链接中的处理方式（如果有）。

.. tab:: 英文

    Word allows a hyperlink to be placed in a document wherever a paragraph can appear. The actual hyperlink element is a peer of |Run|.

    The link may be to an external resource such as a web site, or internal, to another location in the document. The link may also be a `mailto:` URI or a reference to a file on an accessible local or network filesystem.

    The visible text of a hyperlink is held in one or more runs. Technically a hyperlink can have zero runs, but this occurs only in contrived cases (otherwise there would be nothing to click on). As usual, each run can have its own distinct text formatting (font), so for example one word in the hyperlink can be bold, etc. By default, Word applies the built-in `Hyperlink` character style to a newly inserted hyperlink. Like other text, the hyperlink text may often be broken into multiple runs as a result of edits in different "revision-save" editing sessions (between "Save" commands).

    Note that rendered page-breaks can occur in the middle of a hyperlink.

    A |Hyperlink| is a child of |Paragraph|, a peer of |Run|.


    TODO: What about URL-encoding/decoding (like %20) behaviors, if any?


候选协议
------------------

Candidate protocol

.. tab:: 中文

    外部超链接具有一个地址（address）和一个可选的锚点（anchor）。  
    内部超链接仅包含一个锚点。  
    锚点在 Web URL 中更准确地称为 *URI 片段*，  
    并且位于井号（"#"）之后。  
    XML 中不存储片段分隔符 "#" 字符。

    请注意，锚点和地址存储在两个不同的属性中，  
    因此，如果要获取完整的超链接，  
    需要将 `.address` 和 `.anchor` 连接起来，  
    例如：`f"{address}#{anchor}"`。

    此外，Word 并不会严格区分 Web URI 中的片段，  
    因此，它可能作为地址的一部分存储，  
    或者单独存储在 `anchor` 属性中，  
    具体情况取决于超链接的创建方式。  
    根据我的有限经验，  
    通过对话框插入的超链接会分离片段，  
    而直接在文档中输入的地址则不会。

    .. highlight:: python

    **访问段落中的超链接**::

        >>> hyperlinks = paragraph.hyperlinks
        [<docx.text.hyperlink.Hyperlink at 0x7f...>]

    **按文档顺序访问段落中的超链接和 `run`**::

        >>> list(paragraph.iter_inner_content())
        [
          <docx.text.run.Run at 0x7f...>
          <docx.text.hyperlink.Hyperlink at 0x7f...>
          <docx.text.run.Run at 0x7f...>
        ]

    **访问超链接地址**::

        >>> hyperlink.address
        'https://google.com/'

    **访问超链接片段**::

        >>> hyperlink.fragment
        'introduction'

    **访问超链接历史记录（是否已访问，`True` 表示尚未访问）**::

        >>> hyperlink.history
        True

    **访问超链接中的 `run`**::

        >>> hyperlink.runs
        [
          <docx.text.run.Run at 0x7f...>
          <docx.text.run.Run at 0x7f...>
          <docx.text.run.Run at 0x7f...>
        ]

    **访问完整的超链接 URL**::

        >>> hyperlink.url
        'https://us.com#introduction'

    **判断超链接是否包含分页符**::

        >>> hyperlink.contains_page_break
        False

    **访问超链接的可见文本**::

        >>> hyperlink.text
        'an excellent Wikipedia article on ferrets'

    **添加外部超链接** （尚未实现）::

        >>> hyperlink = paragraph.add_hyperlink(
        ...   'About', address='http://us.com', fragment='about'
        ... )
        >>> hyperlink
        <docx.text.hyperlink.Hyperlink at 0x7f...>
        >>> hyperlink.text
        'About'
        >>> hyperlink.address
        'http://us.com'
        >>> hyperlink.fragment
        'about'
        >>> hyperlink.url
        'http://us.com#about'

    **添加内部超链接（到书签）**::

        >>> hyperlink = paragraph.add_hyperlink('Section 1', fragment='Section_1')
        >>> hyperlink.text
        'Section 1'
        >>> hyperlink.fragment
        'Section_1'
        >>> hyperlink.address
        ''

    **修改超链接属性**::

        >>> hyperlink.text = 'Froogle'
        >>> hyperlink.text
        'Froogle'
        >>> hyperlink.address = 'mailto:info@froogle.com?subject=sup dawg?'
        >>> hyperlink.address
        'mailto:info@froogle.com?subject=sup%20dawg%3F'
        >>> hyperlink.anchor = None
        >>> hyperlink.anchor
        None

    **向超链接添加额外的 `run`**::

        >>> hyperlink.text = 'A '
        >>> # `.insert_run` 方法用于在指定索引 `idx` 处插入新的 `run`，默认 `idx=-1`
        >>> hyperlink.insert_run(' link').bold = True
        >>> hyperlink.insert_run('formatted', idx=1).bold = True
        >>> hyperlink.text
        'A formatted link'
        >>> [r for r in hyperlink.iter_runs()]
        [<docx.text.run.Run at 0x7fa...>,
        <docx.text.run.Run at 0x7fb...>,
        <docx.text.run.Run at 0x7fc...>]

    **迭代段落中的 `run` 级别元素**::

        >>> paragraph = document.add_paragraph('A paragraph having a link to: ')
        >>> paragraph.add_hyperlink(text='github', address='http://github.com')
        >>> [item for item in paragraph.iter_run_level_items()]
        [<docx.text.paragraph.Run at 0x7fd...>, <docx.text.paragraph.Hyperlink at 0x7fe...>]

    **`Paragraph.text` 现在包含超链接内的文本**::

        >>> paragraph.text
        'A paragraph having a link to: github'

.. tab:: 英文

    An external hyperlink has an address and an optional anchor. An internal hyperlink has only an anchor. An anchor is more precisely known as a *URI fragment* in a web URL and follows a hash mark ("#"). The fragment-separator hash character is not stored in the XML.

    Note that the anchor and address are stored in two distinct attributes, so you need to concatenate `.address` and `.anchor` like `f"{address}#{anchor}"` if you want the whole thing.

    Also note that Word does not rigorously separate a fragment in a web URI so it may appear as part of the address or separately in the anchor attribute, depending on how the hyperlink was authored. Hyperlinks inserted using the dialog-box seem to separate it and addresses typed into the document directly don't, based on my limited experience.

    .. highlight:: python

    **Access hyperlinks in a paragraph**::

        >>> hyperlinks = paragraph.hyperlinks
        [<docx.text.hyperlink.Hyperlink at 0x7f...>]

    **Access hyperlinks in a paragraph in document order with runs**::

        >>> list(paragraph.iter_inner_content())
        [
          <docx.text.run.Run at 0x7f...>
          <docx.text.hyperlink.Hyperlink at 0x7f...>
          <docx.text.run.Run at 0x7f...>
        ]

    **Access hyperlink address**::

        >>> hyperlink.address
        'https://google.com/'

    **Access hyperlink fragment**::

        >>> hyperlink.fragment
        'introduction'

    **Access hyperlink history (visited or not, True means not visited yet)**::

        >>> hyperlink.history
        True

    **Access hyperlinks runs**::

        >>> hyperlink.runs
        [
          <docx.text.run.Run at 0x7f...>
          <docx.text.run.Run at 0x7f...>
          <docx.text.run.Run at 0x7f...>
        ]

    **Access hyperlink URL**::

        >>> hyperlink.url
        'https://us.com#introduction'

    **Determine whether a hyperlink contains a rendered page-break**::

        >>> hyperlink.contains_page_break
        False

    **Access visible text of a hyperlink**::

        >>> hyperlink.text
        'an excellent Wikipedia article on ferrets'

    **Add an external hyperlink** (not yet implemented)::

        >>> hyperlink = paragraph.add_hyperlink(
        ...   'About', address='http://us.com', fragment='about'
        ... )
        >>> hyperlink
        <docx.text.hyperlink.Hyperlink at 0x7f...>
        >>> hyperlink.text
        'About'
        >>> hyperlink.address
        'http://us.com'
        >>> hyperlink.fragment
        'about'
        >>> hyperlink.url
        'http://us.com#about'

    **Add an internal hyperlink (to a bookmark)**::

        >>> hyperlink = paragraph.add_hyperlink('Section 1', fragment='Section_1')
        >>> hyperlink.text
        'Section 1'
        >>> hyperlink.fragment
        'Section_1'
        >>> hyperlink.address
        ''

    **Modify hyperlink properties**::

        >>> hyperlink.text = 'Froogle'
        >>> hyperlink.text
        'Froogle'
        >>> hyperlink.address = 'mailto:info@froogle.com?subject=sup dawg?'
        >>> hyperlink.address
        'mailto:info@froogle.com?subject=sup%20dawg%3F'
        >>> hyperlink.anchor = None
        >>> hyperlink.anchor
        None

    **Add additional runs to a hyperlink**::

        >>> hyperlink.text = 'A '
        >>> # .insert_run inserts a new run at idx, defaults to idx=-1
        >>> hyperlink.insert_run(' link').bold = True
        >>> hyperlink.insert_run('formatted', idx=1).bold = True
        >>> hyperlink.text
        'A formatted link'
        >>> [r for r in hyperlink.iter_runs()]
        [<docx.text.run.Run at 0x7fa...>,
        <docx.text.run.Run at 0x7fb...>,
        <docx.text.run.Run at 0x7fc...>]

    **Iterate over the run-level items a paragraph contains**::

        >>> paragraph = document.add_paragraph('A paragraph having a link to: ')
        >>> paragraph.add_hyperlink(text='github', address='http://github.com')
        >>> [item for item in paragraph.iter_run_level_items()]:
        [<docx.text.paragraph.Run at 0x7fd...>, <docx.text.paragraph.Hyperlink at 0x7fe...>]

    **Paragraph.text now includes text contained in a hyperlink**::

        >>> paragraph.text
        'A paragraph having a link to: github'


Word 的行为
--------------

Word Behaviors

.. tab:: 中文

    * `w:hyperlink` 元素上的 `w:history` 属性的语义是什么？  
      我怀疑它用于指示链接是否应显示为蓝色（未访问）或紫色（已访问）。  
      我倾向于将其作为 `hyperlink` 的一个可读写属性。  
      我们应该查看 Microsoft API 在这方面的处理方式。

    * 我们可能需要对 `w:anchor` 施加某些字符集限制。  
      例如，Word 似乎不接受空格或连字符。  
      但 `ST_String` 这个简单类型似乎并不能处理这些限制。

    * 我们需要测试 `Hyperlink.address` 中特殊字符的 URL 转义，  
      例如空格和问号。

    * 当 Word 加载一个包含内部超链接的文档，  
      但该超链接的 `anchor` 值与现有书签不匹配时，它会如何处理？  
      我们需要了解这一点，  
      因为肯定会有用户遇到这种情况，  
      他们可能会因此收到修复错误的提示，  
      或者出现其他问题，并向我们寻求支持。


.. tab:: 英文

    * What are the semantics of the w:history attribute on w:hyperlink? I'm suspecting this indicates whether the link should show up blue (unvisited) or purple (visited). I'm inclined to think we need that as a read/write property on hyperlink. We should see what the MS API does on this count.

    * We probably need to enforce some character-set restrictions on w:anchor. Word doesn't seem to like spaces or hyphens, for example. The simple type ST_String doesn't look like it takes care of this.

    * We'll need to test URL escaping of special characters like spaces and question marks in Hyperlink.address.

    * What does Word do when loading a document containing an internal hyperlink having an anchor value that doesn't match an existing bookmark? We'll want to know because we're sure to get support inquiries from folks who don't match those up and wonder why they get a repair error or whatever.


样本 XML
------------

Specimen XML

.. tab:: 中文

.. tab:: 英文

.. highlight:: xml


外部链接
~~~~~~~~~~~~~~

External links

.. tab:: 中文

    外部超链接的地址（URL）存储在 `document.xml.rels` 文件中，  
    并由 `w:hyperlink@r:id` 属性进行索引映射::

        <w:p>
          <w:r>
            <w:t xml:space="preserve">This is an external link to </w:t>
          </w:r>
          <w:hyperlink r:id="rId4">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t>Google</w:t>
            </w:r>
          </w:hyperlink>
        </w:p>

    … 在 `document.xml.rels` 文件中，  
    该 `r:id` 对应的关系映射如下::

        <Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">
          <Relationship Id="rId4" Mode="External" Type="http://..." Target="http://google.com/"/>
        </Relationships>

    超链接可以包含多个文本 `run`（以及许多其他内容，至少从架构上看是这样）::

        <w:p>
          <w:hyperlink r:id="rId2">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t xml:space="preserve">A hyperlink containing an </w:t>
            </w:r>
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
                <w:i/>
              </w:rPr>
              <w:t>italicized</w:t>
            </w:r>
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t xml:space="preserve"> word</w:t>
            </w:r>
          </w:hyperlink>
        </w:p>


.. tab:: 英文

    The address (URL) of an external hyperlink is stored in the document.xml.rels
    file, keyed by the w:hyperlink@r:id attribute::

        <w:p>
          <w:r>
            <w:t xml:space="preserve">This is an external link to </w:t>
          </w:r>
          <w:hyperlink r:id="rId4">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t>Google</w:t>
            </w:r>
          </w:hyperlink>
        </w:p>

    ... mapping to relationship in document.xml.rels::

        <Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">
          <Relationship Id="rId4" Mode="External" Type="http://..." Target="http://google.com/"/>
        </Relationships>

    A hyperlink can contain multiple runs of text (and a whole lot of other stuff, at least
    as far as the schema indicates)::

        <w:p>
          <w:hyperlink r:id="rId2">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t xml:space="preserve">A hyperlink containing an </w:t>
            </w:r>
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
                <w:i/>
              </w:rPr>
              <w:t>italicized</w:t>
            </w:r>
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t xml:space="preserve"> word</w:t>
            </w:r>
          </w:hyperlink>
        </w:p>


内部链接
~~~~~~~~~~~~~~

Internal links

.. tab:: 中文

    在 Word UI 中，内部链接提供“跳转到文档中的另一个位置”的功能。  
    内部链接的特征是 **没有** `r:id` 属性。  
    在这种情况下，`w:anchor` 属性是必需的，其值对应于文档中的书签名称。

    示例::

        <w:p>
          <w:r>
            <w:t xml:space="preserve">See </w:t>
          </w:r>
          <w:hyperlink w:anchor="Section_4">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t>Section 4</w:t>
            </w:r>
          </w:hyperlink>
          <w:r>
            <w:t xml:space="preserve"> for more details.</w:t>
          </w:r>
        </w:p>

    … 该链接指向文档中定义的书签::

        <w:p>
          <w:bookmarkStart w:id="0" w:name="Section_4"/>
            <w:r>
              <w:t>Section 4</w:t>
            </w:r>
          <w:bookmarkEnd w:id="0"/>
        </w:p>

.. tab:: 英文

    An internal link provides "jump to another document location" behavior in the Word UI. An internal link is distinguished by the absence of an `r:id` attribute. In this case, the w:anchor attribute is required. The value of the anchor attribute is the name of a bookmark in the document.

    Example::

        <w:p>
          <w:r>
            <w:t xml:space="preserve">See </w:t>
          </w:r>
          <w:hyperlink w:anchor="Section_4">
            <w:r>
              <w:rPr>
                <w:rStyle w:val="Hyperlink"/>
              </w:rPr>
              <w:t>Section 4</w:t>
            </w:r>
          </w:hyperlink>
          <w:r>
            <w:t xml:space="preserve"> for more details.</w:t>
          </w:r>
        </w:p>

    ... referring to this bookmark elsewhere in the document::

        <w:p>
          <w:bookmarkStart w:id="0" w:name="Section_4"/>
            <w:r>
              <w:t>Section 4</w:t>
            </w:r>
          <w:bookmarkEnd w:id="0"/>
        </w:p>


架构摘录
--------------

Schema excerpt

.. highlight:: xml

::

  <xsd:complexType name="CT_P">
    <xsd:sequence>
      <xsd:element name="pPr" type="CT_PPr" minOccurs="0"/>
      <xsd:group   ref="EG_PContent"        minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="rsidRPr"      type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidR"        type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidDel"      type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidP"        type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidRDefault" type="ST_LongHexNumber"/>
  </xsd:complexType>

  <xsd:group name="EG_PContent">  <!-- denormalized -->
    <xsd:choice>
      <xsd:element name="r"         type="CT_R"/>
      <xsd:element name="hyperlink" type="CT_Hyperlink"/>
      <xsd:element name="fldSimple" type="CT_SimpleField"/>
      <xsd:element name="sdt"       type="CT_SdtRun"/>
      <xsd:element name="customXml" type="CT_CustomXmlRun"/>
      <xsd:element name="smartTag"  type="CT_SmartTagRun"/>
      <xsd:element name="dir"       type="CT_DirContentRun"/>
      <xsd:element name="bdo"       type="CT_BdoContentRun"/>
      <xsd:element name="subDoc"    type="CT_Rel"/>
      <xsd:group ref="EG_RunLevelElts"/>
    </xsd:choice>
  </xsd:group>

  <xsd:complexType name="CT_Hyperlink">
    <xsd:group ref="EG_PContent" minOccurs="0" maxOccurs="unbounded"/>
    <xsd:attribute name="tgtFrame"    type="s:ST_String"/>
    <xsd:attribute name="tooltip"     type="s:ST_String"/>
    <xsd:attribute name="docLocation" type="s:ST_String"/>
    <xsd:attribute name="history"     type="s:ST_OnOff"/>
    <xsd:attribute name="anchor"      type="s:ST_String"/>
    <xsd:attribute ref="r:id"/>
  </xsd:complexType>

  <xsd:group name="EG_RunLevelElts">
    <xsd:choice>
      <xsd:element name="proofErr"                    type="CT_ProofErr"/>
      <xsd:element name="permStart"                   type="CT_PermStart"/>
      <xsd:element name="permEnd"                     type="CT_Perm"/>
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
      <xsd:element name="ins"                         type="CT_RunTrackChange"/>
      <xsd:element name="del"                         type="CT_RunTrackChange"/>
      <xsd:element name="moveFrom"                    type="CT_RunTrackChange"/>
      <xsd:element name="moveTo"                      type="CT_RunTrackChange"/>
      <xsd:group ref="EG_MathContent" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:choice>
  </xsd:group>

  <xsd:complexType name="CT_R">
    <xsd:sequence>
      <xsd:group ref="EG_RPr"             minOccurs="0"/>
      <xsd:group ref="EG_RunInnerContent" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="rsidRPr" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidDel" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidR"   type="ST_LongHexNumber"/>
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

  <xsd:simpleType name="ST_RelationshipId">
    <xsd:restriction base="xsd:string"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_String">
    <xsd:restriction base="xsd:string"/>
  </xsd:simpleType>
