---
description: Дополнительные сведения о строках и DataRowView
title: Объекты DataRow и DataRowView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8f5eec26-b809-4aca-8778-7e202356d856
ms.openlocfilehash: d7700922a9ae76fb9898412b6a08394059e6e494
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724951"
---
# <a name="datarows-and-datarowviews"></a>Объекты DataRow и DataRowView

Представление <xref:System.Data.DataView> предоставляет перечисляемую коллекцию объектов <xref:System.Data.DataRowView>. Объекты **DataRowView** предоставляют значения в виде массивов объектов, индексируемых либо по имени, либо по порядковому номеру столбца в базовой таблице. Доступ к представлению <xref:System.Data.DataRow> , предоставляемому **DataRowView** , можно получить с помощью <xref:System.Data.DataRowView.Row%2A> свойства **DataRowView**.  
  
 При просмотре значений с помощью **DataRowView** <xref:System.Data.DataView.RowStateFilter%2A> свойство **DataView** определяет, какая версия строки базового объекта **DataRow** предоставляется. Сведения о доступе к разным версиям строк с помощью **DataRow** см. в разделе [состояния строк и версии строк](row-states-and-row-versions.md).  
  
 В следующем примере кода показаны все текущие и исходные значения в таблице.  
  
```vb  
Dim catView As DataView = New DataView(catDS.Tables("Categories"))  
Console.WriteLine("Current Values:")  
WriteView(catView)  
Console.WriteLine("Original Values:")  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal  
WriteView(catView)
  
Public Shared Sub WriteView(thisDataView As DataView)  
  Dim rowView As DataRowView  
  Dim i As Integer  
  
  For Each rowView In thisDataView  
    For i = 0 To thisDataView.Table.Columns.Count - 1  
      Console.Write(rowView(i) & vbTab)  
    Next  
    Console.WriteLine()  
  Next  
End Sub  
```  
  
```csharp  
DataView catView = new DataView(catDS.Tables["Categories"]);  
Console.WriteLine("Current Values:");  
WriteView(catView);  
Console.WriteLine("Original Values:");  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal;  
WriteView(catView);  
  
public static void WriteView(DataView thisDataView)  
{  
  foreach (DataRowView rowView in thisDataView)  
  {  
    for (int i = 0; i < thisDataView.Table.Columns.Count; i++)  
      Console.Write(rowView[i] + "\t");  
    Console.WriteLine();  
  }  
}  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.Data.DataRowVersion>
- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataView>
- <xref:System.Data.DataRowView>
- [Объекты DataView](dataviews.md)
- [Общие сведения об ADO.NET](../ado-net-overview.md)
