---
title: "Konfigurieren der Nachverfolgung f&#252;r einen Workflow | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 905adcc9-30a0-4918-acd6-563f86db988a
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Konfigurieren der Nachverfolgung f&#252;r einen Workflow
Es gibt drei Möglichkeiten zum Ausführen eines Workflows:  
  
-   Gehostet in <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
-   Ausgeführt als <xref:System.Activities.WorkflowApplication>  
  
-   Ausgeführt direkt mit <xref:System.Activities.WorkflowInvoker>  
  
 Abhängig von der Workflow\-Hostingoption kann ein Nachverfolgungsteilnehmer entweder über Code oder eine Konfigurationsdatei hinzugefügt werden.  In diesem Thema wird beschrieben, wie die Nachverfolgung konfiguriert wird, indem einer <xref:System.Activities.WorkflowApplication> und einem <xref:System.ServiceModel.Activities.WorkflowServiceHost> ein Nachverfolgungsteilnehmer hinzugefügt wird, und wie die Nachverfolgung bei der Verwendung von  <xref:System.Activities.WorkflowInvoker> aktiviert wird.  
  
## Konfigurieren der Nachverfolgung von Workflowanwendungen  
 Ein Workflow kann mit der <xref:System.Activities.WorkflowApplication>\-Klasse ausgeführt werden.  Dieses Thema veranschaulicht, wie die Nachverfolgung für eine [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]\-Workflowanwendung konfiguriert wird, indem dem <xref:System.Activities.WorkflowApplication>\-Workflowhost ein Nachverfolgungsteilnehmer hinzugefügt wird.  In diesem Fall wird der Workflow als Workflowanwendung ausgeführt.  Sie konfigurieren eine Workflowanwendung über Code \(statt eine Konfigurationsdatei zu verwenden\), der aus einer selbst gehosteten EXE\-Datei unter Verwendung der <xref:System.Activities.WorkflowApplication>\-Klasse besteht.  Der Nachverfolgungsteilnehmer wird der <xref:System.Activities.WorkflowApplication>\-Instanz als Erweiterung hinzugefügt.  Dies geschieht, indem der Erweiterungsauflistung für die WorkflowApplication\-Instanz der <xref:System.Activities.Tracking.TrackingParticipant> hinzugefügt wird.  
  
 Sie können einer Workflowanwendung die Erweiterung zum <xref:System.Activities.Tracking.EtwTrackingParticipant>\-Verhalten hinzufügen. Dies wird im folgenden Code demonstriert.  
  
```csharp  
LogActivity activity = new LogActivity();  
  
WorkflowApplication instance = new WorkflowApplication(activity);  
EtwTrackingParticipant trackingParticipant =  
    new EtwTrackingParticipant  
{  
  
        TrackingProfile = new TrackingProfile  
           {  
               Name = "SampleTrackingProfile",  
               ActivityDefinitionId = "ProcessOrder",  
               Queries = new WorkflowInstanceQuery  
               {  
                  States = { "*" }  
              }  
          }  
       };  
instance.Extensions.Add(trackingParticipant);  
  
```  
  
