Private Sub UserForm_Initialize()
    Dim headerRange As Range
    Set headerRange = ThisWorkbook.Worksheets("Sheet1").Rows(1) ' Replace "Sheet1" with your actual sheet name
    
    Dim headerCell As Range
    Dim visibleRowCount As Integer
    visibleRowCount = 5 ' Set the number of visible rows
    
    For Each headerCell In headerRange
        Me.ComboBox1.AddItem headerCell.Value
        
        ' Limit the number of visible rows
        If Me.ComboBox1.ListCount > visibleRowCount Then
            Me.ComboBox1.DropDown
        End If
    Next headerCell
End Sub
