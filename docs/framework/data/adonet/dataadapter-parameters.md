---
title: "&#39;DataAdapter&#39;-Parameter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# &#39;DataAdapter&#39;-Parameter
Der <xref:System.Data.Common.DbDataAdapter> verfügt über vier Eigenschaften, die zum Abrufen von Daten aus einer Datenquelle und zum Aktualisieren der Daten in der Datenquelle verwendet werden: die <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A>\-Eigenschaft gibt die Daten aus der Datenquelle zurück, und die Eigenschaften <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> und <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> dienen zum Verwalten von Änderungen in der Datenquelle.  Die `SelectCommand`\-Eigenschaft muss vor dem Aufrufen der `Fill`\-Methode des `DataAdapter` festgelegt werden.  Die Eigenschaft `InsertCommand`, `UpdateCommand` oder `DeleteCommand` \(abhängig von der Art der Änderungen in der <xref:System.Data.DataTable>\) muss vor dem Aufruf der `Update`\-Methode des `DataAdapter` festgelegt werden.  Wenn beispielsweise Zeilen hinzugefügt wurden, muss vor dem Aufrufen von `Update` das `InsertCommand` festgelegt werden.  Wenn `Update` eine eingefügte, aktualisierte oder gelöschte Zeile verarbeitet, verwendet der `DataAdapter` die entsprechende `Command`\-Eigenschaft, um die Aktion zu verarbeiten.  Aktuelle Informationen zur geänderten Zeile werden über die `Parameters`\-Auflistung an das `Command`\-Objekt übergeben.  
  
 Rufen Sie zum Aktualisieren einer Zeile in der Datenquelle die UPDATE\-Anweisung auf, die mit einem eindeutigen Bezeichner die Zeile in der Tabelle identifiziert, die aktualisiert werden soll.  Der eindeutige Bezeichner ist im Allgemeinen der Wert eines Primärschlüsselfelds.  Die UPDATE\-Anweisung verwendet Parameter, die sowohl den eindeutigen Bezeichner als auch die Spalten und Werte enthalten, die aktualisiert werden sollen, wie in der folgenden Transact\-SQL\-Anweisung dargestellt.  
  
```  
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
>  Die Syntax für Parameterplatzhalter ist abhängig von der jeweiligen Datenquelle.  Dieses Beispiel zeigt Platzhalter für eine SQL Server\-Datenquelle.  Verwenden Sie Fragezeichenplatzhalter \(?\) für <xref:System.Data.OleDb>\-Parameter und <xref:System.Data.Odbc>\-Parameter.  
  
 In diesem [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\-Beispiel wird das `CompanyName`\-Feld mit dem Wert des `@CompanyName`\-Parameters für die Zeile aktualisiert, in der `CustomerID` dem Wert des `@CustomerID```\-Parameters entspricht.  Die Parameter rufen mithilfe der <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A>\-Eigenschaft des <xref:System.Data.SqlClient.SqlParameter>\-Objekts Informationen aus der geänderten Zeile ab.  Im Folgenden finden Sie die Parameter für das vorherige Beispiel einer UPDATE\-Anweisung.  Der Code geht davon aus, dass die `adapter`\-Variable für ein gültiges <xref:System.Data.SqlClient.SqlDataAdapter>\-Objekt steht.  
  
```  
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 Die `Add`\-Methode der `Parameters`\-Auflistung nimmt den Namen des Parameters, den Datentyp, die Größe \(wenn für den Typ zutreffend\) und den Namen der <xref:System.Data.Common.DbParameter.SourceColumn%2A> aus der `DataTable` an.  Beachten Sie, dass der <xref:System.Data.Common.DbParameter.SourceVersion%2A>\-Wert des `@CustomerID`\-Parameters `Original` lautet.  Dadurch wird sichergestellt, dass die vorhandene Zeile in der Datenquelle aktualisiert wird, wenn sich der Wert der ID\-Spalte oder \-Spalten in der geänderten <xref:System.Data.DataRow> geändert hat.  In diesem Fall stimmt der `Original`\-Zeilenwert mit dem aktuellen Wert in der Datenquelle überein, und der `Current`\-Zeilenwert enthält den aktualisierten Wert.  Die `SourceVersion` für den `@CompanyName`\-Parameter ist nicht festgelegt, und es wird der Standardwert, nämlich der `Current`\-Zeilenwert, verwendet.  
  
> [!NOTE]
>  Sowohl bei den `Fill`\-Vorgängen des `DataAdapter` als auch bei den `Get`\-Methoden des `DataReader` wird der [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]\-Typ von dem Typ hergeleitet, der vom [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]\-Datenanbieter zurückgegeben wird.  Die hergeleiteten [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]\-Typen und Accessormethoden für Datentypen von Microsoft SQL Server, OLE DB und ODBC werden in [Datentypzuordnungen in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md) erläutert.  
  
