Sub CalculateHalfTotal()
    Dim total As Double
    Dim halfTotal As Double
    Dim lastRow As Long
    
    ' Set the worksheet reference
    Dim ws As Worksheet
    Set ws = ThisWorkbook.Sheets("Sheet2")
    
    ' Find the last row in column F
    lastRow = ws.Cells(ws.Rows.Count, "F").End(xlUp).Row
    
    ' Calculate the total of column F, excluding non-numeric values or empty cells
    total = 0
    For i = 1 To lastRow
        If IsNumeric(ws.Cells(i, "F").Value) Then
            total = total + CDbl(ws.Cells(i, "F").Value)
        Else
            Debug.Print "Non-numeric value or empty cell detected in row " & i & ": " & ws.Cells(i, "F").Value
        End If
    Next i
    
    ' Calculate half of the total
    halfTotal = total / 2
    
    ' Print the half total on the last line of column F
    ws.Cells(lastRow + 1, "F").Value = halfTotal
    
    ' Output the calculated values to the Immediate window (View > Immediate Window)
    Debug.Print "Total: " & total
    Debug.Print "Half Total: " & halfTotal
End Sub
