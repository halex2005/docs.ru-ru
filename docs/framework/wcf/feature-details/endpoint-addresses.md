---
description: 'Дополнительные сведения: адреса конечных точек'
title: Адреса конечных точек
ms.date: 03/30/2017
helpviewer_keywords:
- addresses [WCF]
- Windows Communication Foundation [WCF], addresses
- WCF [WCF], addresses
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
ms.openlocfilehash: 009b34a3931bda3b16c9079316b97ea2f1680ffb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704788"
---
# <a name="endpoint-addresses"></a>Адреса конечных точек

С каждой конечной точкой связан адрес, который используется для поиска и идентификации этой конечной точки. Этот адрес в первую очередь включает универсальный код ресурса (URI), задающий расположение конечной точки. Адрес конечной точки представлен в модели программирования Windows Communication Foundation (WCF) <xref:System.ServiceModel.EndpointAddress> классом, который содержит необязательное <xref:System.ServiceModel.EndpointAddress.Identity%2A> свойство, которое обеспечивает проверку подлинности конечной точки другими конечными точками, которые обмениваются сообщениями с ней, и набор необязательных <xref:System.ServiceModel.EndpointAddress.Headers%2A> свойств, определяющих любые другие заголовки SOAP, необходимые для доступа к службе. Необязательные заголовки содержат дополнительную и более подробную информацию для идентификации конечной точки службы и взаимодействия с ней. При передаче данных по каналам связи адрес конечной точки представляется ссылкой на конечную точку WS-Addressing.  
  
## <a name="uri-structure-of-an-address"></a>Структура универсального кода ресурса (URI) адреса  

 Универсальный код ресурса (URI) адреса для большинства видов транспорта состоит из четырех частей. Например, четыре части URI `http://www.fabrikam.com:322/mathservice.svc/secureEndpoint` могут быть детализированы следующим образом:  
  
- Схема: `http:`
  
- Машине `www.fabrikam.com`  
  
- (необязательно) Порт: 322  
  
- Путь: /mathservice.svc/secureEndpoint  
  
## <a name="defining-an-address-for-a-service"></a>Определение адреса службы  

 Адрес конечной точки службы можно задать императивно с помощью кода или декларативно с помощью конфигурации. Как правило, определять конечные точки в коде непрактично, поскольку привязки и адреса для развернутой службы чаще всего отличаются от привязок и адресов, используемых в процессе разработки службы. Обычно более целесообразно задать конечные точки службы в конфигурации, а не в коде. Если не указывать привязку и адрес в коде, их можно изменять, не выполняя повторную компиляцию или повторное развертывание приложения.  
  
### <a name="defining-an-address-in-configuration"></a>Определение адреса в файле конфигурации  

 Чтобы определить конечную точку в файле конфигурации, используйте [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) элемент. Дополнительные сведения и пример см. в разделе [Указание адреса конечной точки](../specifying-an-endpoint-address.md).  
  
### <a name="defining-an-address-in-code"></a>Определение адреса в коде  

 Адрес конечной точки можно создать в коде с помощью класса <xref:System.ServiceModel.EndpointAddress>. Дополнительные сведения и пример см. в разделе [Указание адреса конечной точки](../specifying-an-endpoint-address.md).  
  
### <a name="endpoints-in-wsdl"></a>Конечные точки на языке WSDL  

 Адрес конечной точки также может быть представлен на языке WSDL в виде элемента EPR WS-Addressing в элементе `wsdl:port` соответствующей конечной точки. Ссылка на конечную точку (EPR) содержит адрес конечной точки и любые свойства адреса. Дополнительные сведения и пример см. в разделе [Указание адреса конечной точки](../specifying-an-endpoint-address.md).  
  
