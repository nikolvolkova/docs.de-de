---
title: ".NET Framework Cryptography Model | Microsoft Docs"
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
  - "cryptography [.NET Framework], model"
  - "encryption [.NET Framework], model"
ms.assetid: 12fecad4-fbab-432a-bade-2f05976a2971
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# .NET Framework Cryptography Model
.NET Framework stellt Implementierungen von vielen kryptografischen Standardalgorithmen bereit.  Diese Algorithmen sind einfach zu verwenden und die sichersten möglichen Standardeigenschaften.  Darüber hinaus ist das .NET Framework\-Kryptografiemodell mit Objektvererbung, Streamdesign und Konfiguration äußerst erweiterbar.  
  
## Objektvererbung  
 Das Sicherheitssystem von .NET Framework implementiert ein erweiterbares Muster der abgeleiteten Klassenvererbung.  Die Hierarchie lautet wie folgt:  
  
-   Algorithmustypklasse, etwa <xref:System.Security.Cryptography.SymmetricAlgorithm>, <xref:System.Security.Cryptography.AsymmetricAlgorithm> oder <xref:System.Security.Cryptography.HashAlgorithm>.  Diese Ebene ist abstrakt.  
  
-   Algorithmusklasse, die von einer Algorithmustypklasse erbt; z. B. <xref:System.Security.Cryptography.Aes>, <xref:System.Security.Cryptography.RC2> oder <xref:System.Security.Cryptography.ECDiffieHellman>.  Diese Ebene ist abstrakt.  
  
-   Implementierung einer Algorithmusklasse, die von einer Algorithmusklasse erbt; z. B. <xref:System.Security.Cryptography.AesManaged>, <xref:System.Security.Cryptography.RC2CryptoServiceProvider> oder <xref:System.Security.Cryptography.ECDiffieHellmanCng>.  Diese Ebene ist vollständig implementiert.  
  
 Wird dieses Muster abgeleiteter Klassen verwendet, ist es einfach, einen neuen Algorithmus oder eine neue Implementierung eines vorhandenen Algorithmus hinzuzufügen.  Möchten Sie z. B. einen neuen Algorithmus für einen öffentlichem Schlüssel erstellen, würden Sie von der <xref:System.Security.Cryptography.AsymmetricAlgorithm>\-Klasse erben.  Um eine neue Implementierung eines bestimmten Algorithmus zu erstellen, würden Sie eine nicht abstrakte abgeleitete Klasse dieses Algorithmus erstellen.  
  
## So werden Algorithmen in .NET Framework implementiert  
 Als ein Beispiel für die verschiedenen Implementierungen eines Algorithmus können Sie sich symmetrische Algorithmen ansehen.  Die Basis für alle symmetrischen Algorithmen ist die <xref:System.Security.Cryptography.SymmetricAlgorithm>\-Klasse, die von den folgenden Algorithmen geerbt wird:  
  
1.  <xref:System.Security.Cryptography.Aes>  
  
2.  <xref:System.Security.Cryptography.DES>  
  
3.  <xref:System.Security.Cryptography.RC2>  
  
4.  <xref:System.Security.Cryptography.Rijndael>  
  
5.  <xref:System.Security.Cryptography.TripleDES>  
  
 <xref:System.Security.Cryptography.Aes> wird von zwei Klassen geerbt: <xref:System.Security.Cryptography.AesCryptoServiceProvider> und <xref:System.Security.Cryptography.AesManaged>.  Die <xref:System.Security.Cryptography.AesCryptoServiceProvider>\-Klasse ist ein Wrapper um die Implementierung der Windows\-Kryptografie\-API \(CAPI\) von Aes, während die <xref:System.Security.Cryptography.AesManaged>\-Klasse vollständig in verwaltetem Code geschrieben ist.  Außerdem gibt es einen dritten Typ von Implementierung ,Cryptography Next Generation \(CNG\), zusätzlich zu den verwalteten und den CAPI\-Implementierungen.  Ein Beispiel für einen CNG\-Algorithmus ist <xref:System.Security.Cryptography.ECDiffieHellmanCng>.  CNG\-Algorithmen sind ab Windows Vista verfügbar.  
  
 Sie haben die Wahl, welche Implementierung für Sie am besten geeignet ist.  Die verwalteten Implementierungen sind auf allen Plattformen verfügbar, die .NET Framework unterstützen.  Die CAPI\-Implementierungen sind unter älteren Betriebssystemen verfügbar und werden nicht mehr entwickelt.  CNG ist die neueste Implementierung, in der die neue Entwicklungen erfolgen.  Die verwalteten Implementierungen sind nicht durch die FIPS \(Federal Information Processing Standards\) zertifiziert und möglicherweise langsamer als die Wrapperklassen.  
  
