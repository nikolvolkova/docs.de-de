---
title: "&#220;bersicht &#252;ber das Drucken | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Klassen, PrintCapabilities"
  - "Klassen, PrintQueue"
  - "Klassen, PrintServer"
  - "Klassen, PrintTicket"
  - "GDI-Druckpfad"
  - "Druckpfad, XPS"
  - "PrintCapabilities-Klasse"
  - "Drucker, XPSDrv-basiert"
  - "Drucken"
  - "PrintQueue-Klasse PrintServer-Klasse"
  - "PrintTicket-Klasse"
  - "XML Paper Specification (XPS)-Dateiformat"
  - "XPS (XML Paper Specification)-Dateiformat"
  - "XPSDrv-basierte Drucker"
ms.assetid: 0de8ac41-9aa6-413d-a121-7aa6f41539b1
caps.latest.revision: 35
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# &#220;bersicht &#252;ber das Drucken
Mit [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] steht Anwendungsentwicklern, die [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] verwenden, ein umfassender neuer Satz von [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] für den Druck und die Druckverwaltung zur Verfügung.  Mit [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] stehen einige dieser Erweiterungen des Drucksystems auch Entwicklern zur Verfügung, die [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]\-Anwendungen erstellen, sowie Entwicklern, die nicht verwalteten Code verwenden.  Im Zentrum dieser neuen Funktionen stehen das neue [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)]\-Dateiformat und der [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]\-Druckpfad.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [Info über XPS](#introduction_to_XPS)  
  
-   [XPS\-Druckpfad](#XPS_print_path_intro)  
  
-   [GDI\-Druckpfad](#GDI_Print_Path_intro)  
  
-   [XPSDrv\-Treibermodell](#XPS_Driver_Model_intro)  
  
-   [Verwandte Themen](#seeAlso_Toggle)  
  
<a name="introduction_to_XPS"></a>   
## Info über XPS  
 [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] ist ein Format für elektronische Dokumente, ein Format für Spooldateien und eine Seitenbeschreibungssprache.  Es handelt sich um ein offenes Dokumentformat, das [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)], [!INCLUDE[TLA#tla_opc](../../../../includes/tlasharptla-opc-md.md)] und andere Branchenstandards verwendet, um plattformübergreifend nutzbare Dokumente zu erstellen.  [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] vereinfacht die Vorgänge beim Erstellen, Teilen, Drucken, Anzeigen und Archivieren von digitalen Dokumenten.  Weitere Informationen zu [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] finden Sie auf der [XPS\-Website](http://www.microsoft.com/xps).  
  
 Verschiedene Techniken für das Drucken von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-basierten Inhalten mithilfe von [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sind in [Programmgesteuertes Drucken von XPS\-Dateien](../../../../docs/framework/wpf/advanced/how-to-programmatically-print-xps-files.md) dargestellt.  Es kann sinnvoll sein, diese Beispiele beim Durcharbeiten der in diesem Thema enthaltenen Inhalte hinzuzuziehen. \(Entwickler von nicht verwaltetem Code sollten die Hilfe zum *Microsoft XPS Document Converter\-Druckerescape* konsultieren.  [!INCLUDE[TLA2#tla_winforms#initcap](../../../../includes/tla2sharptla-winformssharpinitcap-md.md)]\-Entwickler müssen die [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] im <xref:System.Drawing.Printing>\-Namespace verwenden, die nicht den vollständigen [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]\-Druckpfad, wohl aber einen hybriden GDI\-nach\-XPS\-Druckpfad unterstützt.  Finden Sie unter **Druckpfadarchitektur** unten.\)  
  
<a name="XPS_print_path_intro"></a>   
## XPS\-Druckpfad  
 Der [!INCLUDE[TLA#tla_metro](../../../../includes/tlasharptla-metro-md.md)]\-Druckpfad ist ein neues [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]\-Feature, das die Druckverarbeitung in [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)]\-Anwendungen neu definiert.  Da [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] eine Sprache zur Dokumentdarstellung \(wie etwa RTF\) , ein Druckerspoolerformat \(wie etwa WMF\) und eine Seitenbeschreibungssprache \(wie etwa PCL oder Postscript\) ersetzen kann, bleibt im neuen Druckpfad das [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Format von der Veröffentlichung der Anwendung bis zur abschließenden Verarbeitung im Druckertreiber oder \-gerät erhalten.  
  
 Der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad baut auf dem [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckermodell \(XPSDrv\) auf, das für Entwickler eine Reihe von Vorzügen bereithält, wie etwa [!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)]\-Druck, verbesserte Farbunterstützung und erheblich gesteigerte Druckleistung.  \(Weitere Informationen zu XPSDrv finden Sie im [Windows\-Treiberentwicklungskit](http://msdn.microsoft.com/library/default.asp?url=/library/dnanchor/html/DeviceDriver.asp).\)  
  
 Der Betrieb des Druckerspoolers ist für [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokumente im Wesentlichen gegenüber früheren Versionen von [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] unverändert.  Er wurde jedoch verbessert und unterstützt nun über den vorhandenen [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-Druckpfad hinaus auch den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad.  Der neue Druckpfad nutzt systemeigen eine [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Spooldatei.  Zwar funktionieren für frühere Versionen von [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] erstellte Druckertreiber für den Benutzermodus weiterhin, für den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad ist jedoch ein [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreiber \(XPSDrv\) erforderlich.  
  
 Die Vorzüge des [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfads sind erheblich und umfassen u.a.:  
  
-   [!INCLUDE[TLA2#tla_wys](../../../../includes/tla2sharptla-wys-md.md)]\-Druckunterstützung  
  
-   Systemeigene Unterstützung für erweiterte Farbprofile, die auch 32 Bit pro Kanal \(bpc\), CMYK, benannte Farben, n\-Tinten und systemeigene Unterstützung von Transparenz und Farbverläufen einschließen.  
  
-   Verbesserte Druckleistung für [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]\- und [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]\-basierte Anwendungen.  
  
-   [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Branchenstandardformat.  
  
 Für einfache Druckszenarien ist eine einfache und intuitiv bedienbare [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] mit einem einzelnen Einstiegspunkt für Benutzeroberfläche, Konfiguration und Auftragsübergabe verfügbar.  Für erweiterte Szenarien steht jetzt zusätzlich Unterstützung für [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]\-Anpassung \(oder Verzicht auf die [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]\), synchronen oder asynchronen Druck und Funktionen zum Druck von Batchaufträgen zur Verfügung.  Beide Optionen bieten Druckunterstützung mit vollständigen oder eingeschränkten Vertrauensstellungen.  
  
 [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] wurde im Hinblick auf Erweiterbarkeit entwickelt.  Mithilfe des Extensibility Frameworks können [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] auf modulare Weise Features und Funktionen hinzugefügt werden.  Zu den Erweiterungsfunktionen gehören:  
  
-   Druckschema.  Das öffentliche Schema wird regelmäßig aktualisiert und ermöglicht die schnelle Erweiterung von Gerätefunktionen.  \(Siehe dazu **PrintTicket und PrintCapabilities** unten.\)  
  
-   Erweiterbare Filterpipeline.  Die Filterpipeline des [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreibers \(XPSDrv\) wurde dafür ausgelegt, sowohl direkten als auch skalierbaren Druck von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokumenten zu ermöglichen.  \(Schlagen Sie "XPSDrv" im [Windows\-Treiberentwicklungskit](http://msdn.microsoft.com/library/default.asp?url=/library/dnanchor/html/DeviceDriver.asp) nach.\)  
  
### Druckpfadarchitektur  
 Zwar unterstützen sowohl [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]\- als auch [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]\-Anwendungen [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)], doch verwenden [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]\- und [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]\-Anwendungen eine Konvertierung von [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] nach [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)], um Inhalte im [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Format für den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreiber \(XPSDrv\) zu erstellen.  Diese Anwendungen müssen den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad nicht zwangsläufig verwenden und können weiterhin den [!INCLUDE[TLA#tla_emf](../../../../includes/tlasharptla-emf-md.md)]\-basierten Druck verwenden.  Die meisten Features und Verbesserungen von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] sind jedoch nur für Anwendungen verfügbar, die den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad zum Ziel haben.  
  
 Um die Verwendung von XPSDrv\-basierten Druckern durch [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]\- und [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]\-Anwendungen zu ermöglichen, unterstützt der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreiber \(XPSDrv\) die Konvertierung von [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] in das [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Format. Das XPSDrv\-Modell umfasst außerdem einen Konverter für das [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Format nach [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)], sodass [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]\-Anwendungen [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]\-Dokumente drucken können.  Für [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]\-Anwendungen erfolgt die Konvertierung von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] in das [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-Format automatisch durch die Methoden <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> und <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> der <xref:System.Windows.Xps.XpsDocumentWriter>\-Klasse, wenn die Druckerwarteschlange des Schreibvorgangsziels nicht über einen XPSDrv\-Treiber verfügt. \([!INCLUDE[TLA2#tla_winforms#initcap](../../../../includes/tla2sharptla-winformssharpinitcap-md.md)]\-Anwendungen können keine [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]\-Dokumente drucken.\)  
  
 Die folgende Abbildung stellt das Drucksubsystem dar und definiert die von [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] bereitgestellten sowie die von Software\- und Hardwareherstellern definierten Anteile.  
  
 ![Das XPS&#45;Drucksystem](../../../../docs/framework/wpf/advanced/media/xpsprint.PNG "XPSPrint")  
  
### Einfacher XPS\-Druck  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] definiert sowohl eine einfache als auch eine erweiterte [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)].  Für Anwendungen, die keine umfangreichen Druckanpassungen oder Zugriff auf die Gesamtmenge der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktionen erfordern, ist eine Unterstützung für einfachen Druck verfügbar.  Die einfache Druckunterstützung wird über ein Druckdialogfeld\-Steuerelement verfügbar gemacht, das nur minimale Konfiguration erfordert und eine vertraute [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] bietet.  Viele [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktionen sind in diesem vereinfachten Druckmodell verfügbar.  
  
#### PrintDialog  
 Das <xref:System.Windows.Controls.PrintDialog?displayProperty=fullName>\-Steuerelement stellt einen einheitlichen Einstiegspunkt für [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], Konfiguration und [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Auftragsübermittlung bereit.  Informationen zum Instanziieren und Verwenden des Steuerelements finden Sie unter [Aufrufen eines Druckdialogfelds](../../../../docs/framework/wpf/advanced/how-to-invoke-a-print-dialog.md).  
  
### Erweiterter XPS\-Druck  
 Für den Zugriff auf die Gesamtmenge der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktionen muss die erweiterte Druck\-[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] verwendet werden.  Mehrere relevante [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] sind ausführlicher unten beschrieben.  Eine vollständige Liste der [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] des [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfads finden Sie in den Referenzen zu den Namespaces <xref:System.Windows.Xps> und <xref:System.Printing>.  
  
#### PrintTicket und PrintCapabilities  
 Die Klassen <xref:System.Printing.PrintTicket> und <xref:System.Printing.PrintCapabilities> bilden die Grundlage der erweiterten [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktionen.  Beide Objekttypen sind Strukturen druckorientierter Funktionen, wie etwa Sortierung, doppelseitiger Druck, Heftung usw. im [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]\-Format.  Diese Strukturen sind durch das Druckschema definiert.  Ein <xref:System.Printing.PrintTicket> weist einen Drucker an, wie ein Druckauftrag verarbeitet werden muss.  Die <xref:System.Printing.PrintCapabilities> \-Klasse definiert die Fähigkeiten eines Druckers.  Durch Abfragen der Funktionen eines Druckers kann ein <xref:System.Printing.PrintTicket> erstellt werden, das die von einem Drucker unterstützten Funktionen in vollem Umfang nutzt.  Analog dazu können nicht unterstützte Funktionen vermieden werden.  
  
 Im folgenden Beispiel wird das Abfragen der <xref:System.Printing.PrintCapabilities> eines Druckers und das Erstellen eines <xref:System.Printing.PrintTicket> mithilfe von Code gezeigt.  
  
 [!code-cpp[xpscreate#PrinterCapabilities](../../../../samples/snippets/cpp/VS_Snippets_Wpf/XpsCreate/CPP/XpsCreate.cpp#printercapabilities)]
 [!code-csharp[xpscreate#PrinterCapabilities](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XpsCreate/CSharp/XpsCreate.cs#printercapabilities)]
 [!code-vb[xpscreate#PrinterCapabilities](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XpsCreate/visualbasic/xpscreate.vb#printercapabilities)]  
  
#### PrintServer und PrintQueue  
 Die <xref:System.Printing.PrintServer>\-Klasse stellt einen Netzwerkdruckerserver und die <xref:System.Printing.PrintQueue>\-Klasse einen Drucker mit zugeordneter Auftragswarteschlange dar.  In Kombination ermöglichen diese [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] die erweiterte Verwaltung der Druckaufträge von Servern.  Ein <xref:System.Printing.PrintServer> oder eine davon abgeleitete Klasse wird verwendet, um eine <xref:System.Printing.PrintQueue> zu verwalten.  Die <xref:System.Printing.PrintQueue.AddJob%2A>\-Methode wird verwendet, um einen neuen Druckauftrag in die Warteschlange einzustellen.  
  
 Das folgende Beispiel zeigt, wie ein <xref:System.Printing.LocalPrintServer> erstellt und mithilfe von Code auf seine Standard\-<xref:System.Printing.PrintQueue> zugegriffen wird.  
  
 [!code-csharp[xpsprint#PrintQueueSnip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XpsPrint/CSharp/XpsPrintHelper.cs#printqueuesnip)]
 [!code-vb[xpsprint#PrintQueueSnip](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XpsPrint/visualbasic/xpsprinthelper.vb#printqueuesnip)]  
  
#### XpsDocumentWriter  
 Ein <xref:System.Windows.Xps.XpsDocumentWriter> mit seinen vielen <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A>\- und <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A>\-Methoden, wird zum Schreiben von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokumenten in eine <xref:System.Printing.PrintQueue> verwendet.  So wird z. B. die Methode <xref:System.Windows.Xps.XpsDocumentWriter.Write%28System.Windows.Documents.FixedPage%2CSystem.Printing.PrintTicket%29> verwendet, um ein [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokument und ein <xref:System.Printing.PrintTicket> synchron auszugeben.  Die Methode <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%28System.Windows.Documents.FixedDocument%2CSystem.Printing.PrintTicket%29> wird verwendet, um ein [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokument und ein <xref:System.Printing.PrintTicket> asynchron auszugeben.  
  
 Im folgenden Beispiel wird veranschaulicht, wie ein <xref:System.Windows.Xps.XpsDocumentWriter> mithilfe von Code erstellt wird.  
  
 [!code-csharp[XpsPrint#PrintQueueSnip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XpsPrint/CSharp/XpsPrintHelper.cs#printqueuesnip)]
 [!code-vb[XpsPrint#PrintQueueSnip](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XpsPrint/visualbasic/xpsprinthelper.vb#printqueuesnip)]  
  
 Die <xref:System.Printing.PrintQueue.AddJob%2A>\-Methoden stellen ebenfalls Druckmöglichkeiten bereit.  Details finden Sie unter [Programmgesteuertes Drucken von XPS\-Dateien](../../../../docs/framework/wpf/advanced/how-to-programmatically-print-xps-files.md) .  
  
<a name="GDI_Print_Path_intro"></a>   
## GDI\-Druckpfad  
 Während [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]\-Anwendungen den [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad systemeigen unterstützen, können [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]\- und [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]\-Anwendungen ebenfalls einige der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktionen nutzen.  Der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreiber \(XPSDrv\) kann [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-basierte Ausgaben in das [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Format konvertieren.  Für erweiterte Szenarien wird die benutzerdefinierte Konvertierung von Inhalten mithilfe von [Microsoft XPS Document Converter\-Druckerescape](_win32_MXDC_ESCAPE) unterstützt.  In ähnlicher Weise können [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]\-Anwendungen durch Aufrufen einer der <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A>\- oder <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A>\-Methoden der <xref:System.Windows.Xps.XpsDocumentWriter>\-Klasse und Zuweisen eines XpsDrv\-fremden Druckers als Zieldruckerwarteschlange ebenfalls Ausgaben an den [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-Druckpfad vornehmen.  
  
 Für Anwendungen, die keine [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Funktion oder \-Unterstützung benötigen, bleibt der aktuelle [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-Druckpfad unverändert.  
  
-   Ergänzendes Referenzmaterial zum [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-Druckpfad und den verschiedenen [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Konvertierungsoptionen finden Sie unter [Microsoft XPS Document Converter\-Druckerescape](_win32_MXDC_ESCAPE) und "XPSDrv" im [Windows\-Treiberentwicklungskit](http://msdn.microsoft.com/library/default.asp?url=/library/dnanchor/html/DeviceDriver.asp).  
  
<a name="XPS_Driver_Model_intro"></a>   
## XPSDrv\-Treibermodell  
 Der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad verbessert die Effizienz des Spoolings durch Verwendung von [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] als systemeigenem Druckerspoolerformat beim Drucken auf [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-fähigen Druckern oder Treibern.  Das vereinfachte Spooling beseitigt die Notwendigkeit, vor dem Spoolen des Dokuments eine temporäre Spoolingdatei, wie etwa eine [!INCLUDE[TLA2#tla_emf](../../../../includes/tla2sharptla-emf-md.md)]\-Datendatei, zu generieren.  Durch geringere Größe der Spooldateien kann der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckpfad den Netzwerkverkehr verringern und die Druckleistung verbessern.  
  
 [!INCLUDE[TLA2#tla_emf](../../../../includes/tla2sharptla-emf-md.md)] ist ein geschlossenes Format, das Anwendungsausgaben als Abfolge von Aufrufen an [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] für Renderdienste darstellt.  Im Gegensatz zu [!INCLUDE[TLA2#tla_emf](../../../../includes/tla2sharptla-emf-md.md)] stellt das [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Spoolingformat das tatsächliche Dokument dar, ohne bei der Ausgabe an einen [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-basierten Druckertreiber \(XPSDrv\) weitere Interpretation zu erfordern.  Die Treiber können direkt mit den Daten im vorliegenden Format arbeiten.  Durch diese Fähigkeit entfallen die Daten\- und Farbraumkonvertierungen, die bei der Verwendung von [!INCLUDE[TLA2#tla_emf](../../../../includes/tla2sharptla-emf-md.md)]\-Dateien und [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\-basierten Druckertreibern erforderlich sind.  
  
 Normalerweise verringert sich die Größe von Spooldateien, wenn [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokumente verwendet werden, die einen [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Druckertreiber \(XPSDrv\) zum Ziel haben, gegenüber ihren [!INCLUDE[TLA2#tla_emf](../../../../includes/tla2sharptla-emf-md.md)]\-Entsprechungen; allerdings gibt es Ausnahmen:  
  
-   Eine Vektorgrafik, die sehr komplex ist, viele Ebenen aufweist oder ineffizient geschrieben wurde, kann größer als die Bitmapversion der gleichen Grafik sein.  
  
-   Zum Zweck der Anzeige am Bildschirm werden in XPS\-Dateien Geräteschriftarten sowie computerbasierte Schriftarten eingebettet, während in GDI\-Spooldateien keine Geräteschriftarten eingebettet sind.  Beide Schriftarten sind jedoch in Teilmengen gegliedert \(siehe unten\), und Druckertreiber können die Geräteschriftarten vor der Übertragung der Datei an den Drucker entfernen.  
  
 Die Reduzierung der Spoolgröße erfolgt mithilfe mehrerer Mechanismen:  
  
-   **Unterklassen von Schriftarten**.  Nur Zeichen, die im Dokument verwendet werden, werden in der [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Datei gespeichert.  
  
-   **Erweiterte Grafikunterstützung**.  Durch die systemeigene Unterstützung von Transparenz und Farbverlaufsprimitiven wird die Rasterung von Inhalten im [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]\-Dokument vermieden.  
  
-   **Erkennung gemeinsamer Ressourcen**.  Ressourcen, die mehrfach verwendet werden \(wie etwa ein Bild, das ein Firmenlogo darstellt\) werden als freigegebene Ressourcen behandelt und nur einmal geladen.  
  
-   **ZIP\-Komprimierung**.  Alle [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)]\-Dokumente verwenden ZIP\-Komprimierung.  
  
## Siehe auch  
 <xref:System.Windows.Controls.PrintDialog>   
 <xref:System.Windows.Xps.XpsDocumentWriter>   
 <xref:System.Windows.Xps.Packaging.XpsDocument>   
 <xref:System.Printing.PrintTicket>   
 <xref:System.Printing.PrintCapabilities>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.PrintQueue>   
 [Gewusst wie\-Themen](../../../../docs/framework/wpf/advanced/printing-how-to-topics.md)   
 [Dokumente in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [XPS](http://www.microsoft.com/xps)   
 [Serialisierung und Speicherung von Dokumenten](../../../../docs/framework/wpf/advanced/document-serialization-and-storage.md)   
 [Microsoft XPS Document Converter\-Druckerescape](_win32_MXDC_ESCAPE)