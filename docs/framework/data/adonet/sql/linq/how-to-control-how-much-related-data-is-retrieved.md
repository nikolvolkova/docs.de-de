---
title: "Vorgehensweise: Steuern der Menge verbundener Daten, die abgerufen werden | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efdc203e-3da9-4477-815e-54f10c3d7c6c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vorgehensweise: Steuern der Menge verbundener Daten, die abgerufen werden
Geben Sie mit der <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A>\-Methode an, welche mit Ihrem Hauptziel verbundenen Daten gleichzeitig abgerufen werden sollen.  Wenn Sie beispielsweise Informationen über die Bestellungen eines Kunden benötigen, können Sie mithilfe von <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> sicherstellen, dass die Bestellinformationen zusammen mit den Kundeninformationen abgerufen werden.  Dadurch können beide Informationssätze in einem Vorgang aus der Datenbank abgerufen werden.  
  
> [!NOTE]
>  Sie können Daten zum Hauptziel Ihrer Anfrage abrufen, indem Sie eine produktübergreifende Abfrage in Form einer großen Projektion abrufen \(z. B. werden Bestellungen abgerufen, wenn Sie auf Kunden abzielen\).  Dieser Ansatz hat oft Nachteile.  Die Ergebnisse sind beispielsweise nur Projektionen und keine Entitäten, die mit [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] geändert und erhalten werden können. Außerdem können Sie viele Daten abrufen, die Sie nicht benötigen.  
  
## Beispiel  
 Im folgenden Beispiel werden alle `Orders` \(Bestellungen\) für alle `Customers` \(Kunden\) in London abgerufen, wenn die Abfrage ausgeführt wird.  Aufgrund dessen wird bei nachfolgenden Zugriffen auf die `Orders`\-Eigenschaft für ein `Customer`\-Objekt keine neue Datenbankabfrage ausgelöst.  
  
 [!code-csharp[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.dataloadoptions/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.dataloadoptions/vb/module1.vb#2)]  
  
## Siehe auch  
 [Abfragen der Datenbank](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)