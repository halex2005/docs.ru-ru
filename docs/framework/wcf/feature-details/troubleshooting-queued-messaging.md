---
description: 'Дополнительные сведения: Устранение неполадок обмена сообщениями в очереди'
title: Устранение неполадок обмена сообщениями с использованием очередей
ms.date: 03/30/2017
ms.assetid: a5f2836f-018d-42f5-a571-1e97e64ea5b0
ms.openlocfilehash: e7cf2706e7c0853f14bad449b6ecaa8dd5983755
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733090"
---
# <a name="troubleshooting-queued-messaging"></a>Устранение неполадок обмена сообщениями с использованием очередей

В этом разделе содержатся часто задаваемые вопросы и Справка по устранению неполадок при использовании очередей в Windows Communication Foundation (WCF).

## <a name="common-questions"></a>Часто задаваемые вопросы

**Вопрос.** Я использовал WCF Beta 1 и установил исправление MSMQ. Требуется ли удалять исправление?

**Ответ.** Да. Это исправление больше не поддерживается. Теперь WCF работает с MSMQ без необходимости исправления.

**Вопрос.** Существует две привязки для MSMQ: <xref:System.ServiceModel.NetMsmqBinding> и <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> . Какую необходимо использовать и когда?

Ответ **.** Используйте, <xref:System.ServiceModel.NetMsmqBinding> Если вы хотите использовать MSMQ в качестве транспорта для обмена данными между двумя приложениями WCF в очереди. Используйте, <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> Если вы хотите использовать существующие приложения MSMQ для взаимодействия с новыми приложениями WCF.

**Вопрос.** Нужно ли обновлять MSMQ для использования <xref:System.ServiceModel.NetMsmqBinding> `MsmqIntegration` привязок и?

**Ответ.** Нет. Обе привязки работают с MSMQ 3,0 в Windows XP и Windows Server 2003. Некоторые функции привязок становятся доступными при обновлении до MSMQ 4,0 в Windows Vista.

**Вопрос.** Какие функции <xref:System.ServiceModel.NetMsmqBinding> и <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> привязки доступны в MSMQ 4,0, но не в MSMQ 3,0?

Ответ **.** Следующие функции доступны в MSMQ 4,0, но не в MSMQ 3,0:

- Пользовательская очередь недоставленных сообщений поддерживается только в MSMQ 4.0.

- MSMQ 3.0 и 4.0 обрабатывают опасные сообщения по-разному.

- Удаленные чтения в транзакциях поддерживаются только MSMQ 4.0.

Дополнительные сведения см. в разделе [различия в возможностях очередей в Windows Vista, Windows Server 2003 и Windows XP](diff-in-queue-in-vista-server-2003-windows-xp.md).

**Вопрос.** Можно ли использовать MSMQ 3,0 на одной стороне связи с очередями и MSMQ 4,0 на другой стороне?

**Ответ.** Да.

**Вопрос.** Я хочу интегрировать существующие приложения MSMQ с новыми клиентами или серверами WCF. Требуются ли обновления для обеих сторон инфраструктуры MSMQ?

**Ответ.** Нет. Для обеих сторон обновление до MSMQ 4.0 не требуется.

## <a name="troubleshooting"></a>Устранение неполадок

Данный раздел содержит ответы на вопросы, связанные с устранением распространенных неполадок. Некоторые вопросы, являющиеся известными ограничениями, описаны также в заметках о выпуске.

**Вопрос.** Я пытаюсь использовать частную очередь и получаю следующее исключение: `System.InvalidOperationException` : недопустимый URL-адрес. URL-адрес очереди не может содержать символ "$". Используйте синтаксис net.msmq://machine/private/queueName, чтобы адресовать частную очередь.

Ответ **.** Проверьте универсальный код ресурса (URI) очереди в конфигурации и коде. Не используйте символ "$" в универсальном коде ресурса (URI). Например, чтобы устранить частную очередь с именем Ордерскуеуе, укажите универсальный код ресурса (URI) `net.msmq://localhost/private/ordersQueue` .

**Вопрос.** Вызов `ServiceHost.Open()` в моем приложении, находящихся в очереди, вызывает следующее исключение: `System.ArgumentException` : базовый адрес не может содержать строку запроса URI. Почему?

Ответ **.** Проверьте URI очереди в файле конфигурации и в коде. Хотя очереди MSMQ поддерживают использование символа "?", универсальные коды ресурсов (URI) интерпретируют этот символ как начало строки запроса. Чтобы избежать этого, не используйте символ "?" в именах очередей.

**Вопрос.** Моя отправка завершилась успехом, но на получателе не вызвана операция службы. Почему?

Ответ **.** Чтобы определить ответ, обратитесь к следующему контрольному списку:

