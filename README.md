Sub PopulateColumnBP()
    Dim wsMapping As Worksheet
    Dim wsSheet1 As Worksheet
    Dim mappingRange As Range
    Dim cell As Range
    Dim searchValue As String
    Dim resultValue As String
    
    ' Set the mapping sheet and Sheet1
    Set wsMapping = ThisWorkbook.Sheets("Mapping") ' Replace "Mapping" with your mapping sheet name
    Set wsSheet1 = ThisWorkbook.Sheets("Sheet1") ' Replace "Sheet1" with your Sheet1 name
    
    ' Set the mapping range
    Set mappingRange = wsMapping.Range("A1:B" & wsMapping.Cells(wsMapping.Rows.Count, "A").End(xlUp).Row)
    
    ' Loop through the cells in column AE of Sheet1
    For Each cell In wsSheet1.Range("AE1:AE" & wsSheet1.Cells(wsSheet1.Rows.Count, "AE").End(xlUp).Row)
        ' Get the search value from column AE
        searchValue = cell.Value
        
        ' Reset the result value
        resultValue = ""
        
        ' Search for the value in the mapping range
        On Error Resume Next
        resultValue = Application.WorksheetFunction.VLookup(searchValue, mappingRange, 2, False)
        On Error GoTo 0
        
        ' Check if a match was found
        If resultValue <> "" Then
            ' Fill in the result value in column BP
            cell.Offset(0, 53).Value = resultValue
        End If
    Next cell
End Sub
