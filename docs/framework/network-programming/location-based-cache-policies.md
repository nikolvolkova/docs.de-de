---
title: Speicherortbasierte Cacherichtlinien
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Cache If Available policy
- reload policy
- location-based cache policies
- Cache Only policy
- local cache
- intermediate cache
- No Cache No Store policy
- cache [.NET Framework], location-based policies
- Revalidate policy
- freshness of cached resources
- Cache Or Next Cache Only policy
- Refresh policy
ms.assetid: e41d7f1a-0a6a-4dee-97d1-c6a8b6a07fc2
caps.latest.revision: 12
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a5b4bf67db3fcbb70d2a93f35976d8d9b4b3a028
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="location-based-cache-policies"></a>Speicherortbasierte Cacherichtlinien
Eine speicherortbasierte Cacherichtlinie definiert die Aktualität gültiger zwischengespeicherter Einträge basierend darauf, woher die angeforderte Ressource stammen kann. Eine zwischengespeicherte Ressource ist gültig, wenn ihre Verwendung keinen Verstoß gegen vom Server angegebene Anforderungen an die erneute Überprüfung darstellt. Eine speicherortbasierte Cacherichtlinie wird programmgesteuert erstellt, indem ein <xref:System.Net.Cache.RequestCachePolicy>- oder <xref:System.Net.Cache.HttpRequestCachePolicy>-Klassenkonstruktor verwendet wird. Der Typ der speicherortbasierten Richtlinie wird mithilfe eines <xref:System.Net.Cache.RequestCacheLevel>- oder <xref:System.Net.Cache.HttpRequestCacheLevel>-Enumerationswerts an den Konstruktor übergeben. Codebeispiele, die speicherortbasierte Cacherichtlinien erstellen, finden Sie unter [Vorgehensweise: Festlegen einer speicherortbasierten Cacherichtlinie für eine Anwendung](../../../docs/framework/network-programming/how-to-set-a-location-based-cache-policy-for-an-application.md). Im folgenden Abschnitt wird jeder Typ der speicherortbasierten Cacherichtlinie für Hypertext Transfer-Protokollressourcen (http und https) erklärt.  
  
## <a name="cache-if-available-policy"></a>Richtlinie „Zwischenspeichern, sofern verfügbar“  
 Wenn sich eine gültige angeforderte Ressource im lokalen Cache befindet, wird die zwischengespeicherte Ressource verwendet. Andernfalls wird die Anforderung für die Ressource an den Server gesendet. Wenn die angeforderte Ressource in einem Cache zwischen dem Client und dem Server verfügbar ist, kann die Anforderung von einem Zwischen-Cache erfüllt werden.  
  
## <a name="cache-only-policy"></a>Richtlinie „Nur zwischenspeichern“  
 Wenn sich eine gültige angeforderte Ressource im lokalen Cache befindet, wird die zwischengespeicherte Ressource verwendet. Wenn diese Cacherichtlinienebene angegeben wird, wird eine <xref:System.Net.WebException>-Ausnahme ausgelöst, wenn sich das Element nicht im lokalen Cache befindet.  
  
## <a name="cache-or-next-cache-only-policy"></a>Richtlinie „Cache oder nur nächster Cache“  
 Wenn sich eine gültige angeforderte Ressource im lokalen Cache oder einem Zwischen-Cache auf dem lokalen Netzwerk befindet, wird die zwischengespeicherte Ressource verwendet. Andernfalls wird eine <xref:System.Net.WebException>-Ausnahme ausgelöst. Im HTTP-Cacheprotokoll wird dies erreicht, indem die Cachesteuerungsanweisung „only-if-cached“ verwendet wird.  
  
## <a name="no-cache-no-store-policy"></a>Richtlinie „Kein Cache, kein Speicher“  
 Eine angeforderte Ressource wird nie aus einem Cache heraus verwendet und nie in einen Cache platziert. Wenn eine angeforderte Ressource im lokalen Cache vorhanden ist, wird sie entfernt. Diese Richtlinienebene gibt für Zwischen-Caches an, dass sie die Ressource ebenfalls entfernen sollten. Im HTTP-Cacheprotokoll wird dies erreicht, indem die Cachesteuerungsanweisung „no-store“ verwendet wird.  
  
## <a name="refresh-policy"></a>Aktualisierungsrichtlinie  
 Eine angeforderte Ressource kann verwendet werden, wenn sie vom Server abgerufen oder in einem anderen Cache als dem lokalen Cache gefunden wurde. Bevor die Anforderung durch einen Zwischen-Cache erfüllt werden kann, muss dieser Cache seinen zwischengespeicherten Eintrag mit dem Server erneut überprüfen. Im HTTP-Cacheprotokoll wird dies erreicht, indem die Cachesteuerungsanweisung „max-age = 0“ und der Pragma-Header „no-cache“ verwendet werden.  
  
## <a name="reload-policy"></a>Richtlinie zum erneuten Laden  
 Angeforderte Ressourcen müssen vom Server abgerufen werden. Die Antwort wird möglicherweise im lokalen Cache gespeichert. Im HTTP-Cacheprotokoll wird dies erreicht, indem die Cachesteuerungsanweisung „no-cache“ und der Pragma-Header „no-cache“ verwendet werden.  
  
## <a name="revalidate-policy"></a>Richtlinie zum erneuten Überprüfen  
 Vergleicht die Kopie der Ressource im Cache mit der Kopie auf dem Server. Wenn die Kopie auf dem Server neuer ist, wird sie zum Erfüllen der Anforderung verwendet und ersetzt die Kopie im Cache. Wenn die Kopie im Cache mit der Serverkopie übereinstimmt, wird die zwischengespeicherte Kopie verwendet. Im HTTP-Cacheprotokoll wird dies erreicht, indem eine bedingte Anforderung verwendet wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Cacheverwaltung für Netzwerkanwendungen](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Cacherichtlinie](../../../docs/framework/network-programming/cache-policy.md)   
 [Zeitbasierte Cacherichtlinien](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Konfigurieren der Zwischenspeicherung in den Netzwerkanwendungen](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)   
 [\<requestCaching>-Element (Netzwerkeinstellungen)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)

