---
title: "&#220;bersicht &#252;ber die BindingSource-Komponente | Microsoft Docs"
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
  - "BindingSource-Komponente [Windows Forms], Informationen über die BindingSource-Komponente"
  - "Steuerelemente [Windows Forms], Binden an Daten"
  - "Datenbindung, BindingSource-Komponente"
  - "Windows Forms, Datenbindung"
ms.assetid: be838caf-fcb0-4b68-827f-58b2c04b747f
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# &#220;bersicht &#252;ber die BindingSource-Komponente
Die <xref:System.Windows.Forms.BindingSource>\-Komponente vereinfacht den Bindungsvorgang von Steuerelementen an eine zugrunde liegende Datenquelle.  Die <xref:System.Windows.Forms.BindingSource>\-Komponente fungiert als Kanal sowie als Datenquelle für andere Steuerelemente, an die eine Bindung erfolgen soll.  Sie stellt eine Abstraktion der Datenverbindung Ihres Formulars bereit, während Befehle an die zugrunde liegende Liste der Daten übergeben werden.  Außerdem können Sie Daten direkt hinzufügen. Die Komponente selbst fungiert daher als Datenquelle.  
  
## BindingSource\-Komponente als Zwischenelement  
 Die <xref:System.Windows.Forms.BindingSource>\-Komponente fungiert als Datenquelle für einige oder alle Steuerelemente im Formular.  In Visual Studio kann die <xref:System.Windows.Forms.BindingSource> mithilfe der Eigenschaft `DataBindings` an ein Steuerelement gebunden werden, auf die über das Fenster **Eigenschaften** zugegriffen werden kann.  Weitere Informationen finden Sie unter [Gewusst wie: Binden von Windows Forms\-Steuerelementen an die BindingSource\-Komponente mithilfe des Designers](../../../../docs/framework/winforms/controls/bind-wf-controls-with-the-bindingsource.md).  
  
 Sie können die <xref:System.Windows.Forms.BindingSource>\-Komponente an einfache Datenquellen \(etwa eine einzelne Eigenschaft eines Objekts oder eine Basisauflistung wie <xref:System.Collections.ArrayList>\) und komplexe Datenquellen \(etwa eine Datenbanktabelle\) binden.  Die <xref:System.Windows.Forms.BindingSource>\-Komponente fungiert als Zwischenelement, das Bindungs\- und Währungsverwaltungsdienste bereitstellt.  Sie können eine <xref:System.Windows.Forms.BindingSource>\-Komponente zur Entwurfszeit oder zur Laufzeit an eine komplexe Datenquelle durch Festlegen der Eigenschaften <xref:System.Windows.Forms.BindingSource.DataSource%2A> und <xref:System.Windows.Forms.BindingSource.DataMember%2A> an die Datenbank bzw. die Tabelle binden.  Die folgende Abbildung zeigt, wie sich die <xref:System.Windows.Forms.BindingSource>\-Komponente in die vorhandene Datenbindungsarchitektur einfügt.  
  
 ![Bindungsquelle und Datenbindungsarchitektur](../../../../docs/framework/winforms/controls/media/net-bindsrcdatabindarch.gif "NET\_BindSrcDataBindArch")  
  
> [!NOTE]
>  Zur Entwurfszeit erstellen einige Aktionen \(z. B. das Ziehen einer Datenbanktabelle aus einem Datenfenster in ein leeres Formular\) die <xref:System.Windows.Forms.BindingSource>\-Komponente, binden diese an die zugrunde liegenden Datenquelle und fügen datenkompatible Steuerelemente in einem Vorgang hinzu.  Siehe auch [Binden von Windows Forms\-Steuerelementen an Daten in Visual Studio](../Topic/Bind%20Windows%20Forms%20controls%20to%20data%20in%20Visual%20Studio.md).  
  
## BindingSource\-Komponente als Datenquelle  
 Wenn Sie damit beginnen, der <xref:System.Windows.Forms.BindingSource>\-Komponente Elemente hinzuzufügen, ohne zunächst eine Liste anzugeben, an die die Bindung erfolgen soll, agiert die Komponente wie eine Listendatenquelle und akzeptiert diese hinzugefügten Elemente.  
  
 Außerdem können Sie Code schreiben, um benutzerdefinierte "AddNew"\-Funktionalität mithilfe des Ereignisses <xref:System.Windows.Forms.BindingSource.AddingNew> bereitzustellen, das ausgelöst wird, wenn die Methode <xref:System.Windows.Forms.BindingSource.AddNew%2A> aufgerufen wird, bevor das Element der Liste hinzugefügt wird.  Weitere Informationen finden Sie unter [Architektur der BindingSource\-Komponente](../../../../docs/framework/winforms/controls/bindingsource-component-architecture.md).  
  
