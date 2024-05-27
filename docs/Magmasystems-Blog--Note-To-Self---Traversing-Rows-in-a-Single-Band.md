<!--yml

category: 未分类

date: 2024-05-18 05:21:21

-->

# Magmasystems Blog: 给自己的一条笔记 - 在单带中遍历行

> 来源：[`magmasystems.blogspot.com/2006/04/note-to-self-traversing-rows-in-single.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/note-to-self-traversing-rows-in-single.html#0001-01-01)

I am not really a hardcore Infragistics person. I find it amazing that some of the features that I consider essential in their Ultra

**WEB**

Grid offering are not found in their Ultra

**WIN**

Grid product.

I am writing a prototype of an app that has multiple levels of grouping. I need to be able to double-click on the column header of a band, and have it do something to only the rows in that band. For instance, if the user double-clicks on the column that says 'Selected', then I want every checkbox in that group to be toggled without affecting the rows in any other group.

![](http://photos1.blogger.com/blogger/138/258/1600/ManualConfs.jpg)

听起来很简单，不是吗？找出你双击了哪个标题，然后获取与该标题相关联的子行。问题是，在 UltraWinGrid 中，标题并不是真正的行。它们是“UI 元素”。它们没有引用直接下面的行。

折腾了好一会儿 HeaderDoubleClicked 事件之后，我最终决定基于 MouseDoubleClick 事件来处理。

经过几小时的鼓捣，我最终想出了这个方法。（顺便说一下，函数'ToggleSelected'是在分组网格中遍历整棵树行的一个好方法。）

```

private UltraGridRow m_firstRowOfTheHeaderThatWasDoubleClickedOn = null;

private void dgTrades_MouseDoubleClick(object sender, MouseEventArgs e)
{
  Infragistics.Win.UIElement element =
  this.dgTrades.DisplayLayout.UIElement.ElementFromPoint(new Point(e.X, e.Y));
  if (element != null)
  {
    this.CalcGridRowForDblClick(element);
    if (element is Infragistics.Win.TextUIElement)
    {
      HeaderBase hdr = element.GetContext(typeof(HeaderBase)) as HeaderBase;
      if (hdr != null)
        this.dgTrades_DoubleClickHeader(hdr);
    }
  }
}

private void dgTrades_DoubleClickHeader(HeaderBase hdr)
{
  if (hdr.Column.Key == "Selected")
  {
    if (this.m_firstRowOfTheHeaderThatWasDoubleClickedOn != null)
      this.ToggleSelected(e.Header, 
                          this.m_firstRowOfTheHeaderThatWasDoubleClickedOn);
  }

  this.m_firstRowOfTheHeaderThatWasDoubleClickedOn = null;
}

private void ToggleSelected(HeaderBase header, UltraGridRow row)
{
  if (row == null)
    return;

  UltraGridBand band = header.Band;
  UltraGridRow childRow = row.GetChild(ChildRow.First, band);
  if (childRow == null)
  {
    // May be a leaf node
    UltraGridColumn colSelected = band.Columns["Selected"];
    if (colSelected == null)
      return;
    int idx = colSelected.Index;
    for (; row != null; row = row.GetSibling(SiblingRow.Next, false))
    {
      row.Cells[idx].Value = !((bool)row.Cells[idx].Value);
    }
  }
  else
  {
    // Is a non-leaf node
    this.ToggleSelected(header, childRow);
    this.ToggleSelected(header, row.GetSibling(SiblingRow.Next, false));
  }
}

private UltraGridRow CalcGridRowForDblClick(Infragistics.Win.UIElement uiElement)
{
  this.m_firstRowOfTheHeaderThatWasDoubleClickedOn = null;

  if (uiElement == null)
  return null;

  object elementContext = uiElement.GetContext(typeof(UltraGridRow));
  if (elementContext == null)
    return null;

  UltraGridRow row = elementContext as UltraGridRow;
  if (row != null)
    this.m_firstRowOfTheHeaderThatWasDoubleClickedOn = row;
  return row;
}

```  这方法有效。关键在于 UIElement.GetContext()函数，我最终是在 Infragistics 网站上的一个两句话的知识库文章中找到的。

©2006 Marc Adler - All Rights Reserved
