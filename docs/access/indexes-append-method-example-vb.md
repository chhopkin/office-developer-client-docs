---
title: "Indexes Append Method Example (VB)"
 
 
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
ms.topic: reference
  
localization_priority: Normal
ms.assetid: 71b18a5b-d000-5184-afac-c5d26b7f17e8
description: "The following code demonstrates how to create a new index. The index is on two columns in the table."
---

# Indexes Append Method Example (VB)

The following code demonstrates how to create a new index. The index is on two columns in the table.
  
```
 
' BeginCreateIndexVB 
Sub Main() 
 On Error GoTo CreateIndexError 
 
 Dim tbl As New Table 
 Dim idx As New ADOX.Index 
 Dim cat As New ADOX.Catalog 
 
 'Open the catalog. 
 ' Open the Catalog. 
 cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" &amp; _ 
 "Data Source='c:\Program Files\Microsoft Office\" &amp; _ 
 "Office\Samples\Northwind.mdb';" 
 
 ' Define the table and append it to the catalog 
 tbl.Name = "MyTable" 
 tbl.Columns.Append "Column1", adInteger 
 tbl.Columns.Append "Column2", adInteger 
 tbl.Columns.Append "Column3", adVarWChar, 50 
 cat.Tables.Append tbl 
 Debug.Print "Table 'MyTable' is added." 
 
 ' Define a multi-column index 
 idx.Name = "multicolidx" 
 idx.Columns.Append "Column1" 
 idx.Columns.Append "Column2" 
 
 ' Append the index to the table 
 tbl.Indexes.Append idx 
 Debug.Print "The index is appended to table 'MyTable'." 
 
 'Delete the table as this is a demonstration 
 cat.Tables.Delete tbl.Name 
 Debug.Print "Table 'MyTable' is deleted." 
 
 'Clean up 
 Set cat.ActiveConnection = Nothing 
 Set cat = Nothing 
 Set tbl = Nothing 
 Set idx = Nothing 
 Exit Sub 
 
CreateIndexError: 
 Set cat = Nothing 
 Set tbl = Nothing 
 Set idx = Nothing 
 
 If Err <> 0 Then 
 MsgBox Err.Source &amp; "-->" &amp; Err.Description, , "Error" 
 End If 
End Sub 
' EndCreateIndexVB 

```

