---
title: "Konfigurationsbasierte Aktivierung unter IIS und WAS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6a927e1f-b905-4ee5-ad0f-78265da38238
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Konfigurationsbasierte Aktivierung unter IIS und WAS
Wenn Sie einen [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienst unter Internetinformationsdienste \(IIS\) oder Windows\-Prozessaktivierungsdienst \(WAS\) hosten, müssen Sie normalerweise eine SVC\-Datei bereitstellen.Die SVC\-Datei enthält den Namen des Diensts und eine optionale benutzerdefinierte Diensthostfactory.Diese Zusatzdatei verursacht einen höheren Verwaltungsmehraufwand.Die konfigurationsbasierte Aktivierungsfunktion entfernt die Anforderung einer SVC\-Datei, sodass auch der damit verbundene Mehraufwand entfällt.  
  
## Konfigurationsbasierte Aktivierung  
 Die konfigurationsbasierte Aktivierung fügt die Metadaten, die zuvor in die SVC\-Datei eingefügt wurden, in die Datei "Web.config" ein.Innerhalb des \<`serviceHostingEnvironment`\>\-Elements befindet sich ein \<`serviceActivations`\>\-Element.Innerhalb des \<`serviceActivations`\>\-Elements sind ein oder mehrere \<`add`\>\-Elemente enthalten, und zwar einer für jeden gehosteten Dienst.Das \<`add`\>\-Element enthält Attribute, mit denen Sie die relative Adresse für den Dienst und den Diensttyp oder eine Diensthostfactory festlegen können.Der folgende Konfigurationsbeispielcode zeigt, wie dieser Abschnitt verwendet wird.  
  
> [!NOTE]
>  Jedes \<`add`\>\-Element muss einen Dienst oder ein Factoryattribut angeben.Es kann auch einen Dienst und Factoryattribute angeben.  
  
```  
<serviceHostingEnvironment>  
  <serviceActivations>  
    <add relativeAddress="MyServiceAddress" service="Service" factory=”MyServiceHostFactory”/>  
  </serviceActivations>  
</serviceHostingEnvironment>  
```  
  
 Wenn dieser Code in der Datei Web.config enthalten ist, können Sie den Dienstquellcode in das Verzeichnis App\_Code der Anwendung oder eine kompilierte Assembly im Verzeichnis Bin der Anwendung einfügen.  
  
> [!NOTE]
>  -   Bei Verwendung der konfigurationsbasierten Aktivierung wird Inlinecode in SVC\-Dateien nicht unterstützt.  
> -   Das `relativeAddress`\-Attribut muss auf eine relative Adresse wie “\<Unterverzeichnis\>\/service.svc” oder “~\/\<Unterverzeichnis\/service.svc” festgelegt sein.  
> -   Es wird eine Konfigurationsausnahme ausgelöst, wenn Sie eine relative Adresse registrieren, für die keine bekannte Erweiterung mit WCF\-Zuordnung vorhanden ist.  
> -   Die angegebene relative Adresse ist relativ zum Stamm der virtuellen Anwendung.  
> -   Aufgrund des hierarchischen Konfigurationsmodells werden die registrierten relativen Adressen auf Computer\- und Siteebene von den virtuellen Anwendungen geerbt.  
> -   Registrierungen in einer Konfigurationsdatei haben Vorrang vor Einstellungen in einer SVC\-, XAMLX\-, XOML\- oder anderen Datei.  
> -   Alle umgekehrten Schrägstriche \('\\'\) in einem URI, der an IIS\/WAS gesendet wird, werden automatisch in einen normalen Schrägstrich \('\/'\) konvertiert.Wenn eine relative Adresse hinzugefügt wird, die '\\' enthält, und Sie einen URI an IIS senden, für den die relative Adresse verwendet wird, wird der umgekehrte Schrägstrich in einen Schrägstrich konvertiert, und IIS kann keine Übereinstimmung mit der relativen Adresse herstellen.IIS sendet Ablaufverfolgungsinformationen, die angeben, dass keine Übereinstimmungen gefunden wurden.  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection.ServiceActivations%2A>   
 [Hosting\-Dienste](../../../../docs/framework/wcf/hosting-services.md)   
 [Übersicht über das Hosten von Workflowdiensten](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)   
 [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)   
 [Windows Server AppFabric\-Hostingfunktionen](http://go.microsoft.com/fwlink/?LinkId=201276)