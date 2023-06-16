Sub ExportToPowerPoint()
    Dim PowerPointApp As Object
    Dim PowerPointPres As Object
    Dim PowerPointSlide As Object
    Dim ExcelRange As Range
    Dim FilePath As String
    
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
    
    ' Copy the Excel range and paste it into the PowerPoint slide
    ExcelRange.Copy
    PowerPointSlide.Shapes.PasteSpecial(DataType:=2) ' 2 represents a picture format
    
    ' Save and close the PowerPoint presentation
    PowerPointPres.Save
    PowerPointPres.Close
    
    ' Clean up the PowerPoint objects
    Set PowerPointSlide = Nothing
    Set PowerPointPres = Nothing
    PowerPointApp.Quit
    Set PowerPointApp = Nothing
End Sub
