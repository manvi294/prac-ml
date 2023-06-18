Sub CopyAndInsertColumns()
    Dim wsSource As Worksheet
    Set wsSource = ThisWorkbook.Sheets("Sheet4")
    
    Dim wsDestination As Worksheet
    Set wsDestination = ThisWorkbook.Sheets("Sheet6")
    
    ' Copy the first table from Sheet4 to Sheet6
    wsSource.Range("C1:G" & wsSource.Cells(wsSource.Rows.Count, "C").End(xlUp).Row).Copy wsDestination.Range("A1")
    
    ' Insert four new columns in the first table
    wsDestination.Range("D1").Resize(wsDestination.UsedRange.Rows.Count, 4).Insert Shift:=xlToRight
    
    ' Copy the second table from Sheet4 to Sheet6
    wsSource.Range("J1:N" & wsSource.Cells(wsSource.Rows.Count, "J").End(xlUp).Row).Copy wsDestination.Cells(wsDestination.Cells(wsDestination.Rows.Count, "A").End(xlUp).Row + 2, "A")
    
    ' Insert four new columns in the second table
    wsDestination.Range("D1").Resize(wsDestination.UsedRange.Rows.Count, 4).Insert Shift:=xlToRight
End Sub
