---
description: 'Дополнительные сведения о: BC36532: вложенная функция не имеет сигнатуры, совместимой с делегатом<delegatename>'
title: Вложенная функция не имеет сигнатуры, совместимой с делегатом "<delegatename>"
ms.date: 07/20/2015
f1_keywords:
- vbc36532
- bc36532
helpviewer_keywords:
- BC36532
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
ms.openlocfilehash: 2220faacdac065718a302ef7b086f99bf1e16cef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795668"
---
# <a name="bc36532-nested-function-does-not-have-a-signature-that-is-compatible-with-delegate-delegatename"></a>BC36532: вложенная функция не имеет сигнатуры, совместимой с делегатом " \<delegatename> "

Лямбда-выражение было назначено делегату с несовместимой сигнатурой. Например, в следующем коде делегат `Del` имеет два целочисленных параметра.

```vb
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer
```

Эта ошибка возникает, если лямбда-выражение с одним аргументом объявлено как тип `Del` :

```vb
' Neither of these is valid.
' Dim lambda1 As Del = Function(n As Integer) n + 1
' Dim lambda2 As Del = Function(n) n + 1
```

**Идентификатор ошибки:** BC36532

## <a name="to-correct-this-error"></a>Исправление ошибки

Измените либо определение делегата, либо назначенное лямбда-выражение, чтобы сигнатуры были совместимыми.

## <a name="see-also"></a>См. также

- [Неявное преобразование делегата](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [Лямбда-выражения](../../programming-guide/language-features/procedures/lambda-expressions.md)