## <a name="multiple-iis-binding-support-in-net-framework-35"></a>Поддержка нескольких привязок IIS в платформа .NET Framework 3,5  

 Поставщики услуг Интернета часто размещают большое число приложений на одном сайте и сервере, чтобы повысить эффективность использования сайта и сократить совокупную стоимость владения. Эти приложения обычно привязываются к различным базовым адресам. Веб-сайт служб IIS может содержать несколько приложений. Доступ к приложениям на сайте может осуществляться через одну или несколько привязок служб IIS.  
  
 Привязки IIS предоставляют два блока данных: протокол привязки и данные привязки. Протокол привязки определяет схему, посредством которой осуществляется связь, а данные привязки содержат сведения, используемые для доступа к сайту.  
  
 Ниже приведен пример элементов, которые могут присутствовать в привязке IIS.  
  
- Протокол привязки: HTTP  
  
- Данные привязки: IP-адрес, порт, заголовок узла  
  
 Службы IIS поддерживают задание нескольких привязок для каждого сайта, что позволяет использовать несколько базовых адресов для каждой схемы. До платформа .NET Framework 3,5 WCF не поддерживала несколько адресов для схемы и, если они были указаны, породил <xref:System.ArgumentException> во время активации.  
  
 Платформа .NET Framework 3,5 позволяет поставщикам услуг Интернета размещать несколько приложений с разными базовыми адресами для одной и той же схемы на одном сайте.  
  
 Например, сайт может содержать следующие базовые адреса:  
  
- `http://payroll.myorg.com/Service.svc`
  
- `http://shipping.myorg.com/Service.svc`
  
 В платформа .NET Framework 3,5 вы указываете фильтр префикса на уровне AppDomain в файле конфигурации. Это можно сделать с помощью [\<baseAddressPrefixFilters>](../../configure-apps/file-schema/wcf/baseaddressprefixfilters.md) элемента, который содержит список префиксов. Входящие базовые адреса, предоставляемые службами IIS, фильтруются с использованием необязательно списка префиксов. Если префикс не задан, по умолчанию пропускаются все адреса. При задании префикса разрешается прохождение данных только с соответствующего базового адреса для данной схемы.  
  
 Ниже приведен пример кода конфигурации, в котором используются фильтры префиксов.  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 В предыдущем примере `net.tcp://payroll.myorg.com:8000` и `http://shipping.myorg.com:8000` являются единственными базовыми адресами для соответствующих схем, которые передаются через.  
  
 Элемент `baseAddressPrefixFilter` не поддерживает подстановочные знаки.  
  
 Среди базовых адресов, предоставляемых службами IIS, могут присутствовать адреса, привязанные к другим схемам, не представленным в списке `baseAddressPrefixFilters`. Эти адреса не фильтруются.  
  
## <a name="multiple-iis-binding-support-in-net-framework-4-and-later"></a>Поддержка нескольких привязок служб IIS в платформе .NET Framework 4 и более поздних версиях  

 Начиная с .NET 4, в службах IIS можно включить поддержку нескольких привязок, при этом не требуется выбирать один базовый адрес. Для этого атрибуту <xref:System.ServiceModel.ServiceHostingEnvironment> элемента <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> необходимо задать значение true. Эта поддержка обеспечивается только для схем протокола HTTP.  
  
 Ниже приведен пример кода конфигурации, в котором используется Мултиплеситебиндингсенаблед On [\<serviceHostingEnvironment>](../../configure-apps/file-schema/wcf/servicehostingenvironment.md) .  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled="true" >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 Если с помощью этого параметра включены несколько привязок к узлам, все параметры baseAddressPrefixFilters не учитываются как для протокола HTTP, так и для других протоколов.  
  
 Дополнительные сведения и примеры см. в разделе [Поддержка нескольких привязок веб-узла IIS](supporting-multiple-iis-site-bindings.md) и <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> .  
  
## <a name="extending-addressing-in-wcf-services"></a>Расширение модели адресов в службах WCF  

 Модель адресации служб WCF по умолчанию использует URI адреса конечной точки в следующих целях:  
  
- задание адреса ожидания передачи данных службы, т. е. расположения, по которому конечная точка ожидает сообщений;  
  
- задание фильтра адресов SOAP, т. е. адреса, ожидаемого конечной точкой в качестве заголовка SOAP.  
  
 Значения в каждом из этих случаев могут задаваться отдельно, что позволяет реализовать несколько расширений модели адресов, которые можно использовать в следующих сценариях:  
  
