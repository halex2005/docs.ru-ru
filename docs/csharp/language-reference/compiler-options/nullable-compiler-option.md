---
description: -nullable (параметры компилятора C#)
title: -nullable (параметры компилятора C#)
author: IEvangelist
ms.author: dapine
ms.date: 06/04/2020
f1_keywords:
- /nullable
helpviewer_keywords:
- nullable compiler option [C#]
- /nullable compiler option [C#]
- -nullable compiler option [C#]
ms.openlocfilehash: 68857d0cb4d0cd1177506e0b7ce897d2cfc3aa5b
ms.sourcegitcommit: 30e9e11dfd90112b8eec6406186ba3533f21eba1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2020
ms.locfileid: "95099228"
---
# <a name="-nullable-c-compiler-options"></a>-nullable (параметры компилятора C#)

Параметр **-nullable** позволяет указать контекст, допускающий значение NULL.

## <a name="syntax"></a>Синтаксис

```console
-nullable[+ | -]
-nullable:{enable | disable | warnings | annotations}
```

## <a name="arguments"></a>Аргументы

`+` &#124; `-`  
При указании `+` или параметра **-nullable** компилятор включит контекст, допускающий значение NULL. При указании `-`, который действует, если не указан параметр **-nullable**, отключается контекст, допускающий значение NULL.

`enable` &#124; `disable` &#124; `warnings` &#124; `annotations`  
Указывает параметр контекста, допускающий значение NULL. Используется аналогично `+` или `-`, чтобы включать и отключать контекст, но обеспечивает больший уровень детализации для контекста, допускающего значение NULL. Аргумент `enable`, который действует так же, как параметр **-nullable**, включает контекст, допускающий значение NULL. При указании `disable` будет отключен контекст, допускающий значение NULL. При указании аргумента `warnings` **-nullable:warnings** будет включен контекст предупреждения, допускающий значение NULL. При указании аргумента `annotations`, **-nullable:annotations**, будет включен контекст с заметками о допустимости значений NULL.

## <a name="remarks"></a>Примечания

Анализ потока используется для определения допустимости значений NULL в переменных в исполняемом коде. Выводимая допустимость переменной значения NULL не зависит от объявленной в переменной допустимости значения NULL. Вызовы методов анализируются, даже если они условно опущены. Например, <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> в режиме выпуска.

Вызов методов, снабженных следующими атрибутами, также повлияет на анализ потока:

- Простые предварительные условия: <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute> и <xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute>
- Простые постусловия: <xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute> и <xref:System.Diagnostics.CodeAnalysis.NotNullAttribute>
- Условные постусловия: <xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute> и <xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute>
- <xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute> (например, `DoesNotReturnIf(false)` для <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>) и <xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute>
- <xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute>
- Постусловия элемента: <xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String)> и <xref:System.Diagnostics.CodeAnalysis.MemberNotNullAttribute.%23ctor(System.String[])>

> [!IMPORTANT]
> Глобальный контекст, допускающий значения NULL, не применяется для созданных файлов кода. Независимо от этого параметра, контекст, допускающий значение NULL, *отключен* для любого исходного файла, помеченного как созданный. Существует четыре способа пометки файла как созданного:
>
> 1. В файле. editorconfig укажите `generated_code = true` в разделе, который применяется к этому файлу.
> 1. Вставьте `<auto-generated>` или `<auto-generated/>` в комментарий в верхней части файла. Он может находиться в любой строке комментария, однако блок комментариев должен быть первым элементом в файле.
> 1. Имя файла следует начинать с *TemporaryGeneratedFile_*
> 1. В конце имени файла следует указать *.designer.cs*, *.generated.cs*, *.g.cs* или *.g.i.cs*.
>
> Генераторы могут явно использовать директиву препроцессора [`#nullable`](../preprocessor-directives/preprocessor-nullable.md).

### <a name="to-set-this-compiler-option-in-a-project"></a>Установка данного параметра компилятора в проекте

Измените файл *CSPROJ*, добавив тег `<Nullable>` в иерархию `Project/PropertyGroup`:

```xml
<Project Sdk="...">

  <PropertyGroup>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>См. также

- [Параметры компилятора C# ](./index.md)
- [Директивы препроцессора`#nullable`](../preprocessor-directives/preprocessor-nullable.md)
- [Ссылочные типы, допускающие значение NULL](../../nullable-references.md)
