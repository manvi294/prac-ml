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
    
    ' Create a temporary image file to store the copied range
    TempFilePath = Environ("TEMP") & "\TempImage.png"
    
    ' Copy the Excel range as an image to the clipboard
    ExcelRange.CopyPicture Appearance:=xlScreen, Format:=xlPicture
    
    ' Create a new instance of PowerPoint
    Set PowerPointApp = CreateObject("PowerPoint.Application")
    
    ' Open the PowerPoint presentation
    Set PowerPointPres = PowerPointApp.Presentations.Open(FilePath)
    
    ' Add a new slide to the presentation
    Set PowerPointSlide = PowerPointPres.Slides.Add(1, 11) ' 11 represents the slide layout
    
    ' Paste the copied range as an image on the slide
    Set PowerPointShape = PowerPointSlide.Shapes.AddPicture(FileName:=TempFilePath, LinkToFile:=msoFalse, SaveWithDocument:=msoTrue, Left:=100, Top:=100, Width:=300, Height:=200)
    
    ' Save and close the PowerPoint presentation
    PowerPointPres.Save
    PowerPointPres.Close
    
    ' Clean up the PowerPoint objects
    Set PowerPointShape = Nothing
    Set PowerPointSlide = Nothing
    Set PowerPointPres = Nothing
    PowerPointApp.Quit
    Set PowerPointApp = Nothing
    
    ' Delete the temporary image file
    Kill TempFilePath
End Sub
