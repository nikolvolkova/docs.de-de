---
title: Verwenden von Ausnahmen (C#-Programmierhandbuch)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 96fc082d135d38f521429de7b4e9a668773982ea
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="using-exceptions-c-programming-guide"></a>Verwenden von Ausnahmen (C#-Programmierhandbuch)
In C# werden Fehler im Programm zur Laufzeit mithilfe von sogenannten Ausnahmen durch das Programm weitergegeben. Ausnahmen werden von Code ausgelöst, der auf einen Fehler stößt. Sie werden von Code abgefangen, der den Fehler beheben kann. Ausnahmen können durch die Common Language Runtime (CLR) von .NET Framework oder durch Code in einem Programm ausgelöst werden. Sobald eine Ausnahme ausgelöst wird, wird sie in der Aufrufliste nach oben weitergegeben, bis eine `catch`-Anweisung für die Ausnahme gefunden wird. Nicht abgefangene Ausnahmen werden von einem generischen Ausnahmehandler behandelt, der vom System bereitgestellt wird, das ein Dialogfeld anzeigt.  
  
 Ausnahmen werden von Klassen dargestellt, die von <xref:System.Exception> abgeleitet sind. Diese Klasse bestimmt den Typ der Ausnahme und enthält Eigenschaften, die über Details zur Ausnahme verfügen. Das Auslösen einer Ausnahme umfasst das Erstellen einer Instanz einer von einer Ausnahme abgeleiteten Klasse, das optionale Konfigurieren von Eigenschaften der Ausnahme und das Auslösen des Objekts mithilfe des Schlüsselworts `throw`. Beispiel:  
  
 [!code-cs[csProgGuideExceptions#1](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_1.cs)]  
  
 Nachdem eine Ausnahme ausgelöst wird, überprüft die Runtime die aktuelle Anweisung, um festzustellen, ob sie sich in einem `try`-Block befindet. Falls dies der Fall ist, werden alle mit dem `try`-Block verknüpften `catch`-Blöcke überprüft, um festzustellen, ob sie die Ausnahme abfangen können. `Catch`-Blöcke geben normalerweise Ausnahmetypen an; wenn der Typ des `catch`-Blocks der gleiche Typ ist wie die Ausnahme oder die Basisklasse der Ausnahme, kann der `catch`-Block die Methode behandeln. Zum Beispiel:  
  
 [!code-cs[csProgGuideExceptions#2](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_2.cs)]  
  
 Wenn sich die Anweisung, die eine Ausnahme auslöst, nicht innerhalb eines `try`-Blocks befindet, oder der `try`-Block, der sie umfasst, über keinen übereinstimmenden `catch`-Block verfügt, überprüft die Runtime die aufrufende Methode auf eine `try`-Anweisung und `catch`-Blöcke. Die Runtime geht die Aufrufliste weiter nach oben durch und sucht nach einem kompatiblen `catch`-Block. Nachdem der `catch`-Block gefunden und ausgeführt wurde, wird die Steuerung an die nächste Anweisung nach diesem `catch`-Block weitergegeben.  
  
 Eine `try`-Anweisung kann mehr als einen `catch`-Block enthalten. Die erste `catch`-Anweisung, die die Ausnahme behandelt, wird ausgeführt; alle folgenden `catch`-Anweisungen werden ignoriert, selbst wenn sie kompatibel sind. Daher sollten catch-Blöcke immer vom spezifischsten Element (oder am meisten abgeleiteten) zum am wenigsten spezifischen sortiert werden. Zum Beispiel:  
  
 [!code-cs[csProgGuideExceptions#3](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_3.cs)]  
  
 Bevor der `catch`-Block ausgeführt wird prüft die Runtime auf `finally`-Blöcke. `Finally`-Blöcke ermöglichen dem Programmierer, mehrdeutige Zustände zu bereinigen, die möglicherweise von einem abgebrochenen `try`-Block übrig sind, oder externe Ressourcen freizugeben (z.B. Grafikhandles, Datenbankverbindungen oder Dateistreams), ohne auf Garbage Collector in der Runtime zum Finalisieren der Objekte zu warten. Zum Beispiel:  
  
 [!code-cs[csProgGuideExceptions#4](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_4.cs)]  
  
 Wenn `WriteByte()` eine Ausnahme auslöst, schlägt der Code im zweiten `try`-Block fehl, der versucht, die Datei erneut zu öffnen, wenn `file.Close()` nicht aufgerufen wird. Die Datei bleibt gesperrt. Da `finally`-Blocke ausgeführt werden, selbst wenn eine Ausnahme ausgelöst wird, ermöglicht es der `finally`-Block im vorherigen Beispiel, dass die Datei korrekt geschlossen wird und trägt so zur Fehlervermeidung bei.  
  
 Wenn in der Aufrufliste kein kompatibler `catch`-Block gefunden wird, nachdem eine Ausnahme ausgelöst wird, tritt eine der folgenden Situationen auf:  
  
-   Wenn die Ausnahme sich in einem Finalizer befindet, wird der Finalizer abgebrochen und der Basisfinalizer (sofern vorhanden) aufgerufen.  
  
-   Wenn die Aufrufliste einen statischen Konstruktor oder einen statischen Feldinitialisierer enthält, wird <xref:System.TypeInitializationException> ausgelöst und die ursprüngliche Ausnahme der <xref:System.Exception.InnerException%2A>-Eigenschaft der neuen Ausnahme zugewiesen.  
  
-   Wenn der Anfang des Threads erreicht wird, wird der Thread beendet.  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Ausnahmen und Ausnahmebehandlung](../../../csharp/programming-guide/exceptions/index.md)

