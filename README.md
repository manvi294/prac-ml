Sub PerformFunctionBasedOnHeaderSelection()
    Dim headerRow As Range
    Dim headerCell As Range
    Dim selectedHeader As Variant
    Dim headerArray() As Variant
    Dim userInputForm As UserFormName
    
    ' Set the header row range (modify as per your worksheet and range)
    Set headerRow = Sheet1.Rows(1)
    
    ' Store the header values in an array
    headerArray = headerRow.Value
    
    ' Check if the user form is already displayed
    On Error Resume Next
    Set userInputForm = New UserFormName
    If Err.Number = 0 Then
        userInputForm.Hide
    Else
        Set userInputForm = Nothing
    End If
    On Error GoTo 0
    
    ' Show the hidden user form
    If userInputForm Is Nothing Then
        Set userInputForm = New UserFormName
    End If
    
    With userInputForm
        ' Set the properties of the user form
        .Caption = "Select Header"
        .Width = 300
        .Height = 100
        
        ' Set the properties of the combo box control on the user form
        With .ComboBox1
            .List = Application.Transpose(headerArray)
            .Style = fmStyleDropDownList
            .Font.Size = 12
        End With
        
        ' Show the user form
        .Show
        
        ' Store the selected header value
        selectedHeader = .ComboBox1.Value
    End With
    
    ' Clean up the user form
    Unload userInputForm
    
    ' Check if a header was selected
    If Not IsEmpty(selectedHeader) Then
        ' Loop through the header row to find the selected header
        For Each headerCell In headerRow
            If headerCell.Value = selectedHeader Then
                ' Perform functions based on the selected header
                ' Add your code here
                
                ' Exit the loop once the header is found
                Exit For
            End If
        Next headerCell
    End If
End Sub
