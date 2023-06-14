# prac-ml
Practise my ML fundamentals

Sub CopyRowsToSheet5()
    Dim sourceSheet As Worksheet
    Dim destinationSheet As Worksheet
    Dim lastRow As Long
    Dim sourceRow As Range
    Dim destinationRow As Range
    Dim headerRow As Range
    
    ' Set the source sheet and destination sheet
    Set sourceSheet = ThisWorkbook.Sheets("Sheet1") ' Modify as needed
    Set destinationSheet = ThisWorkbook.Sheets("Sheet5") ' Modify as needed
    
    ' Find the header row in the source sheet
    Set headerRow = sourceSheet.Rows(1)
    
    ' Find the last row in the source sheet
    lastRow = sourceSheet.Cells(sourceSheet.Rows.Count, "A").End(xlUp).Row
    
    ' Loop through each row in the source sheet
    For Each sourceRow In sourceSheet.Range("A2:A" & lastRow)
        ' Check if the value in the "sow" column is "swe"
        If sourceRow.Offset(0, headerRow.Cells(1, "sow").Column - 1).Value = "swe" Then
            ' Find the corresponding destination row in Sheet5
            Set destinationRow = destinationSheet.Rows(destinationSheet.Rows.Count).End(xlUp).Offset(1)
            
            ' Copy the entire row to Sheet5
            sourceRow.EntireRow.Copy destinationRow
        End If
    Next sourceRow
    
    ' Copy the header row to Sheet5
    headerRow.Copy destinationSheet.Rows(1)
    
    ' Auto-fit the columns in Sheet5
    destinationSheet.UsedRange.Columns.AutoFit
    
    ' Optionally, you can also format the copied data in Sheet5 as needed
    
    MsgBox "Rows with value 'swe' in the 'sow' column have been copied to Sheet5."
End Sub
