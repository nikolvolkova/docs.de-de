---
title: "Gewusst wie: Programmgesteuertes Anpassen der Zellengr&#246;&#223;e an den Inhalt im DataGridView-Steuerelement von Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Zellen, Anpassen der Größe an Inhalt"
  - "Datenblätter, Anpassen der Größe von Zellen an Inhalt"
  - "DataGridView-Steuerelement [Windows Forms], Größenänderung von Zellen"
  - "Raster, Anpassen der Größe von Zellen an Inhalt"
ms.assetid: 63d770dc-b3f5-462b-901a-3125b2753792
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Gewusst wie: Programmgesteuertes Anpassen der Zellengr&#246;&#223;e an den Inhalt im DataGridView-Steuerelement von Windows Forms
Sie können die <xref:System.Windows.Forms.DataGridView>\-Steuerelementmethoden verwenden, um die Größen von Zeilen, Spalten und Headern zu ändern, sodass die darin enthaltenen Werte ungekürzt angezeigt werden.  Mit diesen Methoden können Sie die Größen der <xref:System.Windows.Forms.DataGridView>\-Elemente zu von Ihnen gewählten Zeitpunkten ändern.  Alternativ können Sie das Steuerelement so konfigurieren, dass diese Elemente automatisch angepasst werden, sobald sich der Inhalt ändert.  Dies kann jedoch ineffizient sein, wenn Sie mit großen Datenmengen arbeiten oder wenn sich Ihre Daten häufig ändern.  Weitere Informationen finden Sie unter [Größenänderungsoptionen im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md).  
  
 In der Regel passen Sie <xref:System.Windows.Forms.DataGridView>\-Elemente nur dann programmgesteuert an ihren Inhalt an, wenn Sie neue Daten aus einer Datenquelle laden oder der Benutzer einen Wert bearbeitet hat.  Dies ist nützlich, um die Leistung zu optimieren, ist aber auch nützlich, wenn Sie Ihren Benutzern ermöglichen möchten, die Größen von Zeilen und Spalten manuell mit der Maus ändern zu können.  
  
 Im folgenden Codebeispiel werden die Optionen veranschaulicht, die zur programmgesteuerten Größenanpassung verfügbar sind.  
  
## Beispiel  
 [!code-cpp[System.Windows.Forms.DataGridView.ProgrammaticResizing#0](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.ProgrammaticResizing/CPP/programmaticsizing.cpp#0)]
 [!code-csharp[System.Windows.Forms.DataGridView.ProgrammaticResizing#0](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.ProgrammaticResizing/CS/programmaticsizing.cs#0)]
 [!code-vb[System.Windows.Forms.DataGridView.ProgrammaticResizing#0](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.ProgrammaticResizing/VB/programmaticsizing.vb#0)]  
  
## Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Verweise auf die Assemblys "System", "System.Drawing" und "System.Windows.Forms".  
  
 Informationen zum Erstellen dieses Beispiels über die Befehlszeile für [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] oder [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] finden Sie unter [Erstellen von der Befehlszeile aus](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) oder [Erstellen über die Befehlszeile mit csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  Sie können dieses Beispiel auch in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] erstellen, indem Sie den Code in ein neues Projekt einfügen.  Siehe auch [Gewusst wie: Kompilieren und Ausführen eines vollständigen Windows Forms\-Codebeispiels mit Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Siehe auch  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>   
 <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>   
 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>   
 [Größenanpassung bei Spalten und Zeilen im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)   
 [Größenänderungsoptionen im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)   
 [Gewusst wie: Automatisches Anpassen der Zellengröße bei Änderungen des Inhalts im DataGridView\-Steuerelement von Windows Forms](../../../../docs/framework/winforms/controls/automatically-resize-cells-when-content-changes-in-the-datagrid.md)