---
title: "Gewusst wie: Anpassen der Hinzuf&#252;gung von Elementen mithilfe der BindingSource von Windows Forms | Microsoft Docs"
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
  - "Steuerelemente [Windows Forms], Erstellen von neuen Elementen"
  - "BindingSource-Komponente [Windows Forms], Anpassen des Hinzufügens von Elementen mit"
  - "Beispiele [Windows Forms], BindingSource-Komponente"
  - "BindingSource-Komponente [Windows Forms], Beispiele"
ms.assetid: 1aae11fc-6fb2-4cb9-b3d0-e0638fe77ef0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Gewusst wie: Anpassen der Hinzuf&#252;gung von Elementen mithilfe der BindingSource von Windows Forms
Wenn Sie eine <xref:System.Windows.Forms.BindingSource>\-Komponente zum Binden eines Windows Forms\-Steuerelements an eine Datenquelle verwenden, kann es ggf. erforderlich sein, die Erstellung neuer Elemente anzupassen. Die <xref:System.Windows.Forms.BindingSource>\-Komponente vereinfacht dies durch die Bereitstellung des <xref:System.Windows.Forms.BindingSource.AddingNew>\-Ereignisses, das in der Regel ausgelöst wird, wenn das gebundene Steuerelement ein neues Element erstellen muss. Ihr Ereignishandler kann jedes erforderliche benutzerdefinierte Verhalten \(z. B. das Aufrufen einer Methode für einen Webdienst oder das Abrufen eines neuen Objekts aus einer Klassenfactory\) bereitstellen.  
  
> [!NOTE]
>  Wenn ein Element durch Verarbeiten des <xref:System.Windows.Forms.BindingSource.AddingNew>\-Ereignisses hinzugefügt wird, kann die Hinzufügung nicht abgebrochen werden.  
  
## Beispiel  
 Das folgende Beispiel zeigt, wie ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement mithilfe einer <xref:System.Windows.Forms.BindingSource>\-Komponente an eine Klassenfactory gebunden wird. Wenn der Benutzer auf die neue Zeile des <xref:System.Windows.Forms.DataGridView>\-Steuerelements klickt, wird das <xref:System.Windows.Forms.BindingSource.AddingNew>\-Ereignis ausgelöst. Der Ereignishandler erstellt ein neues `DemoCustomer`\-Objekt, das der Eigenschaft <xref:System.ComponentModel.AddingNewEventArgs.NewObject%2A?displayProperty=fullName> zugewiesen wird. Dies bewirkt, dass das neue `DemoCustomer`\-Objekt der Liste der <xref:System.Windows.Forms.BindingSource>\-Komponente hinzugefügt und in der neuen Zeile des <xref:System.Windows.Forms.DataGridView>\-Steuerelements angezeigt wird.  
  
 [!code-cpp[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/VB/form1.vb#1)]  
  
## Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Verweise auf die Assemblys "System", "System.Data", "System.Drawing" und "System.Windows.Forms".  
  
 Informationen zum Erstellen dieses Beispiels für [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] oder [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] auf der Befehlszeile finden Sie unter [Erstellen von der Befehlszeile aus](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) oder [Erstellen über die Befehlszeile mit csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Sie können dieses Beispiel auch in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] erstellen, indem Sie den Code in ein neues Projekt einfügen.  Siehe auch [Gewusst wie: Kompilieren und Ausführen eines vollständigen Windows Forms\-Codebeispiels mit Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Siehe auch  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [BindingSource\-Komponente](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Gewusst wie: Binden eines Windows Forms\-Steuerelements an einen Typ](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)