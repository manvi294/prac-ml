Sub RemoveTableFormatting()
    Dim ws As Worksheet
    Dim tbl As ListObject
    
    ' Set the worksheet
    Set ws = ThisWorkbook.Sheets("Sheet4") ' Replace "Sheet4" with your desired sheet name
    
    ' Set the table
    Set tbl = ws.ListObjects("Table1") ' Replace "Table1" with the actual table name
    
    ' Check if the table exists
    If Not tbl Is Nothing Then
        ' Unlist the table to remove table formatting
        tbl.Unlist
        
        ' Autofit columns in the range
        tbl.Range.Columns.AutoFit
    End If
End Sub
