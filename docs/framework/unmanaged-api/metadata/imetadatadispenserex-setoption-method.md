---
description: 'Дополнительные сведения о методе: IMetaDataDispenserEx:: SetOption'
title: Метод IMetaDataDispenserEx::SetOption
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.SetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::SetOption
helpviewer_keywords:
- IMetaDataDispenserEx::SetOption method [.NET Framework metadata]
- SetOption method [.NET Framework metadata]
ms.assetid: 9f1c7ccd-7fb2-41d8-aa00-24b823376527
topic_type:
- apiref
ms.openlocfilehash: 0fdaa280619eb750ea9357f590c3b91cf398608f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753514"
---
# <a name="imetadatadispenserexsetoption-method"></a>Метод IMetaDataDispenserEx::SetOption

Задает для указанного параметра заданное значение для текущей области метаданных. Параметр определяет, как обрабатываются вызовы к текущей области метаданных.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT SetOption (  
    [in] REFGUID optionId,
    [in] const VARIANT *pValue  
);  
```  
  
## <a name="parameters"></a>Параметры  

 `optionId`  
 окне Указатель на идентификатор GUID, указывающий параметр, который необходимо задать.  
  
 `pValue`  
 окне Значение, используемое для задания параметра. Тип этого значения должен быть вариантом типа указанного параметра.  
  
## <a name="remarks"></a>Remarks  

 В следующей таблице перечислены доступные идентификаторы GUID, `optionId` на которые может указывать параметр, и соответствующие допустимые значения `pValue` параметра.  
  
|Идентификатор GUID|Описание|`pValue` Параметр|  
|----------|-----------------|------------------------|  
|метадатачеккдупликатесфор|Определяет, какие элементы проверяются на наличие дубликатов. Каждый раз при вызове метода [IMetaDataEmit](imetadataemit-interface.md) , который создает новый элемент, можно попросить метод проверить, существует ли уже данный элемент в текущей области. Например, можно проверить наличие `mdMethodDef` элементов. в этом случае при вызове [IMetaDataEmit::D ефинемесод](imetadataemit-definemethod-method.md)будет проверять, не существует ли этот метод в текущей области. Эта проверка использует ключ, однозначно определяющий данный метод: родительский тип, имя и сигнатура.|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [корчеккдупликатесфор](corcheckduplicatesfor-enumeration.md) .|  
|метадатарефтодефчекк|Определяет, какие элементы, на которые имеются ссылки, преобразуются в определения. По умолчанию ядро метаданных оптимизирует код путем преобразования упоминаемого элемента в его определение, если элемент, на который указывает ссылка, фактически определен в текущей области.|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [коррефтодефчекк](correftodefcheck-enumeration.md) .|  
|метадатанотификатионфортокенмовемент|Определяет, какие повторное сопоставления токенов происходят при слиянии метаданных, создают обратные вызовы. Чтобы установить интерфейс [IMapToken](imaptoken-interface.md) , используйте метод [IMetaDataEmit:: сесандлер](imetadataemit-sethandler-method.md) .|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [корнотификатионфортокенмовемент](cornotificationfortokenmovement-enumeration.md) .|  
|метадатасетенк|Управляет поведением функции "изменить и продолжить" (ENC). В каждый момент времени может быть задан только один режим работы.|Параметр должен быть разновидностью типа UI4 и должен содержать значение перечисления [CorSetENC](corsetenc-enumeration.md) . Значение не является битовой маской.|  
|метадатаеррорифемитаутофордер|Элементы управления, которые выдают ошибки, не являющиеся заказами, создают обратные вызовы. Неупорядоченное порождение метаданных неустранимым; Однако при порождении метаданных в порядке, который подходит для механизма метаданных, метаданные более компактны, и поэтому их можно будет более эффективно искать. Используйте `IMetaDataEmit::SetHandler` метод, чтобы установить интерфейс [IMetaDataError](imetadataerror-interface.md) .|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [кореррорифемитаутофордер](corerrorifemitoutoforder-enumeration.md) .|  
|метадатаимпортоптион|Определяет, какие виды элементов, удаленных во время ENC, извлекаются перечислителем.|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [перечисления коримпортоптионс](corimportoptions-enumeration.md) .|  
|метадатасреадсафетйоптионс|Определяет, получает ли механизм метаданных блокировки потоков чтения/записи, тем самым обеспечивая потокобезопасность. По умолчанию механизм предполагает, что доступ осуществляется с помощью однопотокового вызова, поэтому блокировки не получаются. Клиенты отвечают за поддержание правильной синхронизации потоков при использовании API метаданных.|Параметр должен быть разновидностью типа UI4 и должен содержать значение перечисления [CorThreadSafetyOptions](corthreadsafetyoptions-enumeration.md) . Значение не является битовой маской.|  
|метадатаженератетцеадаптерс|Определяет, должен ли импортер библиотеки типов создавать адаптеры тесно связанных событий (обработки TCE) для контейнеров точек подключения COM.|Должен быть разновидностью типа BOOL. Если параметр `pValue` имеет значение `true` , программа импорта библиотек типов создает адаптеры обработки TCE.|  
|метадататипелибимпортнамеспаце|Задает пространство имен, отличное от используемого по умолчанию, для импортируемой библиотеки типов.|Значение должно быть либо значением NULL, либо вариантом типа BSTR. Если параметр `pValue` имеет значение null, текущее пространство имен устанавливается в NULL. в противном случае текущим пространством имен присваивается строка, которая хранится в ТИПЕ BSTR типа Variant.|  
|метадаталинкероптионс|Определяет, должен ли компоновщик создавать сборку или файл модуля платформа .NET Framework.|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений перечисления [CorLinkerOptions](corlinkeroptions-enumeration.md) .|  
|метадатарунтимеверсион|Указывает версию среды CLR, для которой построен этот образ. Версия хранится в виде строки, например "v 1.0.3705".|Должно быть задано значение null, VT_EMPTY значение или вариант типа BSTR. Если `pValue` параметр имеет значение null, для версии среды выполнения задано значение null. Если `pValue` имеет значение VT_EMPTY, то для версии задается значения по умолчанию, которое извлекается из версии Mscorwks.dll, в которой работает код метаданных. В противном случае версия среды выполнения задается как строка, которая хранится в типе BSTR типа Variant.|  
|метадатамержероптионс|Задает параметры для слияния метаданных.|Параметр должен быть разновидностью типа UI4 и должен содержать сочетание значений `MergeFlags` перечисления, описанное в файле корхдр. h.|  
|метадатапресервелокалрефс|Отключает оптимизацию локальных ссылок в определениях.|Должен содержать сочетание значений перечисления [корлокалрефпресерватион](corlocalrefpreservation-enumeration.md) .|  
  
## <a name="requirements"></a>Требования  

 **Платформа:** См. раздел [требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** COR. h  
  
 **Библиотека:** Используется в качестве ресурса в MsCorEE.dll  
  
 **Платформа .NET Framework версии:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Интерфейс IMetaDataDispenser](imetadatadispenser-interface.md)
