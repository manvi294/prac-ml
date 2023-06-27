Sub FormatDataAsTable()
    Dim ws As Worksheet
    Dim rng As Range
    Dim tbl As ListObject
    
    ' Set the worksheet
    Set ws = ThisWorkbook.Sheets("Sheet4") ' Replace "Sheet4" with your desired sheet name
    
    ' Get the used range in the worksheet
    Set rng = ws.UsedRange
    
    ' Add a table to the range
    Set tbl = ws.ListObjects.Add(xlSrcRange, rng, , xlYes)
    
    ' Apply default Excel table formatting
    With tbl
        ' Table Style
        .TableStyle = "TableStyleMedium2" ' Replace with the desired table style name
        
        ' Header Row
        .HeaderRowRange.Interior.Color = RGB(79, 129, 189) ' Replace with the desired header row color
        .HeaderRowRange.Font.Color = RGB(255, 255, 255) ' Replace with the desired header font color
        .HeaderRowRange.Font.Bold = True
        
        ' Data Body Range
        .DataBodyRange.Interior.Color = RGB(255, 255, 255) ' Replace with the desired data body color
        
        ' Alternating Row Color
        .TableStyle = "TableStyleMedium2" ' Replace with the desired table style name
        .ShowTableStyleColumnStripes = True
        .ShowTableStyleRowStripes = False
    End With
    
    ' Autofit columns in the table
    rng.Columns.AutoFit
End Sub
