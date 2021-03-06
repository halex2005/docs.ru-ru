---
title: События времени выполнения метода
description: Ознакомьтесь с событиями среды выполнения .NET, собирающими диагностические сведения о методах, таких как события методов CLR, маркер метода CLR или подробные события в методах CLR, а также событие methodjittingstarted.
ms.date: 11/13/2020
helpviewer_keywords:
- Method events (CoreCLR)
- ETW, EventPipe, LTTng method events (CoreCLR)
ms.openlocfilehash: f9d08efa420670cf7a8c863f115ff270998f2dca
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "96594041"
---
# <a name="net-runtime-method-events"></a>События метода среды выполнения .NET

Эти события собирают сведения, связанные с методами. Полезные данные этих событий необходимы для разрешения символов. Кроме того, эти события предоставляют полезную информацию, такую как методы, которые загружаются и выгружаются. Дополнительные сведения об использовании этих событий в целях диагностики см. в разделе [ведение журнала и трассировка приложений .NET](../../core/diagnostics/logging-tracing.md) .

Все события методов имеют уровень «Информационный (4)». Все подробные события методов имеют уровень «Подробный (5)».

Все события методов вызываются ключевыми словами `JITKeyword` (0x10) или `NGenKeyword` (0x20) при использовании поставщика среды выполнения или ключевыми словами `JitRundownKeyword` (0x10) или `NGENRundownKeyword` (0x20) при использовании поставщика очистки.

Версии v2 этих событий включают Режитид, а версии v1 — нет.

## <a name="methodload_v1-event"></a>MethodLoad_V1 событие

В таблице ниже представлены сведения о событии.

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodLoad_V1`|141|Вызывается, когда метод является JIT-загружаемым или загружается образ NGEN. Динамические и универсальные методы не используют эту версию для загрузки методов. Вспомогательные методы JIT никогда не используют эту версию.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Информационный (4)|
|`NGenKeyword` (0x20)|Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес метода.|
|`MethodSize`|`win:UInt32`|Размер метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод с кодом, скомпилированным JIT-компилятором (в противном случае машинный код образа NGEN).<br /><br /> 0x8: вспомогательный метод.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodload_v2-event"></a>MethodLoad_V2 событие

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`MethodLoad_V2`|141|Вызывается, когда метод является JIT-загружаемым или загружается образ NGEN. Динамические и универсальные методы не используют эту версию для загрузки методов. Вспомогательные методы JIT никогда не используют эту версию.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Информационный (4)|
|`NGenKeyword` (0x20)|Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес метода.|
|`MethodSize`|`win:UInt32`|Размер метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод с кодом, скомпилированным JIT-компилятором (в противном случае машинный код образа NGEN).<br /><br /> 0x8: вспомогательный метод.|
|`ReJITID`|`win:UInt64`|Идентификатор ReJIT метода.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodunload_v1-event"></a>MethodUnLoad_V1 событие

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`MethodUnLoad_V1`|142|Вызывается, когда выгружается модуль или уничтожается домен приложения. Динамические методы никогда не используют эту версию для выгрузки методов.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Информационный (4)|
|`NGenKeyword` 0x20|Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес метода.|
|`MethodSize`|`win:UInt32`|Размер метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод с кодом, скомпилированным JIT-компилятором (в противном случае машинный код образа NGEN).<br /><br /> 0x8: вспомогательный метод.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodunload_v2-event"></a>MethodUnLoad_V2 событие

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`MethodUnLoad_V2`|142|Вызывается, когда выгружается модуль или уничтожается домен приложения. Динамические методы никогда не используют эту версию для выгрузки методов.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Информационный (4)|
|`NGenKeyword` 0x20|Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес метода.|
|`MethodSize`|`win:UInt32`|Размер метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод с кодом, скомпилированным JIT-компилятором (в противном случае машинный код образа NGEN).<br /><br /> 0x8: вспомогательный метод.|
|`ReJITID`|`win:UInt64`|Идентификатор ReJIT метода.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="r2rgetentrypoint-event"></a>Событие R2RGetEntryPoint

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`R2RGetEntryPoint`|159|Возникает при завершении поиска точки входа R2R.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода R2R.|
|`MethodNamespace`|`win:UnicodeString`|Пространство имен метода, поиск которого выполняется.|
|`MethodName`|`win:UnicodeString`|Имя метода, поиск которого выполняется.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`EntryPoint`|`win:UInt64`|Указатель на точку входа метода R2R|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="r2rgetentrypointstart-event"></a>Событие R2RGetEntryPointStart

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`R2RGetEntryPointStart`|160|Возникает при начале поиска точки входа R2R.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода R2R.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodloadverbose_v1-event"></a>MethodLoadVerbose_V1 событие

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Вызывается, когда метод является JIT-загружаемым или загружается образ NGEN. Динамические и универсальные методы всегда используют эту версию для загрузки методов. Вспомогательные методы JIT всегда используют эту версию.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес.|
|`MethodSize`|`win:UInt32`|Длина метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод, скомпилированный JIT-компилятором (в противном случае созданный программой NGen.exe).<br /><br /> 0x8: вспомогательный метод.|
|`MethodNameSpace`|`win:UnicodeString`|Полное имя пространства имен, связанного с методом.|
|`MethodName`|`win:UnicodeString`|Полное имя класса, связанного с методом.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodloadverbose_v2-event"></a>MethodLoadVerbose_V2 событие

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Вызывается, когда метод является JIT-загружаемым или загружается образ NGEN. Динамические и универсальные методы всегда используют эту версию для загрузки методов. Вспомогательные методы JIT всегда используют эту версию.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес.|
|`MethodSize`|`win:UInt32`|Длина метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод, скомпилированный JIT-компилятором (в противном случае созданный программой NGen.exe).<br /><br /> 0x8: вспомогательный метод.|
|`MethodNameSpace`|`win:UnicodeString`|Полное имя пространства имен, связанного с методом.|
|`MethodName`|`win:UnicodeString`|Полное имя класса, связанного с методом.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`ReJITID`|`win:UInt64`|Идентификатор ReJIT метода.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodunloadverbose_v1-event"></a>MethodUnLoadVerbose_V1 событие

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V1`|144|Вызывается, когда уничтожается динамический метод, выгружается модуль или разрушается домен приложения. Динамические методы всегда используют эту версию для выгрузки методов.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес.|
|`MethodSize`|`win:UInt32`|Длина метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод, скомпилированный JIT-компилятором (в противном случае созданный программой NGen.exe).<br /><br /> 0x8: вспомогательный метод.|
|`MethodNameSpace`|`win:UnicodeString`|Полное имя пространства имен, связанного с методом.|
|`MethodName`|`win:UnicodeString`|Полное имя класса, связанного с методом.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodunloadverbose_v2-event"></a>MethodUnLoadVerbose_V2 событие

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V2`|144|Вызывается, когда уничтожается динамический метод, выгружается модуль или разрушается домен приложения. Динамические методы всегда используют эту версию для выгрузки методов.|

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Информационный (4)|
|`NGenKeyword` 0x20 |Информационный (4)|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода. Для вспомогательных методов JIT устанавливается равным начальному адресу метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод (0 для вспомогательных методов JIT).|
|`MethodStartAddress`|`win:UInt64`|Начальный адрес.|
|`MethodSize`|`win:UInt32`|Длина метода.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodFlags`|`win:UInt32`|0x1: динамический метод.<br /><br /> 0x2: универсальный метод.<br /><br /> 0x4: метод, скомпилированный JIT-компилятором (в противном случае созданный программой NGen.exe).<br /><br /> 0x8: вспомогательный метод.|
|`MethodNameSpace`|`win:UnicodeString`|Полное имя пространства имен, связанного с методом.|
|`MethodName`|`win:UnicodeString`|Полное имя класса, связанного с методом.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`ReJITID`|`win:UInt64`|Идентификатор ReJIT метода.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodjittingstarted_v1-event"></a>MethodJittingStarted_V1 событие

