---
title: "Anhalten und Fortsetzen eines Workflows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11f38339-79c7-4295-b610-24a7223bbf6d
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Anhalten und Fortsetzen eines Workflows
Workflows werden in Abhängigkeit von Lesezeichen und Blockieraktivitäten wie <xref:System.Activities.Statements.Delay> angehalten und fortgesetzt, können jedoch auch durch Persistenz explizit angehalten, entladen und wieder aufgenommen werden.  
  
## Anhalten eines Workflows  
 Verwenden Sie <xref:System.Activities.WorkflowApplication.Unload%2A>, um einen Workflow anzuhalten.Mit dieser Methode wird das Beibehalten und Entladen des Workflows angefordert, und eine <xref:System.TimeoutException> wird ausgelöst, wenn der Workflow nicht innerhalb von 30 Sekunden entladen wird.  
  
```csharp  
try  
{  
    // attempt to unload will fail if the workflow is idle within a NoPersistZone  
    application.Unload(TimeSpan.FromSeconds(5));  
}  
catch (TimeoutException e)  
{  
    Console.WriteLine(e.Message);  
}  
  
```  
  
## Wiederaufnehmen von Workflows  
 Verwenden Sie <xref:System.Activities.WorkflowApplication.Load%2A>, um einen Workflow wiederaufzunehmen, der angehalten und entladen wurde.Diese Methode lädt einen Workflow aus einem Persistenzspeicher in den Arbeitsspeicher.  
  
```csharp  
WorkflowApplication application = new WorkflowApplication(activity);  
application.InstanceStore = instanceStore;  
application.Load(id);  
  
```  
  
## Beispiel  
 Im folgenden Codebeispiel wird veranschaulicht, wie ein Workflow mithilfe der Persistenz angehalten und fortgesetzt werden kann.  
  
```csharp  
static string bkName = "bkName";  
static void Main(string[] args)   
{  
    StartAndUnloadInstance();  
}  
  
static void StartAndUnloadInstance()   
{  
    AutoResetEvent waitHandler = new AutoResetEvent(false);  
    WorkflowApplication wfApp = new WorkflowApplication(GetDelayedWF());  
    SqlWorkflowInstanceStore instanceStore = SetupSqlpersistenceStore();  
    wfApp.InstanceStore = instanceStore;  
    wfApp.Extensions.Add(SetupMyFileTrackingParticipant);  
    wfApp.PersistableIdle = (e) => {          ///persists application state and remove it from memory   
    return PersistableIdleAction.Unload;  
    };  
    wfApp.Unloaded = (e) => {  
        waitHandler.Set();  
    };  
    Guid id = wfApp.Id;  
    wfApp.Run();  
    waitHandler.WaitOne();  
    LoadAndCompleteInstance(id);  
}  
  
static void LoadAndCompleteInstance(Guid id)   
{            
    Console.WriteLine("Press <enter> to load the persisted workflow");  
    Console.ReadLine();  
    AutoResetEvent waitHandler = new AutoResetEvent(false);  
    WorkflowApplication wfApp = new WorkflowApplication(new Workflow1());  
    wfApp.InstanceStore =  
        new SqlWorkflowInstanceStore(ConfigurationManager.AppSettings["SqlWF4PersistenceConnectionString"].ToString());  
    wfApp.Completed = (workflowApplicationCompletedEventArgs) => {  
        Console.WriteLine("\nWorkflowApplication has Completed in the {0} state.",  
            workflowApplicationCompletedEventArgs.CompletionState);  
    };  
    wfApp.Unloaded = (workflowApplicationEventArgs) => {  
        Console.WriteLine("WorkflowApplication has Unloaded\n");  
        waitHandler.Set();  
    };  
    wfApp.Load(id);  
    wfApp.Run();  
    waitHandler.WaitOne();  
}  
  
public static Activity GetDelayedWF()   
{  
    return new Sequence {  
        Activities ={  
            new WriteLine{Text="Workflow Started"},  
            new Delay{Duration=TimeSpan.FromSeconds(10)},  
            new WriteLine{Text="Workflow Ended"}  
        }  
    };  
}  
  
private static SqlWorkflowInstanceStore SetupSqlpersistenceStore()   
{   
     string connectionString = ConfigurationManager.AppSettings["SqlWF4PersistenceConnectionString"].ToString();  
    SqlWorkflowInstanceStore sqlWFInstanceStore = new SqlWorkflowInstanceStore(connectionString);  
    sqlWFInstanceStore.InstanceCompletionAction = InstanceCompletionAction.DeleteAll;  
    InstanceHandle handle = sqlWFInstanceStore.CreateInstanceHandle();  
    InstanceView view = sqlWFInstanceStore.Execute(handle, new CreateWorkflowOwnerCommand(), TimeSpan.FromSeconds(5));  
    handle.Free();  
    sqlWFInstanceStore.DefaultInstanceOwner = view.InstanceOwner;  
    return sqlWFInstanceStore;  
}  
  
```