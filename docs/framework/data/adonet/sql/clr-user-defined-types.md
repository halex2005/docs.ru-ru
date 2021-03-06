---
description: 'Дополнительные сведения: типы User-Defined CLR'
title: Пользовательские типы CLR
ms.date: 03/30/2017
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
ms.openlocfilehash: f1732c254d3bf3cb8aa4ba727c420c46ef55c2cf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663369"
---
# <a name="clr-user-defined-types"></a>Пользовательские типы CLR

Microsoft SQL Server предоставляет поддержку определяемых пользователем типов данных (UDT), реализованную при помощи среды CLR в Microsoft .NET Framework. Среда CLR встроена в SQL Server. Этот механизм позволяет расширять систему типов базы данных. Определяемые пользователем типы дают возможность расширять систему типов данных SQL Server, а также позволяют определять сложные структурированные типы.  
  
 Для архитектуры приложений использование определяемых пользователем типов имеет два основных преимущества.  
  
- Строгая инкапсуляция (и на клиенте, и на сервере) между внутренним состоянием и внешней функциональностью.  
  
- Тесная интеграция между другими связанными возможностями сервера. После определения собственного типа данных его можно использовать во всех контекстах, где в SQL Server можно использовать системные типы, включая определения столбцов, а также в качестве переменных, параметров, результатов функций, курсоров, триггеров и репликации.  
  
 Дополнительные сведения см. в документации по [SQL Server](/sql) версии SQL Server, которую вы используете.
  
 **Документация по SQL Server**
  
1. [Пользовательские типы CLR](/sql/relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types)  
  
## <a name="see-also"></a>См. также

- [Общие сведения об ADO.NET](../ado-net-overview.md)
