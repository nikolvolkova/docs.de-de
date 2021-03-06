---
title: "Benutzerdefinierter Nachrichtenfilter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98dd0af8-fce6-4255-ac32-42eb547eea67
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Benutzerdefinierter Nachrichtenfilter
In diesem Beispiel wird gezeigt, wie die Nachrichtenfilter ersetzt werden, mit denen [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] Nachrichten auf Endpunkte verteilt.  
  
> [!NOTE]
>  Die Setupprozedur und die Erstellungsanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Wenn die erste Nachricht auf einem Kanal beim Server eintrifft, muss der Server bestimmen, welcher der mit diesem URI verknüpften Endpunkte \(sofern zutreffend\) die Nachricht erhalten soll.Dieser Prozess wird von den an den <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> angefügten <xref:System.ServiceModel.Dispatcher.MessageFilter>\-Objekten kontrolliert.  
  
 Jeder Endpunkt eines Diensts hat einen einzelnen <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.Der <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> besitzt sowohl einen <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> als auch einen <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>.Die Verbindung dieser beiden Filter ist der für diesen Endpunkt verwendete Nachrichtenfilter.  
  
 Standardmäßig stimmt der <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> für einen Endpunkt mit jeder Nachricht überein, die an eine Adresse gesendet wird, die wiederum mit der <xref:System.ServiceModel.EndpointAddress> des Dienstendpunkts übereinstimmt.Der <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> für einen Endpunkt überprüft standardmäßig die Aktion der eingehenden Nachricht und gleicht jede Nachricht mit einer Aktion ab, die einer der Aktionen der Vorgänge des Dienstendpunktvertrags entspricht \(es werden nur `IsInitiating`\=`true`\-Aktionen berücksichtigt\).Demzufolge stimmt der Filter für einen Endpunkt standardmäßig nur überein, wenn sowohl der To\-Header der Nachricht die <xref:System.ServiceModel.EndpointAddress> des Endpunkts ist als auch die Aktion der Nachricht mit einer der Aktionen der Endpunktvorgänge übereinstimmt.  
  
 Diese Filter können mit einer Verhaltensweise geändert werden.Im folgenden Beispiel erstellt der Dienst ein <xref:System.ServiceModel.Description.IEndpointBehavior>, das den <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> und den <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> auf dem <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> ersetzt:  
  
```  
class FilteringEndpointBehavior : IEndpointBehavior …  
```  
  
 Es werden zwei Adressfilter definiert:  
  
```  
// Matches any message whose To address contains the letter 'e'  
class MatchEAddressFilter : MessageFilter …  
// Matches any message whose To address does not contain the letter 'e'  
class MatchNoEAddressFilter : MessageFilter  
```  
  
 Das `FilteringEndpointBehavior` wird konfigurierbar gemacht und ermöglicht zwei verschiedene Varianten.  
  
```  
public class FilteringEndpointBehaviorExtension : BehaviorExtensionElement  
  
```  
  
 Variante 1 gleicht nur Adressen ab, die ein "e" \(aber eine beliebige Aktion\) enthalten, wohingegen Variante 2 nur die Adressen ohne "e" abgleicht:  
  
```  
if (Variation == 1)  
    return new FilteringEndpointBehavior(  
        new MatchEAddressFilter(), new MatchAllMessageFilter());  
else  
    return new FilteringEndpointBehavior(  
        new MatchNoEAddressFilter(), new MatchAllMessageFilter());  
  
```  
  
 Der Dienst registriert das neue Verhalten in der Konfigurationsdatei:  
  
```  
<extensions>  
    <behaviorExtensions>  
        <add name="filteringEndpointBehavior" type="Microsoft.ServiceModel.Samples.FilteringEndpointBehaviorExtension, service" />  
    </behaviorExtensions>  
</extensions>      
```  
  
 Anschließend erstellt der Dienst `endpointBehavior`\-Konfigurationen für jede Variante:  
  
```  
<endpointBehaviors>  
    <behavior name="endpoint1">  
        <filteringEndpointBehavior variation="1" />  
    </behavior>  
    <behavior name="endpoint2">  
        <filteringEndpointBehavior variation="2" />  
    </behavior>  
</endpointBehaviors>  
  
```  
  
 Schließlich verweist der Endpunkt des Diensts auf eine der `behaviorConfigurations`:  
  
```  
<endpoint address=""  
        bindingConfiguration="ws"  
        listenUri=""   
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IHello"   
        behaviorConfiguration="endpoint2" />  
  
```  
  
 Die Implementierung der Clientanwendung ist einfach. Sie erstellt zwei Kanäle zum URI des Diensts \(indem der Wert als der zweite \(`via`\)\-Parameter an <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29> übergeben wird\) und sendet eine einzelne Nachricht auf jedem Kanal, verwendet aber jeweils verschiedene Endpunktadressen.Infolgedessen besitzen die vom Client ausgehenden Nachrichten unterschiedliche To\-Ziele, und der Server antwortet entsprechend, wie von der Ausgabe des Clients veranschaulicht:  
  
```  
Sending message to urn:e...  
Exception: The message with To 'urn:e' cannot be processed at the receiver, due to an AddressFilter mismatch at the EndpointDispatcher.  Check that the sender and receiver's EndpointAddresses agree.  
  
Sending message to urn:a...  
Hello  
```  
  
 Durch einen Wechsel der Variante in der Konfigurationsdatei des Servers wird der Filter getauscht, und der Client sieht das andere Verhalten \(die Nachricht an `urn:e` ist erfolgreich, die Nachricht an `urn:a` jedoch nicht\).  
  
```  
<endpoint address=""  
          bindingConfiguration="ws"  
          listenUri=""   
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.IHello"   
          behaviorConfiguration="endpoint1" />  
  
```  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Überprüfen Sie das folgende \(standardmäßige\) Verzeichnis, bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageFilter`  
  
### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Folgen Sie den unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen, um die Projektmappe zu erstellen.  
  
2.  Wenn Sie das Beispiel in einer Konfiguration mit einem einzigen Computer ausführen möchten, folgen Sie den unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md) aufgeführten Anweisungen.  
  
3.  Wenn Sie das Beispiel in einer computerübergreifenden Konfiguration ausführen möchten, befolgen Sie die Anweisungen in [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md), und ändern Sie die folgende Zeile in "Client.cs".  
  
    ```  
    Uri serviceVia = new Uri("http://localhost/ServiceModelSamples/service.svc");  
    ```  
  
     Ersetzen Sie "localhost" mit dem Namen des Servers.  
  
    ```  
    Uri serviceVia = new Uri("http://servermachinename/ServiceModelSamples/service.svc");  
    ```  
  
## Siehe auch