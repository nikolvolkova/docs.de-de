---
title: "Gewusst wie: Verzögerte Initialisierung von Objekten"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- lazy initialization in .NET, how to perform
ms.assetid: 8cd68620-dcc3-4f20-8835-c728a6820e71
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ab1ae0eae8d78d4b7f14444e78ff5a741fe02d95
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-perform-lazy-initialization-of-objects"></a>Gewusst wie: Verzögerte Initialisierung von Objekten
Die <xref:System.Lazy%601?displayProperty=fullName>-Klasse vereinfacht die verzögerte Initialisierung und Instanziierung von Objekten. Beim verzögerten Initialisieren von Objekten können Sie die Erstellung vermeiden, wenn diese nie gebraucht werden, oder Sie können die Initialisierung verschieben, bis ein erster Zugriff erfolgt. Weitere Informationen finden Sie unter [Verzögerte Initialisierung](../../../docs/framework/performance/lazy-initialization.md).  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt, wie ein Wert mit <xref:System.Lazy%601> initialisiert wird. Gehen wir davon aus, dass die verzögerte Variable abhängig von anderem Code, der die `someCondition`-Variable auf TRUE oder FALSE festlegt, nicht gebraucht wird.  
  
```vb  
Dim someCondition As Boolean = False  
  
Sub Main()  
    'Initializing a value with a big computation, computed in parallel  
    Dim _data As Lazy(Of Integer) = New Lazy(Of Integer)(Function()  
                                                             Dim result =  
                                                                 ParallelEnumerable.Range(0, 1000).  
                                                                 Aggregate(Function(x, y)  
                                                                               Return x + y  
                                                                           End Function)  
                                                             Return result  
                                                         End Function)  
  
    '  do work that may or may not set someCondition to True  
    ' ...  
    '  Initialize the data only if needed  
    If someCondition = True Then  
  
        If (_data.Value > 100) Then  
  
            Console.WriteLine("Good data")  
        End If  
    End If  
End Sub  
```  
  
```csharp  
  static bool someCondition = false;    
  //Initializing a value with a big computation, computed in parallel  
  Lazy<int> _data = new Lazy<int>(delegate  
  {  
      return ParallelEnumerable.Range(0, 1000).  
          Select(i => Compute(i)).Aggregate((x,y) => x + y);  
  }, LazyExecutionMode.EnsureSingleThreadSafeExecution);  
  
  // Do some work that may or may not set someCondition to true.  
  //  ...  
  // Initialize the data only if necessary  
  if (someCondition)  
{  
    if (_data.Value > 100)  
      {  
          Console.WriteLine("Good data");  
      }  
}  
```  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt, wie Sie die <xref:System.Threading.ThreadLocal%601?displayProperty=fullName>-Klasse verwenden, um die Initialisierung eines Typs durchzuführen, der nur für die aktuelle Objektinstanz für den aktuellen Thread sichtbar ist.  
  
 [!code-csharp[CDS#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds2.cs#13)] [!code-vb[CDS#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/lazyhowto.vb#13)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Threading.LazyInitializer?displayProperty=fullName>   
 [Verzögerte Initialisierung](../../../docs/framework/performance/lazy-initialization.md)

