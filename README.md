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
    Dim count As Long
    Dim i As Long
    
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
    
    ' Loop through each unique Us lead
    For i = LBound(usLeadValues) To UBound(usLeadValues)
        usLead = Trim(usLeadValues(i, 1))
        
        ' Check if Us lead is not empty
        If Len(usLead) > 0 Then
            ' Write the Us lead to destination sheet
            destinationSheet.Cells(destinationRow, 1).Value = usLead
            
            ' Find all corresponding India leads and their counts
            count = 0
            For j = LBound(indiaLeadValues) To UBound(indiaLeadValues)
                indiaLead = Trim(indiaLeadValues(j, 1))
                
                ' Check if India lead is not empty
                If Len(indiaLead) > 0 And usLead = Trim(usLeadValues(j, 1)) Then
                    ' Write the India lead to destination sheet
                    destinationSheet.Cells(destinationRow + count, 2).Value = indiaLead
                    
                    ' Write the head count to destination sheet
                    destinationSheet.Cells(destinationRow + count, 3).Value = Application.WorksheetFunction.CountIfs(sourceData.Columns(usLeadColumn.Column), usLead, sourceData.Columns(indiaLeadColumn.Column), indiaLead)
                    
                    count = count + 1
                End If
            Next j
            
            ' Increment the destination row
            destinationRow = destinationRow + count
        End If
    Next i
    
    MsgBox "Data table generated successfully!", vbInformation
End Sub
