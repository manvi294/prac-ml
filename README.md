Sub FillColumnAF()
    Dim ws As Worksheet
    Dim lastRow As Long
    Dim i As Long
    
    ' Set the worksheet to work with
    Set ws = ThisWorkbook.Sheets("Sheet1") ' Replace "Sheet1" with your sheet name
    
    ' Find the last row in column AE
    lastRow = ws.Cells(ws.Rows.Count, "AE").End(xlUp).Row
    
    ' Loop through the cells in column AE
    For i = 1 To lastRow
        ' Check if the cell in column AE is blank
        If ws.Cells(i, "AE").Value = "" Then
            ' Fill in a value in column AF
            ws.Cells(i, "AF").Value = "YourValue" ' Replace "YourValue" with the desired value
        End If
    Next i
End Sub