## Parameter.SourceColumn, Parameter.SourceVersion  
 Die `SourceColumn` und die `SourceVersion` können als Argumente an den `Parameter`\-Konstruktor übergeben oder als Eigenschaften eines vorhandenen `Parameter` festgelegt werden.  Die `SourceColumn` ist der Name der <xref:System.Data.DataColumn> aus der <xref:System.Data.DataRow>, aus der der Wert des `Parameter` abgerufen wird.  Die `SourceVersion` gibt die `DataRow`\-Version an, die der `DataAdapter` zum Abrufen des Werts verwendet.  
  
 Die folgende Tabelle zeigt die <xref:System.Data.DataRowVersion>\-Enumerationswerte an, die für die Verwendung mit `SourceVersion` zur Verfügung stehen.  
  
|DataRowVersion\-Enumeration|Beschreibung|  
|---------------------------------|------------------|  
|`Current`|Der Parameter verwendet den aktuellen Wert der Spalte.  Dies ist die Standardeinstellung.|  
|`Default`|Der Parameter verwendet den `DefaultValue` der Spalte.|  
|`Original`|Der Parameter verwendet den ursprünglichen Wert der Spalte.|  
|`Proposed`|Der Parameter verwendet einen vorgeschlagenen Wert.|  
  
 Das `SqlClient`\-Codebeispiel im nächsten Abschnitt definiert einen Parameter für einen <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>, bei dem die `CustomerID`\-Spalte als `SourceColumn` für die folgenden beiden Parameter verwendet wird: `@CustomerID` \(`SET CustomerID = @CustomerID`\) und `@OldCustomerID` \(`WHERE CustomerID = @OldCustomerID`\).  Der `@CustomerID`\-Parameter wird zum Aktualisieren der **CustomerID**\-Spalte auf den aktuellen Wert in der `DataRow` verwendet.  Daraufhin wird die `CustomerID`\-`SourceColumn` mit einer `SourceVersion` von `Current` verwendet.  Der *@OldCustomerID*\-Parameter wird dazu verwendet, die aktuelle Zeile in der Datenquelle anzugeben.  Da sich der passende Spaltenwert in der `Original`\-Version der Zeile befindet, wird die gleiche `SourceColumn` \(`CustomerID`\) mit einer `SourceVersion` von `Original` verwendet.  
  
## Verwenden von "SqlClient"\-Parametern  
 Im folgenden Beispiel wird gezeigt, wie Sie einen <xref:System.Data.SqlClient.SqlDataAdapter> erstellen und für die <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> <xref:System.Data.MissingSchemaAction> festlegen können, um zusätzliche Schemainformationen aus der Datenbank abzurufen.  Die Eigenschaften <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> und <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> werden festgelegt, und die zugehörigen <xref:System.Data.SqlClient.SqlParameter>\-Objekte werden der <xref:System.Data.SqlClient.SqlCommand.Parameters%2A>\-Auflistung hinzugefügt.  Die Methode gibt ein `SqlDataAdapter`\-Objekt zurück.  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## "OleDb"\-Parameterplatzhalter  
 Für das <xref:System.Data.OleDb.OleDbDataAdapter>\-Objekt und das <xref:System.Data.Odbc.OdbcDataAdapter>\-Objekt müssen zum Identifizieren der Parameter Fragezeichenplatzhalter \(?\) verwendet werden.  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 Die parametrisierten Abfrageanweisungen definieren, welche Eingabe\- und Ausgabeparameter erstellt werden müssen.  Verwenden Sie zum Erstellen eines Parameters die `Parameters.Add`\-Methode oder den `Parameter`\-Konstruktor, um den Spaltennamen, den Datentyp und die Größe anzugeben.  Für systeminterne Datentypen, wie `Integer`, muss die Größe nicht angegeben werden. Sie können auch die Standardgröße angeben.  
  
 Das folgende Codebeispiel erstellt die Parameter für eine SQL\-Anweisung und füllt dann ein `DataSet`.  
  
## OLE DB\-Beispiel  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## ODBC\-Parameter  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  Wenn für einen Parameter kein Parametername angegeben ist, erhält der Parameter einen Standardnamen der Form "Parameter*N*". Der erste Parameter heißt damit "Parameter1", der zweite "Parameter2" usw.  Allerdings wird davon abgeraten, die Benennungskonvention "Parameter*N*" zu verwenden, wenn Sie einen Parameternamen bereitstellen, da der so bereitgestellte Name möglicherweise mit dem Standardparameternamen in der `ParameterCollection` in Konflikt geraten kann.  Wenn der angegebene Name bereits vorhanden ist, wird eine Ausnahme ausgelöst.  
  
## Siehe auch  
 [DataAdapter und DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Befehle und Parameter](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Aktualisieren von Datenquellen mit DataAdapters](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Ändern von Daten mit gespeicherten Prozeduren](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [Datentypzuordnungen in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)