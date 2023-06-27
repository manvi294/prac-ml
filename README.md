Sub FormatTableAlignments()
    Dim ws As Worksheet
    Dim tbl As ListObject
    
    ' Set the worksheet
    Set ws = ThisWorkbook.Sheets("Sheet4") ' Replace "Sheet4" with your desired sheet name
    
    ' Check if there is at least one table in the worksheet
    If ws.ListObjects.Count > 0 Then
        ' Get the first table in the worksheet
        Set tbl = ws.ListObjects(1)
        
        ' Align the text in the header row
        With tbl.HeaderRowRange
            .HorizontalAlignment = xlCenter ' Set the horizontal alignment (e.g., xlLeft, xlCenter, xlRight)
            .VerticalAlignment = xlCenter ' Set the vertical alignment (e.g., xlTop, xlCenter, xlBottom)
            .WrapText = True ' Enable text wrapping if needed
        End With
        
        ' Align the text in the data body range
        With tbl.DataBodyRange
            .HorizontalAlignment = xlCenter ' Set the horizontal alignment (e.g., xlLeft, xlCenter, xlRight)
            .VerticalAlignment = xlCenter ' Set the vertical alignment (e.g., xlTop, xlCenter, xlBottom)
            .WrapText = True ' Enable text wrapping if needed
        End With
    End If
End Sub
