---
title: "Endpunktadressen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Adressen [WCF]"
  - "WCF [WCF], Adressen"
  - "Windows Communication Foundation [WCF], Adressen"
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Endpunktadressen
Jedem Endpunkt ist eine Adresse zugeordnet, um den Endpunkt suchen und identifizieren zu können.Diese Adresse besteht hauptsächlich aus einem Uniform Resource Identifier \(URI\), der den Speicherort des Endpunkts angibt.Die Endpunktadresse wird im [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Programmierungsmodell durch die <xref:System.ServiceModel.EndpointAddress>\-Klasse dargestellt, die eine optionale <xref:System.ServiceModel.EndpointAddress.Identity%2A>\-Eigenschaft für die Authentifizierung des Endpunkts durch andere Endpunkte, die Nachrichten mit ihm austauschen, sowie einen Satz optionaler <xref:System.ServiceModel.EndpointAddress.Headers%2A>\-Eigenschaften enthält, die eventuelle weitere SOAP\-Header definieren, die für das Erreichen des Diensts erforderlich sind.Die optionalen Header stellen zusätzliche und ausführlichere Adressinformationen bereit, um den Dienstendpunkt zu identifizieren oder mit ihm zu interagieren.Die Adresse eines Endpunkts wird während der Übertragung als WS\-Adressierungsendpunktverweis \(Endpoint Reference, EPR\) dargestellt.  
  
## URI\-Struktur einer Adresse  
 Der Adress\-URI besteht für die meisten Transporte aus vier Teilen.Der URI http:\/\/www.fabrikam.com:322\/mathservice.svc\/secureEndpoint setzt sich beispielsweise aus folgenden vier Teilen zusammen:  
  
-   Schema: http:  
  
-   Computer: www.fabrikam.com  
  
-   \(optional\) Anschluss: 322  
  
-   Pfad: \/mathservice.svc\/secureEndpoint  
  
## Definieren einer Adresse für einen Dienst  
 Die Endpunktadresse für einen Dienst kann entweder verbindlich durch Verwenden von Code oder deklarativ durch Konfiguration angegeben werden.Die Definition von Endpunkten im Code ist normalerweise nicht geeignet, da sich die Bindungen und die Adressen eines bereitgestellten Diensts normalerweise von denen unterscheiden, die während der Entwicklung des Diensts verwendet wurden.Im Allgemeinen ist es praktischer, Dienstendpunkte nicht mit Code, sondern mit Konfiguration zu definieren.Werden die Bindung und die Adressinformationen nicht in den Code integriert, ist eine Änderung ohne Neukompilierung oder eine erneute Bereitstellung der Anwendung möglich.  
  
### Definieren einer Adresse in der Konfiguration  
 Verwenden Sie das [\<Endpunkt \(endpoint\)\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)\-Element, um eine Endpunktadresse in der Konfigurationsdatei zu definieren.Weitere Informationen hierzu sowie ein Beispiel finden Sie unter [Angeben einer Endpunktadresse](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
### Definieren einer Adresse im Code  
 Eine Endpunktadresse kann mit der <xref:System.ServiceModel.EndpointAddress>\-Klasse im Code erstellt werden.Weitere Informationen hierzu sowie ein Beispiel finden Sie unter [Angeben einer Endpunktadresse](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
### Endpunkt in WSDL  
 Eine Endpunktadresse kann auch in WSDL \(Web Services Description Language\) als ein WS\-Addressierungs\-EPR\-Element innerhalb des `wsdl:port`\-Elements des entsprechenden Endpunkts dargestellt werden.Der EPR enthält die Endpunktadresse sowie eventuelle Adresseigenschaften.Weitere Informationen hierzu sowie ein Beispiel finden Sie unter [Angeben einer Endpunktadresse](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
## Unterstützung für mehrere IIS\-Bindungen in .NET Framework 3.5  
 Internetdienstanbieter hosten oftmals viele Anwendungen auf demselben Server und derselben Website, um die Websitedichte zu erhöhen und die Gesamtkosten \(TCO\) zu senken.Diese Anwendungen werden i. d. R. an unterschiedliche Basisadressen gebunden.Eine Internetinformationsdienste\(IIS\)\-Website kann mehrere Anwendungen enthalten.Auf die Anwendungen auf einer Website kann über eine oder mehrere IIS\-Bindungen zugegriffen werden.  
  
 IIS\-Bindungen stellen zwei Angaben bereit: ein Bindungsprotokoll und Bindungsinformationen.Das Bindungsprotokoll definiert das Schema, das für die Kommunikation verwendet wird, und die Bindungsinformationen dienen dem Zugriff auf die Website.  
  
 Das folgende Beispiel zeigt die Komponenten, die in einer IIS\-Bindung enthalten sein können:  
  
-   Bindungsprotokoll: HTTP  
  
-   Bindungsinformationen: IP\-Adresse, Anschluss, Hostheader  
  
 IIS kann mehrere Bindungen für jede Site angeben, was zu mehreren Basisadressen für jedes Schema führt.Vor [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] wurde die Verwendung mehrerer Adressen für ein Schema von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nicht unterstützt. Wurden dennoch mehrere Adressen angegeben, wurde bei der Aktivierung eine <xref:System.ArgumentException>.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] ermöglicht es Internetdienstanbietern, mehrere Anwendungen mit unterschiedlichen Basisadressen für dasselbe Schema auf derselben Website zu hosten.  
  
 Eine Website kann beispielsweise die folgenden Basisadressen enthalten:  
  
-   http:\/\/payroll.myorg.com\/Service.svc  
  
-   http:\/\/shipping.myorg.com\/Service.svc  
  
 Bei [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] geben Sie in der Konfigurationsdatei auf der AppDomain\-Ebene einen Präfixfilter an.Hierzu verwenden Sie das [\<baseAddressPrefixFilters\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md)\-Element, das eine Liste von Präfixen enthält.Die eingehenden, von IIS angegebenen Basisadressen werden anhand der optionalen Präfixliste gefiltert.Standardmäßig werden alle Adressen übergeben, wenn ein Präfix nicht angegeben ist.Wenn die Präfixergebnisse angegeben werden, wird nur die Basisadresse übergeben, die dem Schema entspricht.  
  
 Es folgt ein Beispiel für Konfigurationscode, der die Präfixfilter verwendet.  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 Im vorangehenden Beispiel sind net.tcp:\/\/payroll.myorg.com:8000 und http:\/\/shipping.myorg.com:8000 die einzigen Basisadressen \(für die entsprechenden Schemas\), die übergeben werden.  
  
 Der `baseAddressPrefixFilter` unterstützt keine Platzhalter.  
  
 Die von IIS angegebenen Basisadressen verfügen möglicherweise über Adressen, die an andere, nicht in der `baseAddressPrefixFilters`\-Liste vorhandene Schemas gebunden sind.Diese Adressen werden nicht herausgefiltert.  
  
## Unterstützung für mehrere IIS\-Bindungen in .NET Framework 4 und höher  
 Ab .NET 4 können Sie die Unterstützung für mehrere Bindungen in IIS aktivieren, ohne eine Basisadresse auswählen zu müssen. Legen Sie dazu die Einstellung <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> von <xref:System.ServiceModel.ServiceHostingEnvironment> auf True fest.Die Unterstützung ist auf HTTP\-Protokollschemas begrenzt.  
  
 Es folgt ein Beispiel für Konfigurationscode, der multipleSiteBindingsEnabled in [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) verwendet.  
  
```  
  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled=”true” >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 Wenn mehrere Websitebindungen mit dieser Einstellung aktiviert wurden, werden alle Einstellungen von baseAddressPrefixFilters sowohl für HTTP\-Protokolle als auch für andere Protokolle ignoriert.  
  
 Detaillierte Informationen und Beispiele finden Sie unter [Unterstützen mehrerer IIS\-Sitebindungen](../../../../docs/framework/wcf/feature-details/supporting-multiple-iis-site-bindings.md) und <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A>.  
  
## Erweitern der Adressierung in WCF\-Diensten  
 Das Standardadressierungsmodell von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Diensten verwendet den Endpunktadress\-URI für die folgenden Zwecke:  
  
-   Um die Abhöradresse des Diensts anzugeben, d. h. den Speicherort, den der Endpunkt auf Nachrichten abhört  
  
-   Um den SOAP\-Adressfilter anzugeben, d. h. die Adresse, die ein Endpunkt als SOAP\-Header erwartet  
  
 Die Werte für beide Situationen können separat angegeben werden. Dadurch werden mehrere Adressierungserweiterungen für nützliche Szenarien möglich:  
  
-   SOAP\-Vermittler: Eine von einem Client gesendete Nachricht durchläuft einen oder mehrere zusätzliche Dienste, die die Nachricht verarbeiten, bevor sie ihr endgültiges Ziel erreicht.SOAP\-Vermittler können verschiedene Aufgaben ausführen, z. B. Caching, Routing, Lastenausgleich oder Schemavalidierung für Nachrichten.Dieses Szenario wird durch das Senden von Nachrichten an eine separate physische Adresse erreicht \(`via`\), die auf den Vermittler verweist, anstatt nur an eine logische Adresse \(`wsa:To`\), die auf das endgültige Ziel verweist.  
  
-   Die Abhöradresse des Endpunkts ist ein privater URI und wird auf einen anderen Wert als seine `listenURI`\-Eigenschaft festgelegt.  
  
 Nachrichten sollten zunächst an die Transportadresse gesendet werden, die von `via` angegeben wird, bevor sie an eine andere Remoteadresse gesendet werden, die vom `to`\-Parameter angegeben wird und an der sich der Dienst befindet.In den meisten Internetszenarien sind der `via`\-URI der <xref:System.ServiceModel.EndpointAddress.Uri%2A>\-Eigenschaft und die endgültige `to`\-Adresse des Diensts identisch.Eine Unterscheidung zwischen den beiden Adressen ist nur beim manuellen Routing erforderlich.  
  
### Adressierungsheader  
 Ein Endpunkt kann neben seinem Basis\-URI von einem oder mehreren SOAP\-Headern adressiert werden.Dies ist beispielsweise in SOAP\-Vermittlerszenarien nützlich, in denen ein Endpunkt es erfordert, dass seine Clients SOAP\-Header einfügen, die sich an Vermittler richten.  
  
 Sie können benutzerdefinierte Adressheader auf zweierlei Weise definieren – entweder mit Code oder einer Konfiguration:  
  
-   Im Code werden benutzerdefinierte Adressheader mithilfe der <xref:System.ServiceModel.Channels.AddressHeader>\-Klasse erstellt und dann bei der Erstellung einer <xref:System.ServiceModel.EndpointAddress> verwendet.  
  
-   In Konfigurationen werden benutzerdefinierte [\<Kopfzeilen\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)[\<endpoint\> als untergeordnete Elemente des](http://msdn.microsoft.com/de-de/13aa23b7-2f08-4add-8dbf-a99f8127c017)\-Elements angegeben.  
  
 Die Konfiguration ist im Allgemeinen dem Code vorzuziehen, da sie es Ihnen ermöglicht, die Header nach der Bereitstellung zu ändern.  
  
### Benutzerdefinierte Abhöradressen  
 Sie können die Abhöradresse auf einen anderen Wert als den URI des Endpunkts festlegen.Das ist in Vermittlerszenarios nützlich, in denen die SOAP\-Adresse, die verfügbar gemacht werden soll, die eines öffentlichen SOAP\-Vermittlers ist, während die Adresse, an der der Endpunkt lauscht, eine private Netzwerkadresse ist.  
  
 Sie können eine benutzerdefinierte Abhöradresse angeben, indem Sie entweder Code oder eine Konfiguration verwenden:  
  
-   Im Code geben Sie eine benutzerdefinierte Abhöradresse durch Hinzufügen einer <xref:System.ServiceModel.Description.ClientViaBehavior>\-Klasse zur Verhaltensauflistung des Endpunkts an.  
  
-   In einer Konfiguration geben Sie eine benutzerdefinierte Lauschadresse mit dem `ListenUri`\-Attribut des [\<endpoint\>](http://msdn.microsoft.com/de-de/13aa23b7-2f08-4add-8dbf-a99f8127c017)\-Elements des Diensts an.  
  
### Benutzerdefinierter SOAP\-Adressenfilter  
 Der <xref:System.ServiceModel.EndpointAddress.Uri%2A> wird in Verbindung mit einer beliebigen <xref:System.ServiceModel.EndpointAddress.Headers%2A>\-Eigenschaft zur Definition des SOAP\-Adressfilters eines Endpunkts verwendet \(<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>\).Standardmäßig prüft dieser Filter, ob eine eingehende Nachricht über einen `To`\-Nachrichtenheader verfügt, der mit dem URI des Endpunkts übereinstimmt, und ob alle erforderlichen Endpunktheader in der Nachricht vorhanden sind.  
  
 In einigen Szenarien empfängt ein Endpunkt alle Nachrichten, die mit dem zugrunde liegenden Transport ankommen, und nicht nur die mit dem entsprechenden `To`\-Header.Um dies zu aktivieren, kann der Benutzer die <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter>\-Klasse verwenden.  
  
## Siehe auch  
 [Angeben einer Endpunktadresse](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)   
 [Dienstidentität und Authentifizierung](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)