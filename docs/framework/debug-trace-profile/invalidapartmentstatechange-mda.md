---
title: invalidApartmentStateChange-MDA
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid apartment state
- managed debugging assistants (MDAs), invalid apartment state
- InvalidApartmentStateChange MDA
- invalid apartment state changes
- threading [.NET Framework], apartment states
- apartment states
- threading [.NET Framework], managed debugging assistants
- COM apartment states
ms.assetid: e56fb9df-5286-4be7-b313-540c4d876cd7
caps.latest.revision: 12
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f42a2b840a0cf678cfc2a06be0e9ed252c355a2a
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="invalidapartmentstatechange-mda"></a>invalidApartmentStateChange-MDA
Der `invalidApartmentStateChange`-MDA (Assistent für verwaltetes Debuggen) wird durch eines der folgenden zwei Probleme aktiviert:  
  
-   Es wird versucht, den COM-Apartmentzustand eines Threads zu ändern, der bereits von COM an einen anderen Apartmentzustand initialisiert wurde.  
  
-   Der COM-Apartmentzustand eines Threads verändert sich unerwartet.  
  
## <a name="symptoms"></a>Symptome  
  
-   Der COM-Apartmentzustand eines Threads ist nicht das, was angefordert wurde. Dies kann möglicherweise dazu führen, dass Proxys für COM-Komponenten verwendet werden, die ein anderes Threadmodell als das aktuelle aufweisen. Dies wiederum kann dazu führen, dass ein <xref:System.InvalidCastException> ausgelöst wird, wenn das COM-Objekt über Schnittstellen aufgerufen wird, die nicht für das apartmentübergreifende Marshalling eingerichtet sind.  
  
-   Der COM-Apartmentzustand des Threads ist anders als erwartet. Dies kann dazu führen, dass eine <xref:System.Runtime.InteropServices.COMException> mit einem HRESULT von RPC_E_WRONG_THREAD sowie ein <xref:System.InvalidCastException> ausgelöst wird, wenn ein [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md) (RCW) aufgerufen wird. Dies kann auch dazu führen, dass mehrere Threads gleichzeitig auf einige Singlethread-COM-Komponenten zugreifen können, was zu einer Beschädigung oder einem Verlust von Daten führen kann.  
  
## <a name="cause"></a>Ursache  
  
-   Der Thread wurde zuvor in einen anderen COM-Apartmentzustand initialisiert. Beachten Sie, dass ein Apartmentzustand eines Threads explizit oder implizit festgelegt werden kann. Zu den expliziten Vorgängen zählen die <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=fullName>-Eigenschaft und die <xref:System.Threading.Thread.SetApartmentState%2A>- und <xref:System.Threading.Thread.TrySetApartmentState%2A>-Methoden. Ein Thread, der mit der <xref:System.Threading.Thread.Start%2A>-Methode erstellt wurde, wird implizit auf <xref:System.Threading.ApartmentState.MTA> festgelegt, wenn <xref:System.Threading.Thread.SetApartmentState%2A> vor dem Start des Threads aufgerufen wird. Der Hauptthread der Anwendung wird ebenfalls implizit auf <xref:System.Threading.ApartmentState.MTA> initialisiert, sofern das <xref:System.STAThreadAttribute>-Attribut für die Hauptmethode angegeben ist.  
  
-   Die `CoUninitialize`-Methode (oder die `CoInitializeEx`-Methode) wird mit einem anderen Parallelitätsmodell für den Thread aufgerufen.  
  
## <a name="resolution"></a>Auflösung  
 Legen Sie den Apartmentzustand des Threads fest, bevor die Ausführung beginnt, oder wenden Sie entweder das <xref:System.STAThreadAttribute>- oder das <xref:System.MTAThreadAttribute>-Attribut auf die Hauptmethode der Anwendung an.  
  
 Hinsichtlich der zweiten Ursache sollte der Code, der die `CoUninitialize`-Methode aufruft, idealerweise geändert werden, um den Aufruf zu verzögern, bis der Thread beendet wird und keine RCWs und ihre zugrunde liegenden COM-Komponenten noch vom Thread verwendet werden. Sollte es jedoch nicht möglich sein, den Code zu ändern, der die `CoUninitialize`-Methode aufruft, dann sollten keine RCWs aus Threads verwendet werden, die auf diese Weise nicht initialisiert werden.  
  
## <a name="effect-on-the-runtime"></a>Auswirkungen auf die Laufzeit  
 Dieser MDA hat keine Auswirkungen auf die CLR.  
  
## <a name="output"></a>Ausgabe  
 Der COM-Apartmentzustand des aktuellen Threads und der Zustand, den der Code versucht hat anzuwenden.  
  
## <a name="configuration"></a>Konfiguration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidApartmentStateChange />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird eine Situation veranschaulicht, die zum Aktivieren dieses MDA führen kann.  
  
```  
using System.Threading;  
namespace ApartmentStateMDA  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Thread.CurrentThread.SetApartmentState(ApartmentState.STA);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants (Diagnostizieren von Fehlern mit Assistenten für verwaltetes Debuggen)](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling (Interop-Marshalling)](../../../docs/framework/interop/interop-marshaling.md)

