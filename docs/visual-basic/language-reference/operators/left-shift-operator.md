---
description: 'Дополнительные сведения о операторе:  << (Visual Basic)'
title: Оператор <<
ms.date: 07/20/2015
f1_keywords:
- vb.<<
helpviewer_keywords:
- bit shift operators [Visual Basic]
- << operator [Visual Basic]
- operator <<, Visual Basic left shift operator
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
ms.openlocfilehash: 079af61e5c4ce3834db0877feace724c74c8169c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99665631"
---
# <a name="-operator-visual-basic"></a>\<\< Оператор (Visual Basic)

Выполняет арифметический сдвиг битового шаблона влево.  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
result = pattern << amount  
```  
  
## <a name="parts"></a>Компоненты  

 `result`  
 Обязательный элемент. Целое числовое значение. Результат сдвига битового шаблона. Тип данных такой же, как для `pattern`.  
  
 `pattern`  
 Обязательный. Целое числовое выражение. Битовый шаблон, подлежащий сдвигу. Данные должны быть целого типа (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` или `ULong`).  
  
 `amount`  
 Обязательный. Числовое выражение. Количество разрядов, на которое следует сдвинуть битовый шаблон. Данные должны относиться к типу `Integer` или допускать расширение до типа `Integer`.  
  
## <a name="remarks"></a>Remarks  

 Арифметические сдвиги не являются циклическими, то есть биты, сдвинутые за пределы результата, не переносятся на другой конец. При выполнении арифметического сдвига влево биты, сдвинутые за пределы диапазона результирующего типа данных, отбрасываются, а позиции битов, освобожденные справа, устанавливаются в ноль.  
  
 Чтобы предотвратить сдвиг на больше бит, чем может вместить результат, Visual Basic маскирует значение `amount` с маской размера, соответствующей типу данных `pattern` . Двоичные значения и этих значений используются для величины сдвига. Ниже приведены маски размера.  
  
|Тип данных `pattern`|Маска размера (десятичная)|Маска размера (шестнадцатеричная)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 Если `amount` равен нулю, значение `result` идентично значению `pattern` . Если `amount` имеет отрицательное значение, оно принимается в качестве значения без знака и маскируется с соответствующей маской размера.  
  
 Арифметические сдвиги никогда не создают исключений переполнения.  
  
> [!NOTE]
> `<<`Оператор можно *перегрузить*, что означает, что класс или структура может переопределить свое поведение, когда операнд имеет тип этого класса или структуры. Если код использует этот оператор для такого класса или структуры, убедитесь, что вы понимаете его переопределенное поведение. Для получения дополнительной информации см. [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Пример  

 В следующем примере оператор используется `<<` для выполнения арифметических сдвигов влево по целочисленным значениям. Результат всегда имеет тот же тип данных, что и выражение, для которого выполняется сдвиг.  
  
 [!code-vb[VbVbalrOperators#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#12)]  
  
 Результаты предыдущего примера выглядят следующим образом:  
  
- `result1` — 192 (0000 0000 1100 0000).  
  
- `result2` — 3072 (0000 1100 0000 0000).  
  
- `result3` — 32768 (1000 0000 0000 0000).  
  
- `result4` — 384 (0000 0001 1000 0000).  
  
- `result5` равно 0 (смещено 15 позиций влево).  
  
 Сумма сдвига для `result4` вычисляется как 17 и 15, что равно 1.  
  
## <a name="see-also"></a>См. также

- [Операторы сдвига битов](bit-shift-operators.md)
- [Операторы присваивания](assignment-operators.md)
- [ Оператор<<=](left-shift-assignment-operator.md)
- [Порядок применения операторов в Visual Basic](operator-precedence.md)
- [Список операторов, сгруппированных по функциональному назначению](operators-listed-by-functionality.md)
- [Арифметические операторы в Visual Basic](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
