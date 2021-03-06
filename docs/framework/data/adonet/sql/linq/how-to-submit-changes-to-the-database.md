---
description: Дополнительные сведения см. в статье как отправлять изменения в базу данных.
title: Практическое руководство. Как отправить изменения в базу данных
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: 31d85d94c74315a127b18bd41b4d1d1a7fe7d0b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785862"
---
# <a name="how-to-submit-changes-to-the-database"></a>Практическое руководство. Как отправить изменения в базу данных

Независимо от количества изменений, произведенных над объектами, эти изменения выполняются только над репликам, содержащимся в памяти. Фактические данные в базе данных при этом не изменяются. Изменения не передаются на сервер до тех пор, пока не будет явно вызван метод <xref:System.Data.Linq.DataContext.SubmitChanges%2A> класса <xref:System.Data.Linq.DataContext>.  
  
 При вызове этого метода класс <xref:System.Data.Linq.DataContext> пытается преобразовать сделанные изменения в эквивалентные команды SQL. Можно использовать собственную пользовательскую логику для переопределения этих действий, но порядок отправки управляется службой, <xref:System.Data.Linq.DataContext> известной как *обработчик изменений*. Ниже представлена последовательность событий.  
  
1. При вызове метода <xref:System.Data.Linq.DataContext.SubmitChanges%2A> технология [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] просматривает набор известных объектов, чтобы определить, присоединены ли к ним новые экземпляры. При положительном результате новые экземпляры добавляются в набор отслеживаемых объектов.  
  
2. Все объекты, содержащие ожидающие изменения, упорядочиваются в последовательности объектов на основе зависимостей между ними. Объекты, изменения которых зависят от других объектов, располагаются после своих зависимостей.  
  
3. Непосредственно после передачи фактических изменений [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] начинает транзакцию для инкапсуляции ряда отдельных команд.  
  
4. Изменения объектов последовательно преобразуются в команды SQL и отправляются на сервер.  
  
 В данный момент любые ошибки, обнаруженные базой данных, приводят к остановке процесса отправки и вызову исключения. Выполняется откат всех изменений базы данных к состоянию до начала отправки. Класс <xref:System.Data.Linq.DataContext> по-прежнему содержит запись всех изменений. Поэтому можно попытаться исправить проблему и вызвать метод <xref:System.Data.Linq.DataContext.SubmitChanges%2A> еще раз, как показано в следующем примере кода.  
  
## <a name="example"></a>Пример  

 После успешного завершения транзакции, содержащей отправку, класс <xref:System.Data.Linq.DataContext> принимает изменения объектов, пропуская сведения об отслеживании изменений.  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Как обнаруживать и разрешать конфликты отправки](how-to-detect-and-resolve-conflicting-submissions.md)
- [Практическое руководство. Как управлять конфликтами изменений](how-to-manage-change-conflicts.md)
- [Загрузка примеров баз данных](downloading-sample-databases.md)
- [Внесение и отправка изменений данных](making-and-submitting-data-changes.md)
