---
title: '&lt;netNamedPipeBinding&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
ms.assetid: 00a8580b-face-47a4-838d-b9fed48e72df
caps.latest.revision: 29
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a5854b3f2630c1e27ec77976eccfe6765acefcab
ms.contentlocale: de-de
ms.lasthandoff: 09/25/2017

---
# <a name="ltnetnamedpipebindinggt"></a>&lt;netNamedPipeBinding&gt;
Definiert eine Bindung, die sicher und zuverlässig ist und für eine prozessübergreifende Kommunikation auf einem Computer optimiert ist. Sie generiert standardmäßig einen Laufzeitkommunikationsstapel mit WS-ReliableMessaging für Verlässlichkeit, Transport- und Übertragungssicherheit, benannte Pipes für den Nachrichtentransport sowie binäre Nachrichtencodierung.  
  
 \<System. ServiceModel >  
\<Bindungen >  
\<NetNamedPipeBinding >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<netNamedPipeBinding>  
   <binding   
      closeTimeout="TimeSpan"  
      hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"  
      maxBufferPoolSize="Integer"  
      maxBufferSize="Integer"  
      maxConnections="Integer"   
      maxReceivedMessageSize="Integer"  
            name="string"  
      openTimeout="TimeSpan"   
      receiveTimeout="TimeSpan"  
      sendTimeout="TimeSpan"  
      transactionFlow="Boolean"  
      transactionProtocol="OleTransactions/WS-AtomicTransactionOctober2004"  
            transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"  
      <security mode="None/Transport">  
            <transport  protectionLevel="None/Sign/EncryptAndSign" />  
      </security>  
       <readerQuotas             maxArrayLength="Integer"            maxBytesPerRead="Integer"            maxDepth="Integer"             maxNameTableCharCount="Integer"                     maxStringContentLength="Integer" />   </binding>  
