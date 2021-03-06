---
title: invalidOverlappedToPinvoke-MDA
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
- overlapped pointers
- managed debugging assistants (MDAs), overlapped pointers
- invalid overlapped pointer to platform invoke
- InvalidOverlappedToPinvoke MDA
- MDAs (managed debugging assistants), overlapped pointers
- pointers, overlapped
ms.assetid: 28876047-58bd-4fed-9452-c7da346d67c0
caps.latest.revision: 14
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: bafadcaf244cb9c4d6a36bcc10c74f8526df5c0c
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="invalidoverlappedtopinvoke-mda"></a>invalidOverlappedToPinvoke-MDA
Der `invalidOverlappedToPinvoke`-MDA (Managed Debugging Assistant, Assistent für verwaltetes Debuggen) wird aktiviert, wenn ein überlappender Zeiger, der nicht auf dem Garbage Collection-Heap erstellt wurde, an spezifische Win32-Funktionen übergeben wird.  
  
> [!NOTE]
>  Dieser MDA wird standardmäßig nur aktiviert, wenn der Plattformaufruf im Code definiert wurde und der Debugger den JustMyCode-Status der einzelnen Methoden anzeigt. Dieser MDA wird von Debuggern, die JustMyCode nicht interpretieren können (z. B. MDbg.exe ohne Erweiterungen) nicht aktiviert. Dieser MDA kann für diese Debugger mithilfe einer Konfigurationsdatei aktiviert werden, indem `justMyCode="false"` in der Datei ".mda.config" explizit festgelegt wird: `(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>`.  
  
## <a name="symptoms"></a>Symptome  
 Abstürze oder unerklärliche Heapbeschädigungen.  
  
## <a name="cause"></a>Ursache  
 Ein überlappender Zeiger, der nicht auf dem Garbage Collection-Heap erstellt wurde, wird an spezifische Betriebssystemfunktionen übergeben.  
  
 In der folgenden Tabelle werden die Funktionen gezeigt, die von diesem MDA überwacht werden.  
  
|Modul|Funktion|  
|------------|--------------|  
|HttpApi.dll|`HttpReceiveHttpRequest`|  
|IpHlpApi.dll|`NotifyAddrChange`|  
|kernel32.dll|`ReadFile`|  
|kernel32.dll|`ReadFileEx`|  
|kernel32.dll|`WriteFile`|  
|kernel32.dll|`WriteFileEx`|  
|kernel32.dll|`ReadDirectoryChangesW`|  
|kernel32.dll|`PostQueuedCompletionStatus`|  
|MSWSock.dll|`ConnectEx`|  
|WS2_32.dll|`WSASend`|  
|WS2_32.dll|`WSASendTo`|  
|WS2_32.dll|`WSARecv`|  
|WS2_32.dll|`WSARecvFrom`|  
|MQRT.dll|`MQReceiveMessage`|  
  
 Unter dieser Bedingung besteht eine hohe Wahrscheinlichkeit von Heapbeschädigungen, da die <xref:System.AppDomain>, die den Aufruf durchführt, möglicherweise entladen wird. Falls die <xref:System.AppDomain> entladen wird, gibt der Anwendungscode den Speicher für den überlappenden Zeiger frei, was beim Ende des Vorgangs zu Beschädigungen führt, oder der Code verursacht einen Speicherverlust, was später zu Schwierigkeiten führt.  
  
## <a name="resolution"></a>Auflösung  
 Verwenden Sie ein <xref:System.Threading.Overlapped>-Objekt mit einem Aufruf der <xref:System.Threading.Overlapped.Pack%2A>-Methode, um eine <xref:System.Threading.NativeOverlapped>-Struktur abzurufen, die an die Funktion übergeben werden kann. Wenn die <xref:System.AppDomain> entladen wird, wartet die CLR auf den Abschluss des asynchronen Vorgangs, bevor der Zeiger freigegeben wird.  
  
## <a name="effect-on-the-runtime"></a>Auswirkungen auf die Laufzeit  
 Dieser MDA hat keine Auswirkungen auf die CLR.  
  
## <a name="output"></a>Ausgabe  
 Im Folgenden finden Sie ein Beispiel für die Ausgabe dieses MDA.  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the Win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlapped structure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a>Konfiguration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidOverlappedToPinvoke/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants (Diagnostizieren von Fehlern mit Assistenten für verwaltetes Debuggen)](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling (Interop-Marshalling)](../../../docs/framework/interop/interop-marshaling.md)

