# prac-ml
Practise my ML fundamentals

Sub GenerateDataTable()
    Dim sourceSheet As Worksheet
    Dim destinationSheet As Worksheet
    Dim sourceData As Range
    Dim usLeadColumn As Range
    Dim indiaLeadColumn As Range
    Dim destinationRow As Long
    Dim usLeadArea As Range
    Dim indiaLeadArea As Range
    Dim usLeadCell As Range
    Dim indiaLeadCell As Range
    Dim usLead As String
    Dim indiaLead As String
    
    ' Set the source sheet and range
    Set sourceSheet = ThisWorkbook.Sheets("Sheet1")
    Set sourceData = sourceSheet.UsedRange
    
    ' Set the destination sheet
    Set destinationSheet = ThisWorkbook.Sheets("Sheet2")
    
    ' Clear previous data in destination sheet
    destinationSheet.Cells.Clear
    
    ' Find the columns with headings "hr" and "us lead"
    Set usLeadColumn = sourceData.Rows(1).Find("us lead", LookIn:=xlValues, LookAt:=xlWhole)
    Set indiaLeadColumn = sourceData.Rows(1).Find("hr", LookIn:=xlValues, LookAt:=xlWhole)
    
    ' Exit if either column is not found
    If usLeadColumn Is Nothing Or indiaLeadColumn Is Nothing Then
        MsgBox "Columns not found!", vbExclamation
        Exit Sub
    End If
    
    ' Set the initial destination row
    destinationRow = 2
    
    ' Loop through each unique combination of Us lead and India lead
    Set usLeadArea = sourceData.Columns(usLeadColumn.Column).SpecialCells(xlCellTypeConstants).Areas
    Set indiaLeadArea = sourceData.Columns(indiaLeadColumn.Column).SpecialCells(xlCellTypeConstants).Areas
    
    For Each usLeadCell In usLeadArea.Cells
        For Each indiaLeadCell In indiaLeadArea.Cells
            usLead = usLeadCell.Value
            indiaLead = indiaLeadCell.Value
            
            ' Write the Us lead to destination sheet
            destinationSheet.Cells(destinationRow, 1).Value = usLead
            
            ' Write the India lead to destination sheet
            destinationSheet.Cells(destinationRow, 2).Value = indiaLead
            
            ' Write the head count to destination sheet
            destinationSheet.Cells(destinationRow, 3).Value = Application.WorksheetFunction.CountIfs(sourceData.Columns(usLeadColumn.Column), usLead, sourceData.Columns(indiaLeadColumn.Column), indiaLead)
            
            ' Increment the destination row
            destinationRow = destinationRow + 1
        Next indiaLeadCell
    Next usLeadCell
    
    MsgBox "Data table generated successfully!", vbInformation
End Sub
