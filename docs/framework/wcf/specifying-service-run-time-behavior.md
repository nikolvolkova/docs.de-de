---
title: "Angeben des Dienstlaufzeitverhaltens | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Angeben des Dienstlaufzeitverhaltens
Nachdem Sie einen Dienstvertrag entworfen \([Entwerfen von Dienstverträgen](../../../docs/framework/wcf/designing-service-contracts.md)\) und implementiert \([Implementieren von Dienstverträgen](../../../docs/framework/wcf/implementing-service-contracts.md)\) haben, können Sie das Vorgangsverhalten der Dienstlaufzeit konfigurieren. In diesem Thema werden vom System bereitgestellte Dienste und Vorhangsverhalten erörtert und beschrieben, wo Sie weitere Informationen zur Erstellung neuer Verhalten finden. Einige Verhalten werden als Attribute angewendet, aber viele Verhalten werden mithilfe einer Konfigurationsdatei oder programmgesteuert angewendet.[!INCLUDE[crabout](../../../includes/crabout-md.md)] zur Konfiguration einer Dienstanwendung finden Sie unter [Konfigurieren von Diensten](../../../docs/framework/wcf/configuring-services.md).  
  
## Übersicht  
 Der Vertrag definiert die Eingaben, Ausgaben, Datentypen und Fähigkeiten eines Diensts dieses Typs. Durch die Implementierung eines Dienstvertrags wird eine Klasse erstellt, die den durch sie implementierten Vertrag erfüllt, wenn sie mit einer Bindung an einer Adresse konfiguriert wird. Der Vertrag kennt Vertrags\-, Bindungs\- und Adressinformationen. Ohne sie kann der Client den Dienst nicht nutzen.  
  
 Aber Vorgangseinzelheiten, z.&\#160;B. Threadingprobleme oder Instanzenverwaltung, sind für Clients nicht transparent. Nachdem ein Dienstvertrag implementiert wurde, können Sie mithilfe von *Verhalten* eine Vielzahl von Vorgangseigenschaften konfigurieren. Verhalten sind die Objekte, die das [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]\-Laufzeitmodul verändern, indem eine Laufzeiteigenschaft festgelegt oder ein Anpassungstyp in das Laufzeitmodul eingefügt wird.[!INCLUDE[crabout](../../../includes/crabout-md.md)] zur Änderung des Laufzeitmoduls durch benutzerdefinierte Verhalten finden Sie unter [Erweitern von ServiceHost und der Dienstmodellebene](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md).  
  
 Das <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=fullName>\-Attribut und das <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=fullName>\-Attribute sind die Verhalten, die am häufigsten verwendet werden, und sie machen die am häufigsten angeforderten Vorgangsfunktionen verfügbar. Weil es sich um Attribute handelt, wenden Sie sie auf die Dienst\- oder Vorgangsimplementierung an. Andere Verhalten, wie z.&\#160;B. <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> oder <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=fullName>, werden in der Regel mithilfe einer Anwendungskonfigurationsdatei angewendet, obwohl sie auch im Code verwendet werden können.  
  
 Dieses Thema bietet einen Überblick über die Attribute <xref:System.ServiceModel.ServiceBehaviorAttribute> und <xref:System.ServiceModel.OperationBehaviorAttribute>. Es werden die verschiedenen Bereiche beschrieben, in denen Verhalten wirksam sein können, und das Thema enthält Kurzbeschreibungen vieler vom System bereitgestellten Verhalten für die verschiedenen Bereiche, die für [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Entwickler von Interesse sein können.  
  
## ServiceBehaviorAttribute und OperationBehaviorAttribute  
 Die wichtigsten Verhalten sind das <xref:System.ServiceModel.ServiceBehaviorAttribute>\-Attribut und das <xref:System.ServiceModel.OperationBehaviorAttribute>\-Attribut, mit denen Sie Folgendes steuern können:  
  
-   Lebensdauer von Instanzen  
  
-   Unterstützung für Parallelität und Synchronisierung  
  
-   Konfigurationsverhalten  
  
-   Transaktionsverhalten  
  
-   Serialisierungsverhalten  
  
-   Metadatentransformation  
  
-   Sitzungslebensdauer  
  
-   Adressfilterung und Headerverarbeitung  
  
-   Identitätswechsel  
  
-   Sie verwenden diese Attribute, indem Sie eine Dienst\- oder Vorgangsimplementierung mit dem für den betreffenden Bereich geeigneten Attribut markieren und die Eigenschaften festlegen. Im folgenden Codebeispiel wird eine Vorgangsimplementierung veranschaulicht, in der mithilfe der <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=fullName>\-Eigenschaft festgelegt wird, dass Aufrufer dieses Vorgangs Identitätswechsel unterstützen müssen.  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 Viele dieser Eigenschaften erfordern zusätzliche Unterstützung von der Bindung. Beispielsweise muss ein Vorgang, der von einem Client eine Transaktion erfordert, so konfiguriert werden, dass eine Bindung verwendet wird, die übergegangene Transaktionen unterstützt.  
  
### Bekannte Singleton\-Dienste  
 Sie können mit dem <xref:System.ServiceModel.ServiceBehaviorAttribute>\-Attribut und dem <xref:System.ServiceModel.OperationBehaviorAttribute>\-Attribut sowohl bei <xref:System.ServiceModel.InstanceContext> als auch bei den Dienstobjekten, die die Vorgänge implementieren, die Lebensdauer bestimmter Objekte steuern.  
  
 Beispielsweise wird über die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName>\-Eigenschaft gesteuert, wie oft der <xref:System.ServiceModel.InstanceContext> freigegeben wird, und die <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName>\-Eigenschaft und die <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=fullName>\-Eigenschaft bestimmen, wann das Dienstobjekt freigegeben wird.  
  
 Sie können jedoch auch selbst ein Dienstobjekt und den Diensthost, der dieses Objekt verwendet, erstellen. Hierfür müssen Sie auch die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName>\-Eigenschaft auf <xref:System.ServiceModel.InstanceContextMode> festlegen, damit keine Ausnahme ausgelöst wird, sobald der Diensthost geöffnet wird.  
  
 Verwenden Sie zum Erstellen eines solchen Diensts den [ServiceHost.ServiceHost\(Object, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=fullName>\-Konstruktor. Dieser stellt eine Alternative zur Implementierung eines benutzerdefinierten <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=fullName> dar, wenn Sie eine bestimmte Objektinstanz für einen Singleton\-Dienst bereitstellen möchten. Sie können diese Überladung verwenden, wenn der Dienstimplementierungstyp schwer zu erstellen ist \(wenn er z.&\#160;B. keinen öffentlichen parameterlosen Standardkonstruktor implementiert\).  
  
 Beachten Sie, dass einige Funktionen im Zusammenhang mit dem [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]\-Instanziierungsverhalten anders arbeiten, wenn ein Objekt für diesen Konstruktor bereitgestellt wird. So zeigt zum Beispiel der Aufruf von <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=fullName> keine Wirkung, wenn eine bekannte Objektinstanz bereitgestellt wird. Dementsprechend werden auch alle anderen Instanzfreigabemechanismen ignoriert. Die <xref:System.ServiceModel.ServiceHost>\-Klasse verhält sich immer so, als ob die <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName>\-Eigenschaft für alle Vorgänge auf <xref:System.ServiceModel.ReleaseInstanceMode?displayProperty=fullName> festgelegt ist.  
  
## Andere Dienst\-, Endpunkt\-, Vertrags\- und Vorgangsverhalten  
 Dienstverhalten, z.&\#160;B. das <xref:System.ServiceModel.ServiceBehaviorAttribute>\-Attribut, wirken sich auf den gesamten Dienst aus. Wenn Sie beispielsweise die <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName>\-Eigenschaft auf <xref:System.ServiceModel.ConcurrencyMode?displayProperty=fullName>\-festlegen, müssen Sie Threadsynchronisierungsprobleme in jedem Vorgang innerhalb des betreffenden Diensts selbst behandeln. Endpunktverhalten operieren über einen Endpunkt. Viele der vom System bereitgestellten Endpunktverhalten beeinflussen die Clientfunktionalität. Vertragsverhalten operieren auf Vertragsebene, und Vorgangsverhalten ändern die Vorgangszustellung.  
  
 Viele dieser Verhalten werden über Attribute implementiert, und Sie verwenden sie ebenso wie das <xref:System.ServiceModel.ServiceBehaviorAttribute>\-Attribut und das <xref:System.ServiceModel.OperationBehaviorAttribute>\-Attribut, indem Sie sie auf die betreffende Dienstklassen\- oder Vorgangsimplementierung anwenden. Andere Verhalten, wie z. B. das <xref:System.ServiceModel.Description.ServiceMetadataBehavior>\-Objekt oder das <xref:System.ServiceModel.Description.ServiceDebugBehavior>\-Objekt, werden in der Regel mithilfe einer Anwendungskonfigurationsdatei angewendet, obwohl sie auch im Code verwendet werden können.  
  
 Zum Beispiel wird die Veröffentlichung der Metadaten durch den Einsatz des <xref:System.ServiceModel.Description.ServiceMetadataBehavior>\-Objekts konfiguriert. Die folgende Anwendungskonfigurationsdatei veranschaulicht die gängigste Verwendungsweise.  
  
 [!code-csharp[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.cs#1)]  
  
 In den folgenden Abschnitten werden viele der nützlichsten vom System bereitgestellten Verhalten beschrieben, mit denen die Bereitstellung eines Diensts oder Clients zur Laufzeit geändert werden kann. Informationen dazu, wann die einzelnen Verhalten verwendet werden, finden Sie im Referenzthema.  
  
### Dienstverhalten  
 Die folgenden Verhalten wirken sich auf Dienste aus.  
  
-   <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>. Wird auf einen [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Dienst angewendet, um anzugeben, ob dieser Dienst im [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]\-Kompatibilitätsmodus ausgeführt werden kann.  
  
-   <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. Steuert, wie der Dienst Clientansprüche autorisiert.  
  
-   <xref:System.ServiceModel.Description.ServiceCredentials>. Konfiguriert Dienstanmeldeinformationen. Verwenden Sie diese Klasse, um die Anmeldeinformationen für den Dienst anzugeben, beispielsweise ein X.509\-Zertifikat.  
  
-   <xref:System.ServiceModel.Description.ServiceDebugBehavior>. Aktiviert Debugging\- und Hilfeinformationsfunktionen für einen [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Dienst.  
  
-   <xref:System.ServiceModel.Description.ServiceMetadataBehavior>. Steuert die Veröffentlichung von Dienstmetadaten und zugehörigen Informationen.  
  
-   <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>. Legt das Überwachungsverhalten für Sicherheitsereignisse fest.  
  
-   <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>. Konfiguriert Laufzeitdurchsatzeinstellungen, die es Ihnen ermöglichen, die Dienstleistung zu optimieren.  
  
### Endpunktverhalten  
 Die folgenden Verhalten wirken sich auf Endpunkte aus. Viele dieser Verhalten werden in Clientanwendungen verwendet.  
  
-   <xref:System.ServiceModel.CallbackBehaviorAttribute>. Konfiguriert eine Rückrufdienstimplementierung in einer Duplexclientanwendung.  
  
-   <xref:System.ServiceModel.Description.CallbackDebugBehavior>. Aktiviert das Dienstdebugging für ein [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Rückrufobjekt.  
  
-   <xref:System.ServiceModel.Description.ClientCredentials>. Ermöglicht es dem Benutzer, die Client\- und Dienstanmeldeinformationen sowie die auf dem Client zu verwendenden Authentifizierungseinstellungen für die Dienstanmeldeinformationen zu konfigurieren.  
  
-   <xref:System.ServiceModel.Description.ClientViaBehavior>. Wird von Clients verwendet, um den URI \(Uniform Resource Identifier\) anzugeben, für den der Transportkanal erstellt werden soll.  
  
-   <xref:System.ServiceModel.Description.MustUnderstandBehavior>. Weist [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] an, die Verarbeitung von `MustUnderstand` zu deaktivieren.  
  
-   <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>. Weist das Laufzeitmodul an, für Kanäle einen synchronen Empfangsprozess zu verwenden.  
  
-   <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. Optimiert die Empfangsvorgänge für Transporte, die transaktionale Empfangsprozesse unterstützen.  
  
### Vertragsverhalten  
 <xref:System.ServiceModel.DeliveryRequirementsAttribute>. Gibt die Feature\-Anforderungen an, die Bindungen für die Dienst\- oder Client\-Implementierung liefern müssen.  
  
### Vorgangsverhalten  
 Die folgenden Vorgangsverhalten geben die Serialisierungs\- und Transaktionssteuermechanismen für Vorgänge an.  
  
-   <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>. Stellt das Laufzeitverhalten des <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> dar.  
  
-   <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>. Steuert das Laufzeitverhalten vom `XmlSerializer` und ordnet es einem Vorgang zu.  
  
-   <xref:System.ServiceModel.TransactionFlowAttribute>. Gibt die Ebene an, auf der ein Dienstvorgang einen Transaktionsheader akzeptiert.  
  
## Siehe auch  
 [Konfigurieren von Diensten](../../../docs/framework/wcf/configuring-services.md)   
 [Gewusst wie: Steuern der Dienstinstanzierung](../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)