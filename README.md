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
    
    ' Create a temporary PDF file path to save the range as a PDF
    TempFilePath = Environ("TEMP") & "\TempRange.pdf"
    
    ' Print the range to a PDF file
    ExcelRange.ExportAsFixedFormat Type:=xlTypePDF, Filename:=TempFilePath
    
    ' Create a new instance of PowerPoint
    Set PowerPointApp = CreateObject("PowerPoint.Application")
    
    ' Open the PowerPoint presentation
    Set PowerPointPres = PowerPointApp.Presentations.Open(FilePath)
    
    ' Add a new slide to the presentation
    Set PowerPointSlide = PowerPointPres.Slides.Add(1, 11) ' 11 represents the slide layout
    
    ' Insert the PDF file onto the slide
    Set PowerPointShape = PowerPointSlide.Shapes.AddOLEObject(Left:=100, Top:=100, Width:=300, Height:=200, FileName:=TempFilePath, DisplayAsIcon:=False)
    
    ' Save and close the PowerPoint presentation
    PowerPointPres.Save
    PowerPointPres.Close
    
    ' Clean up the PowerPoint objects
    Set PowerPointShape = Nothing
    Set PowerPointSlide = Nothing
    Set PowerPointPres = Nothing
    PowerPointApp.Quit
    Set PowerPointApp = Nothing
    
    ' Delete the temporary PDF file
    Kill TempFilePath
End Sub
