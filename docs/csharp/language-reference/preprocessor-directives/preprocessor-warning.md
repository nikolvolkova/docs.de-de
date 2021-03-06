---
title: '#<a name="warning-c-reference"></a>warning (C#-Referenz)'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#warning'
dev_langs:
- CSharp
helpviewer_keywords:
- '#warning directive [C#]'
ms.assetid: e6fb496d-bb8b-4018-baf6-5b60a0c8902b
caps.latest.revision: 9
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8630101a90bd6d4ed2036b495b254c9475531dc0
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="warning-c-reference"></a>#warning (C#-Referenz)
Mit `#warning` können Sie von einem bestimmten Ort in Ihrem Code aus eine Warnung der Stufe 1 generieren. Zum Beispiel:  
  
```csharp
#warning Deprecated code in this method.  
```  
  
## <a name="remarks"></a>Hinweise  
 Eine übliche Verwendung von `#warning` ist die Verwendung in einer bedingten Anweisung. Es ist auch möglich, einen benutzerdefinierten Fehler mit [#error](../../../csharp/language-reference/preprocessor-directives/preprocessor-error.md) zu generieren.  
  
## <a name="example"></a>Beispiel  
  
```csharp
// preprocessor_warning.cs  
// CS1030 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#warning DEBUG is defined  
#endif  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#-Präprozessoranweisungen](../../../csharp/language-reference/preprocessor-directives/index.md)