В таблице ниже показаны ключевое слово и уровень.

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Подробный (5)|
|`NGenKeyword` 0x20 |Подробный (5)|

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodJittingStarted_V1`|145|Вызывается, когда метод компилируется JIT-компилятором.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода.|
|`ModuleID`|`win:UInt64`|Идентификатор модуля, к которому относится этот метод.|
|`MethodToken`|`win:UInt32`|0 для динамических методов и вспомогательных методов JIT.|
|`MethodILSize`|`win:UInt32`|Размер общего промежуточного языка (CIL) для метода, компилируемого JIT-компилятором.|
|`MethodNameSpace`|`win:UnicodeString`|Полное имя класса, связанного с методом.|
|`MethodName`|`win:UnicodeString`|Имя метода.|
|`MethodSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов).|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodjitinliningsucceeded-event"></a>Событие Месоджитинлинингсукцеедед

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Подробный (5)|

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodJitInliningSucceeded`|185|Возникает, когда метод успешно встроен в компилятор JIT.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Пространство имен компилируемого метода.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Имя компилируемого метода.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов) для компиляции.|
|`InlinerNamespace`|`win:UnicodeString`|Пространство имен метода Inline ("Parent").|
|`InlinerName`|`win:UnicodeString`|Имя метода подставляемого кода ("Parent").|
|`InlinerNameSignature`|`win:UnicodeString`|Сигнатура метода Inline ("Parent") (разделенный запятыми список имен типов).|
|`InlineeNamespace`|`win:UnicodeString`|Пространство имен метода встраивания (дочернего).|
|`InlineeName`|`win:UnicodeString`|Имя метода встраивания (дочернего).|
|`InlineeNameSignature`|`win:UnicodeString`|Сигнатура метода встраивания (дочернего) (разделенный запятыми список имен типов).|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodjitinliningfailed-event"></a>Событие Месоджитинлинингфаилед

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Подробный (5)|

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodJitInliningFailed`|192|Возникает, когда метод не был встроен JIT-компилятором.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Пространство имен компилируемого метода.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Имя компилируемого метода.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов) для компиляции.|
|`InlinerNamespace`|`win:UnicodeString`|Пространство имен метода Inline ("Parent").|
|`InlinerName`|`win:UnicodeString`|Имя метода подставляемого кода ("Parent").|
|`InlinerNameSignature`|`win:UnicodeString`|Сигнатура метода Inline ("Parent") (разделенный запятыми список имен типов).|
|`InlineeNamespace`|`win:UnicodeString`|Пространство имен метода встраивания (дочернего).|
|`InlineeName`|`win:UnicodeString`|Имя метода встраивания (дочернего).|
|`InlineeNameSignature`|`win:UnicodeString`|Сигнатура метода встраивания (дочернего) (разделенный запятыми список имен типов).|
|`FailAlways`|`win:Boolean`|Помечен ли метод как NOT инлинабле.|
|`FailReason`|`win:UnicodeString`|Сбой встраивания причины.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodjittailcallsucceeded-event"></a>Событие Месоджиттаилкаллсукцеедед

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Подробный (5)|

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodJitTailCallSucceeded`|192|Вызывается JIT-компилятором, когда метод может быть успешно вызван с помощью метода tail.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Пространство имен компилируемого метода.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Имя компилируемого метода.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов) для компиляции.|
|`CallerNamespace`|`win:UnicodeString`|Пространство имен вызывающего метода.|
|`CallerName`|`win:UnicodeString`|Имя вызывающего метода.|
|`CallerNameSignature`|`win:UnicodeString`|Сигнатура вызывающего метода (разделенный запятыми список имен типов).|
|`CalleeNamespace`|`win:UnicodeString`|Пространство имен вызываемого метода.|
|`CalleeName`|`win:UnicodeString`|Имя вызываемого метода.|
|`CalleeNameSignature`|`win:UnicodeString`|Сигнатура вызываемого метода (разделенный запятыми список имен типов).|
|`TailPrefix`|`win:Boolean`|Является ли это префиксной инструкцией.|
|`TailCallType`|`win:UInt32`|Тип вызова с префиксом tail.<br/><br/>0: оптимизированный вызов с префиксом tail (эпилога + переход)<br/><br/>1: рекурсивный вызов хвоста (метод с префиксом tail вызывает сам себя)<br/><br/>2: вспомогательный вызов с префиксом tail|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodjittailcallfailed-event"></a>Событие Месоджиттаилкаллфаилед

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Подробный (5)|

|Событие|Идентификатор события|Описание|
|-----------|--------------|-----------------|
|`MethodJitTailCallFailed`|191|Вызывается JIT-компилятором, когда метод не был вызван с помощью метода tail.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Пространство имен компилируемого метода.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Имя компилируемого метода.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Сигнатура метода (разделенный запятыми список имен типов) для компиляции.|
|`CallerNamespace`|`win:UnicodeString`|Пространство имен вызывающего метода.|
|`CallerNam`e|`win:UnicodeString`|Имя вызывающего метода.|
|`CallerNameSignature`|`win:UnicodeString`|Сигнатура вызывающего метода (разделенный запятыми список имен типов).|
|`CalleeNamespace`|`win:UnicodeString`|Пространство имен вызываемого метода.|
|`CalleeName`|`win:UnicodeString`|Имя вызываемого метода.|
|`CalleeNameSignature`|`win:UnicodeString`|Сигнатура вызываемого метода (разделенный запятыми список имен типов).|
|`TailPrefix`|`win:Boolean`|Является ли это префиксной инструкцией.|
|`FailReason`|`win:UnicodeString`|Причина сбоя вызова с префиксом tail.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|

## <a name="methodiltonativemap-event"></a>Событие Месодилтонативемап

|Ключевое слово для вызова события|Level|
|-----------------------------------|-----------|
|`JittedMethodILToNativeMapKeyword` (0x20000) |Подробный (5)|

|Событие|Идентификатор события|Описание|
|----------------|---------------|-----------------|
|`MethodILToNativeMap`|190|Сопоставляет событие сопоставления IL-Native с JIT-скомпилированными методами.|

|Имя поля|Тип данных|Описание|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Уникальный идентификатор метода.|
|`ReJITID`|`win:UInt64`|Идентификатор ReJIT метода.|
|`MethodExtent`|`win:UInt8`|Экстент для откомпилированного метода.|
|`CountOfMapEntries`|`win:UInt8`|Число записей карт|
|`ILOffsets`|`win:UInt32`|Смещение IL.|
|`NativeOffsets`|`win:UInt32`|Смещение машинного кода.|
|`ClrInstanceID`|`win:UInt16`|Уникальный идентификатор для экземпляра CoreCLR.|
