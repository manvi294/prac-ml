# prac-ml
Practise my ML fundamentals

Sub GenerateDataTable()
    Dim sourceSheet As Worksheet
    Dim destinationSheet As Worksheet
    Dim sourceData As Range
    Dim usLeadColumn As Range
    Dim indiaLeadColumn As Range
    Dim destinationRow As Long
    Dim usLeadValues As Variant
    Dim indiaLeadValues As Variant
    Dim usLead As String
    Dim indiaLead As String
    Dim i As Long
    Dim j As Long
    
    ' Set the source sheet and range
    Set sourceSheet = ThisWorkbook.Sheets("Sheet1")
    Set sourceData = sourceSheet.UsedRange
    
    ' Set the destination sheet
    Set destinationSheet = ThisWorkbook.Sheets("Sheet4")
    
    ' Clear previous data in destination sheet
    destinationSheet.Cells.Clear
    
    ' Find the columns with headings "HR_LEVEL_12" and "US Lead"
    Set usLeadColumn = sourceData.Rows(1).Find("US Lead", LookIn:=xlValues, LookAt:=xlWhole)
    Set indiaLeadColumn = sourceData.Rows(1).Find("HR_LEVEL_12", LookIn:=xlValues, LookAt:=xlWhole)
    
    ' Exit if either column is not found
    If usLeadColumn Is Nothing Or indiaLeadColumn Is Nothing Then
        MsgBox "Columns not found!", vbExclamation
        Exit Sub
    End If
    
    ' Set the initial destination row
    destinationRow = 2
    
    ' Get the values from Us lead and India lead columns into arrays
    usLeadValues = usLeadColumn.Offset(1).Resize(sourceData.Rows.Count - 1).Value
    indiaLeadValues = indiaLeadColumn.Offset(1).Resize(sourceData.Rows.Count - 1).Value
    
    ' Loop through each unique combination of Us lead and India lead
    On Error Resume Next
    For i = LBound(usLeadValues) To UBound(usLeadValues)
        On Error Resume Next
        For j = LBound(indiaLeadValues) To UBound(indiaLeadValues)
            usLead = Trim(usLeadValues(i, 1))
            indiaLead = Trim(indiaLeadValues(j, 1))
            
            ' Check if Us lead and India lead are not empty
            If Len(usLead) > 0 And Len(indiaLead) > 0 Then
                ' Write the Us lead to destination sheet
                destinationSheet.Cells(destinationRow, 1).Value = usLead
                
                ' Write the India lead to destination sheet
                destinationSheet.Cells(destinationRow, 2).Value = indiaLead
                
                ' Write the head count to destination sheet
                destinationSheet.Cells(destinationRow, 3).Value = Application.WorksheetFunction.CountIfs(sourceData.Columns(usLeadColumn.Column), usLead, sourceData.Columns(indiaLeadColumn.Column), indiaLead)
                
                ' Increment the destination row
                destinationRow = destinationRow + 1
            End If
        Next j
        On Error Resume Next
    Next i
    
    MsgBox "Data table generated successfully!", vbInformation
End Sub
