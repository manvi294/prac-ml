Option Explicit

Private selectedHeader As Variant
Private formClosed As Boolean

Private Sub UserForm_Initialize()
    Dim headerRow As Range
    Dim headerArray() As Variant
    
    ' Set the header row range (modify as per your worksheet and range)
    Set headerRow = Sheet1.Rows(1)
    
    ' Store the header values in an array
    headerArray = headerRow.Value
    
    ' Set the properties of the combo box control on the user form
    With ComboBox1
        .List = Application.Transpose(headerArray)
        .Style = fmStyleDropDownList
        .Font.Size = 12
    End With
End Sub

Private Sub ComboBox1_Change()
    ' Store the selected header value
    selectedHeader = ComboBox1.Value
    
    ' Set the formClosed flag to True
    formClosed = True
    
    ' Hide the user form
    Me.Hide
    
    ' Check if a header was selected
    If Not IsEmpty(selectedHeader) Then
        ' Perform functions based on the selected header
        ' Add your code here
        
        ' Example: Count the number of non-empty cells in the selected column
        Dim selectedColumn As Range
        Dim rowCount As Long
        Set selectedColumn = Sheet1.Rows(1).Find(selectedHeader).EntireColumn
        rowCount = Application.WorksheetFunction.CountA(selectedColumn)
        
        ' Print the count in Sheet2
        Sheet2.Range("A1").Value = "Count: " & rowCount
    End If
End Sub

Private Sub UserForm_QueryClose(Cancel As Integer, CloseMode As Integer)
    ' Check if the form is closed without selecting a header
    If Not formClosed Then
        ' Prompt the user to make a selection
        MsgBox "Please select a header before closing the form.", vbExclamation, "Selection Required"
        Cancel = True ' Prevent the form from closing
    End If
End Sub
