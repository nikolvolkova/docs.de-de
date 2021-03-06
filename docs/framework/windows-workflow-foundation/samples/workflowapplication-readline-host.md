---
title: "WorkflowApplication-ReadLine-Host | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7b362be-cb42-40d7-b9ef-cfc4aed2455b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# WorkflowApplication-ReadLine-Host
Dieses Beispiel stellt einen generischen ReadLine\-Host dar.Sie können einen beliebigen Workflow mithilfe der eingeschlossenen `ReadLine`\-Aktivität \(oder anderen ähnlichen Aktivitäten, die Daten aus Lesezeichen abrufen, die mit Zeichenfolgen wieder aufgenommen werden\) laden und ausführen.Ausgaben von der `WriteLine`\-Aktivität oder Ausgaben, die in die <xref:System.Activities.Statements.WriteLine.TextWriter%2A>\-Erweiterung schreiben, werden an das Hostfenster weitergeleitet.Wenn sich eine Instanz im Leerlauf befindet, werden die verfügbaren Lesezeichen für diese Instanz in einem Kombinationsfeld angezeigt.Durch Auswählen eines Lesezeichens, Eingeben von Text und Drücken der Schaltfläche zum Wiederaufnehmen von Lesezeichen wird die Ausführung des Workflows fortgesetzt.Sie können einen ausgewählten Workflow auch abbrechen oder beenden.Persistenz ist standardmäßig aktiviert. Sie können den Host herunterfahren und neu starten; die Instanzliste wird daraufhin mit den in der Datenbank gespeicherten Instanzen aufgefüllt.Die Nachverfolgung wird verwendet, um Ereignisse auf <xref:System.Activities.WorkflowApplication>\-Ebene an den Host auszugeben, mit der Option, eine ausführliche Nachverfolgung auf Aktivitätsebene hinzuzufügen.  
  
## Beispieldetails  
 Es gibt zwei Ebenen für diesen Host: die Ansicht und den Instanz\-Manager.Die Ansicht besteht aus der `HostView`\-Klasse und der `WorkflowApplicationInfo`\-Klasse.Das allgemeine Muster für diesen Host besteht darin, dass die `HostView`\-Klasse dem Benutzer basierend auf `WorkflowApplicationInfo`\-Objekten, die mit den Instanzen, die sie darstellen, in angemessener Weise synchron sind, verfügbare Optionen anzeigt.Die Instanz\-Manager\-Ebene besteht aus der `WorkflowApplicationManager`\-Klasse, die den Kern der gesamten Hostkommunikation bildet, und der `WorkflowDefinitionExtension`\-Klasse, die die Beziehung zwischen einer Instanz und der Programmdefinition, mit der diese gestartet wurde, sowie einigen anderen Klassen beibehält.Die `HostView` ruft Steuerungsvorgänge im `WorkflowApplicationManager` auf.Diese Aufrufe sind in der Regel asynchron, um eine reaktionsfreudige Benutzeroberfläche aufrechtzuerhalten.Wenn die asynchronen Aufrufe abgeschlossen sind, führt der `WorkflowApplicationManager` Aufrufe an die Ansichtsebene über eine ordnungsgemäß definierte Schnittstelle \(`IHostView`\) durch.Die `HostView`\-Klasse leitet diese Aufrufe in den meisten Fällen von der `WorkflowApplicationManager`\-Klasse an den Benutzeroberflächenthread weiter.Das Schreiben von Text erfolgt mit threadsicheren <xref:System.Activities.Statements.WriteLine.TextWriter%2A>\-Objekten, die von der `HostView`\-Klasse bereitgestellt werden.Die Benutzeroberfläche ist nicht der einzige Ort, an dem Ereignisse generiert werden.Die <xref:System.Activities.WorkflowApplication>\-Objekte signalisieren dem `WorkflowApplicationManager` beispielsweise, wann sie in den Zustand `Idle` oder `Complete` übergehen oder `Aborted` werden.Die `WorkflowApplicationManager`\-Klasse verlässt den Ereignisthread, indem sie Bereinigungs\- oder Aktualisierungsaufgaben an den Host weiterleitet.  
  
 Die Aufzeichnung der Datei, die zum Starten einer <xref:System.Activities.WorkflowApplication> verwendet wird, wird von der`WorkflowDefinitionExtension`\-Klasse bereitgestellt.Diese implementiert die <xref:System.Activities.Persistence.PersistenceIOParticipant>\-Schnittstelle, um an der Persistenz teilzunehmen und den Pfad an die Workflowdefinition weiterzugeben.  
  
 Die `WorkflowApplicationManager.Load`\-Methode verwendet den gespeicherten Pfad zur Instanziierung der Workflowprogramme, die zum Laden von nicht abgeschlossenen <xref:System.Activities.WorkflowApplication>\-Objekten erforderlich sind.  
  
#### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Für dieses Beispiel muss SQL Express installiert sein.SQL Express wird mit [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] ausgeliefert.  
  
2.  Öffnen Sie eine Visual Studio 2010\-Eingabeaufforderung.  
  
3.  Navigieren Sie zum Beispielverzeichnis \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\), und führen Sie "CreateInstanceStore.cmd" aus.  
  
4.  Das Skript "CreateInstanceStore.cmd" versucht, die Datenbank auf der Standardinstanz von SQL Server 2008 Express zu erstellen.Wenn Sie die Datenbank auf einer anderen Instanz installieren möchten, ändern Sie hierfür das Skript.  
  
5.  Kompilieren Sie das WorkflowApplicationReadLineHost\-Projekt, und führen Sie es in der Befehlszeile aus.  
  
6.  Sobald es ausgeführt wird, können Sie die Persistenz optional aktivieren oder deaktivieren.Außerdem können Sie optional die ausführliche Aktivitätsnachverfolgung aktivieren oder deaktivieren.  
  
7.  Drücken Sie Schaltfläche mit den Auslassungszeichen neben der Schaltfläche **Ausführen**, um nach einem in einer XAML\-Datei definierten Workflow zu suchen.  
  
     Im Ordner "SampleWorkflows" finden Sie zwei Beispiele.Das Beispiel "parallel1.xaml" tritt in den Leerlauf ein.  
  
8.  Nachdem Sie ein Beispiel ausgewählt haben, klicken Sie die Schaltfläche **Ausführen**.  
  
9. Wenn der Workflow in den Leerlauf eintritt, wird das Kombinationsfeld **Lesezeichen** mit verfügbaren Lesezeichen aufgefüllt.  
  
10. Sie können nun entweder ein Lesezeichen wiederaufnehmen oder den Workflow abbrechen bzw. beenden.Sie können auch den Host herunterfahren und ihn neu starten.Wenn die Persistenz aktiviert bleibt, werden die Instanzen beim Herunterfahren entladen und beim Starten erneut geladen.  
  
     Um ein Lesezeichen wiederaufzunehmen, wählen Sie das gewünschte Lesezeichen aus, geben Sie einen Wert in das Textfeld neben dem Kombinationsfeld ein, und klicken Sie auf die Schaltfläche zur Wiederaufnahme des Lesezeichens.  
  
#### So entfernen Sie die Instanzspeicherdatenbank  
  
1.  Öffnen Sie eine Visual Studio 2010\-Eingabeaufforderung.  
  
2.  Navigieren Sie zum Beispielverzeichnis \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\), und führen Sie "RemoveInstanceStore.cmd" aus.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Überprüfen Sie das folgende \(standardmäßige\) Verzeichnis, bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Execution\ControllingWorkflowApplications`  
  
## Siehe auch