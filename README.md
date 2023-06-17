Sub CalculateHalfTotal()
    Dim total As Double
    Dim halfTotal As Double
    Dim lastRow As Long
    
    ' Set the worksheet reference
    Dim ws As Worksheet
    Set ws = ThisWorkbook.Sheets("Sheet2")
    
    ' Find the last row in column F
    lastRow = ws.Cells(ws.Rows.Count, "F").End(xlUp).Row
    
    ' Calculate the total of column F
    total = WorksheetFunction.Sum(ws.Range("F1:F" & lastRow))
    
    ' Calculate half of the total
    halfTotal = total / 2
    
    ' Display the result in a message box
    MsgBox "Half of the total is: " & halfTotal
End Sub
