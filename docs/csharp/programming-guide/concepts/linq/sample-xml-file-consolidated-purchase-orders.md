---
title: 'Beispiel-XML-Datei: Konsolidierte Bestellungen2'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9d9698a5-95f2-4564-813b-ba536cdf3bfb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 81699b266e67c006a707a3941349a41189a3b442
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="sample-xml-file-consolidated-purchase-orders"></a>Beispiel-XML-Datei: Konsolidierte Bestellungen
Die folgende XML-Datei wird in verschiedenen Beispielen in der [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]-Dokumentation verwendet. Diese Datei besteht aus einem Satz von unterschiedlich geformten Aufträgen verschiedener Unternehmen. Für die Aufträge eines Unternehmens gibt es jeweils einen eigenen Namespace.  
  
## <a name="consolidatedpurchaseordersxml"></a>ConsolidatedPurchaseOrders.xml  
  
```xml  
<?xml version="1.0"?>  
<PurchaseOrders xmlns="www.contoso.com">  
  <PurchaseOrder  
      PurchaseOrderNumber="99503"  
      OrderDate="1999-10-20">  
    <Address Type="Shipping">  
      <Name>Ellen Adams</Name>  
      <Street>123 Maple Street</Street>  
      <City>Mill Valley</City>  
      <State>CA</State>  
      <Zip>10999</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Tai Yee</Name>  
      <Street>8 Oak Avenue</Street>  
      <City>Old Town</City>  
      <State>PA</State>  
      <Zip>95819</Zip>  
      <Country>USA</Country>  
    </Address>  
    <DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>  
    <Items>  
      <Item PartNumber="872-AA">  
        <ProductName>Lawnmower</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>148.95</USPrice>  
        <Comment>Confirm this is electric</Comment>  
      </Item>  
      <Item PartNumber="926-AA">  
        <ProductName>Baby Monitor</ProductName>  
        <Quantity>2</Quantity>  
        <USPrice>39.98</USPrice>  
        <ShipDate>1999-05-21</ShipDate>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
  <PurchaseOrder PurchaseOrderNumber="99505" OrderDate="1999-10-22">  
    <Address Type="Shipping">  
      <Name>Cristian Osorio</Name>  
      <Street>456 Main Street</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Cristian Osorio</Name>  
      <Street>456 Main Street</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <DeliveryNotes>Please notify by email before shipping.</DeliveryNotes>  
    <Items>  
      <Item PartNumber="456-NM">  
        <ProductName>Power Supply</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>45.99</USPrice>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
  <PurchaseOrder PurchaseOrderNumber="99504" OrderDate="1999-10-22">  
    <Address Type="Shipping">  
      <Name>Jessica Arnold</Name>  
      <Street>4055 Madison Ave</Street>  
      <City>Seattle</City>  
      <State>WA</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Jessica Arnold</Name>  
      <Street>4055 Madison Ave</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <DeliveryNotes>Please do not deliver on Saturday.</DeliveryNotes>  
    <Items>  
      <Item PartNumber="898-AZ">  
        <ProductName>Computer Keyboard</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>29.99</USPrice>  
      </Item>  
      <Item PartNumber="898-AM">  
        <ProductName>Wireless Mouse</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>14.99</USPrice>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
  <aw:PurchaseOrder  
    PONumber="11223"  
    Date="2000-01-15"  
    xmlns:aw="http://www.adventure-works.com">  
    <aw:ShippingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:ShippingAddress>  
    <aw:BillingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:BillingAddress>  
    <aw:DeliveryInstructions>Ship only complete order.</aw:DeliveryInstructions>  
    <aw:Item PartNum="LIT-01">  
      <aw:ProductID>Litware Networking Card</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>20.99</aw:Price>  
    </aw:Item>  
    <aw:Item PartNum="LIT-25">  
      <aw:ProductID>Litware 17in LCD Monitor</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>199.99</aw:Price>  
    </aw:Item>  
  </aw:PurchaseOrder>  
</PurchaseOrders>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Beispieldokumente (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)

