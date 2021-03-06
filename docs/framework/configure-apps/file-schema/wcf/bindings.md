---
description: 'Дополнительные сведения: <bindings>'
title: <bindings>
ms.date: 01/22/2018
ms.assetid: b62cd369-5409-4030-8490-9759a462dd3a
ms.openlocfilehash: 2cf5b42b8478e34a528cd36435023cac62bf0c1e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99639384"
---
# \<bindings>

Элемент можно использовать `bindings` для настройки коллекции стандартных и пользовательских привязок для Windows Communication Foundation (WCF). Каждый элемент коллекции представляет собой элемент `binding`, который может быть идентифицирован по своему уникальному имени `name`. Службы используют привязки, связывая их с помощью параметра `name`. Начиная с платформа .NET Framework 4, привязки и поведения не обязательно должны иметь имя. Дополнительные сведения о конфигурации по умолчанию и привязках и поведении, которые не имеют имен, см. в разделе [упрощенная конфигурация](../../../wcf/simplified-configuration.md) и [упрощенная конфигурация для служб WCF](../../../wcf/samples/simplified-configuration-for-wcf-services.md).

## <a name="system-provided-bindings"></a>Привязки, предоставляемые системой

Привязки, предоставляемые системой, скрывают сложность стека обмена сообщениями WCF. Приложениям, использующим предоставляемые системой привязки, не требуется полный контроль над стеком. Атрибутами в каждой привязке, предоставляемой системой, являются атрибуты, наиболее подходящие для области применения привязки.

В разделе конфигурации для каждой привязки, предоставляемой системой, можно определить несколько конфигураций, используемых для настройки привязки. Каждая конфигурация идентифицируется по уникальному имени.

Невозможно добавить элементы или атрибуты к привязке, предоставляемой системой. Для этого следует реализовать пользовательскую привязку, как описано в разделе [пользовательские привязки](#custom-bindings) . Можно определить пользовательскую привязку, которая имитирует предоставляемую системой привязку и добавляет несколько параметров, которые пользовательское приложение хочет контролировать.  

Список привязок, предоставляемых системой, см. в разделе [привязки, предоставляемые системой](../../../wcf/system-provided-bindings.md).

## <a name="custom-bindings"></a>Пользовательские привязки

Пользовательские привязки предоставляют полный контроль над стеком обмена сообщениями WCF. Отдельная привязка определяет стек обмена сообщениями, задавая элементы конфигурации для элементов стека в том порядке, в котором они присутствуют в стеке. Каждый элемент определяет и настраивает один элемент стека. В каждой пользовательской привязке должен быть один и только один элемент `transport`. Без этого элемента стек обмена сообщениями является неполным.

Важен порядок, в котором элементы присутствуют в стеке, поскольку именно в этом порядке к сообщению применяются операции. Необходим следующий порядок элементов стека:  

1. Транзакции (необязательный)  

2. Надежный обмен сообщениями (необязательно)  

3. Безопасность (необязательный)  

4. Кодировщик  

5. Транспорт  

 Пользовательские привязки идентифицируются по атрибуту `name`. Дополнительные сведения о пользовательских привязках см. в разделе [пользовательские привязки](../../../wcf/extending/custom-bindings.md).

## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.BindingsSection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Binding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>
- [Привязки](../../../wcf/bindings.md)
- [Пользовательские привязки](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