### Konfigurieren der Überwachung von Workflowdiensten  
 Ein Workflow kann als [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Dienst verfügbar gemacht werden, wenn er im <xref:System.ServiceModel.Activities.WorkflowServiceHost>\-Diensthost gehostet wird.  <xref:System.ServiceModel.Activities.WorkflowServiceHost> ist eine spezialisierte .NET ServiceHost\-Implementierung für einen workflowbasierten Dienst.  In diesem Abschnitt wird erläutert, wie Sie die Nachverfolgung für einen im [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] ausgeführten <xref:System.ServiceModel.Activities.WorkflowServiceHost>\-Workflowdienst konfigurieren.  Er wird durch eine Web.config\-Datei \(für einen im Web gehosteten Dienst\) oder eine App.config\-Datei \(für einen Dienst, der in einer eigenständigen Anwendung, z. B. einer Konsolenanwendung, gehostet wird\) konfiguriert, indem ein Dienstverhalten angegeben wird, oder durch Code, indem der <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A>\-Auflistung für den Diensthost ein nachverfolgungsspezifisches Verhalten hinzugefügt wird.  
  
 Bei einem Workflowhost, der im <xref:System.ServiceModel.WorkflowServiceHost> gehostet wird, können Sie den <xref:System.Activities.Tracking.EtwTrackingParticipant> mithilfe des \<`behavior`\>\-Elements in einer Konfigurationsdatei hinzufügen. Dies wird im folgenden Beispiel demonstriert.  
  
```  
  
<behaviors>  
   <serviceBehaviors>  
        <behavior>  
          <etwTracking profileName="Sample Tracking Profile" />  
        </behavior>              
   </serviceBehaviors>  
<behaviors>  
  
```  
  
 Alternativ können Sie einem Workflowdienst, der im <xref:System.ServiceModel.WorkflowServiceHost> gehostet wird, die Erweiterung für das <xref:System.Activities.Tracking.EtwTrackingParticipant>\-Verhalten über Code hinzufügen.  Um einen benutzerdefinierten Überwachungsteilnehmer hinzuzufügen, erstellen Sie eine neue Verhaltenserweiterung, und fügen Sie diese dem <xref:System.ServiceModel.ServiceHost> hinzu, wie im folgenden Beispielcode gezeigt.  
  
> [!NOTE]
>  Wenn Sie Beispielcode anzeigen möchten, aus dem hervorgeht, wie ein benutzerdefiniertes Verhaltenselement erstellt wird, das einen benutzerdefinierten Nachverfolgungsteilnehmer hinzufügt, lesen Sie die Informationen in den Beispielen zum Thema [Nachverfolgung](../../../docs/framework/windows-workflow-foundation/samples/tracking.md).  
  
```  
ServiceHost svcHost = new ServiceHost(typeof(WorkflowService), new   
                                 Uri("http://localhost:8001/Sample"));  
EtwTrackingBehavior trackingBehavior =   
    new EtwTrackingBehavior  
    {  
        ProfileName = "Sample Tracking Profile"  
    };  
svcHost.Description.Behaviors.Add(trackingBehavior);  
svcHost.Open();  
  
```  
  
 Der Überwachungsteilnehmer wird dem Workflow\-Diensthost als Erweiterung zum Verhalten hinzugefügt.  
  
 Aus dem unten angezeigten Beispielcode können Sie ersehen, wie ein Überwachungsprofil aus der Konfigurationsdatei gelesen wird.  
  
```  
TrackingProfile GetProfile(string profileName, string displayName)  
        {  
            TrackingProfile trackingProfile = null;  
            TrackingSection trackingSection = (TrackingSection)WebConfigurationManager.GetSection("system.serviceModel/tracking");  
            if (trackingSection == null)   
            {  
                return null;  
            }  
  
            if (profileName == null)   
            {  
                profileName = "";  
            }  
  
            //Find the profile with the specified profile name in the list of profile found in config  
            var match = from p in new List<TrackingProfile>(trackingSection.TrackingProfiles)  
                        where (p.Name == profileName) && ((p.ActivityDefinitionId == displayName) || (p.ActivityDefinitionId == "*"))  
                        select p;  
  
            if (match.Count() == 0)  
            {  
                //return an empty profile  
                trackingProfile = new TrackingProfile()  
                {  
                    ActivityDefinitionId = displayName  
                };  
  
            }  
            else  
            {  
                trackingProfile = match.First();  
            }  
  
            return trackingProfile;  
  
```  
  
 In diesem Beispielcode wird gezeigt, wie einem Workflowhost ein Nachverfolgungsprofil hinzugefügt wird.  
  
```  
WorkflowServiceHost workflowServiceHost = serviceHostBase as WorkflowServiceHost;  
if (null != workflowServiceHost)  
{  
              string workflowDisplayName = workflowServiceHost.Activity.DisplayName;  
               TrackingProfile trackingProfile = GetProfile(this.profileName, workflowDisplayName);  
                workflowServiceHost.WorkflowExtensions.Add(()  => new EtwTrackingParticipant  {  
               TrackingProfile = trackingProfile  
                        });  
 }  
```  
  
> [!NOTE]
>  Weitere Informationen über Nachverfolgungsprofile finden Sie unter [Nachverfolgungsprofile](http://go.microsoft.com/fwlink/?LinkId=201310).  
  
### Konfigurieren der Nachverfolgung mit WorkflowInvoker  
 Um die Nachverfolgung für einen mit <xref:System.Activities.WorkflowInvoker> ausgeführten Workflow zu konfigurieren, fügen Sie den Nachverfolgungsanbieter als Erweiterung einer <xref:System.Activities.WorkflowInvoker>\-Instanz hinzu.  Der folgende Beispielcode stammt aus dem Beispiel [Benutzerdefinierte Nachverfolgung](../../../docs/framework/windows-workflow-foundation/samples/custom-tracking.md).  
  
```  
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());  
invoker.Extensions.Add(customTrackingParticipant);  
invoker.Invoke();  
  
```  
  
### Anzeigen von Nachverfolgungsdatensätzen in der Ereignisanzeige  
 Es gibt zwei Ereignisanzeigeprotokolle, die bei der Nachverfolgung der WF\-Ausführung besonders von Interesse sind: das Analyseprotokoll und das Debugprotokoll.  Beide befinden sich unter dem Knoten "Microsoft&#124;Windows&#124;Application Server\-Applications".  Protokolle in diesem Abschnitt enthalten Ereignisse einer einzelnen Anwendung und keine Ereignisse, die Auswirkungen auf das gesamte System haben.  
  
 Ereignisse zur Debugablaufverfolgung werden in das Debugprotokoll geschrieben.  Um WF\-Debugablaufverfolgungs\-Ereignisse in der Ereignisanzeige zu sammeln, aktivieren Sie das Debugprotokoll.  
  
1.  Um die Ereignisanzeige zu öffnen, klicken Sie auf **Start** und dann auf **Ausführen.** Geben Sie im Dialogfeld Ausführen `eventvwr` ein.  
  
2.  Erweitern Sie im Dialogfeld Ereignisanzeige den Knoten **Anwendungs\- und Dienstprotokolle**.  
  
3.  Erweitern Sie die Knoten **Microsoft**, **Windows** und **Anwendungsserver\-Anwendungen**.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Knoten **Debuggen** unter dem Knoten **Anwendungsserver\-Anwendungen**, und wählen Sie **Protokoll aktivieren** aus.  
  
5.  Führen Sie die für die Ablaufverfolgung aktivierte Anwendung aus, um Ablaufverfolgungsereignisse zu generieren.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Knoten **Debuggen**, und wählen Sie **Aktualisieren** aus. Ablaufverfolgungsereignisse sollten im mittleren Bereich sichtbar sein.  
  
 WF4 stellt einen Nachverfolgungsteilnehmer bereit, der Nachverfolgungsdatensätze in eine ETW \(Ereignisablaufverfolgung für Windows\)\-Sitzung schreibt.  Der ETW\-Überwachungsteilnehmer ist mit einem Überwachungsprofil konfiguriert, um Überwachungsdatensätze zu abonnieren.  Wenn die Nachverfolgung aktiviert ist, werden Nachverfolgungsdatensätze für Fehler in ETW ausgegeben.  ETW\-Nachverfolgungsereignisse \(im Bereich von 100\-113\), die den vom ETW\-Nachverfolgungsteilnehmer ausgegebenen Nachverfolgungsereignissen entsprechen, werden in das Analyseprotokoll geschrieben.  
  
 Gehen Sie wie folgt vor, um Nachverfolgungsdatensätze anzuzeigen.  
  
1.  Um die Ereignisanzeige zu öffnen, klicken Sie auf **Start** und dann auf **Ausführen.** Geben Sie im Dialogfeld Ausführen `eventvwr` ein.  
  
2.  Erweitern Sie im Dialogfeld Ereignisanzeige den Knoten **Anwendungs\- und Dienstprotokolle**.  
  
3.  Erweitern Sie die Knoten **Microsoft**, **Windows** und **Anwendungsserver\-Anwendungen**.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Knoten **Analytisch** unter dem Knoten **Anwendungsserver\- Anwendungen**, und wählen Sie **Protokoll aktivieren** aus.  
  
5.  Führen Sie die für die Nachverfolgung aktivierte Anwendung aus, um Nachverfolgungsdatensätze zu generieren.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Knoten **Analytisch**, und wählen Sie **Aktualisieren** aus. Nachverfolgungsdatensätze sollten im mittleren Bereich sichtbar sein.  
  
 Das folgende Bild zeigt Nachverfolgungsereignisse in der Ereignisanzeige an.  
  
 ![Ereignisanzeige mit Nachverfolgungsdatensätzen](../../../docs/framework/windows-workflow-foundation//media/trackingeventviewer.PNG "TrackingEventViewer")  
  
### Registrieren einer anwendungsspezifischen Anbieter\-ID  
 Wenn Ereignisse in ein bestimmtes Anwendungsprotokoll geschrieben werden müssen, führen Sie folgende Schritte aus, um das neue Anbietermanifest zu registrieren.  
  
1.  Deklarieren Sie die Anbieter\-ID in der Anwendungskonfigurationsdatei.  
  
    ```  
    <system.serviceModel>  
        <diagnostics etwProviderId="2720e974-9fe9-477a-bb60-81fe3bf91eec"/>  
    </system.serviceModel>  
  
    ```  
  
2.  Kopieren Sie die Manifestdatei aus "%windir%\\Microsoft.NET\\Framework\\\<neueste Version von [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]\>\\Microsoft.Windows.ApplicationServer.Applications.man" an einen temporären Speicherort, und benennen Sie sie in "Microsoft.Windows.ApplicationServer.Applications\_Provider1.man" um.  
  
3.  Ändern Sie die GUID in der Manifestdatei in die neue GUID.  
  
    ```  
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"  
  
    ```  
  
4.  Ändern Sie den Anbieternamen, wenn Sie den Standardanbieter nicht deinstallieren wollen.  
  
    ```  
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"  
  
    ```  
  
5.  Wenn Sie den Anbieternamen im vorherigen Schritt änderten, ändern Sie die Kanalnamen in der Manifestdatei in den neuen Anbieternamen.  
  
    ```  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Admin" chid="ADMIN_CHANNEL" symbol="ADMIN_CHANNEL" type="Admin" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ADMIN_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Operational" chid="OPERATIONAL_CHANNEL" symbol="OPERATIONAL_CHANNEL" type="Operational" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.OPERATIONAL_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Debug" chid="DEBUG_CHANNEL" symbol="DEBUG_CHANNEL" type="Debug" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.DEBUG_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Perf" chid="PERF_CHANNEL" symbol="PERF_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.PERF_CHANNEL.message)" />  
  
    ```  
  
6.  Generieren Sie die Ressourcen\-DLL, indem Sie folgende Schritte ausführen.  
  
    1.  Installieren Sie das Windows SDK.  Das Windows SDK enthält den Meldungscompiler \([mc.exe](http://go.microsoft.com/fwlink/?LinkId=184606)\) und den Ressourcencompiler \([rc.exe](http://go.microsoft.com/fwlink/?LinkId=184605)\).  
  
    2.  Führen Sie in einer Windows SDK\-Eingabeaufforderung mc.exe für die neue Manifestdatei aus.  
  
        ```  
        mc.exe Microsoft.Windows.ApplicationServer.Applications_Provider1.man  
  
        ```  
  
    3.  Führen Sie rc.exe für die im vorherigen Schritt generierte Ressourcendatei aus.  
  
        ```  
        rc.exe  Microsoft.Windows.ApplicationServer.Applications_Provider1.rc  
  
        ```  
  
    4.  Erstellen Sie eine leere CS\-Datei mit dem Namen NewProviderReg.cs.  
  
    5.  Erstellen Sie eine Ressourcen\-DLL mithilfe des C\#\-Compilers.  
  
        ```  
        csc /target:library /win32res:Microsoft.Windows.ApplicationServer.Applications_Provider1.res NewProviderReg.cs /out:Microsoft.Windows.ApplicationServer.Applications_Provider1.dll  
        ```  
  
    6.  Ändern Sie den Ressourcen\- und Meldungs\-DLL\-Namen in der Manifestdatei von `Microsoft.Windows.ApplicationServer.Applications.Provider1.man` in den neuen DLL\-Namen.  
  
        ```  
        <provider name="Microsoft-Windows-Application Server-Applications_Provider1" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" symbol="Microsoft_Windows_ApplicationServer_ApplicationEvents" resourceFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" messageFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll">  
  
        ```  
  
    7.  Verwenden Sie [wevtutil](http://go.microsoft.com/fwlink/?LinkId=184608) zum Registrieren des Manifests.  
  
        ```  
        wevtutil im Microsoft.Windows.ApplicationServer.Applications_Provider1.man  
        ```  
  
## Siehe auch  
 [Überwachung mit Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Überwachen von Anwendungen mit AppFabric](http://go.microsoft.com/fwlink/?LinkId=201275)