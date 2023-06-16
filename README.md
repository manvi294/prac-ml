Sub ExportToPowerPoint()
    Dim PowerPointApp As Object
    Dim PowerPointPres As Object
    Dim PowerPointSlide As Object
    Dim ExcelRange As Range
    Dim PowerPointShape As Object
    Dim FilePath As String
    Dim TempFilePath As String
    
    ' Set the file path of the PowerPoint presentation
    FilePath = "C:\Path\to\PowerPoint.pptx"
    
    ' Set the range of data to be copied from Excel
    Set ExcelRange = ThisWorkbook.Sheets("Sheet1").Range("A1:D10")
    
    ' Create a new instance of PowerPoint
    Set PowerPointApp = CreateObject("PowerPoint.Application")
    
    ' Open the PowerPoint presentation
    Set PowerPointPres = PowerPointApp.Presentations.Open(FilePath)
    
    ' Add a new slide to the presentation
    Set PowerPointSlide = PowerPointPres.Slides.Add(1, 11) ' 11 represents the slide layout
    
    ' Copy the Excel range
    ExcelRange.Copy
    
    ' Paste the copied range onto the slide
    PowerPointSlide.Shapes.Paste.Select
    Set PowerPointShape = PowerPointApp.ActiveWindow.Selection.ShapeRange
    
    ' Set the position and size of the pasted range
    PowerPointShape.Left = 100
    PowerPointShape.Top = 100
    
    ' Save and close the PowerPoint presentation
    PowerPointPres.Save
    PowerPointPres.Close
    
    ' Clean up the PowerPoint objects
    Set PowerPointShape = Nothing
    Set PowerPointSlide = Nothing
    Set PowerPointPres = Nothing
    PowerPointApp.Quit
    Set PowerPointApp = Nothing
End Sub
