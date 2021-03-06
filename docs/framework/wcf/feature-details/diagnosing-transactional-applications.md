---
title: "Erkennen einer Transaktionsanwendung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a993492-1088-4d10-871b-0c09916af05f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Erkennen einer Transaktionsanwendung
Dieses Thema beschreibt die Verwendung der Verwaltungs\- und Diagnosefunktionen in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] zum Beheben von Fehlern in der Transaktionsanwendung.  
  
## Leistungsindikatoren  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] stellt einen Standardsatz von Leistungsindikatoren bereit, damit Sie die Leistung der Transaktionsanwendung messen können.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Leistungsindikatoren](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md).  
  
 Leistungsindikatoren werden in drei verschiedene Stufen unterteilt: Dienst, Endpunkt und Vorgang, gemäß folgender Tabellen.  
  
### Dienst\-Leistungsindikatoren  
  
|Leistungsindikator|Beschreibung|  
|------------------------|------------------|  
|Übergegangene Transaktionen|Die Anzahl der Transaktionen, die in Vorgänge in diesem Dienst übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn die Nachricht, die an den Dienst gesendet wird, eine Transaktion enthält.|  
|Übergegangene Transaktionen pro Sekunde|Die Anzahl der Transaktionen, die innerhalb von einer Sekunde in Vorgänge in diesem Dienst übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn die Nachricht, die an den Dienst gesendet wird, eine Transaktion enthält.|  
|Übermittelte abgewickelte Vorgänge|Die Anzahl der durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "übermittelt" abgeschlossen wurde.  Arbeiten, die im Rahmen dieser Vorgänge ausgeführt werden, wurden komplett übermittelt.  Ressourcen werden in Übereinstimmung mit der im Vorgang erledigten Arbeit aktualisiert.|  
|Transacted Operations Committed Per Second|Die Anzahl der pro Sekunde durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "übermittelt" abgeschlossen wurde.  Arbeiten, die im Rahmen dieser Vorgänge ausgeführt werden, wurden komplett übermittelt.  Ressourcen werden in Übereinstimmung mit der im Vorgang erledigten Arbeit aktualisiert.|  
|Abgebrochene abgewickelte Vorgänge|Die Anzahl der durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "abgebrochen" abgeschlossen wurde.  Arbeiten, die im Rahmen dieser Vorgänge ausgeführt werden, werden komplett zurückgesetzt.  Ressourcen werden in ihren vorherigen Zustand zurückgesetzt.|  
|Abgebrochene abgewickelte Vorgänge pro Sekunde|Die Anzahl der pro Sekunde durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "abgebrochen" abgeschlossen wurde.  Arbeiten, die im Rahmen dieser Vorgänge ausgeführt werden, werden komplett zurückgesetzt.  Ressourcen werden in ihren vorherigen Zustand zurückgesetzt.|  
|Transacted Operations In Doubt|Die Anzahl der durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "zweifelhaft" abgeschlossen wurde.  Eine Arbeit, deren Ergebnis zweifelhaft ist, befindet sich in einem unbestimmten Zustand.  Für das ausstehende Ergebnis werden Ressourcen bereitgehalten.|  
|Transacted Operations In Doubt Per Second|Die Anzahl der pro Sekunde durchgeführten abgewickelten Vorgänge, deren Transaktion mit dem Ergebnis "zweifelhaft" abgeschlossen wurde.  Eine Arbeit, deren Ergebnis zweifelhaft ist, befindet sich in einem unbestimmten Zustand.  Für das ausstehende Ergebnis werden Ressourcen bereitgehalten.|  
  
### Endpunktleistungsindikatoren  
  
|Leistungsindikator|Beschreibung|  
|------------------------|------------------|  
|Übergegangene Transaktionen|Die Anzahl der Transaktionen, die an diesem Endpunkt in Vorgänge übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn eine Nachricht, die an den Endpunkt gesendet wird, eine Transaktion enthält.|  
|Übergegangene Transaktionen pro Sekunde|Die Anzahl der Transaktionen, die innerhalb von einer Sekunde an diesem Endpunkt in Vorgänge übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn eine Nachricht, die an den Endpunkt gesendet wird, eine Transaktion enthält.|  
  
### Vorgangsleistungsindikatoren  
  
|Leistungsindikator|Beschreibung|  
|------------------------|------------------|  
|Übergegangene Transaktionen|Die Anzahl der Transaktionen, die an diesem Endpunkt in Vorgänge übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn eine Nachricht, die an den Endpunkt gesendet wird, eine Transaktion enthält.|  
|Übergegangene Transaktionen pro Sekunde|Die Anzahl der Transaktionen, die innerhalb von einer Sekunde an diesem Endpunkt in Vorgänge übergegangen sind.  Dieser Indikator wird jedes Mal gesteigert, wenn eine Nachricht, die an den Endpunkt gesendet wird, eine Transaktion enthält.|  
  
## Windows\-Verwaltungsinstrumentation \(Windows Management Instrumentation\)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] macht zur Laufzeit Inspektionsdaten eines Diensts über einen Windows\-Verwaltungsinstrumentation \(WMI\)\-Anbieter von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verfügbar.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] Zugreifen auf WMI\-Daten finden Sie unter [Verwenden der Windows\-Verwaltungsinstrumentation für die Diagnose](../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
 Einige schreibgeschützte WMI\-Eigenschaften geben die angewendeten Transaktionseinstellungen für einen Dienst an.  In der folgenden Tabelle sind alle diese Einstellungen aufgeführt.  
  
 In einem Dienst weist  `ServiceBehaviorAttribute` die folgenden Eigenschaften auf.  
  
