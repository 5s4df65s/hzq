# Excel_PowerQuery_Autocolumns
let
    源 = Folder.Files("C:\Users\LZBHZQ\Desktop\临时文件\0_DATA"),
    删除的其他列 = Table.SelectColumns(源,{"Content"}),
    已添加自定义 = Table.AddColumn(删除的其他列, "sorce", each Excel.Workbook([Content],true)),
    #"展开的“sorce”" = Table.ExpandTableColumn(已添加自定义, "sorce", {"Name", "Data", "Item", "Kind", "Hidden"}, {"Name", "Data", "Item", "Kind", "Hidden"}),
    删除的其他列1 = Table.SelectColumns(#"展开的“sorce”",{"Data"}),
    列名=List.Select(Table.ColumnNames(删除的其他列1{0}[Data]),each _<>null),
    #"展开的“Data”" = Table.ExpandTableColumn(删除的其他列1, "Data", 列名, 列名)
in
    #"展开的“Data”"
