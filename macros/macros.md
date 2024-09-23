Sub SaveAttachments()
Dim objItem As Object
Dim objAttachment As Outlook.Attachment
Dim saveFolder As String

saveFolder = "C:\Users\1653764\Sprint\Sprint41\TDS-FINDailyMonitoring\"
For Each objItem In Application.ActiveExplorer.Selection
    If TypeOf objItem Is MailItem Then
        For Each objAttachment In objItem.Attachments
            objAttachment.SaveAsFile (saveFolder) & objAttachment.FileName
        Next objAttachment
    End If
Next objItem

End Sub



Sub HighlightUniqueValues()
    Dim cell As Range
    Dim uniqueValues As New Collection
    Dim colorIndex As Integer
    Dim ws As Worksheet
    Dim lastRow As Long
    Dim rng As Range
    
    Set ws = ActiveSheet
    ws.Cells.FormatConditions.Delete
    
    For Each cell In Selection
    If Not Contains(uniqueValues, cell.Value) Then
        uniqueValues.Add cell.Value
        colorIndex = colorIndex + 2
        With ws.Range(ws.Cells(cell.Row, 2), ws.Cells(cell.Row, 6)).Cells.FormatConditions.Add(Type:=xlCellValue, Operator:=xlEqual, Formula1:=cell.Value)
            .Interior.colorIndex = colorIndex
        End With
    End If
    Next cell
        
End Sub

Function Contains(col As Collection, val As Variant)
On Error Resume Next
Contains = col(val) > 0
On Error GoTo 0
End Function
