Excel formulas

=IF(TDS!A1<>FIN!A1,"TDS:"&TDS!A1&" and FIN:"&FIN!A1,"")

=IF(TDS_FIC!A1<>FIC!A1,"TDS_FIC:"&TDS_FIC!A1&" and FIC:"&FIC!A1,"")

=IF(TDS!A1<>FIC!A1,"TDS:"&TDS!A1&" and FIC:"&FIC!A1,"")

=IF(dealer!A1<>support!A1,"dealer:"&dealer!A1&" and support:"&support!A1,"")

=A1<>Sheet1!A1
=A1<>Main!A1

=IF(ISNUMBER(MATCH(cell,F:F(list),0)),1,0)

=countif(list(a;a),cell(a2)) -> for counting duplicates without case sensitive
=sum(--exact(list(a;a),cell(a2))

=IFERROR(VLOOKUP(A2,G1:K299300,3,0),"NOT IN RT TABLE")

Find if any of the column has 1 then return 1.

=sum(f2+


=IF(ISNUMBER(MATCH(E2,Q:Q,0)),1,IF(ISNUMBER(MATCH(E2,R:R,0)),2,IF(ISNUMBER(MATCH(E2,S:S,0)),3,"NOT FOUND")))


How to make Active row and column highlight:
Private Sub Worksheet_SelectionChange(ByVal Target As Range) If Target.Cells.Count > 1 Then Exit Sub Application.ScreenUpdating = False 'Clear the color of all cells Cells.Interior.ColorIndex = 0 With Target 'Highlight row and column of the selected cell .EntireRow.Interior.ColorIndex = 38 .EntireColumn.Interior.ColorIndex = 24 End With Application.ScreenUpdating = True End Sub


Search field:
=CHOOSECOLS(FILTER(_T24,ISNUMBER(SEARCH($B$1,_T24[ORIG_FIELD_IDENT]))+ISNUMBER(SEARCH($B$1,_T24[DICT_TEXT])),"NotFound"),1,2,7,8,9,10,11)