- Проверьте, совместимы ли требования транзакционной очереди с заданными гарантиями. Обратите внимание на следующие принципы.

  - Устойчивые сообщения (датаграммы и сеансы) можно отправить с "только один раз" гарантиями ( <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A>  =  `true` ) только в транзакционную очередь.

  - Сеансы можно отправлять только с гарантиями доставки точно по одному разу.

  - Необходимо, чтобы в сеансе транзакция получала сообщения из транзакционной очереди.

  - Вы можете отправлять или получать временные или устойчивые сообщения (только датаграммы) без гарантии ( <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A>  =  `false` ) только в нетранзакционную очередь.

- Проверьте очередь недоставленных писем. Если в этой очереди есть сообщения, определите причину, по которой они не были доставлены.

- Проверьте очереди исходящих сообщений на наличие проблем с подключением и адресацией.

**Вопрос.** Я указал пользовательскую очередь недоставленных сообщений, но когда я запускаю приложение отправителя, я получаю исключение, что либо очередь недоставленных сообщений не найдена, либо у отправляющего приложения нет разрешения на доступ к очереди недоставленных сообщений. Почему это происходит?

Ответ **.** Пользовательский URI очереди недоставленных сообщений должен включать в первый сегмент "localhost" или имя компьютера, например очередь NET. msmq://ЛОКАЛХОСТ/привате/мяппдеад-Леттер.

**Вопрос.** Нужно ли всегда определять пользовательскую очередь недоставленных сообщений или очередь недоставленных сообщений по умолчанию?

Ответ **.** Если в качестве гарантии используются «только один раз» ( <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A>  =  `true` ) и не указана пользовательская очередь недоставленных сообщений, по умолчанию используется транзакционная очередь недоставленных сообщений на уровне системы.

Если <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A>  =  `false` параметру Assurance присвоено значение None (), то по умолчанию функция очереди недоставленных сообщений не используется.

**Вопрос.** Моя служба создает исключение в SvcHost. Open с сообщением «EndpointListener требования не могут быть удовлетворены Листенерфактори». Почему?

A. Проверьте контракт службы. Возможно, вы забыли разместить "IsOneWay = `true` " во всех операциях службы. Очереди поддерживают только односторонние операции службы.

**Вопрос.** В очереди есть сообщения, но не вызвана операция службы. В чем заключается проблема?

Ответ **.** Определение сбоя узла службы. Убедиться в этом можно, просмотрев трассировку или реализовав `IErrorHandler`. По умолчанию сбой узла службы происходит при обнаружении подозрительного сообщения.

**Вопрос.** В очереди есть сообщения, но служба, размещенная в очереди, не активируется. Почему?

Ответ **.** Наиболее распространенная причина — разрешения.

1. Убедитесь в том, что выполняется процесс `NetMsmqActivator` и удостоверению процесса `NetMsmqActivator` предоставлено разрешение на чтение и поиск для данной очереди.

2. Если процесс `NetMsmqActivator` отслеживает очереди на удаленном компьютере, убедитесь в том, что `NetMsmqActivator` не выполняется с маркером ограниченного доступа. Чтобы выполнить процесс `NetMsmqActivator` с маркером неограниченного доступа, используется следующий код.

    ```console
    sc sidtype NetMsmqActivator unrestricted
    ```

Для проблем с веб-узлом, не связанными с безопасностью, см. [веб-узел, в котором размещено приложение в очереди](web-hosting-a-queued-application.md).

**Вопрос.** Каков самый простой способ доступа к сеансам?

Ответ **.** Задать Автозаполнение = `true` для операции, которая соответствует последнему сообщению в сеансе, и задать Автозаполнение = `false` для всех оставшихся операций службы.

**Вопрос.** Почему моя служба создает исключение `ProtocolException` при чтении из очереди, содержащей сообщения, помещенные в очередь, и сообщения, поставленные в очередь?

Ответ **.** Существует фундаментальное различие в способе обмена сообщениями сеанса в очереди и сообщениями с датаграммами в очереди. Вследствие этого, служба, ожидающая чтения сообщения сеанса из очереди не может получить сообщение датаграммы из очереди, а служба, ожидающая чтения сообщения датаграммы из очереди не может получить сообщения сеанса. При попытке чтения сообщений обоих типов из одной очереди будет получено следующее исключение.

```console
System.ServiceModel.MsmqPoisonMessageException: The transport channel detected a poison message. This occurred because the message exceeded the maximum number of delivery attempts or because the channel detected a fundamental problem with the message. The inner exception may contain additional information.
---> System.ServiceModel.ProtocolException: An incoming MSMQ message contained invalid or unexpected .NET Message Framing information in its body. The message cannot be received. Ensure that the sender is using a compatible service contract with a matching SessionMode.
```

