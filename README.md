Sub PerformFunctionBasedOnHeaderSelection()
    Dim headerRow As Range
    Dim headerCell As Range
    Dim selectedHeader As Variant
    Dim headerArray() As Variant
    Dim userInputForm As Object
    
    ' Set the header row range (modify as per your worksheet and range)
    Set headerRow = Sheet1.Rows(1)
    
    ' Store the header values in an array
    headerArray = headerRow.Value
    
    ' Create a user form and add a combo box to display the header options
    Set userInputForm = VBA.UserForms.Add
    
    With userInputForm
        .Caption = "Select Header"
        .Width = 300
        .Height = 100
        
        With .Controls.Add("Forms.ComboBox.1")
            .Left = 10
            .Top = 10
            .Width = 280
            .List = Application.Transpose(headerArray)
            .DropDownStyle = fmDropDownList
            .Font.Size = 12
        End With
        
        With .Controls.Add("Forms.CommandButton.1")
            .Left = 110
            .Top = 40
            .Width = 80
            .Caption = "OK"
            .Font.Size = 12
        End With
        
        ' Show the user form
        .Show
        ' Store the selected header value
        selectedHeader = .Controls(0).Value
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
