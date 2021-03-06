---
title: "Zwischenspeichern von Channels mit Send | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e69a2502-25cb-43bf-b8d2-95fbdecb41cb
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Zwischenspeichern von Channels mit Send
Der <xref:System.ServiceModel.Activities.SendMessageChannelCache> ermöglicht unterschiedliche Ebenen des Zwischenspeicherns von Channels mit der <xref:System.ServiceModel.Activities.Send>\-Aktivität und der <xref:System.ServiceModel.Activities.SendParametersContent>\-Aktivität für Benutzer.Das Zwischenspeichern auf Instanzebene ist standardmäßig aktiviert, und in diesem Beispiel werden die folgenden Funktionen veranschaulicht:  
  
1.  Freigeben eines <xref:System.ServiceModel.Activities.SendMessageChannelCache> über eine Anwendungsdomäne hinweg.  
  
2.  Deaktivieren Sie des Zwischenspeicherns von Channels.  
  
3.  Freigeben eines <xref:System.ServiceModel.Activities.SendMessageChannelCache> in Workflowinstanzen in einem <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
## Veranschaulicht  
 <xref:System.ServiceModel.Activities.SendMessageChannelCache>\-Erweiterung, <xref:System.ServiceModel.Activities.Send>\-Aktivität, <xref:System.ServiceModel.Activities.Receive>\-Aktivität, <xref:System.ServiceModel.Activities.ReceiveContent>\-Aktivität und <xref:System.ServiceModel.Activities.SendReply>\-Aktivität.  
  
#### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Laden Sie die Projektmappe in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], und erstellen Sie das Projekt.  
  
2.  Führen Sie die unter "\\EchoWorkflowService\\bin\\debug generierte Anwendung "EchoWorkflowService" aus.  
  
3.  Führen Sie die EchoWorkflowClient\-Anwendung aus, die in \\EchoWorkflowClient\\bin\\debug generiert wird.  
  
4.  Der Client ruft den Echo\-Vorgang für den Dienst auf, und gibt die Ergebnisse aus.Wenn die Ergebnisse ausgegeben wurden, drücken Sie die EINGABETASTE, um den Client und den Dienst zu beenden.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\ChannelCache`