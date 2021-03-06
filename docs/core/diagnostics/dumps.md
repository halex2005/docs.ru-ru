---
title: Дампы — .NET
description: Общие сведения о дампах в .NET.
ms.date: 10/12/2020
ms.openlocfilehash: f68d9bd804350366625df014df4d9ca0641d5d4d
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188560"
---
# <a name="dumps"></a>Файлы дампа

Дамп — это файл, который содержит моментальный снимок процесса во время его создания и может быть полезен для проверки состояния приложения. Дампы можно использовать для отладки приложения .NET, когда трудно подключить к нему отладчик (например, в рабочей среде или в среде CI). Использование дампов позволяет записать состояние проблемного процесса и изучить его без необходимости приостанавливать работу приложения.

## <a name="collect-dumps"></a>Сбор дампов

Дампы можно собирать различными способами в зависимости от того, на какой платформе вы используете приложение.

> [!NOTE]
> Для сбора дампа внутри контейнера требуется возможность PTRACE, которую можно добавить с помощью `--cap-add=SYS_PTRACE` или `--privileged`.
> [!NOTE]
> Дампы могут содержать конфиденциальные сведения, поскольку они могут содержать всю память выполняющегося процесса. При их обработке следует учитывать ограничения безопасности и рекомендации.

### <a name="collecting-dumps-on-crash"></a>Сбор дампов при сбое

Вы можете использовать переменные среды, чтобы настроить приложение на сбор дампа при сбое. Это полезно, если вы хотите получить представление о причинах сбоя. Например, запись дампа при возникновении исключения помогает выявить проблемы путем проверки состояния приложения при его сбое.

В следующей таблице приведены переменные среды, которые можно настроить для сбора дампов при сбое.

|Переменная среды|Описание|Значение по умолчанию|
|-------|---------|---|
|`COMPlus_DbgEnableMiniDump`|Если задано значение 1, включите создание дампа ядра.|0|
|`COMPlus_DbgMiniDumpType`|Тип собираемого дампа. Дополнительные сведения см. в таблице ниже.|2 (`MiniDumpWithPrivateReadWriteMemory`)|
|`COMPlus_DbgMiniDumpName`|Файл, в который записывается дамп.|`/tmp/coredump.<pid>`|
|`COMPlus_CreateDumpDiagnostics`|Если задано значение 1, включите ведение журнала диагностики для процесса дампа.|0|

В таблице ниже показаны все параметры, доступные для использования для `COMPlus_DbgMiniDumpType`, которые можно указать в качестве значения. Например, если установить для параметра `COMPlus_DbgMiniDumpType` значение 1, при сбое будет собираться дамп типа `MiniDumpNormal`.

|Значение|Имя|Описание|
|-----|----|-----------|
|1|`MiniDumpNormal`|Включение только сведений, необходимых для записи трассировок стека для всех существующих потоков в процессе. Ограниченная память кучи сборки мусора и информация.|
|2|`MiniDumpWithPrivateReadWriteMemory`|Включение кучи сборки мусора и сведений, необходимых для записи трассировок стека для всех существующих потоков в процессе.|
|3|`MiniDumpFilterTriage`|Включение только сведений, необходимых для записи трассировок стека для всех существующих потоков в процессе. Ограниченная память кучи сборки мусора и информация.|
|4|`MiniDumpWithFullMemory`|Включение в процесс всей доступной памяти. Необработанные данные памяти включаются в конец, чтобы начальные структуры можно было сопоставить напрямую без необработанных данных памяти. Этот вариант может привести к созданию очень большого файла.|

### <a name="collecting-dumps-at-specific-point-in-time"></a>Сбор дампов в определенный момент времени

Вы можете собрать дамп, когда приложение еще не завершило работу. Например, если вы хотите проверить состояние приложения, в котором, на ваш взгляд, возникла взаимоблокировка, настройка переменных среды для сбора дампов при сбое не будет полезна, так как приложение все еще работает.

Для сбора дампа в собственном запросе можно использовать `dotnet-dump`, который является средством CLI для сбора и анализа дампов. Дополнительные сведения об использовании этого средства для сбора дампов с помощью `dotnet-dump` см. в разделе [Служебная программа для сбора и анализа дампа](dotnet-dump.md).

## <a name="analyze-dumps"></a>Анализ дампов

Дампы можно проанализировать с помощью средства CLI [`dotnet-dump`](dotnet-dump.md) или посредством [Visual Studio](/visualstudio/debugger/using-dump-files).

> [!NOTE]
> Visual Studio версии 16.8 и более поздних версий позволяет [открывать дампы Linux](https://devblogs.microsoft.com/visualstudio/linux-managed-memory-dump-debugging/), созданные в .NET Core 3.1.7 и более поздних версий.  
> [!NOTE]
> Если необходима отладка машинного кода, можно использовать [расширение отладчика SOS](sos-debugging-extension.md) совместно с [LLDB в Linux и macOS](debug-linux-dumps.md#analyze-dumps-on-linux). SOS также поддерживается в Windows c [Windbg/cdb](/windows-hardware/drivers/debugger/debugger-download-tools), хотя рекомендуется использовать Visual Studio.

## <a name="see-also"></a>См. также раздел

Узнайте подробнее о том, как можно использовать дампы для диагностики проблем в приложении .NET.

* В [руководстве по отладке дампов Linux](debug-linux-dumps.md) представлены пошаговые инструкции по отладке дампа, собранного в Linux.

* В [руководстве по отладке взаимоблокировок](debug-deadlock.md) описывается отладка взаимоблокировок в приложении .NET с помощью дампов.