## Navigation  
 Für Benutzer, die in den Daten eines Formulars navigieren müssen, ermöglicht die <xref:System.Windows.Forms.BindingNavigator>\-Komponente das Navigieren und Bearbeiten von Daten in Kombination mit einer <xref:System.Windows.Forms.BindingSource>\-Komponente.  Weitere Informationen finden Sie unter [BindingNavigator\-Steuerelement](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md).  
  
## Datenbearbeitung  
 Die <xref:System.Windows.Forms.BindingSource> fungiert als ein <xref:System.Windows.Forms.CurrencyManager> für alle Bindungen und kann daher Zugriff auf Währungs\- und Positionsinformationen hinsichtlich der Datenquelle bereitstellen.  Die folgende Tabelle enthält die Elemente, die die <xref:System.Windows.Forms.BindingSource>\-Komponente für den Zugriff auf die und das Bearbeiten der zugrunde liegenden Daten bereitstellt.  
  
|Member|Beschreibung|  
|------------|------------------|  
|<xref:System.Windows.Forms.BindingSource.Current%2A>\-Eigenschaft|Ruft das aktuelle Element der Datenquelle ab.|  
|<xref:System.Windows.Forms.BindingSource.Position%2A>\-Eigenschaft|Ruft die aktuelle Position in der zugrunde liegenden Liste ab oder legt diese fest.|  
|<xref:System.Windows.Forms.BindingSource.List%2A>\-Eigenschaft|Ruft die Liste ab, die die Auswertung der Auswertung <xref:System.Windows.Forms.BindingSource.DataSource%2A> und <xref:System.Windows.Forms.BindingSource.DataMember%2A> darstellt.  Wenn <xref:System.Windows.Forms.BindingSource.DataMember%2A> nicht festgelegt ist, wird die durch <xref:System.Windows.Forms.BindingSource.DataSource%2A> angegebene Liste zurückgegeben.|  
|<xref:System.Windows.Forms.BindingSource.Insert%2A>\-Methode|Fügt ein Element am angegebenen Index in die Liste ein.|  
|<xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A>\-Methode|Entfernt das aktuelle Element aus der Liste.|  
|<xref:System.Windows.Forms.BindingSource.EndEdit%2A>\-Methode|Wendet anstehende Änderungen auf die zugrunde liegende Datenquelle an.|  
|<xref:System.Windows.Forms.BindingSource.CancelEdit%2A>\-Methode|Bricht den aktuellen Bearbeitungsvorgang ab.|  
|<xref:System.Windows.Forms.BindingSource.AddNew%2A>\-Methode|Fügt der zugrunde liegenden Liste ein neues Element hinzu.  Wenn die Datenquelle <xref:System.ComponentModel.IBindingList> implementiert und ein Element aus dem <xref:System.Windows.Forms.BindingSource.AddingNew>\-Ereignis zurückgibt, wird dieses Element hinzugefügt.  Andernfalls wird die Anforderung an die Methode <xref:System.ComponentModel.IBindingList.AddNew%2A> der Liste übergeben.  Wenn die zugrunde liegende Liste keine <xref:System.ComponentModel.IBindingList> ist, wird das Element automatisch über seinen öffentlichen Standardkonstruktor erstellt.|  
  
## Sortieren und Filtern  
 In der Regel sollten Sie mit einer sortierten oder gefilterten Sicht der Datenquelle arbeiten.  Die folgende Tabelle zeigt die Elemente, die die <xref:System.Windows.Forms.BindingSource>\-Komponentendatenquelle bereitstellt.  
  
|Member|Beschreibung|  
|------------|------------------|  
|<xref:System.Windows.Forms.BindingSource.Sort%2A>\-Eigenschaft|Wenn die Datenquelle eine <xref:System.ComponentModel.IBindingList> ist, wird ein Spaltenname abgerufen oder festgelegt, der für das Sortieren und für Informationen zur Sortierreihenfolge verwendet wird.  Wenn die Datenquelle eine <xref:System.ComponentModel.IBindingListView> ist und erweiterte Sortierung unterstützt, werden mehrere Spaltennamen abgerufen, die für das Sortieren und für Informationen zur Sortierreihenfolge verwendet werden.|  
|<xref:System.Windows.Forms.BindingSource.Filter%2A>\-Eigenschaft|Wenn die Datenquelle eine <xref:System.ComponentModel.IBindingListView> ist, wird der Ausdruck abgerufen, der zum Filtern der anzuzeigenden Zeilen verwendet wird, oder dieser Ausdruck wird festgelegt.|  
  
## Siehe auch  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.BindingNavigator>   
 [Architektur der BindingSource\-Komponente](../../../../docs/framework/winforms/controls/bindingsource-component-architecture.md)   
 [BindingSource\-Komponente](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [BindingNavigator\-Steuerelement](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)   
 [Datenbindung in Web Forms](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Steuerelemente für Windows Forms](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)