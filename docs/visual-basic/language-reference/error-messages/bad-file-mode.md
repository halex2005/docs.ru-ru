---
description: 'Дополнительные сведения: неправильный режим файла'
title: Недопустимый режим файла
ms.date: 07/20/2015
f1_keywords:
- vbrID54
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
ms.openlocfilehash: da792407fb37f5c206be7ff39da14d314ef1e2d2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797085"
---
# <a name="bad-file-mode"></a>Недопустимый режим файла

Инструкции, используемые для манипулирования содержимым файлов, должны соответствовать режиму, в котором был открыт файл. Возможные причины:  
  
- `FilePutObject`Оператор или `FileGetObject` указывает последовательный файл.  
  
- `Print`Оператор указывает файл, Открытый для режима доступа, отличного от `Output` или `Append` .  
  
- `Input`Оператор указывает файл, Открытый для режима доступа, отличного от`Input`  
  
- Попытка записи в файл, доступный только для чтения.  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
- Убедитесь `FilePutObject` , что `FileGetObject` ссылки ссылаются только на файлы, открытые для `Random` или `Binary` Access.  
  
- Убедитесь `Print` , что файл открыт для `Output` `Append` режима доступа или. В противном случае используйте другую инструкцию для размещения данных в файле или повторно откройте файл в соответствующем режиме.  
  
- Убедитесь `Input` , что файл открыт для `Input` . В противном случае используйте другую инструкцию для размещения данных в файле или повторного открытия файла в соответствующем режиме.  
  
- При записи в файл, доступный только для чтения, измените состояние чтения/записи файла или не пытайтесь выполнить запись в него.  
  
- Используйте функциональность объекта `My.Computer.FileSystem` .  
  
## <a name="see-also"></a>См. также

- <xref:Microsoft.VisualBasic.FileSystem>
- [Устранение неполадок: Чтение из текстовых файлов и запись в такие файлы](../../developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
