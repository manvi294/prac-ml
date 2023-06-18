Sub CalculateHalfTotal()
    Dim total As Double
    Dim halfTotal As Double
    Dim lastRow As Long
    
    ' Set the worksheet reference
    Dim ws As Worksheet
    Set ws = ThisWorkbook.Sheets("Sheet2")
    
    ' Find the last row in column F
    lastRow = ws.Cells(ws.Rows.Count, "F").End(xlUp).Row
    
    ' Convert the values in column F to numeric
    For i = 1 To lastRow
        If Not IsEmpty(ws.Cells(i, "F").Value) Then
            Dim cellValue As String
            cellValue = CStr(ws.Cells(i, "F").Value)
            
            ' Remove any non-numeric characters except decimal separator
            Dim cleanValue As String
            cleanValue = ""
            
            For j = 1 To Len(cellValue)
                Dim char As String
                char = Mid(cellValue, j, 1)
                
                If IsNumeric(char) Or char = "." Then
                    cleanValue = cleanValue & char
                End If
            Next j
            
            ' Convert the cleaned value to numeric using TryParse
            Dim numericValue As Double
            If Double.TryParse(cleanValue, numericValue) Then
                ws.Cells(i, "F").Value = numericValue
            Else
                Debug.Print "Non-numeric value detected in row " & i & ": " & cellValue
            End If
        End If
    Next i
    
    ' Calculate the total of column F
    total = WorksheetFunction.Sum(ws.Range("F1:F" & lastRow))
    
    ' Calculate half of the total
    halfTotal = total / 2
    
    ' Print the half total on the last line of column F
    ws.Cells(lastRow + 1, "F").Value = halfTotal
    
    ' Output the calculated values to the Immediate window (View > Immediate Window)
    Debug.Print "Total: " & total
    Debug.Print "Half Total: " & halfTotal
End Sub
