---
title: "LINQ to Objects-Aktivit&#228;t | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 403c82e8-7f2b-42f6-93cd-95c35bc76ead
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# LINQ to Objects-Aktivit&#228;t
Dieses Beispiel veranschaulicht, wie eine Aktivität so erstellt wird, dass LINQ to Objects verwendet wird, um Elemente in einer Auflistung abzufragen.  
  
## Aktivitätsdetails für FindInCollection  
 Diese Aktivität ermöglicht Benutzern die Abfrage von Elementen aus Auflistungen im Arbeitsspeicher mit LINQ to Objects.Zum Filtern der Ergebnisse müssen Sie ein LINQ\-Prädikat in Form eines Lambda\-Ausdrucks bereitstellen.Diese Aktivität kann in Verbindung mit <xref:System.Activities.Statements.AddToCollection%601>\-Aktivitäten verwendet werden.  
  
 In der folgenden Tabelle werden die Eigenschaft und die Rückgabewerte für die Aktivität aufgelistet.  
  
|Eigenschaft oder Rückgabewert|Beschreibung|  
|-----------------------------------|------------------|  
|`Collection`\-Eigenschaft|Eine erforderliche Eigenschaft, die die Quellauflistung angibt.|  
|`Predicate`\-Eigenschaft|Eine erforderliche Eigenschaft, die den Filter für die Auflistung in Form eines Lambda\-Ausdrucks angibt.|  
|Rückgabewert|Die gefilterte Auflistung.|  
  
## Codebeispiel, in dem die benutzerdefinierte Aktivität verwendet wird  
 Im folgenden Codebeispiel wird die benutzerdefinierte `FindInCollection`\-Aktivität verwendet, um alle Zeilen in einer Auflistung von Mitarbeitern zu suchen, deren `Role`\-Eigenschaft auf `Manager` und deren `Location`\-Eigenschaft auf `Redmond` festgelegt ist.  
  
```csharp  
// Find all program managers in Redmond in the employees collection.  
  
Activity wf = new FindInCollection<Employee>  
{  
    Collections = new LambdaValue<IEnumerable<Employee>>(c => employees),                
    Predicate = new LambdaValue<Func<Employee, bool>>(c => new Func<Employee, bool>(e => e.Role.Equals("Manager") && e.Location.Equals("Redmond")))  
};  
  
```  
  
 Im folgenden Code wird gezeigt, wie ein Workflowprogramm erstellt wird, das die benutzerdefinierte FindInCollection\-Aktivität, die <xref:System.Activities.Statements.AddToCollection%601>\-Aktivität und die <xref:System.Activities.Statements.ForEach%601>\-Aktivität verwendet, um eine Auflistung mit Mitarbeitern aufzufüllen, alle Mitarbeiter zu suchen, die Entwickler in Redmond sind, und dann die Ergebnisliste zu durchlaufen.  
  
```csharp  
// Create the Linq predicate for the find expression  
  
Func<Employee, bool> predicate = e => e.Role == "DEV" && e.Location.Equals("Redmond");  
  
// Create workflow program  
Activity sampleWorkflow = new Sequence  
{  
    Variables = { employees, devsFromRedmond },  
    Activities =  
    {  
        new Assign<IList<Employee>>  
        {  
            To = employees,  
            Value = new LambdaValue<IList<Employee>>(c => new List<Employee>())  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(1, "Employee 1", "DEV", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(2, "Employee 2", "DEV", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(3, "Employee 3", "PM", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(4, "Employee 4", "PM", "China"))  
        },  
        new FindInCollection<Employee>  
        {  
            Collections = new InArgument<IEnumerable<Employee>>(employees),  
            Predicate = new LambdaValue<Func<Employee, bool>>(c => predicate),  
            Result = new OutArgument<IList<Employee>>(devsFromRedmond)  
        },  
        new ForEach<Employee>  
        {  
            Values = new InArgument<IEnumerable<Employee>>(devsFromRedmond),  
            Body = new ActivityAction<Employee>  
            {  
                Argument = iterationVariable,  
                Handler = new WriteLine  
                {  
                    Text = new InArgument<string>(env => iterationVariable.Get(env).ToString())  
                }  
            }  
        }  
    }  
};  
```  
  
#### So verwenden Sie dieses Beispiel  
  
1.  Öffnen Sie in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] die Projektmappendatei "LinqToObjects.sln".  
  
2.  Drücken Sie STRG\+UMSCHALT\+B, um die Projektmappe zu erstellen.  
  
3.  Drücken Sie F5, um die Projektmappe auszuführen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Überprüfen Sie das folgende \(standardmäßige\) Verzeichnis, bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Linq\LinqToObjects`  
  
## Siehe auch  
 [Lambda Expressions \(C\# Programming Guide\)](http://go.microsoft.com/fwlink/?LinkId=150381)   
 [LINQ to Objects](http://go.microsoft.com/fwlink/?LinkID=150380)