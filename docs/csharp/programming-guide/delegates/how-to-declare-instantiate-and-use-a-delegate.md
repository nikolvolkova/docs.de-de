---
title: 'Gewusst wie: Deklarieren, Instanziieren und Verwenden von Delegaten (C#-Programmierhandbuch)'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- delegates [C#], declaring and instantiating
ms.assetid: 61c4895f-f785-48f8-8bfe-db73b411c4ae
caps.latest.revision: 21
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
ms.openlocfilehash: 5a16fe4c627989f701ba523769cd87839d074849
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-declare-instantiate-and-use-a-delegate-c-programming-guide"></a>Gewusst wie: Deklarieren, Instanziieren und Verwenden von Delegaten (C#-Programmierhandbuch)
In C# 1.0 und höher können Delegaten wie im folgenden Beispiel gezeigt deklariert werden.  
  
 [!code-cs[csProgGuideDelegates#13](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#14](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_2.cs)]  
  
 C# 2.0 bietet eine einfachere Möglichkeit zum Schreiben der vorangegangenen Deklaration, siehe folgendes Beispiel.  
  
 [!code-cs[csProgGuideDelegates#32](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_3.cs)]  
  
 In C# 2.0 und höher ist es außerdem möglich, eine anonyme Methode zum Deklarieren und Initialisieren eines [Delegaten](../../../csharp/language-reference/keywords/delegate.md) zu verwenden. Dies wird im nachstehenden Beispiel gezeigt.  
  
 [!code-cs[csProgGuideDelegates#15](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_4.cs)]  
  
 In C# 3.0 und höher können Delegaten auch mithilfe eines Lamdaausdrucks deklariert und instanziiert werden, wie im folgenden Beispiel dargestellt.  
  
 [!code-cs[csProgGuideDelegates#31](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_5.cs)]  
  
 Weitere Informationen finden Sie unter [Lambdaausdrücke](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Im folgenden Beispiel wird verdeutlicht, wie Sie einen Delegaten deklarieren, instanziieren und verwenden. In der `BookDB`-Klasse ist eine Buchhandlungsdatenbank gekapselt, die eine Buchtiteldatenbank enthält. Sie stellt eine `ProcessPaperbackBooks`-Methode zur Verfügung, durch die alle Taschenbücher in der Datenbank gefunden werden und für jedes Taschenbuch ein Delegat aufgerufen wird. Der verwendete `delegate`-Typ hat den Namen `ProcessBookDelegate`. Die `Test`-Klasse verwendet diese Klasse, um die Buchtitel und Durchschnittspreise der Taschenbücher auszugeben.  
  
 Die Verwendung von Delegaten beinhaltet eine sinnvolle Trennung der Funktionalitäten von Buchhandlungsdatenbank und Clientcode. Der Clientcode hat keine Kenntnis darüber, wie die Bücher archiviert werden oder wie der Buchhandlungscode Taschenbücher sucht. Der Buchhandlungscode wiederum hat keine Kenntnis darüber, wie ein Taschenbuchtitel weiterverarbeitet wird, nachdem er gefunden wurde.  
  
## <a name="example"></a>Beispiel  
 [!code-cs[csProgGuideDelegates#12](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_6.cs)]  
  
## <a name="robust-programming"></a>Stabile Programmierung  
  
-   Deklarieren von Delegaten  
  
     Mit der folgenden Anweisung wird ein neuer Delegattyp deklariert.  
  
     [!code-cs[csProgGuideDelegates#16](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_7.cs)]  
  
     Durch die einzelnen Delegattypen werden Anzahl und Typen von Argumenten sowie Rückgabewerte von Methoden beschrieben, die gekapselt werden können. Sobald neue Argumenttypen benötigt werden oder ein neuer Rückgabewerttyp erforderlich ist, muss ein neuer Delegattyp deklariert werden.  
  
-   Instanziieren von Delegaten  
  
     Nachdem ein Delegattyp deklariert wurde, muss ein Delegatobjekt erstellt und einer bestimmten Methode zugeordnet werden. Im vorherigen Beispiel übergeben Sie dazu die `PrintTitle`-Methode an die `ProcessPaperbackBooks`-Methode, wie im folgenden Beispiel gezeigt:  
  
     [!code-cs[csProgGuideDelegates#17](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_8.cs)]  
  
     Hierdurch wird ein neues Delegatobjekt erstellt, das der [statischen](../../../csharp/language-reference/keywords/static.md) Methode `Test.PrintTitle` zugeordnet ist. Auf ähnliche Weise wird die nicht statische Methode `AddBookToTotal` für das Objekt `totaller` übergeben, wie im folgenden Beispiel gezeigt:  
  
     [!code-cs[csProgGuideDelegates#18](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_9.cs)]  
  
     In beiden Fällen wird ein neues Delegatobjekt an die `ProcessPaperbackBooks`-Methode übergeben.  
  
     Nach der Erstellung eines Delegaten wird die diesem zugeordnete Methode nicht mehr geändert. Delegatobjekte sind unveränderlich.  
  
-   Aufrufen von Delegaten  
  
     Nachdem ein Delegatobjekt erstellt wurde, wird es normalerweise an anderen Code übergeben, durch den der Delegat aufgerufen wird. Ein Delegatobjekt wird über seinen Namen aufgerufen. Auf den Namen folgen (in Klammern gesetzte) Argumente, die an den Delegaten übergeben werden sollen. Es folgt ein Beispiel für einen Delegataufruf:  
  
     [!code-cs[csProgGuideDelegates#19](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_10.cs)]  
  
     Ein Delegat kann entweder (wie in diesem Beispiel) synchron oder mithilfe der `BeginInvoke`-Methode und der `EndInvoke`-Methode asynchron aufgerufen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Ereignisse](../../../csharp/programming-guide/events/index.md)   
 [Delegaten](../../../csharp/programming-guide/delegates/index.md)

