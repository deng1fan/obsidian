![](../_resources/PPT%20%E6%B7%BB%E5%8A%A0%E5%BA%95%E9%83%A8%E8%BF%9B%E5%BA%A6%E6%9D%A1%E5%8F%8A%E9%A1%B5%E7%A0%81/1cc9ed80567b421be71c1973b4c20af6_MD5.png)

点击 + 号添加新的宏

![](../_resources/PPT%20%E6%B7%BB%E5%8A%A0%E5%BA%95%E9%83%A8%E8%BF%9B%E5%BA%A6%E6%9D%A1%E5%8F%8A%E9%A1%B5%E7%A0%81/3493e29e1b822acd1a0efcb37456f451_MD5.png)

在上图的位置中的内容替换为下面的代码

```
Sub ProgressBar()

    Dim mySlides As Slides
    Dim pageBar As ShapeRange
    Dim pageSHower As Shape
    Dim pageWidth, pageHeight, pageStep
    Dim MyArray() As Variant  '增加一个数组以便统计隐藏的幻灯片
    Dim i, j, k
    j = 0
    k = 0

    Set mySlides = Application.ActivePresentation.Slides

    pageWidth = Application.ActivePresentation.SlideMaster.Width
    pageHeight = Application.ActivePresentation.SlideMaster.Height
    ' pageStep = pageWidth / mySlides.Count

    ReDim MyArray(mySlides.Count, 0)
    
    For i = 1 To mySlides.Count '统计隐藏的幻灯片数
        If mySlides.Item(i).SlideShowTransition.Hidden = True Then
            j = j + 1
            MyArray(i, 0) = 1
        Else
            MyArray(i, 0) = 0
        End If
    Next

    '除去首页和隐藏的幻灯片后计算进度条长度增量
    If mySlides.Count - 1 - j > 0 Then
        pageStep = pageWidth / (mySlides.Count - 1 - j)
    Else
        pageStep = 0
    End If

    On Error Resume Next

    For i = 1 To mySlides.Count    ' 改为从1开始
        k = k + MyArray(i, 0)      ' 计算当前隐藏的幻灯片数
        Set pageBar = mySlides.Item(i).Shapes.Range(Array())
        Set pageBar = _
           mySlides.Item(i).Shapes.Range(Array("RectanglePageNum"))

        If IsNull(pageBar) Or pageBar.Count = 0 Then GoTo newBar
        Set pageSHower = pageBar.Item(1)
        GoTo nextPage

newBar:
        Set pageSHower = mySlides.Item(i).Shapes.AddShape( _
                           msoShapeRectangle, 0, _
                           pageHeight - 3, i * pageStep, 3)
        pageSHower.Name = "RectanglePageNum"

nextPage:
        pageSHower.Fill.ForeColor.RGB = RGB(6,109,232)
        pageSHower.Line.Visible = msoFalse
        ' pageSHower.Width = i * pageStep
        ' 计算进度条长度时除去首页和隐藏的幻灯片
        pageSHower.Width = (i - 1 - k) * pageStep
        pageSHower.Top = pageHeight - 3
        pageSHower.Left = 0
        pageSHower.Height = 3
        ' 删除首页和隐藏的幻灯片的进度条
        If i = 1 Or MyArray(i, 0) = 1 Then pageSHower.Delete
    Next
End Sub

Sub Add_or_Remove_Custome_TextBox()
    answer = MsgBox("你想要添加（删除）自定义页码文本框吗？" & vbLf & vbLf & "「是」：“添加”操作" & vbLf & vbLf & "「否」：“删除”操作" & vbLf & vbLf & "「取消」：放弃操作", vbQuestion + vbYesNoCancel + vbDefaultButton1, "添加或删除自定义页码文本框")
    ' answer = MsgBox("Do you want to add (remove) custom page-number textboxes?" & vbLf & vbLf & "[Yes]: add custom textboxes" & vbLf & vbLf & "[No]: remove custom textboxes" & vbLf & vbLf & "[Cancel]: cancel the operation", vbQuestion + vbYesNoCancel + vbDefaultButton1, "Add or Remove Custom Page-number Textboxes")

    If answer = vbYes Then
        Debug.Print "Add"
        Add_Custom_TextBox
    ElseIf answer = vbNo Then
        Debug.Print "Remove"
        Remove_Custom_TextBox
    ElseIf answer = vbCancel Then
        Debug.Print "Cancel"
    End If
End Sub

Sub Add_Custom_TextBox()
    Dim shp, selectedShp, newTextBox As Shape
    Dim sld As Slide
    Dim count, i, numSlides, numVisibleSlides As Long
    Dim visibleSlides() As Slide
    Dim errorSlides As String

    If ActiveWindow.Selection.Type = ppSelectionShapes Or ActiveWindow.Selection.Type = ppSelectionText Then
        ' A shape is selected or a textbox is focused (text is selected)
        Set selectedShp = ActiveWindow.Selection.ShapeRange(1)

        ' get all slides in the current presentation
        numSlides = ActivePresentation.Slides.count
        count = 0
        errorSlides = ""
        For i = 1 To numSlides
            Set sld = ActivePresentation.Slides(i)
            ' Skip hidden slides
            If sld.SlideShowTransition.Hidden = msoFalse Then
                count = count + 1
                ReDim Preserve visibleSlides(count) As Slide
                Set visibleSlides(count) = sld
            End If
        Next i

        numVisibleSlides = UBound(visibleSlides)
        On Error GoTo ErrHandler
        For i = 1 To UBound(visibleSlides)
            Set sld = visibleSlides(i)
            Set newTextBox = sld.Shapes.AddTextbox( _
                Orientation:=msoTextOrientationHorizontal, _
                Left:=selectedShp.Left, _
                Top:=selectedShp.Top, _
                Width:=selectedShp.Width, _
                Height:=selectedShp.Height _
            )
            newTextBox.Name = "page_footer"
            With newTextBox.TextFrame.TextRange
                .Text = CStr(i) & " / " & CStr(numVisibleSlides)
                .Font.Bold = selectedShp.TextFrame.TextRange.Font.Bold
                .Font.Italic = selectedShp.TextFrame.TextRange.Font.Italic
                .Font.Underline = selectedShp.TextFrame.TextRange.Font.Underline
                .Font.Name = selectedShp.TextFrame.TextRange.Font.Name
                .Font.NameFarEast = selectedShp.TextFrame.TextRange.Font.NameFarEast
                .Font.Size = selectedShp.TextFrame.TextRange.Font.Size
                .Font.Color.RGB = selectedShp.TextFrame.TextRange.Font.Color.RGB
                .ParagraphFormat.Alignment = selectedShp.TextFrame.TextRange.ParagraphFormat.Alignment
            End With
        Next i

        If Len(Trim(errorSlides)) > 0 Then
            MsgBox "操作完成。但处理以下 PPT 页时出现错误：" & error_slides, vbExclamation, "添加自定义页码文本框"
            ' MsgBox "Finished. But some errors occur in the following slides: " & errorSlides, vbExclamation, "Insert footers in all slides"
        Else
            MsgBox "操作完成", vbExclamation, "添加自定义页码文本框"
            ' MsgBox "Finished without error", vbExclamation, "Insert footers in all slides"
        End If
    Else
        MsgBox "请选择一个文本框来作为添加页码文本框的参考，然后重试！", vbExclamation, "未选择文本框"
        ' MsgBox "Please select a text box to determine the position & font style and retry!", vbExclamation, "No Selected TextBox Found"
    End If

    Exit Sub

ErrHandler:
    If error_slides = "" Then
        errorSlides = CStr(i)
    Else
        errorSlides = errorSlides & ", " & CStr(i)
    End If
    Resume Next
End Sub


Sub Remove_Custom_TextBox()
    Dim sld As Slide
    Dim i, L As Long
    Dim errorSlides As String

    errorSlides = ""
    i = 0
    On Error GoTo ErrHandler2
    For Each sld In ActivePresentation.Slides
        i = i + 1
        For L = sld.Shapes.count To 1 Step -1
            If sld.Shapes(L).Name = "page_footer" Then sld.Shapes(L).Delete
        Next L
    Next sld

    If Len(Trim(errorSlides)) > 0 Then
        MsgBox "操作完成。但处理以下 PPT 页时出现错误：" & error_slides, vbExclamation, "添加自定义页码文本框"
        ' MsgBox "Finished. But some errors occur in the following slides: " & errorSlides, vbExclamation, "Insert footers in all slides"
    Else
        MsgBox "操作完成", vbExclamation, "添加自定义页码文本框"
        ' MsgBox "Finished without error", vbExclamation, "Insert footers in all slides"
    End If

    Exit Sub

ErrHandler2:
    If error_slides = "" Then
        errorSlides = CStr(i)
    Else
        errorSlides = errorSlides & ", " & CStr(i)
    End If
    Resume Next
End Sub
```

然后保存返回就可以在宏的页面看到刚才添加的

![](../_resources/PPT%20%E6%B7%BB%E5%8A%A0%E5%BA%95%E9%83%A8%E8%BF%9B%E5%BA%A6%E6%9D%A1%E5%8F%8A%E9%A1%B5%E7%A0%81/3af77c82998ad7a79f9a4eb0993d9d58_MD5.png)

> 添加页码的宏需要先在 PPT 页面中选中一个文本框再运行。

> 增减幻灯片(总页数改变)后要重新运行一次宏。如果确定不修改了，也可以再次另存为 pptx 等非宏运行格式，进度条还在，但是宏没有了。



