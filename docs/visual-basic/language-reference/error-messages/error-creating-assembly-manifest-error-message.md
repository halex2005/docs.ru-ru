---
description: 'Дополнительные сведения о: BC30140: ошибка при создании манифеста сборки: <error message>'
title: 'Ошибка при создании манифеста сборки: <error message>'
ms.date: 07/20/2015
f1_keywords:
- bc30140
- vbc30140
helpviewer_keywords:
- BC30140
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
ms.openlocfilehash: 4116f3293a36f4592712c3e39c988aa730753de4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796539"
---
# <a name="bc30140-error-creating-assembly-manifest-error-message"></a>BC30140: ошибка при создании манифеста сборки: \<error message>

Компилятор Visual Basic вызывает компоновщик сборок (Al.exe, также известный как ALink) для создания сборки с манифестом. Компоновщик сообщил об ошибке на этапе предварительного выпуска процедуры создания сборки.

 Такая ситуация может возникнуть при наличии проблем с указанным файлом ключа или контейнером ключей. Чтобы использовать для сборки полную подпись, необходимо предоставить допустимый файл ключа с информацией об открытом и закрытом ключах. Чтобы использовать для сборки отложенную подпись, необходимо установить флажок **Только отложенная подпись** и предоставить допустимый файл ключа с информацией о ключах. При использовании отложенной подписи для сборки наличие закрытого ключа не требуется. Дополнительные сведения см. в разделе [Как подписать сборку строгим именем](../../../standard/assembly/sign-strong-name.md).

 **Идентификатор ошибки:** BC30140

## <a name="to-correct-this-error"></a>Исправление ошибки

1. Изучите сообщение об ошибке в кавычках и ознакомьтесь с разделом [Al.exe](../../../framework/tools/al-exe-assembly-linker.md). дополнительные объяснения и советы по ошибке AL1019

2. Если ошибка не устранена, соберите сведения об условиях ее возникновения и уведомите службу технической поддержки Майкрософт.

## <a name="see-also"></a>См. также раздел

- [Практическое руководство. Подписание сборки строгим именем](../../../standard/assembly/sign-strong-name.md)
- [Страница "Подписывание" в конструкторе проектов](/visualstudio/ide/reference/signing-page-project-designer)
- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [Обращайтесь к нам](/visualstudio/ide/feedback-options)
