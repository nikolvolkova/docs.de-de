---
title: "&lt;participants&gt; von WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d99dbddc-0057-4e18-8e42-f91411d39970
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;participants&gt; von WCF
Konfiguriert eine Liste von Nachverfolgungsteilnehmern, die den direkt von der Laufzeit ausgegebenen Nachverfolgungsdatensätzen lauschen und sie entsprechend der Weise verarbeiten, wie sie konfiguriert wurden.  Dies umfasst das Schreiben in ein bestimmtes Ausgabemedium \(z. B. Datei, Konsole, ETW\), das Verarbeiten\/Aggregieren der Datensätze oder eine beliebige andere Kombination, die erforderlich sein könnte.  
  
 Weitere Informationen zur Workflowüberwachung und zu Nachverfolgungsteilnehmern finden Sie unter [Nachverfolgung und Ablaufverfolgung für Workflows](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md) und [Überwachungsteilnehmer](../../../../../docs/framework/windows-workflow-foundation//tracking-participants.md).  
  
## Syntax  
  
```vb  
  
<tracking>   
   <participants>   
      <add name="String"   
           profileName="String"  
           type="String" />   
   </participants>   
</tracking>  
  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
 Keine  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/add-of-participants.md)|Enthält Einstellungen für einen Nachverfolgungsteilnehmer.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<tracking\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/tracking.md)|Stellt einen Konfigurationsabschnitt zum Definieren von Nachverfolgungseinstellungen für einen Workflowdienst dar.|  
  
## Hinweise  
 Nachverfolgungsteilnehmer werden verwendet, um die vom Workflow ausgegebenen Nachverfolgungsdaten zu erfassen und in verschiedenen Medien zu speichern.  Außerdem kann jede Nachverarbeitung der Nachverfolgungsdatensätze auch innerhalb des Nachverfolgungsteilnehmers erfolgen.  
  
 Die Nachverfolgungsereignisse können von mehreren Nachverfolgungsteilnehmern gleichzeitig verarbeitet werden.  Jedem Nachverfolgungsteilnehmer kann ein anderes Nachverfolgungsprofil zugeordnet sein.  
  
 Standardmäßig wird ein Nachverfolgungsteilnehmer bereitgestellt, der die Nachverfolgungsdatensätze in eine ETW\-Sitzung schreibt.  Der Teilnehmer wird für einen Workflowdienst konfiguriert, indem einer Konfigurationsdatei ein nachverfolgungsspezifisches Verhalten hinzugefügt wird.  Durch Aktivierung eines ETW\-Nachverfolgungsteilnehmers können Nachverfolgungsdatensätze in der Ereignisanzeige angezeigt werden.  Wenn dies nicht Ihren Anforderungen entspricht, können Sie auch einen benutzerdefinierten Überwachungsteilnehmer schreiben.  
  
## Beispiel  
 In der folgenden Beispielkonfiguration wird der standardmäßige ETW\-Nachverfolgungsteilnehmer gezeigt, der in der Datei Web.config konfiguriert ist.  
  
 Die Anbieter\-ID, die der ETW\-Nachverfolgungsteilnehmer verwendet, um die Nachverfolgungsdatensätze an ETW weiterzuleiten, ist im Abschnitt `<diagnostics>` definiert.  Dem Nachverfolgungsteilnehmer ist ein Profil zugeordnet, das die Nachverfolgungsdatensätze angibt, die er abonniert hat.  Dieses Profil wird durch das `profileName`\-Attribut des `<add>`\-Elements definiert.  Sobald alles definiert ist, wird der Nachverfolgungsteilnehmer dem `<etwTracking>`\-Dienstverhalten hinzugefügt.  Dadurch wird der ausgewählte Nachverfolgungsteilnehmer den Erweiterungen der Workflowinstanz hinzugefügt, die daraufhin die Nachverfolgungsdatensätze empfangen.  
  
```  
  
<configuration>   
  <system.web>   
    <compilation targetFrameworkMoniker=".NETFramework,Version=v4.0"/>   
  </system.web>   
  <system.serviceModel>   
    <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />                
    <tracking>   
      <participants>   
        <add name="EtwTrackingParticipant"   
             type="System.Activities.Tracking.EtwTrackingParticipant, System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"   
             profileName="HealthMonitoring_Tracking_Profile"/>   
      </participants>   
    </tracking>   
    <behaviors>   
      <serviceBehaviors>   
        <behavior>   
          <etwTracking profileName="Sample Tracking Profile"/>  
        </behavior>   
      </serviceBehaviors>   
    </behaviors>   
  </system.serviceModel>   
</configuration>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection>   
 <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.EtwTrackingBehavior>   
 [Nachverfolgung und Ablaufverfolgung für Workflows](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Überwachungsteilnehmer](../../../../../docs/framework/windows-workflow-foundation//tracking-participants.md)