Системная очередь недоставленных сообщений, а также любая пользовательская очередь недоставленных сообщений особенно чувствительна к этой проблеме, если приложение отправляет с одного компьютера как сообщения сеанса в очереди, так и сообщения датаграммы. Если сообщение не удается отправить, оно перемещается в очередь недоставленных сообщений. При этих обстоятельствах в очереди недоставленных сообщений могут быть как сообщения сеанса, так и сообщения датаграмм. При чтении из очереди во время выполнения отсутствует возможность разделения двух типов сообщений, поэтому приложения не должны отправлять сообщения сеанса в очереди и сообщения датаграмм в очереди с одного компьютера.

### <a name="msmq-integration-specific-troubleshooting"></a>Интеграция MSMQ: устранение конкретных неполадок

**Вопрос.** При отправке сообщения или открытии узла службы появляется сообщение об ошибке, показывающее, что схема неверна. Почему?

Ответ **.** При использовании привязки интеграции MSMQ необходимо использовать схему MSMQ. formatname. Например, msmq.formatname:DIRECT=OS:.\private$\OrdersQueue. Однако если задана пользовательская очередь недоставленных сообщений, необходимо использовать схему net.msmq.

**Вопрос.** При использовании имени открытого или закрытого формата и открытии узла службы в Windows Vista появляется сообщение об ошибке. Почему?

Ответ **.** Канал интеграции WCF в Windows Vista проверяет, можно ли открыть подочередь для основной очереди приложения для обработки подозрительных сообщений. Имя подочереди является производным от URI MSMQ. formatname, переданного прослушивателю. Имя подочереди в MSMQ может иметь только прямое имя формата. Из-за этого возникает ошибка. Измените URI очереди на непосредственное имя формата.

**Вопрос.** При получении сообщения от приложения MSMQ оно находится в очереди и не считывается принимающим приложением WCF. Почему?

Ответ **.** Проверьте, есть ли у сообщения текст. Если в сообщении отсутствует тело, канал интеграции MSMQ игнорирует его. Реализуйте интерфейс `IErrorHandler`, чтобы получать уведомления об исключениях, и проверьте трассировки.

### <a name="security-related-troubleshooting"></a>Устранение неполадок, связанных с безопасностью

**Вопрос.** При запуске примера, использующего привязку по умолчанию в режиме рабочей группы, сообщения могут отправляться, но никогда не получаются получателем.

Ответ **.** По умолчанию сообщения подписываются с помощью внутреннего сертификата MSMQ, для которого требуется служба Active Directory Directory. В режиме рабочей группы происходит сбой подписи сообщения, так как служба каталогов Active Directory недоступна. Таким образом, в очереди недоставленных сообщений и причинах сбоя, например "Неправильная подпись", указывается.

Чтобы обойти эту проблему, можно отключить систему безопасности. Это делается путем настройки <xref:System.ServiceModel.NetMsmqSecurity.Mode%2A>  =  <xref:System.ServiceModel.NetMsmqSecurityMode.None> для обеспечения работы в режиме рабочей группы.

Как вариант можно получить <xref:System.ServiceModel.MsmqTransportSecurity> из свойства <xref:System.ServiceModel.NetMsmqSecurity.Transport%2A> и присвоить ему значение <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate>, а затем задать сертификат клиента.

Еще одним обходным путем является установка MSMQ с интеграцией Active Directory.

**Вопрос.** При отправке сообщения с привязкой по умолчанию (включена безопасность транспорта) в Active Directory в очередь я получаю сообщение "внутренний сертификат не найден". Как устранить эту проблему?

Ответ **.** Это означает, что сертификат в Active Directory для отправителя должен быть продлен. Для этого откройте **Панель управления**, **Администрирование**, **Управление компьютером**, щелкните правой кнопкой мыши **MSMQ** и выберите пункт **Свойства**. Выберите вкладку **сертификат пользователя** и нажмите кнопку **продлить** .

**Вопрос.** Когда я отправил сообщение с помощью <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> и указал сертификат для использования, я получаю сообщение "Недопустимый сертификат". Как устранить эту проблему?

Ответ **.** Нельзя использовать хранилище сертификатов локального компьютера с режимом сертификата. Необходимо скопировать сертификат из хранилища сертификатов компьютера в хранилище текущего пользователя с помощью оснастки сертификатов. Чтобы получить оснастку сертификатов, выполните следующие действия.

1. Нажмите кнопку **Пуск**, выберите **выполнить**, введите `mmc` и нажмите кнопку **ОК**.

2. В **консоли управления (MMC**) откройте меню **файл** и выберите **Добавить или удалить оснастку**.

