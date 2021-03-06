---
title: "Kanonische Datums- und Uhrzeitfunktionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9628b74f-1585-436a-b385-8b02ed0cdd63
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Kanonische Datums- und Uhrzeitfunktionen
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] enthält kanonische Datums\- und Uhrzeitfunktionen.  
  
## Hinweise  
 Die folgende Tabelle zeigt die kanonischen Datums\- und Uhrzeitfunktionen von [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. `datetime` ist ein <xref:System.DateTime>\-Wert.  
  
|Funktion|Beschreibung|  
|--------------|------------------|  
|`AddNanoseconds(` `expression`, `number``)`|Fügt `expression` den angegebenen `number`\-Wert \(in Nanosekunden\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddMicroseconds(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert \(in Mikrosekunden\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddMilliseconds(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert \(in Millisekunden\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddSeconds(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert \(in Sekunden\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddMinutes(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert \(in Minuten\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddHours(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert \(in Stunden\) hinzu.<br /><br /> **Argumente**<br /><br /> `expression`, `DateTime`, `DateTimeOffset` oder `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddDays(` `expression`, `number``)`|Fügt am Ende der `expression` den angegebenen `number`\-Wert für die Tage hinzu.<br /><br /> **Argumente**<br /><br /> `expression`: `DateTime` oder `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddMonths(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert für die Monate hinzu.<br /><br /> **Argumente**<br /><br /> `expression`: `DateTime` oder `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`AddYears(` `expression`, `number``)`|Fügt dem `expression` den angegebenen `number`\-Wert für die Jahre hinzu.<br /><br /> **Argumente**<br /><br /> `expression`: `DateTime` oder `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`CreateDateTime(` `year`, `month`, `day`, `hour`, `minute`, `second``)`|Gibt das aktuelle Datum und die aktuelle Zeit des Servers in der Zeitzone des Servers als neuen `DateTime`\-Wert zurück.<br /><br /> **Argumente**<br /><br /> `year`, `month`, `day`, `hour`, `minute`: `Int16` und `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Rückgabewert**<br /><br /> Ein `DateTime`|  
|`CreateDateTimeOffset(` `year`, `month`, `day`, `hour`, `minute`, `second`, `tzoffset``)`|Gibt einen neuen `DateTimeOffset`\-Wert zurück, der das aktuelle Datum und die aktuelle Uhrzeit des Servers im Verhältnis zur koordinierten Weltzeit \(UTC\) darstellt.<br /><br /> **Argumente**<br /><br /> `year`, `month`, `day`, `hour`, `minute`, `tzoffset`: `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Rückgabewert**<br /><br /> Ein `DateTimeOffset`|  
|`CreateTime(` `hour`, `minute`, `second``)`|Gibt einen neuen `Time`\-Wert als aktuelle Zeit zurück.<br /><br /> **Argumente**<br /><br /> `hour` und `minute`: `Int32`<br /><br /> `second`: `Double`.<br /><br /> **Rückgabewert**<br /><br /> Ein `Time`|  
|`CurrentDateTime()`|Gibt das aktuelle Datum und die aktuelle Uhrzeit des Servers in der Zeitzone des Servers als `DateTime`\-Wert zurück.<br /><br /> **Rückgabewert**<br /><br /> Ein `DateTime`|  
|`CurrentDateTimeOffset()`|Gibt das aktuelle Datum, die aktuelle Uhrzeit sowie einen Offset als `DateTimeOffset` zurück.<br /><br /> **Rückgabewert**<br /><br /> Ein `DateTimeOffset`|  
|`CurrentUtcDateTime()`|Gibt das aktuelle Datum und die aktuelle Zeit des Servers in der UTC\-Zeitzone als <xref:System.DateTime>\-Wert zurück.<br /><br /> **Rückgabewert**<br /><br /> Ein `DateTime`|  
|`Day(` `expression` `)`|Gibt den Tagteil von `expression` als `Int32` zwischen 1 und 31 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime` und `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 12.`<br /><br /> `Day(cast('03/12/1998' as DateTime))`|  
|`DayOfYear(` `expression` `)`|Gibt den Tagteil von `expression` als `Int32`\-Wert zwischen 1 und 366 zurück, wobei 366 für den letzten Tag eines Schaltjahrs zurückgegeben wird.<br /><br /> **Argumente**<br /><br /> `DateTime` oder `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffNanoseconds(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Nanosekunden\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffMilliseconds(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Millisekunden\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffMicroseconds(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Mikrosekunden\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffSeconds(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Sekunden\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffMinutes(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Minuten\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffHours(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Stunden\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset` oder `Time`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffDays(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Tagen\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime` oder `DateTimeOffset`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffMonths(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Monaten\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime` oder `DateTimeOffset`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`DiffYears(` `startExpression`, `endExpression``)`|Gibt die Differenz von `startExpression` und `endExpression` \(in Jahren\) zurück.<br /><br /> **Argumente**<br /><br /> `startExpression`, `endExpression`: `DateTime` oder `DateTimeOffset`. **Note:**  `startExpression` und `endExpression` müssen den gleichen Typ aufweisen. <br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`GetTotalOffsetMinutes(` `datetimeoffset` `)`|Gibt die Anzahl von Minuten zurück, die `datetimeoffset` von GMT abweicht.  Der Wert liegt im Allgemeinen zwischen \+780 und \-780 \(\+ oder \- 13 Stunden\). **Note:**  Diese Funktion wird nur in SQL Server 2008 unterstützt. <br /><br /> **Argumente**<br /><br /> Ein `DateTimeOffset`<br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`Hour (` `expression` `)`|Gibt den Stundenteil von `expression` als `Int32` zwischen 0 und 23 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime, Time` und `DateTimeOffset`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 22.`<br /><br /> `Hour(cast('22:35:5' as DateTime))`|  
|`Millisecond(` `expression` `)`|Gibt den Millisekundenteil von `expression` als `Int32` zwischen 0 und 999 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime, Time` und `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.|  
|`Minute(` `expression` `)`|Gibt den Minutenteil von `expression` als `Int32` zwischen 0 und 59 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime, Time` oder `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 35`<br /><br /> `Minute(cast('22:35:5' as DateTime))`|  
|`Month` `(``expression``)`|Gibt den Monatsteil von `expression` als `Int32` zwischen 1 und 12 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime` oder `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 3.`<br /><br /> `Month(cast('03/12/1998' as DateTime))`|  
|`Second(` `expression` `)`|Gibt den Sekundenteil von `expression` als `Int32` zwischen 0 und 59 zurück.<br /><br /> **Argumente**<br /><br /> `DateTime, Time` und `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 5`<br /><br /> `Second(cast('22:35:5' as DateTime))`|  
|`TruncateTime(` `expression` `)`|Gibt `expression` mit abgeschnittenen Zeitwerten zurück.<br /><br /> **Argumente**<br /><br /> `DateTime` oder `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> Der `expression`\-Typ.|  
|`Year(` `expression` `)`|Gibt den Jahresteil von `expression` als `Int32``YYYY` zurück.<br /><br /> **Argumente**<br /><br /> `DateTime` und `DateTimeOffset`.<br /><br /> **Rückgabewert**<br /><br /> `Int32`.<br /><br /> **Beispiel**<br /><br /> `-- The following example returns 1998.`<br /><br /> `Year(cast('03/12/1998' as DateTime))`|  
  
 Diese Funktionen geben `null` zurück, wenn die Eingabe `null` ist.  
  
 Entsprechende Funktionen sind für den verwalteten Anbieter des Microsoft SQL\-Clients verfügbar.  Weitere Informationen finden Sie unter [SqlClient für Entity Framework\-Funktionen](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md).  
  
## Siehe auch  
 [Kanonische Funktionen](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)