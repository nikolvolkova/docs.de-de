---
title: "ToolBar-Steuerelement (Windows&#160;Forms) | Microsoft Docs"
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
  - "ToolBar-Steuerelement [Windows Forms]"
  - "Symbolleisten [Windows Forms]"
ms.assetid: 6b40e9ce-6a7a-4784-bfc9-7f1d36b7462e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# ToolBar-Steuerelement (Windows&#160;Forms)
> [!NOTE]
>  Obwohl das <xref:System.Windows.Forms.ToolStrip>\-Steuerelement das `ToolBar`\-Steuerelement ersetzt und funktionell erweitert, wird das `ToolBar`\-Steuerelement sowohl aus Gründen der Abwärtskompatibilität als auch, falls gewünscht, für die zukünftige Verwendung beibehalten.  
  
 Das `ToolBar`\-Steuerelement von Windows Forms wird in Formularen als eine Steuerleiste verwendet, auf der eine Zeile aus Dropdownmenüs und Bitmapschaltflächen angezeigt wird, die Befehle aktivieren.  Daher ist ein Klicken auf eine Symbolleistenschaltfläche mit dem Auswählen eines Menübefehls identisch.  Die Schaltflächen können so konfiguriert werden, dass sie so angezeigt werden und sich so verhalten wie Schaltflächen, Dropdownmenüs oder Trennzeichen.  In der Regel enthält eine Symbolleiste Schaltflächen und Menüs, die Elementen in der Menüstruktur einer Anwendung entsprechen. Dadurch wird schneller Zugriff auf die am häufigsten verwendeten Funktionen und Befehle einer Anwendung ermöglicht.  
  
> [!NOTE]
>  Die <xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A>\-Eigenschaft des `ToolBar`\-Steuerelements übernimmt eine Instanz der <xref:System.Windows.Forms.ContextMenu>\-Klasse als Verweis.  Wenn Sie diese Art von Schaltfläche auf einer Symbolleiste in Ihrer Anwendung implementieren, sollten Sie sorgfältig auf den Verweis achten, den Sie übergeben, denn die Eigenschaft akzeptiert jedes Objekt, das von der <xref:System.Windows.Forms.Menu>\-Klasse erbt.  
  
## In diesem Abschnitt  
 [Übersicht über das ToolBar\-Steuerelement](../../../../docs/framework/winforms/controls/toolbar-control-overview-windows-forms.md)  
 Stellt die allgemeinen Konzepte des `ToolBar`\-Steuerelements vor, mit dem Sie benutzerdefinierte Symbolleisten entwerfen können, mit denen Benutzer arbeiten können.  
  
 [Gewusst wie: Hinzufügen von Schaltflächen zu einem ToolBar\-Steuerelement](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)  
 Beschreibt, wie ein `ToolBar`\-Steuerelement hinzugefügt wird.  
  
 [Gewusst wie: Definieren eines Symbols für eine Symbolleisten\-Schaltfläche](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)  
 Beschreibt, wie Symbole auf den Schaltflächen eines `ToolBar`\-Steuerelements angezeigt werden.  
  
 [Gewusst wie: Auslösen von Menüereignissen für Symbolleisten\-Schaltflächen](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)  
 Bietet Anweisungen zum Schreiben von Code, in dem interpretiert wird, auf welche Schaltfläche ein Benutzer in einem `ToolBar`\-Steuerelement geklickt hat.  
  
 Siehe auch [Gewusst wie: Definieren eines Symbols für eine Symbolleisten\-Schaltfläche mithilfe des Designers](http://msdn.microsoft.com/library/ms233659%20\(v=vs.110\)), [Gewusst wie: Hinzufügen von Schaltflächen zu einem ToolBar\-Steuerelement mithilfe des Designers](http://msdn.microsoft.com/library/ms233650%20\(v=vs.110\)).  
  
## Referenz  
 <xref:System.Windows.Forms.ToolBar>\-Klasse  
 Enthält Referenzinformationen zur Klasse und zu ihren Membern.  
  
## Verwandte Abschnitte  
 [Steuerelemente für Windows Forms](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)  
 Enthält eine vollständige Liste der Windows Forms\-Steuerelemente mit Links zu Informationen zur jeweiligen Verwendung.  
  
 [ToolStrip\-Steuerelement](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)  
 Beschreibt Symbolleisten, die Menüs, Steuerelemente und Benutzersteuerelemente in Windows Forms\-Anwendungen enthalten können.