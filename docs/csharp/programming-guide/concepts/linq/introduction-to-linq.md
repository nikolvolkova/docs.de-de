---
title: "Einführung in LINQ (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 54874feb-55e5-4ca8-a9d6-1c1127fd7fb1
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d90ea2503ba94df8ddb750b6f328168ddf22a65a
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="introduction-to-linq-c"></a>Einführung in LINQ (C#)
Language Integrated Query (LINQ) ist eine in .NET Framework-Version 3.5 eingeführte Innovation, die die Lücke zwischen der Welt der Objekte und der Welt der Daten überbrückt.  
  
 Abfragen von Daten werden gewöhnlich als einfache Zeichenfolgen ohne Typüberprüfung zur Kompilierzeit oder IntelliSense-Unterstützung ausgedrückt. Darüber hinaus müssen Sie für jeden Typ von Datenquelle eine andere Abfragesprache erlernen: SQL-Datenbanken, XML-Dokumente, verschiedene Webdienste usw. Durch LINQ wird eine *Abfrage* zu einem erstklassigen Sprachkonstrukt in C#. Sie schreiben Abfragen für stark typisierte Auflistungen von Objekten mithilfe von Sprachschlüsselwörtern und bekannten Operatoren.  
  
 Sie können LINQ-Abfragen in C# für SQL Server-Datenbanken, XML-Dokumente, ADO.NET-Datasets und jede Auflistung von Objekten schreiben, die <xref:System.Collections.IEnumerable> oder die generische <xref:System.Collections.Generic.IEnumerable%601>-Schnittstelle unterstützt. LINQ-Unterstützung wird auch von Drittanbietern für viele Webdienste und andere Datenbankimplementierungen bereitgestellt.  
  
 Sie können LINQ-Abfragen in neuen Projekten oder zusammen mit nicht-LINQ-Abfragen in vorhandenen Projekten verwenden. Die einzige Voraussetzung ist, dass sich das Projekt auf .NET Framework 3.5 oder höher bezieht.  
  
 Die folgende Abbildung aus Visual Studio zeigt eine teilweise abgeschlossene LINQ-Abfrage für eine SQL Server-Datenbank in C# und Visual Basic mit vollständiger Typüberprüfung und IntelliSense-Unterstützung.  
  
 ![LINQ-Abfrage mit IntelliSense](../../../../csharp/programming-guide/concepts/linq/media/query_intell.png "Query_Intell")  
  
## <a name="next-steps"></a>Nächste Schritte  
 Für weitere Informationen über LINQ können Sie sich zunächst mit einigen grundlegenden Konzepten im Abschnitt [Erste Schritte mit LINQ in C#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md) vertraut machen und dann die Dokumentation für die LINQ-Technologie, die Sie interessiert, lesen:  
  
-   SQL Server-Datenbanken: [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)  
  
-   XML-Dokumente: [LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml.md)  
  
-   ADO.NET-Datasets: [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)  
  
-   .NET-Auflistungen, -Dateien, -Zeichenfolgen usw.: [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Language-Integrated Query (LINQ) (Sprachintegrierte Abfrage (LINQ))](../../../../csharp/programming-guide/concepts/linq/index.md)

