Dim rowCount As Long
        rowCount = .DataBodyRange.Rows.Count
        
        Dim i As Long
        For i = 2 To rowCount Step 2
            .ListRows(i).Range.Interior.Color = RGB(204, 230, 255) ' Light sky blue color
        Next i