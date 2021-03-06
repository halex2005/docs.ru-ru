---
title: Добавление содержимого в текстовое поле с помощью модели автоматизации пользовательского интерфейса
description: См. Пример добавления содержимого в однострочное текстовое поле с помощью Microsoft UI Automation в .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adding content to text boxes
- text boxes, adding content
- UI Automation, adding content to text boxes
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
ms.openlocfilehash: 9108cb586700474f7f855751000944212a3cef29
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235731"
---
# <a name="add-content-to-a-text-box-using-ui-automation"></a>Добавление содержимого в текстовое поле с помощью модели автоматизации пользовательского интерфейса

> [!NOTE]
> Эта документация предназначена для разработчиков .NET Framework, желающих использовать управляемые классы [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , заданные в пространстве имен <xref:System.Windows.Automation> . Последние сведения о [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]см. в разделе [API автоматизации Windows. Автоматизация пользовательского интерфейса](/windows/win32/winauto/entry-uiauto-win32).  
  
 Этот раздел содержит пример кода, демонстрирующий, как использовать [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] для вставки текста в однострочное текстовое поле. Альтернативный метод предоставляется для многострочных и многофункциональных элементов управления текстом, где [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] неприменимо. Для сравнения в примере также демонстрируется использование методов Win32 для выполнения одинаковых результатов.  
  
## <a name="example"></a>Пример  

 В следующем примере выполняется пошаговая последовательность элементов управления текстом в целевом приложении. Каждый элемент управления "текст" тестируется, чтобы определить, <xref:System.Windows.Automation.ValuePattern> можно ли получить объект из него с помощью <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> метода. Если элемент управления "текст" поддерживает <xref:System.Windows.Automation.ValuePattern> , <xref:System.Windows.Automation.ValuePattern.SetValue%2A> метод используется для вставки пользовательской строки в элемент управления Text. В противном случае <xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=nameWithType> используется метод.  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## <a name="see-also"></a>См. также

- [Пример вставки текста TextPattern](/previous-versions/dotnet/netframework-3.5/ms771478(v=vs.90))
