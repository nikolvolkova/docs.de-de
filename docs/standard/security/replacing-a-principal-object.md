---
title: "Replacing a Principal Object | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "principal objects, replacing"
  - "security [.NET Framework], replacing principal objects"
  - "security [.NET Framework], principals"
ms.assetid: c323687e-b196-487b-beba-f38f9b3f961b
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Replacing a Principal Object
Anwendungen, die Authentifizierungsdienste bereitstellen, müssen das **Principal**\-Objekt \(<xref:System.Security.Principal.IPrincipal>\) für einen vorhandenen Thread ersetzen können. Zusätzlich muss das Sicherheitssystem Schutz für ein Ersetzen von **Principal**\-Objekten bieten, weil ein in böswilliger Absicht zugewiesenes falsches **Principal**\-Objekt die Sicherheit der Anwendung durch Angabe einer falschen Identität oder Rolle beeinträchtigt. Daher muss Anwendungen, die in der Lage sind, **Principal**\-Objekte zu ersetzen, das <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName>\-Objekt gewährt werden, damit Prinzipale gesteuert werden können. \(Beachten Sie, dass diese Berechtigung nicht dazu erforderlich ist, rollenbasierte Sicherheitsüberprüfungen auszuführen oder **Principal**\-Objekte zu erstellen.\)  
  
 Das aktuelle **Principal**\-Objekt kann ersetzt werden, indem die folgenden Schritte ausgeführt werden:  
  
1.  Erstellen Sie das ersetzende **Principal**\-Objekt und das zugeordnete **Identity**\-Objekt.  
  
2.  Ordnen Sie das neue **Principal**\-Objekt dem Aufrufkontext zu.  
  
## Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie ein allgemeines Principal\-Objekt erstellt und dann dazu verwendet wird, den Prinzipal eines Threads festzulegen.  
  
 [!code-csharp[SetCurrentPrincipal#1](../../../samples/snippets/csharp/VS_Snippets_CLR/SetCurrentPrincipal/CS/program.cs#1)]
 [!code-vb[SetCurrentPrincipal#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/SetCurrentPrincipal/VB/program.vb#1)]  
  
## Siehe auch  
 <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName>   
 [Principal and Identity Objects](../../../docs/standard/security/principal-and-identity-objects.md)