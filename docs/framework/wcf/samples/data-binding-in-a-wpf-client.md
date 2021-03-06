---
title: "Datenbindung in einem Windows Presentation Foundation-Client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb8c8293-5973-4aef-9b07-afeff5d3293c
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Datenbindung in einem Windows Presentation Foundation-Client
In diesem Beispiel wird die Verwendung der Datenbindung in einem Windows Presentation Foundation \(WPF\)\-Client veranschaulicht.  Im Beispiel wird ein [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienst verwendet, der zufällig ein Array von Alben generiert, die an den Client zurückgegeben werden.  Jedes Album hat einen Namen, einen Preis und eine Liste von Albumtiteln.  Die Albumtitel haben einen Namen und eine Dauer.  Die vom Dienst zurückgegebenen Informationen werden automatisch an die vom [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)]\-Client bereitgestellte Benutzeroberfläche gebunden.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Durch die Datenbindung kann eine Datenquelle automatisch an eine Benutzeroberfläche gebunden werden.  Dadurch wird das Programmiermodell vereinfacht, da Sie nicht jedes Element der Benutzeroberfläche programmgesteuert mit den Daten aus einem Datenobjekt oder einem Array von Datenobjekten aktualisieren müssen.  Sie können ein Objekt an ein Benutzeroberflächenelement oder ein Array an ein Steuerelement mit mehreren Eingaben binden, beispielsweise `ListBox`.  Im folgenden Codebeispiel wird das Binden von Daten an den `DataContext` eines Benutzeroberflächenelements veranschaulicht.  
  
```  
// Event handler executed when call is complete  
void client_GetAlbumListCompleted(object sender, GetAlbumListCompletedEventArgs e)  
{  
    // This is on the UI thread, myPanel can be accessed directly  
    myPanel.DataContext = e.Result;   
}  
  
```  
  
 Im obigen Beispiel wird der `DataContext` für das `grid`\-Layoutelement `myPanel` auf die von der `GetAlbumList`\-Methode zurückgegebenen Daten festgelegt.  Durch den `DataContext` können Elemente Informationen zu der für die Bindung verwendete Datenquelle sowie andere Merkmale der Bindung \(beispielsweise den Pfad\) von den übergeordneten Elementen erben.  Die Codezeile muss jedes Mal ausgeführt werden, wenn die Daten auf dem Server aktualisiert werden.  Sie wird beispielsweise ausgeführt, wenn das Fenster initialisiert wird und wenn ein neues Album hinzugefügt wird.  
  
 Im folgenden XAML\-Beispielcode wird `ItemsSource="{Binding }"` von `ListBox` angegeben.  
  
```  
<ListBox   
          ItemTemplate="{StaticResource AlbumStyle}"  
          ItemsSource="{Binding }"   
          IsSynchronizedWithCurrentItem="true" />  
  
```  
  
 Dies gibt an, dass die an das Benutzeroberflächenelement der obersten Ebene gebundenen Daten auch an dieses Steuerelement gebunden werden \(d.&\#160;h. an das Array von Alben\).  Außerdem gibt `ItemTemplate="{StaticResource AlbumStyle}"` die Datenvorlage an, die in `ListBox` für jedes Element verwendet werden soll.  Sie können auch Datenvorlagen definieren, um anzugeben, wie die Daten formatiert werden sollen.  Diese Datenvorlagen können für andere Benutzeroberflächenelemente in der Anwendung wiederverwendet werden. Der Vorteil liegt darin, dass die Datenvorlage an einem Ort definiert und verwaltet wird.  
  
 Die `AlbumStyle`\-Datenvorlage definiert ein Raster mit zwei nebeneinanderliegenden `TextBlock`s.  In einem wird der Name des Albums angegeben, im anderen die Anzahl der Titel auf dem Album.  
  
```  
<DataTemplate x:Key="AlbumStyle">  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="260" />  
            <ColumnDefinition Width="60" />  
        </Grid.ColumnDefinitions>  
        <TextBlock Grid.Column="0" TextContent="{Binding Path=Title}" />  
        <TextBlock Grid.Column="1" TextContent="{Binding Path=Tracks#.Count}" HorizontalAlignment="Right" />  
    </Grid>  
</DataTemplate>  
  
```  
  
 Mit dem folgenden XAML\-Code wird eine zweite `ListBox` erstellt.  
  
```  
<ListBox Grid.Row="2"   
            Grid.ColumnSpan="2"   
            ItemTemplate="{StaticResource TrackStyle}"  
            ItemsSource="{Binding Path=Tracks}" />  
  
```  
  
 Im Code wird ein Pfad für `ItemsSource` angegeben.  Damit wird angegeben, dass die an dieses Steuerelement gebundenen Daten keine Daten der obersten Ebene, sondern eine Eigenschaft der Daten der obersten Ebene namens `Tracks` sind.  Diese Eigenschaft stellt das Array der im Album enthaltenen Titel dar.  Außerdem wird eine weitere `DataTemplate` namens `TrackStyle` angegeben.  Das Layout der `TrackStyle`\-Vorlage entspricht weitgehend dem der `AlbumStyle`\-Vorlage, die `TextBlock`s sind jedoch an andere Eigenschaften gebunden.  Dies liegt daran, dass die beiden Vorlagen mit unterschiedlichen Datenobjekten verwendet werden.  
  
### So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Zum Erstellen der C\#\- oder Visual Basic .NET\-Edition der Projektmappe befolgen Sie die unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen.  
  
3.  Um das Beispiel in einer Konfiguration mit einem Computer oder computerübergreifend auszuführen, befolgen Sie die Anweisungen unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.  Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.  Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WPFDataBinding`  
  
## Siehe auch