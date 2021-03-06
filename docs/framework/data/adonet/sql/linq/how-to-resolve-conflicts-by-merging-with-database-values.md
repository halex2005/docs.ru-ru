---
description: Дополнительные сведения см. в статье как разрешить конфликты путем слияния со значениями базы данных.
title: Практическое руководство. Как разрешать конфликты путем слияния значений базы данных
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1988b79c-3bfc-4c5c-a08a-86cf638bbe17
ms.openlocfilehash: 83cae4c98fdd2e51065c66d36ef04202bdc86c9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767769"
---
# <a name="how-to-resolve-conflicts-by-merging-with-database-values"></a>Практическое руководство. Как разрешать конфликты путем слияния значений базы данных

Чтобы согласовать различия между ожидаемыми и фактическими значениями базы данных до повторной отправки изменений, можно воспользоваться <xref:System.Data.Linq.RefreshMode.KeepChanges> для слияния значений базы данных с текущими значениями члена клиента. Дополнительные сведения см. в разделе [Оптимистическая блокировка: обзор](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> Во всех случаях запись на клиенте сначала обновляется путем извлечения обновленных данных из базы данных. Это действие гарантирует успешное выполнение следующей попытки обновления при тех же проверках параллелизма.  
  
## <a name="example"></a>Пример  

 В данном сценарии, когда Пользователь1 пытается отправить изменения, возникает исключение <xref:System.Data.Linq.ChangeConflictException>, поскольку Пользователь2 в это время изменил столбцы "Помощник" и "Отдел". Эта ситуация представлена в следующей таблице.  
  
||Manager|Помощник|отдел;|  
|------|-------------|---------------|----------------|  
|Исходное состояние базы данных при отправке запросов Пользователем1 и Пользователем2.|Алексеи|Мария|Sales|  
|Пользователь1 готовится отправить изменения.|Алексей||Marketing|  
|Пользователь2 уже отправил изменения.||Инна|Служба|  
  
 Пользователь1 решает устранить этот конфликт путем объединения значений базы данных с текущими значениями члена клиента. Ожидаемый результат: значения базы данных будут переопределены только при изменении значения текущим набором изменений.  
  
 При устранении Пользователем1 конфликта с помощью <xref:System.Data.Linq.RefreshMode.KeepChanges> результат в базе данных будет соответствовать данным в следующей таблице.  
  
||Manager|Помощник|отдел;|  
|------|-------------|---------------|----------------|  
|Новое состояние после устранения конфликта.|Алексей<br /><br /> (от Пользователя1)|Инна<br /><br /> (от Пользователя2)|Marketing<br /><br /> (от Пользователя1)|  
  
 В следующем примере показано объединение значений базы данных с текущими значениями члена клиента (если клиент также не изменил это значение). Конфликты проверки или пользовательской обработки отдельных членов не возникают.  
  
 [!code-csharp[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#3)]
 [!code-vb[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#3)]  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Как разрешать конфликты путем переписывания значений базы данных](how-to-resolve-conflicts-by-overwriting-database-values.md)
- [Практическое руководство. Как разрешать конфликты параллелизма путем сохранения значений базы данных](how-to-resolve-conflicts-by-retaining-database-values.md)
- [Практическое руководство. Как управлять конфликтами изменений](how-to-manage-change-conflicts.md)