3. В диалоговом окне " **Добавление или удаление оснастки** " нажмите кнопку " **Добавить** ".

4. В диалоговом окне **Добавить изолированную оснастку** выберите Сертификаты и нажмите кнопку **Добавить**.

5. В диалоговом окне Оснастка " **Сертификаты** " выберите **Моя учетная запись пользователя** и нажмите кнопку **Готово**.

6. Затем добавьте вторую оснастку сертификатов, выполнив предыдущие действия, но на этот раз выберите **учетная запись компьютера** и нажмите кнопку **Далее**.

7. Выберите **Локальный компьютер**, а затем нажмите кнопку **Готово**. Теперь сертификаты можно перетаскивать из хранилища сертификатов компьютера в хранилище текущего пользователя.

**Вопрос.** Когда моя служба считывает данные из очереди на другом компьютере в режиме рабочей группы, я получаю исключение "доступ запрещен".

Ответ **.** В режиме рабочей группы для удаленного приложения, чтобы получить доступ к очереди, приложение должно иметь разрешение на доступ к очереди. Добавьте анонимный вход в список управления доступом (ACL) очереди и предоставьте ему разрешение на чтение.

**Вопрос.** Если клиент сетевой службы (или любой клиент, не имеющий учетной записи домена) отправляет сообщение в очереди, происходит сбой отправки с недопустимым сертификатом. Как устранить эту проблему?

Ответ **.** Проверьте конфигурацию привязки. В привязке по умолчанию включена безопасность транспорта MSMQ для подписи сообщения. Отключите ее.

### <a name="remote-transacted-receives"></a>Удаленное получение транзакций

**Вопрос.** Если у меня есть очередь на компьютере а и служба WCF, считывающая сообщения из очереди на компьютере б (сценарий удаленного приема транзакций), сообщения не считываются из очереди. Сведения трассировки указывают на сбой получения с сообщением "не удается импортировать транзакцию". Как это исправить?

Ответ **.** Существует три возможных причины этого.

- В режиме домена для удаленного получения транзакций требуется доступ к сети координатора распределенных транзакций (Майкрософт) (MSDTC). Его можно включить с помощью **компонента "Добавление и удаление компонентов**".

  ![Снимок экрана, показывающий включение доступа к сети DTC.](./media/troubleshooting-queued-messaging/enable-distributed-transaction-coordinator-access.jpg)

- Проверьте режим проверки подлинности для взаимодействия с диспетчером транзакций. Если вы используете режим рабочей группы, необходимо выбрать параметр "не требуется проверка подлинности". Если вы используете режим домена, необходимо выбрать "требуется взаимная проверка подлинности".

  ![Включение транзакций XA](media/4f3695e0-fb0b-4c5b-afac-75f8860d2bb0.jpg "4f3695e0-fb0b-4c5b-afac-75f8860d2bb0")

- Убедитесь, что служба MSDTC находится в списке исключений в параметрах **брандмауэра подключения к Интернету** .

- Убедитесь, что используется Windows Vista. MSMQ в Windows Vista поддерживает удаленное чтение транзакций. MSMQ в более ранних версиях Windows не поддерживает удаленное чтение в транзакциях.

**Вопрос.** Если служба считывается из очереди в качестве сетевой службы, например, на веб-узле, почему при чтении из очереди возникает исключение "доступ запрещен"?

Ответ **.** Доступ для чтения сетевой службы должен быть добавлен к списку ACL очереди, чтобы сетевая служба могла выполнять чтение из очереди.

**Вопрос.** Можно ли использовать службу активации MSMQ для активации приложений на основе сообщений в очереди на удаленном компьютере?

**Ответ.** Да. Для этого необходимо настроить службу активации MSMQ для выполнения в качестве сетевой службы, а также добавить доступ сетевой службы к очереди на удаленном компьютере.

## <a name="using-custom-msmq-bindings-with-receivecontext-enabled"></a>Использование пользовательских привязок MSMQ с включенным ReceiveContext

При использовании настраиваемой привязки MSMQ с <xref:System.ServiceModel.Channels.ReceiveContext> включенной функцией обработка входящего сообщения использует поток пула потоков, так как собственный MSMQ не поддерживает завершение ввода-вывода для асинхронного <xref:System.ServiceModel.Channels.ReceiveContext> получения. Это обусловлено тем, что обработка такого сообщения использует внутренние транзакции для <xref:System.ServiceModel.Channels.ReceiveContext> и MSMQ не поддерживает асинхронную обработку. Чтобы обойти эту ошибку, можно добавить <xref:System.ServiceModel.Description.SynchronousReceiveBehavior> в конечную точку, чтобы принудительно выполнить синхронную обработку или установить значение <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.MaxPendingReceives%2A> 1.
