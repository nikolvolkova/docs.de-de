---
title: "&lt;comContract&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f8e1c0c-cfdf-4c79-ac65-c64e9323a51c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;comContract&gt;
Gibt einen Dienstvertrag für die COM\+\-Integration an.  
  
## Syntax  
  
```  
  
<comContracts>  
  <comContract  
      contract="string"  
      namespace="string"  
      name="string"  
      requireSession="Boolean">  
      <exposedMethods>  
         <exposedMethod name="string" />  
      </exposedMethods>  
      <userDefinedTypes>  
         <userDefinedType name="string"  
            typeLibID="string"  
            typeLibVersion="string"  
            typeDefID="string">  
         </userDefinedType>  
      </userDefinedTypes>  
      <persistableTypes>  
         <persistableType id="string"  
            name="string">  
         </persistableType>  
      </persistableTypes>  
  </comContract>  
</comContracts>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|Vertrag \(Contract\)|Eine Zeichenfolge, die den Vertragstyp enthält.|  
|Name|Eine Zeichenfolge, die den Vertragsnamen enthält.|  
|namespace|Eine Zeichenfolge, die den Vertragsnamespace enthält.|  
|requiresSession|Ein boolescher Wert, der angibt, ob der Vertrag nur für sitzungsbasierte Bindungen verwendet werden kann.  Bei der Initialisierung des Diensts wird von der Integrationslaufzeit sichergestellt, dass diese Einstellung mit dem verwendeten Bindungstyp übereinstimmt.  Eine Ausnahme wird generiert, wenn eine oder mehrere Bindungen für den Vertrag miteinander in Konflikt stehen.  Wenn die Eigenschaft `false` ist, ein Einwegkanal verwendet wird und \[out\]\-Parameter vorhanden sind, wird ebenfalls eine Ausnahme generiert.|  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|persistableTypes|Alle dauerhaften Typen.|  
|userDefinedTypes|Eine Auflistung benutzerdefinierter Typen \(UDT\), die im Dienstvertrag verwendet werden soll.|  
|exposedMethods|Eine Auflistung von COM\+\-Methoden, die verfügbar gemacht werden, wenn die Schnittstelle für eine COM\+\-Komponente als Webdienst bereitgestellt wird.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|comContracts|Enthält eine Auflistung von `comContract`\-Elementen.|  
  
## Hinweise  
 Die COM\+\-Integrationsdienstverträge sind aktuell auf den Namespace 'http:\/\/tempuri.org' beschränkt, und der Vertragsname wird von der unterstützenden COM\-Schnittstelle abgeleitet.  Sie können Alternativen aber angeben, indem Sie den `comContracts`\-Abschnitt und das `comContract`\-Element in der Konfigurationsdatei verwenden.  Sie können beispielsweise folgende Konfiguration zum Angeben des Namespaces, des Vertragsnamens, der benutzerdefinierten Typen und anderer Einstellungen für einen Dienstvertrag verwenden.  
  
```  
<comContracts>  
  <comContract  
      contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"  
      namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"  
      name="_Broker"  
      requireSession="true">  
      <exposedMethods>  
         <exposedMethod name="BuyStock" />  
         <exposedMethod name="SellStock" />  
         <exposedMethod name="ExecuteTransaction" />  
      </exposedMethods>  
  </comContract>  
</comContracts>  
```  
  
 Wenn der Dienst initialisiert wird, werden die angegebenen Namespaces und Vertragsnamen auf die generierten Dienstbeschreibungen angewendet.  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>   
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>   
 <xref:System.ServiceModel.Configuration.ComContractElement>   
 [\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)   
 [Integrieren von COM\+\-Anwendungen](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Vorgehensweise: Konfigurieren von COM\+\-Diensteinstellungen](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)