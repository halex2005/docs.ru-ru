---
title: Удаление потоков
description: Вы можете узнать о доступных возможностях, когда требуется уничтожить поток в .NET, таких как совместная отмена или метод Thread.Abort. Сведения об обработке исключения ThreadAbortException.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- destroying threads
- threading [.NET], destroying threads
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
ms.openlocfilehash: bdba09f5709cf99bc0d076e3875a914cc7c5a11e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723770"
---
# <a name="destroying-threads"></a>Удаление потоков

[Модель совместной отмены](cancellation-in-managed-threads.md) используется для остановки потока. Иногда выполнить совместную отмену потока невозможно, так как он выполняет код сторонних производителей, не поддерживающий такую отмену. Метод <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> в .NET Framework можно использовать для принудительного завершения управляемого потока. При вызове <xref:System.Threading.Thread.Abort%2A> общеязыковая среда выполнения создает в целевом потоке исключение <xref:System.Threading.ThreadAbortException>, которое целевой поток может перехватить. Для получения дополнительной информации см. <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>. Метод <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> не поддерживается в .NET 5 (включая .NET Core) и более поздних версий. Если необходимо принудительно завершить выполнение кода сторонних производителей в .NET 5 или более поздней версии, запустите его в отдельном процессе и воспользуйтесь <xref:System.Diagnostics.Process.Kill%2A?displayProperty=nameWithType>.

> [!NOTE]
> Если в потоке выполняется неуправляемый код при вызове его метода <xref:System.Threading.Thread.Abort%2A>, в среде выполнения он отмечается как <xref:System.Threading.ThreadState.AbortRequested?displayProperty=nameWithType>. В этом случае исключение вызывается после возврата потока в управляемый код.  
  
 После прерывания поток не перезапускается.  
  
 Метод <xref:System.Threading.Thread.Abort%2A> не приводит к немедленному прерыванию потока, так как целевой поток может перехватить <xref:System.Threading.ThreadAbortException> и выполнить любой объем кода в блоке `finally`. Если необходимо дождаться завершения потока, вы можете вызвать <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>. Блокирующий вызов <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> не завершится, пока поток полностью не закончит выполнение или не истечет указанный (необязательный) интервал времени ожидания. Прерванный поток может вызвать метод <xref:System.Threading.Thread.ResetAbort%2A> или выполнить любой объем операций в блоке `finally`, поэтому завершение ожидания не гарантируется, если вы не укажете время ожидания.  
  
 Потоки, ожидающие завершения метода <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>, могут быть прерваны другими потоками, которые вызывают <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>.  
  
## <a name="handling-threadabortexception"></a>Обработка ThreadAbortException  

 Если вы ожидаете, что поток будет прерван вызовом <xref:System.Threading.Thread.Abort%2A> из вашего кода или в результате выгрузки домена приложения, в котором выполняется поток (<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> использует <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> для прерывания потоков), в таком потоке необходимо обработать <xref:System.Threading.ThreadAbortException>, включив в предложение `finally` все операции последней обработки, как показано в следующем примере.  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try
{  
    // Code that is executing when the thread is aborted.  
}
catch (ThreadAbortException ex)
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.
}  
// Do not put clean-up code here, because the exception
// is rethrown at the end of the Finally clause.  
```  
  
 Код завершения работы следует поместить в предложении `catch` или `finally`, так как система повторно создаст исключение <xref:System.Threading.ThreadAbortException> в конце предложения `finally` или `catch`, если отсутствует предложение `finally`.  
  
 Чтобы предотвратить повторное создание исключения, вы можете вызвать метод <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=nameWithType>. Но этот вариант следует использовать только в том случае, если <xref:System.Threading.ThreadAbortException> вызывается в пользовательском коде.  
  
## <a name="see-also"></a>См. также

- <xref:System.Threading.ThreadAbortException>
- <xref:System.Threading.Thread>
- [Использование потоков и работа с потоками](using-threads-and-threading.md)
