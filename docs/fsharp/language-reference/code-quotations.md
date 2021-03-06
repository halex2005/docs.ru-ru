---
title: Цитирование кода
description: 'Узнайте о цитатах кода F #, языковой функции, позволяющей программно создавать выражения кода F # и работать с ними.'
ms.date: 08/13/2020
ms.openlocfilehash: dc37fdbd6cd29e5ee94e5c0186dfe2bfeb666f32
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557198"
---
# <a name="code-quotations"></a>Цитаты кода

В этой статье описываются *цитаты кода* , функции языка, позволяющие программно создавать выражения кода F # и работать с ними. Эта функция позволяет создать абстрактное дерево синтаксиса, представляющее код F #. Затем дерево абстрактного синтаксиса можно просмотреть и обработать в соответствии с потребностями приложения. Например, дерево можно использовать для создания кода F # или создания кода на другом языке.

## <a name="quoted-expressions"></a>Выражения в кавычках

*Заключенное в кавычки выражение* — это выражение F # в коде, которое отделяется таким образом, что оно не компилируется как часть программы, а компилируется в объект, представляющий выражение f #. Можно пометить выражение в кавычках одним из двух способов: с информацией о типе или без сведений о типе. Если вы хотите включить сведения о типах, используйте символы `<@` и `@>` для разделения выражения в кавычках. Если сведения о типах не требуются, используются символы `<@@` и `@@>` . В следующем коде показаны типизированные и нетипизированные предложения.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet501.fs)]

Обход большого дерева выражения выполняется быстрее, если не включать сведения о типе. Результирующий тип выражения, заключенного в кавычки с типизированными символами, — это `Expr<'T>` , где параметр типа имеет тип выражения, как определено алгоритмом вывода типа компилятора F #. При использовании цитат кода без сведений о типе тип выражения, заключенного в кавычки, является выражением типа, не являющимся универсальным типом [expr](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html). [Raw](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr-1.html#Raw) `Expr` Для получения нетипизированного объекта можно вызвать свойство RAW для типизированного класса `Expr` .

Существуют разнообразные статические методы, позволяющие программно создавать объекты выражений F # в `Expr` классе без использования заключенных в кавычки выражений.

Обратите внимание, что цитата кода должна включать выражение Complete. Например, для `let` привязки требуется как определение связанного имени, так и дополнительное выражение, использующее привязку. В подробном синтаксисе это выражение, следующее за `in` ключевым словом. На верхнем уровне в модуле это просто следующее выражение в модуле, но в кавычках оно требуется явным образом.

Поэтому следующее выражение является недопустимым.

```fsharp
// Not valid:
// <@ let f x = x + 1 @>
```

Однако следующие выражения являются допустимыми.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet502.fs)]

Для вычисления предложений F # необходимо использовать [средство оценки предложений f #](https://github.com/fsprojects/FSharp.Quotations.Evaluator). Он обеспечивает поддержку оценки и исполнения объектов выражений F #.

В кавычки F # также сохранены сведения об ограничениях типов. Рассмотрим следующий пример.

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

Ограничение, созданное `inline` функцией, сохраняется в коде кутоатион. `negate`Теперь можно вычислить форму куотатед функции.

## <a name="expr-type"></a>Тип выражения

Экземпляр `Expr` типа представляет выражение F #. Универсальные и неуниверсальные `Expr` типы описаны в документации по библиотеке F #. Дополнительные сведения см. в разделе Классы [FSharp. цитирований](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations.html) и [предложения. expr](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html).

## <a name="splicing-operators"></a>Операторы объединения

Объединение позволяет комбинировать цитаты с литеральным кодом с выражениями, созданными программно или из другой цитаты в виде кода. `%`Операторы и `%%` позволяют добавлять объект выражения F # в цитату кода. `%`Оператор используется для вставки объекта типизированного выражения в типизированную кавычку; `%%` оператор используется для вставки нетипизированного объекта выражения в нетипизированное предложение. Оба оператора являются унарными префиксными операторами. Таким образом `expr` , если является нетипизированным выражением типа `Expr` , следующий код является допустимым.

```fsharp
<@@ 1 + %%expr @@>
```

И если `expr` является типизированной кавычкой типа `Expr<int>` , следующий код является допустимым.

```fsharp
<@ 1 + %expr @>
```

## <a name="example"></a>Пример

### <a name="description"></a>Описание

В следующем примере показано использование цитат кода для помещения кода F # в объект выражения, а затем Печать кода F #, представляющего выражение. `println`Определена функция, которая содержит рекурсивную функцию `print` , которая отображает объект выражения F # (типа `Expr` ) в удобном формате. Существует несколько активных шаблонов в модулях [FSharp. цитирований. Patterns](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-patternsmodule.html) и [FSharp. цитирований. активный шаблон derivedpatterns](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html) , которые можно использовать для анализа объектов выражений. Этот пример не включает все возможные закономерности, которые могут появляться в выражении F #. Любой нераспознанный шаблон активирует совпадение с шаблоном шаблона ( `_` ) и подготавливается к просмотру с помощью `ToString` метода, который в `Expr` типе позволяет знать активный шаблон для добавления в выражение соответствия.

### <a name="code"></a>Код

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet601.fs)]

### <a name="output"></a>Выходные данные

```fsharp
fun (x:System.Int32) -> x + 1
a + 1
let f = fun (x:System.Int32) -> x + 10 in f 10
```

## <a name="example"></a>Пример

### <a name="description"></a>Описание

Вы также можете использовать три активных шаблона в [модуле експршапе](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html) для прохода по деревьям выражений с меньшим количеством активных шаблонов. Эти активные шаблоны могут оказаться полезными, если требуется пройти по дереву, но не требуется вся информация в большинстве узлов. При использовании этих шаблонов любое выражение F # соответствует одному из следующих трех шаблонов: `ShapeVar` , если выражение является переменной, `ShapeLambda` Если выражение является лямбда-выражением, или `ShapeCombination` Если выражение является любым другим. Если вы просматриваете дерево выражения с помощью активных шаблонов, как в предыдущем примере кода, необходимо использовать гораздо больше шаблонов для управления всеми возможными типами выражений F #, и код будет более сложен. Дополнительные сведения см. в разделе [експршапе. шапевар&#124;шапеламбда&#124;Шапекомбинатион Active Pattern](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html#(%20|ShapeVar|ShapeLambda|ShapeCombination|%20)).

Следующий пример кода можно использовать в качестве основания для более сложных обходов. В этом коде дерево выражения создается для выражения, включающего вызов функции, `add` . Активный шаблон [спеЦификкалл](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html#(%20|SpecificCall|_|%20)) используется для обнаружения любого вызова `add` в дереве выражения. Этот активный шаблон назначает аргументы вызова `exprList` значения. В этом случае существует только два, поэтому они извлекаются, и функция вызывается рекурсивно для аргументов. Результаты вставляются в цитату кода, которая представляет вызов с `mul` помощью оператора splice ( `%%` ). `println`Функция из предыдущего примера используется для вывода результатов.

Код в других активных ветвях шаблонов просто повторно создает одно и то же дерево выражения, поэтому единственное изменение в результирующем выражении — это изменение с `add` на `mul` .

### <a name="code"></a>Код

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet701.fs)]

### <a name="output"></a>Вывод

```fsharp
1 + Module1.add(2,Module1.add(3,4))
1 + Module1.mul(2,Module1.mul(3,4))
```

## <a name="see-also"></a>См. также

- [Справочник по языку F#](index.md)
