Sub RemoveTableFormatting()
    Dim ws As Worksheet
    Dim tbl As ListObject
    
    ' Set the worksheet
    Set ws = ThisWorkbook.Sheets("Sheet4") ' Replace "Sheet4" with your desired sheet name
    
    ' Check if there is at least one table in the worksheet
    If ws.ListObjects.Count > 0 Then
        ' Get the first table in the worksheet
        Set tbl = ws.ListObjects(1)
        
        ' Unlist the table to remove table formatting
        tbl.Unlist
        
        ' Autofit columns in the range
        tbl.Range.Columns.AutoFit
    End If
End Sub