- посредники протокола SOAP: сообщение, отправляемое клиентом, проходит через одну или несколько дополнительных служб, обрабатывающих это сообщение, прежде чем оно достигнет конечной точки назначения. Посредники протокола SOAP могут выполнять с сообщениями различные задачи, например кэширование, маршрутизацию или проверку схемы. Этот сценарий также можно реализовать путем отправки сообщения по отдельному физическому адресу (`via`), нацеленному на посредник, а не просто по логическому адресу (`wsa:To`), который нацелен на конечную точку назначения;  
  
- адрес ожидания передачи данных конечной точки является закрытым универсальным кодом ресурса (URI) и имеет значение, отличное от значения свойства `listenURI`.  
  
 Адрес транспорта, задаваемый параметром `via`, определяет расположение, через которое сообщение должно предварительно пройти по пути на какой-либо другой удаленный адрес, задаваемый параметром `to` и определяющий расположение службы. В большинстве случаев работы через Интернет значение универсального кода ресурса (URI) `via` совпадает со значением свойства <xref:System.ServiceModel.EndpointAddress.Uri%2A> конечного адреса `to` службы. При осуществлении маршрутизации вручную приходится выбирать только между этими двумя адресами.  
  
### <a name="addressing-headers"></a>Заголовки адресов  

 Помимо базового универсального кода ресурса (URI) к конечной точке можно обратиться по одному или нескольким заголовкам SOAP. К сценариям, в которых это бывает удобно, относятся сценарии с посредниками протокола SOAP, в которых конечная точка требует, чтобы клиенты включали заголовки SOAP, нацеленные на посредники.  
  
 Пользовательские заголовки адресов можно определять двумя способами - с помощью кода или файла конфигурации:  
  
- в коде создайте пользовательские заголовки адреса с помощью класса <xref:System.ServiceModel.Channels.AddressHeader>, а затем используйте их в конструкторе класса <xref:System.ServiceModel.EndpointAddress>;  
  
- В конфигурации пользовательские параметры задаются [\<headers>](../../configure-apps/file-schema/wcf/headers.md) как дочерние элементы [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) элемента.  
  
 Обычно рекомендуется использовать не код, а файл конфигурации, поскольку в этом случае заголовки можно будет менять после развертывания.  
  
### <a name="custom-listening-addresses"></a>Пользовательские адреса ожидания передачи данных  

 Можно задать адрес ожидания передачи данных, который отличается от универсального кода ресурса (URI) конечной точки. Это бывает удобно в сценариях с посредниками, когда предоставляемый адрес SOAP является адресом открытого посредника протокола SOAP, а адрес, по которому конечная точка ожидает передачи данных, является закрытым сетевым адресом.  
  
 Пользовательский адрес ожидания передачи данных можно задать с помощью кода или файла конфигурации:  
  
- для задания пользовательского адреса ожидания передачи данных в коде необходимо добавить класс <xref:System.ServiceModel.Description.ClientViaBehavior> в коллекцию расширений функциональности конечной точки;  
  
- В поле Конфигурация укажите настраиваемый адрес прослушивания с помощью `ListenUri` атрибута элемента Service [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) .  
  
### <a name="custom-soap-address-filter"></a>Пользовательский фильтр адресов SOAP  

 Свойство <xref:System.ServiceModel.EndpointAddress.Uri%2A> в сочетании со свойством <xref:System.ServiceModel.EndpointAddress.Headers%2A> позволяет определить фильтр адресов SOAP конечной точки (<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>). По умолчанию этот фильтр проверяет, что заголовок `To` входящего сообщения совпадает с универсальным кодом ресурса (URI) конечной точки и что в сообщении имеются все обязательные заголовки конечной точки.  
  
 В некоторых сценариях конечная точка получает все сообщения, которые приходят через соответствующий транспорт, а не только те, у которых есть соответствующий заголовок `To`. Чтобы включить такой режим, можно воспользоваться классом <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter>.  
  
## <a name="see-also"></a>См. также

- [Задание адреса конечной точки](../specifying-an-endpoint-address.md)
- [Идентификация и проверка подлинности службы](service-identity-and-authentication.md)
