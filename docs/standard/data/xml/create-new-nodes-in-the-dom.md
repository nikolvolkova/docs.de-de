---
title: "Erstellen von neuen Knoten im Dokumentobjektmodell | Microsoft Docs"
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
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Erstellen von neuen Knoten im Dokumentobjektmodell
Die <xref:System.Xml.XmlDocument> hat eine Create-Methode für alle Knotentypen. Stellen Sie der Methode, falls erforderlich, einen Namen und Inhalt oder andere Parameter für die Knoten bereit, die Inhalt aufweisen (z. B. ein Textknoten), und der Knoten wird erstellt. Für die folgenden Methoden muss ein Name angegeben sein und es müssen einige andere Parameter ausgefüllt sein, damit ein entsprechender Knoten erstellt wird.  
  
-   <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 Für andere Knoten müssen über das Bereitstellen von Daten für Parameter hinausgehende Anforderungen erfüllt werden.  
  
 Weitere Informationen zu Attributen finden Sie unter [Erstellen von neuen Attributen für Elemente im DOM](../../../../docs/standard/data/xml/creating-new-attributes-for-elements-in-the-dom.md). Informationen zur Validierung von Element- und Attributnamen finden Sie unter [-XML-Element- und-Attributnamen beim Erstellen neuer Knoten](../../../../docs/standard/data/xml/xml-element-and-attribute-name-verification-when-creating-new-nodes.md). Zum Erstellen von Entitätsverweisen finden Sie unter [Erstellen neuer Entitätsverweise](../../../../docs/standard/data/xml/creating-new-entity-references.md). Informationen über die Auswirkungen von Namespaces auf die Erweiterung von Entitätsverweisen finden Sie unter [Namespace Auswirkung auf die Entitätsverweiserweiterung für neue Knoten mit Elementen und Attributen](../../../../docs/standard/data/xml/namespace-affect-on-entity-ref-expansion-for-new-nodes.md).  
  
 Nach dem Erstellen von neuen Knoten stehen verschiedene Methoden zum Einfügen der Knoten in die Struktur zur Verfügung. In der Tabelle sind die Methoden und eine Beschreibung der Position des neuen Knotens im XML-DOM (Dokumentobjektmodell) aufgelistet.  
  
|Methode|Knotenposition|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|Vor dem Referenzknoten eingefügt. So fügen Sie beispielsweise den neuen Knoten an Position 5 ein:<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> Weitere Informationen finden Sie unter der <xref:System.Xml.XmlNode.InsertBefore%2A> Methode.|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|Nach dem Referenzknoten eingefügt. Zum Beispiel:<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> Weitere Informationen finden Sie unter der <xref:System.Xml.XmlNode.InsertAfter%2A> Methode.|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|Fügt den Knoten am Ende der Liste der untergeordneten Knoten für den angegebenen Knoten an. Wenn der Knoten, der hinzugefügt wird ein <xref:System.Xml.XmlDocumentFragment>, den gesamten Inhalt des Dokumentfragments in die Liste untergeordneten Elemente dieses Knotens verschoben. Weitere Informationen finden Sie unter der <xref:System.Xml.XmlNode.AppendChild%2A> Methode.|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|Fügt den Knoten am Anfang der Liste der untergeordneten Knoten für den angegebenen Knoten an. Wenn der Knoten, der hinzugefügt wird ein <xref:System.Xml.XmlDocumentFragment>, den gesamten Inhalt des Dokumentfragments in die Liste untergeordneten Elemente dieses Knotens verschoben. Weitere Informationen finden Sie unter der <xref:System.Xml.XmlNode.PrependChild%2A> Methode.|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|Fügt ein <xref:System.Xml.XmlAttribute> Knoten am Ende der Auflistung ein Element zugeordnet. Weitere Informationen finden Sie unter der <xref:System.Xml.XmlAttributeCollection.Append%2A> Methode.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Dokumentobjektmodell (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)