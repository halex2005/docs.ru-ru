---
title: Критические изменения, миграция с .NET Framework на .NET Core
titleSuffix: ''
description: Список критических изменений, миграция с .NET Framework на .NET Core версий 1.0–3.1.
ms.date: 05/05/2020
ms.openlocfilehash: 5904a359813b6d07bd2a27d882ade4395efe3256
ms.sourcegitcommit: 1e8382d0ce8b5515864f8fbb178b9fd692a7503f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89656370"
---
# <a name="breaking-changes-for-migration-from-net-framework-to-net-core"></a>Критические изменения для миграции с .NET Framework на .NET Core

Если вы переносите приложение с .NET Framework на .NET Core версий 1.0–3.1, критические изменения, перечисленные в этой статье, могут повлиять на работу приложения. Критические изменения сгруппированы по категориям, а в этих категориях — по версии .NET Core, в которых они были представлены.

> [!NOTE]
> Эта статья не является исчерпывающим списком критических изменений между .NET Framework и .NET Core. Здесь добавляются самые важные критические изменения, как только мы о них узнаем.

## <a name="core-net-libraries"></a>Библиотеки Core .NET

- [Изменено значение по умолчанию для UseShellExecute](#change-in-default-value-of-useshellexecute)
- [Исключение UnauthorizedAccessException, вызванное FileSystemInfo.Attributes](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes)
- [Обработка исключений с поврежденным состоянием процесса не поддерживается](#handling-corrupted-state-exceptions-is-not-supported)
- [Для свойств UriBuilder больше не добавляются начальные символы](#uribuilder-properties-no-longer-prepend-leading-characters)
- [Process.StartInfo выдает исключение InvalidOperationException для процессов, которые не были запущены](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start)

### <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Process.Start changes](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

### <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

***

## <a name="cryptography"></a>Шифрование

- [Логический параметр SignedCms.ComputeSignature учитывается](#boolean-parameter-of-signedcmscomputesignature-is-respected)

### <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE [Boolean parameter of SignedCms.ComputeSignature is respected](~/includes/core-changes/cryptography/2.1/compute-signature-silent-parameter.md)]

***

## <a name="msbuild"></a>MSBuild

- [Изменение имен файлов манифеста ресурса](#resource-manifest-file-name-change)

### <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***

## <a name="networking"></a>Сети

- [WebClient.CancelAsync не всегда сразу отменяет запрос](#webclientcancelasync-doesnt-always-cancel-immediately)

### <a name="net-core-20"></a>.NET Core 2.0;

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***

## <a name="windows-forms"></a>Windows Forms

Поддержка Windows Forms была добавлена в .NET Core в версии 3.0. Если вы переносите приложение Windows Forms с .NET Framework на .NET Core, критические изменения, перечисленные здесь, могут повлиять на работу приложения.

- [Удаленные элементы управления](#removed-controls)
- [При отображении подсказки не возникает событие CellFormatting](#cellformatting-event-not-raised-if-tooltip-is-shown)
- [Шрифт Control.DefaultFont изменен на Segoe UI 9 пт](#default-control-font-changed-to-segoe-ui-9-pt)
- [Модернизация FolderBrowserDialog](#modernization-of-the-folderbrowserdialog)
- [Из некоторых типов Windows Forms удален атрибут SerializableAttribute](#serializableattribute-removed-from-some-windows-forms-types)
- [Параметр совместимости AllowUpdateChildControlIndexForTabControls не поддерживается](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported)
- [Параметр совместимости DomainUpDown.UseLegacyScrolling не поддерживается](#domainupdownuselegacyscrolling-compatibility-switch-not-supported)
- [Параметр совместимости DoNotLoadLatestRichEditControl не поддерживается](#donotloadlatestricheditcontrol-compatibility-switch-not-supported)
- [Параметр совместимости DoNotSupportSelectAllShortcutInMultilineTextBox не поддерживается](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported)
- [Параметр совместимости DontSupportReentrantFilterMessage не поддерживается](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported)
- [Параметр совместимости EnableVisualStyleValidation не поддерживается](#enablevisualstylevalidation-compatibility-switch-not-supported)
- [Параметр совместимости UseLegacyContextMenuStripSourceControlValue не поддерживается](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported)
- [Параметр совместимости UseLegacyImages не поддерживается](#uselegacyimages-compatibility-switch-not-supported)

### <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

### <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9 pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

## <a name="see-also"></a>См. также

- [API, которые всегда создают исключения в .NET Core](unsupported-apis.md)
- [Технологии .NET Framework, недоступные в .NET Core](../porting/net-framework-tech-unavailable.md)
