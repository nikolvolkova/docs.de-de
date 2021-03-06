---
title: "Verwenden einer benutzerdefinierten Bindung mit dem Suchclientchannel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 36f95e75-04f7-44f3-a995-a0d623624d7f
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Verwenden einer benutzerdefinierten Bindung mit dem Suchclientchannel
Wenn Sie eine benutzerdefinierte Bindung mit <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> verwenden, müssen Sie ein <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>\-Objekt definieren, das <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>\-Instanzen erstellt.  
  
## Erstellen eines DiscoveryEndpointProvider\-Objekts  
 Das <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>\-Objekt ist für die Erstellung von [T:System:ServiceModel.Discovery.DiscoveryEndpoints](assetId:///T:System:ServiceModel.Discovery.DiscoveryEndpoints?qualifyHint=False&amp;autoUpgrade=True) nach Bedarf zuständig.Um einen Suchendpunktanbieter zu definieren, leiten Sie eine Klasse von <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> ab, überschreiben die <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider.GetDiscoveryEndpoint%2A>\-Methode und geben einen neuen Suchendpunkt zurück.Das folgende Beispiel zeigt, wie Sie einen Suchendpunktanbieter erstellen.  
  
```  
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
// to the DiscoveryClientBindingElement. The Discovery ClientChannel   
// uses this endpoint to send Probe message.  
public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
{  
   public override DiscoveryEndpoint GetDiscoveryEndpoint()  
   {  
      return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
   }  
}  
```  
  
 Sobald Sie den Suchendpunktanbieter definiert haben, können Sie eine benutzerdefinierte Bindung erstellen und das <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> hinzufügen, das auf den Suchendpunktanbieter verweist. Dies wird im folgenden Beispiel veranschaulicht.  
  
```  
DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
// Provide the search criteria and the endpoint over which the probe is sent.  
discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
// Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
// An exception is thrown if this binding element is not at the top.  
customBinding.Elements.Insert(0, discoveryBindingElement);  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zum Suchclientchannel finden Sie unter [Verwenden des Suchclientchannels](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md).Ein vollständiges Codebeispiel finden Sie unter [Beispiel für Ermittlungsbindungselement](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md)  
  
## Siehe auch  
 [Übersicht über die WCF\-Suche](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Verwenden des Suchclientchannels](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)   
 [Beispiel für Ermittlungsbindungselement](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md)