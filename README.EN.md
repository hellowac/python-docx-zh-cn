# python-docx

*python-docx* 是一个用于读取、创建和更新 Microsoft Word 2007+ (.docx) 文件的 Python 库。

## 安装

```shell
pip install python-docx
```

## 示例

```python
>>> from docx import Document

>>> document = Document()
>>> document.add_paragraph("It was a dark and stormy night.")
<docx.text.paragraph.Paragraph object at 0x10f19e760>
>>> document.save("dark-and-stormy.docx")

>>> document = Document("dark-and-stormy.docx")
>>> document.paragraphs[0].text
'It was a dark and stormy night.'
```

更多信息请参阅 [python-docx 文档](https://hellowac.github.io/python-docx-zh-cn/)