</netNamedPipeBinding>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute, untergeordnete Elemente sowie übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|closeTimeout|Ein <xref:System.TimeSpan>-Wert, der das Zeitintervall für den Abschluss eines Schließvorgangs angibt. Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein. Der Standardwert ist 00:01:00.|  
|hostnameComparisonMode|Gibt den HTTP-Hostnamen-Vergleichsmodus an, der verwendet wird, um URIs zu analysieren. Dieses Attribut ist vom Typ `System.ServiceModel.HostnameComparisonMode` und gibt an, ob beim Abgleich des URI der Hostname zum Erreichen des Dienstes verwendet wird. Der Standardwert lautet `StrongWildcard`, wodurch der Hostname beim Abgleich ignoriert wird.|  
|maxBufferPoolSize|Eine ganze Zahl, die die maximale Pufferpoolgröße für diese Bindung angibt. Der Standardwert ist 524.288 Byte (512 * 1024). Viele Teile von Windows Communication Foundation (WCF) verwenden Puffer. Das Erstellen und Zerstören von Puffern bei jeder Verwendung ist kostspielig. Dasselbe gilt für die Garbage Collection für Puffer. Bei Pufferpools können Sie einen zu verwendenden Puffer aus dem Pool nehmen und ihn nach der Verwendung wieder dem Pool zuführen. So wird der Aufwand beim Erstellen und Zerstören von Puffern vermieden.|  
|maxBufferSize|Eine positive ganze Zahl, die die maximale Größe des Puffers in Bytes angibt, der zum Speichern von Nachrichten verwendet wird. Falls der Puffer voll ist, verbleiben die überzähligen Daten so lange im zugrunde liegenden Socket, bis der Puffer wieder Platz bietet. Dieser Wert darf nicht kleiner sein als das `maxReceivedMessageSize`-Attribut. Der Standard ist 65536. Weitere Informationen finden Sie unter <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.|  
|maxConnections|Eine ganze Zahl, die die maximale Anzahl ausgehender und eingehender Verbindungen angibt, die der Dienst erstellt bzw. akzeptiert. Eingehende und ausgehende Verbindungen werden mit einem separaten, von diesem Attribut angegebenen Grenzwert verglichen.<br /><br /> Eingehende Verbindungen, die diesen Grenzwert überschreiten, werden in die Warteschlange gestellt, bis wieder Speicherplatz verfügbar wird.<br /><br /> Ausgehende Verbindungen, die diesen Grenzwert überschreiten, werden in die Warteschlange gestellt, bis wieder Speicherplatz verfügbar wird.<br /><br /> Der Standard ist 10.|  
|maxReceivedMessageSize|Eine positive ganze Zahl, die die maximale Nachrichtengröße in Bytes einschließlich Header angibt, die in einem für diese Bindung konfigurierten Kanal beim Nachrichtenempfang zulässig ist. Der Absender einer Nachricht, die diese Grenze überschreitet, erhält einen SOAP-Fehler. Der Empfänger verwirft die Nachricht und erstellt einen Eintrag des Ereignisses im Ablaufverfolgungsprotokoll. Der Standard ist 65536.|  
|Name|Eine Zeichenfolge, die den Konfigurationsnamen der Bindung enthält. Dieser Wert sollte eindeutig sein, da er von der Bindung zur Identifizierung verwendet wird. Ab [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] müssen Bindungen und Verhalten keinen Namen aufweisen. Weitere Informationen zur Standardkonfiguration und namenlos Bindungen und Verhaltensweisen finden Sie unter [vereinfachte Konfiguration](../../../../../docs/framework/wcf/simplified-configuration.md) und [vereinfachte Konfiguration für WCF-Dienste](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Ein <xref:System.TimeSpan>-Wert, der das Zeitintervall für den Abschluss eines Öffnungsvorgangs angibt. Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein. Der Standardwert ist 00:01:00.|  
|receiveTimeout|Ein <xref:System.TimeSpan>-Wert, der das Zeitintervall für den Abschluss eines Empfangsvorgangs angibt. Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein. Der Standardwert ist 00:10:00.|  
|sendTimeout|Ein <xref:System.TimeSpan>-Wert, der das Zeitintervall für den Abschluss eines Sendevorgangs angibt. Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein. Der Standardwert ist 00:01:00.|  
|transactionFlow|Ein boolescher Wert, der angibt, ob die Bindung geleitete WS-Transaktionen unterstützt. Die Standardeinstellung ist `false`.|  
|transactionProtocol|Gibt das Transaktionsprotokoll an, das mit dieser Bindung verwendet werden soll. Folgende Werte sind gültig:<br /><br /> -OleTransactions<br />WS-AtomicTransactionOctober2004<br /><br /> Der Standardwert ist OleTransactions. Dieses Attribut ist vom Typ <xref:System.ServiceModel.TransactionProtocol>.|  
|transferMode|Ein <xref:System.ServiceModel.TransferMode>-Wert, der angibt, ob Nachrichten bei einer Anforderung oder Antwort gepuffert oder per Stream übertragen werden.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Sicherheit >](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netnamedpipebinding.md)|Definiert die Sicherheitseinstellungen für die Bindung. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement>.|  
|[\<ReaderQuotas >](http://msdn.microsoft.com/library/3e5e42ff-cef8-478f-bf14-034449239bfd)|Definiert die Beschränkungen der Komplexität von SOAP-Nachrichten, die von Endpunkten verarbeitet werden können, die mit dieser Bindung konfiguriert wurden. Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Bindungen >](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Dieses Element enthält eine Auflistung von standardmäßigen und benutzerdefinierten Bindungen.|  
  
## <a name="remarks"></a>Hinweise  
 `NetNamedPipeBinding` generiert standardmäßig eine Laufzeitkommunikation, die Transportsicherheit, Named Pipes zur Nachrichtenübermittlung und eine binäre Nachrichtencodierung verwendet. Diese Bindung ist eine entsprechende vom System bereitgestellte Windows Communication Foundation (WCF)-Wahl für die computerinterne Kommunikation. Sie unterstützt auch Transaktionen.  
  
 Die Standardkonfiguration für `NetNamedPipeBinding` ähnelt der Konfiguration, die von `NetTcpBinding` bereitgestellt wird, sie ist jedoch einfacher, da die WCF-Implementierung nur für die computerinterne Verwendung konzipiert ist und daher weniger Funktionen verfügbar sind. Der wichtigste Unterschied besteht darin, dass die `securityMode`-Einstellung nur die Optionen `None` und `Transport` anbietet. SOAP-Sicherheitsunterstützung ist keine eingeschlossene Option. Das Sicherheitsverhalten ist mit dem optionalen `securityMode`-Attribut konfigurierbar.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die netNamedPipeBinding-Bindung, die prozessübergreifende Kommunikation auf dem gleichen Computer bereitstellt, veranschaulicht. Benannte Pipes funktionieren nicht computerübergreifend.  
  
 Die Bindung wird in den Konfigurationsdateien für den Client und Dienst angegeben. Der Bindungstyp wird im `binding`-Attribut des `<endpoint>`-Elements angegeben. Wenn Sie die netNamedPipeBinding-Bindung konfigurieren und einige der Einstellungen ändern möchten, müssen Sie eine Bindungskonfiguration definieren. Der Endpunkt muss auf die Bindungskonfiguration mithilfe des `bindingConfiguration`-Attributs mit einem Namen verweisen. In diesem Beispiel wird die Bindungskonfiguration „Binding1“ genannt.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
               behaviorConfiguration="CalculatorServiceBehavior">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
          </baseAddresses>  
        </host>  
        <!-- this endpoint is exposed at the base address provided by host: net.pipe://localhost/ServiceModelSamples/service  -->  
        <endpoint address="net.pipe://localhost/ServiceModelSamples/service"  
                  binding="netNamedPipeBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <bindings>  
      <netNamedPipeBinding>  
        <binding   
                 closeTimeout="00:01:00"  
                 openTimeout="00:01:00"   
                 receiveTimeout="00:10:00"   
                 sendTimeout="00:01:00"  
                 transactionFlow="false"   
                 transferMode="Buffered"   
                 transactionProtocol="OleTransactions"  
                 hostNameComparisonMode="StrongWildcard"   
                 maxBufferPoolSize="524288"  
                 maxBufferSize="65536"   
                 maxConnections="10"   
                 maxReceivedMessageSize="65536">  
          <security mode="Transport">  
            <transport protectionLevel="EncryptAndSign" />  
          </security>  
        </binding>  
      </netNamedPipeBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement>   
 <xref:System.ServiceModel.NetNamedPipeBinding>   
 [\<Binden von >](../../../../../docs/framework/misc/binding.md)   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Konfigurieren der vom System bereitgestellte Bindungen](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Verwenden von Bindungen, um Windows Communication Foundation-Dienste und Clients konfigurieren](http://msdn.microsoft.com/en-us/bd8b277b-932f-472f-a42a-b02bb5257dfb)