## Streamdesign \(Datenstromdesign\)  
 Die Common Language Runtime verwendet ein streamorientiertes Design für die Implementierung von symmetrischen Algorithmen und Hashalgorithmen.  Der Kern dieses Designs ist die <xref:System.Security.Cryptography.CryptoStream>\-Klasse, die aus der <xref:System.IO.Stream>\-Klasse abgeleitet ist.  Streambasierte kryptografische Objekte unterstützen eine einzelne Standardschnittstelle \(`CryptoStream`\) für die Verarbeitung des Datenübertragungsanteils des jeweiligen Objekts.  Da alle Objekte auf Basis einer Standardschnittstelle erstellt werden, können Sie mehrere Objekte verketten \(z. B. ein Hashobjekt, auf das ein Verschlüsselungsobjekt folgt\), und Sie können mehrere Vorgänge für die Daten ausführen, ohne eine temporäre Speicherung für die Daten zu benötigen.  Das Streamingmodell ermöglicht es Ihnen auch, Objekte aus kleineren Objekten zu erstellen.  Beispielsweise kann ein kombinierter Verschlüsselungs\- und Hashalgorithmus als einzelnes Streamobjekt \(Datenstromobjekt\) angezeigt werden, obwohl dieses Objekt möglicherweise aus einem Satz von Streamobjekten erstellt wurde.  
  
## Kryptografische Konfiguration  
 Mit einer kryptografischen Konfiguration können Sie eine bestimmte Implementierung eines Algorithmus zu einem Algorithmusnamen auflösen, wodurch Erweiterbarkeit der Kryptografieklassen von .NET Framework ermöglicht wird.  Sie können Ihre eigene Hardware\- oder Softwareimplementierung eines Algorithmus hinzufügen und die Implementierung dem von Ihnen gewählten Algorithmusnamen zuordnen.  Ist in der Konfigurationsdatei kein Algorithmus angegeben, werden die Standardeinstellungen verwendet.  Weitere Informationen zu einer kryptografischen Konfiguration finden Sie unter [Konfigurieren kryptografischer Klassen](../../../docs/framework/configure-apps/configure-cryptography-classes.md).  
  
## Wählen eines Algorithmus  
 Sie können einen Algorithmus für unterschiedliche Zwecke wählen: z. B. für Datenintegrität, für Datenschutz oder zum Generieren eines Schlüssels.  Symmetrische und Hashalgorithmen sind dazu vorgesehen, Daten entweder aus Integritätsgründen \(Schutz vor Änderungen\) oder aus Datenschutzgründen \(Schutz vor Anzeigen\) zu schützen.  Hashalgorithmen werden hauptsächlich für die Datenintegrität verwendet.  
  
 Es folgt eine Liste empfohlener Algorithmen nach Anwendung:  
  
-   Datenschutz:  
  
    -   <xref:System.Security.Cryptography.Aes>  
  
-   Datenintegrität:  
  
    -   <xref:System.Security.Cryptography.HMACSHA256>  
  
    -   <xref:System.Security.Cryptography.HMACSHA512>  
  
-   Digitale Signatur:  
  
    -   <xref:System.Security.Cryptography.ECDsa>  
  
    -   <xref:System.Security.Cryptography.RSA>  
  
-   Schlüsselaustausch:  
  
    -   <xref:System.Security.Cryptography.ECDiffieHellman>  
  
    -   <xref:System.Security.Cryptography.RSA>  
  
-   Zufallszahlengenerierung:  
  
    -   <xref:System.Security.Cryptography.RNGCryptoServiceProvider>  
  
-   Generieren eines Schlüssels aus einem Kennwort:  
  
    -   <xref:System.Security.Cryptography.Rfc2898DeriveBytes>  
  
## Siehe auch  
 [Kryptografische Dienste](../../../docs/standard/security/cryptographic-services.md)   
 [Kryptografische Dienste](../../../docs/standard/security/cryptographic-services.md)