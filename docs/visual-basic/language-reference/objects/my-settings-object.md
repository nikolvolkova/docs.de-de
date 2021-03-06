---
title: My.Settings-Objekt | Microsoft-Dokumentation
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.MySettingsProperty.Settings
- My.Settings
dev_langs:
- VB
helpviewer_keywords:
- My.Settings object
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d48d3556f55ef286e2f501e2df5bf5035d3aff90
ms.lasthandoff: 03/13/2017

---
# <a name="mysettings-object"></a>My.Settings-Objekt
Stellt Eigenschaften und Methoden für den Zugriff auf die Einstellungen der Anwendung.  
  
## <a name="remarks"></a>Hinweise  
 Das `My.Settings` -Objekt bietet Zugriff auf die Einstellungen der Anwendung und ermöglicht es Ihnen, dynamisch speichern und Abrufen von Eigenschaften und andere Informationen für Ihre Anwendung. Weitere Informationen finden Sie unter [Verwalten von Einstellungen (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet).  
  
## <a name="properties"></a>Eigenschaften  
 Die Eigenschaften der `My.Settings` Objekt ermöglichen den Zugriff auf die Einstellungen Ihrer Anwendung. Verwenden Sie zum Hinzufügen oder entfernen Sie die Einstellungen, die **Einstellungs-Designer**.  
  
 Jede Einstellung hat eine **Namen**, **Typ**, **Bereich**, und **Wert**, und diese Einstellungen bestimmen, wie diese Eigenschaft auf jede Einstellung in wird die `My.Settings` Objekt:  
  
-   **Namen** bestimmt den Namen der Eigenschaft.  
  
-   **Typ** bestimmt den Typ der Eigenschaft.  
  
-   **Bereich** gibt an, ob die Eigenschaft schreibgeschützt ist. Wenn der Wert **Anwendung**, die Eigenschaft ist schreibgeschützt, wenn der Wert **Benutzer**, die Eigenschaft ist schreibgeschützt.  
  
-   **Wert** ist der Standardwert der Eigenschaft.  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|---|---|  
|`Reload`|Lädt die Einstellungen aus der zuletzt gespeicherten Werte.|  
|`Save`|Speichert die aktuellen Einstellungen.|  
  
 Die `My.Settings` Objekt stellt auch erweiterte Eigenschaften und Methoden, die von der <xref:System.Configuration.ApplicationSettingsBase>Klasse</xref:System.Configuration.ApplicationSettingsBase> geerbt  
  
## <a name="tasks"></a>Aufgaben  
 Die folgende Tabelle enthält Beispiele für Aufgaben mit der `My.Settings` Objekt.  
  
|Beschreibung|Siehe|  
|---|---|  
|Lesen Sie eine anwendungseinstellung|[Gewusst wie: Lesen von Anwendungseinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|Ändern einer benutzereinstellung|[Gewusst wie: Ändern von Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|Beibehalten von benutzereinstellungen|[Gewusst wie: Beibehalten von Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|Erstellen Sie ein Eigenschaftenraster für benutzereinstellungen|[Gewusst wie: Erstellen von Eigenschaftenrastern für Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)|  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird der Wert der `Nickname` Einstellung.  
  
 [!code-vb[VbVbalrMyResources&14;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-settings-object_1.vb)]  
  
 Für dieses Beispiel funktioniert, müssen die Anwendung eine `Nickname` -Einstellung vom Typ `String`.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Configuration.ApplicationSettingsBase></xref:System.Configuration.ApplicationSettingsBase>   
 [Gewusst wie: Lesen von Anwendungseinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [Gewusst wie: Ändern von Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [Gewusst wie: Beibehalten von Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [Gewusst wie: Erstellen von Eigenschaftenrastern für Benutzereinstellungen in Visual Basic](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [Verwalten von Anwendungseinstellungen (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)
