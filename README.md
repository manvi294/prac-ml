Sub ResizeAndRepositionTable()
    Dim ppApp As PowerPoint.Application
    Dim ppPres As PowerPoint.Presentation
    Dim ppSlide As PowerPoint.Slide
    Dim ppShape As PowerPoint.Shape
    Dim ppTable As PowerPoint.Table
    Dim ppCell As PowerPoint.Cell
    Dim rowIndex As Long
    Dim colIndex As Long
    
    ' Create a reference to the PowerPoint application
    Set ppApp = New PowerPoint.Application
    
    ' Open the PowerPoint presentation
    Set ppPres = ppApp.Presentations.Open("C:\Path\to\Your\Presentation.pptx")
    
    ' Set the target slide index where the table is located
    Dim targetSlideIndex As Integer
    targetSlideIndex = 1
    
    ' Set the target shape index of the table within the slide
    Dim targetShapeIndex As Integer
    targetShapeIndex = 1
    
    ' Reference the target slide
    Set ppSlide = ppPres.Slides(targetSlideIndex)
    
    ' Reference the target shape (table)
    Set ppShape = ppSlide.Shapes(targetShapeIndex)
    
    ' Check if the shape is a table
    If ppShape.HasTable Then
        ' Reference the table
        Set ppTable = ppShape.Table
        
        ' Loop through each cell in the table
        For Each ppCell In ppTable.Cells
            ' Get the row and column indexes of the current cell
            rowIndex = ppCell.Row
            colIndex = ppCell.Column
            
            ' Increase the font size of the cell text
            ppTable.Cell(rowIndex, colIndex).Shape.TextFrame.TextRange.Font.Size = 20 ' Set the desired font size
        Next ppCell
    End If
    
    ' Save and close the PowerPoint presentation
    ppPres.Save
    ppPres.Close
    
    ' Quit the PowerPoint application
    ppApp.Quit
    
    ' Clean up
    Set ppCell = Nothing
    Set ppTable = Nothing
    Set ppShape = Nothing
    Set ppSlide = Nothing
    Set ppPres = Nothing
    Set ppApp = Nothing
End Sub