|Name|Typ|Beschreibung|  
|----------|---------|------------------|  
|ReleaseServiceInstanceOnTransactionComplete|Boolesch|Gibt an, ob das Dienstobjekt wiederverwendet wird, wenn die aktuelle Transaktion abgeschlossen wird.|  
|TransactionAutoCompleteOnSessionClose|Boolesch|Gibt an, ob ausstehende Transaktionen abgeschlossen werden, wenn die aktuelle Sitzung schließt.|  
|TransactionIsolationLevel|Eine Zeichenfolge, die einen gültigen Wert der Enumeration <xref:System.Transactions.IsolationLevel> enthält.|Gibt die Transaktionsisolationsstufe an, die dieser Dienst unterstützt.|  
|TransactionTimeout|<xref:System.DateTime>|Gibt den Zeitraum an, innerhalb dessen eine Transaktion abgeschlossen werden muss.|  
  
 `ServiceTimeoutsBehavior` verfügt über die folgende Eigenschaft.  
  
|Name|Typ|Beschreibung|  
|----------|---------|------------------|  
|TransactionTimeout|<xref:System.DateTime>|Gibt den Zeitraum an, innerhalb dessen eine Transaktion abgeschlossen werden muss.|  
  
 In einer Bindung weist  `TransactionFlowBindingElement` die folgenden Eigenschaften auf.  
  
|Name|Typ|Beschreibung|  
|----------|---------|------------------|  
|TransactionProtocol|Eine Zeichenfolge, die einen gültigen Wert des Typs <xref:System.ServiceModel.TransactionProtocol> enthält.|Gibt das Transaktionsprotokoll an, das beim Durchführen einer Transaktion verwendet werden sollte.|  
|TransactionFlow\-|Boolesch|Gibt an, ob der eingehende Transaktionsfluss aktiviert ist.|  
  
 In einem Vorgang weist `OperationBehaviorAttribute` die folgenden Eigenschaften auf:  
  
|Name|Typ|Beschreibung|  
|----------|---------|------------------|  
|TransactionAutoComplete|Boolesch|Gibt an, ob die aktuelle Transaktion automatisch übermittelt werden soll, wenn keine nicht behandelten Ausnahmen auftreten.|  
|TransactionScopeRequired|Boolesch|Gibt an, ob der Vorgang eine Transaktion erfordert.|  
  
 In einem Vorgang weist `TransactionFlowAttribute` die folgenden Eigenschaften auf.  
  
|Name|Typ|Beschreibung|  
|----------|---------|------------------|  
|TransactionFlowOption|Eine Zeichenfolge, die einen gültigen Wert der Enumeration <xref:System.ServiceModel.TransactionFlowOption> enthält.|Gibt den Umfang an, in dem ein Transaktionsfluss erforderlich ist.|  
  
## Ablaufverfolgung  
 Ablaufverfolgungen ermöglichen es, Fehler in den Transaktionsanwendungen zu überwachen und zu analysieren.  Die Ablaufverfolgung kann auf verschiedene Weise aktiviert werden:  
  
-   Standard\-[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Ablaufverfolgung  
  
     Dieser Typ der Ablaufverfolgung entspricht der Ablaufverfolgung in jeder beliebigen [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Anwendung.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Konfigurieren der Ablaufverfolgung](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).  
  
-   WS\-AtomicTransaction\-Ablaufverfolgung  
  
     Die WS\-AtomicTransaction\-Ablaufverfolgung kann über das [WS\-AtomicTransaction\-Konfigurationsdienstprogramm \(wsatConfig.exe\)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md) aktiviert werden.  Eine derartige Ablaufverfolgung bietet einen Einblick in den Zustand der Transaktionen und Teilnehmer innerhalb eines Systems.  Zum Aktivieren der Service Model\-Ablaufverfolgung muss der `HKLM\SOFTWARE\Microsoft\WSAT\3.0\ServiceModelDiagnosticTracing`\-Registrierungsschlüssel auf einen gültigen Wert der Enumeration <xref:System.Diagnostics.SourceLevels> festgelegt sein.  Die Nachrichtenprotokollierung kann auf die gleiche Weise wie andere [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Anwendungen aktiviert werden.  
  
-   `System.Transactions`\-Ablaufverfolgung  
  
     Bei Verwendung des OleTransactions\-Protokolls können Protokollnachrichten nicht aufgezeichnet werden.  Die Ablaufverfolgung, die von der <xref:System.Transactions>\-Infrastruktur geboten wird \(die OleTransactions nutzt\), ermöglicht es den Benutzern, Ereignisse, die bei den Transaktionen geschehen sind, anzusehen.  Um die Ablaufverfolgung für eine <xref:System.Transactions>\-Anwendung zu aktivieren, integrieren Sie den folgenden Code in die Konfigurationsdatei `App.config`.  
  
    ```  
    <configuration>  
      <system.diagnostics>  
         <sources>  
            <source name="System.Transactions" switchValue="Verbose, ActivityTracing">  
               <listeners>  
                  <add name="Text"  
                     type="System.Diagnostics.XmlWriterTraceListener"  
                     initializeData="SysTx.log"  
                     traceOutputOptions="Callstack" />  
               </listeners>  
            </source>  
         </sources>  
         <trace autoflush="true" indentsize="4">  
         </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
     Dies aktiviert außerdem [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Ablaufverfolgung, da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] auch die <xref:System.Transactions>\-Infrastruktur nutzt.  
  
## Siehe auch  
 [Verwaltung und Diagnose](../../../../docs/framework/wcf/diagnostics/index.md)   
 [Konfigurieren der Ablaufverfolgung](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [WS\-AtomicTransaction\-Konfigurationsdienstprogramm \(wsatConfig.exe\)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)