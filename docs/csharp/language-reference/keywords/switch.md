---
title: "Schlüsselwort „switch“ (C#-Referenz)"
ms.date: 2017-03-07
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- switch_CSharpKeyword
- switch
- case
- case_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- switch statement [C#]
- switch keyword [C#]
- case statement [C#]
- default keyword [C#]
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
caps.latest.revision: 47
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 387c8c7e44ab818ca97e686330746f50df091bb9
ms.openlocfilehash: 5c151e3bbd46212f1234d46ff05d389f2384ca0e
ms.contentlocale: de-de
ms.lasthandoff: 09/25/2017

---
# <a name="switch-c-reference"></a>switch (C#-Referenz)
`switch` ist eine Auswahlanweisung, die einen einzelnen *switch-Abschnitt* zum Ausführen aus einer Liste von Kandidaten auswählt, die auf einem Mustertreffer mit dem *Vergleichsausdruck* basiert. 
  
 [!code-cs[switch#1](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch1.cs#1)]  

Die Anweisung `switch` wird häufig als Alternative zu einem [if-else](if-else.md)-Konstrukt verwendet, wenn ein einzelner Ausdruck mit drei oder mehr Bedingungen getestet wird. Die folgende Anweisung `switch` bestimmt z.B., ob eine Variable des Typs `Color` einen von drei Werten hat: 

[!code-cs[switch#3](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch3.cs#1)] 

Dies entspricht dem folgenden Beispiel, das ein `if`-`else`-Konstrukt verwendet. 

[!code-cs[switch#3a](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch3a.cs#1)] 

## <a name="the-match-expression"></a>Der Vergleichsausdruck

Der Vergleichsausdruck stellt den Wert bereit, mit dem die Muster in den Bezeichnungen `case` verglichen werden. Die Syntax lautet:

```csharp
   switch (expr)
```

In C# 6 muss der Vergleichsausdruck ein Ausdruck sein, der einen Wert der folgenden Typen zurückgibt:

- Ein [char](char.md)
- Eine [Zeichenfolge](string.md)
- Ein [bool](bool.md) 
- Ein ganzzahliger Wert wie [int](int.md) oder [long](long.md)
- Ein [Enumerations](enum.md)wert

Ab C# 7 kann der Vergleichsausdruck jeder Ausdruck sein, der nicht NULL ist.
 
## <a name="the-switch-section"></a>Der switch-Abschnitt
 
 Eine `switch`-Anweisung enthält eine oder mehrere switch-Abschnitte. Jeder switch-Abschnitt enthält eine oder mehrere *case-Bezeichnungen* und eine Liste mit mindestens einer Anweisung. Das folgende Beispiel zeigt eine einfache `switch`-Anweisung, die über drei switch-Abschnitte verfügt. Jeder switch-Abschnitt enthält eine case-Bezeichnung, z. B. `case 1:`, und zwei Anweisungen.
 
  Eine `switch`-Anweisung kann eine beliebige Anzahl von switch-Abschnitten enthalten, und jeder Abschnitt kann eine oder mehrere case-Bezeichnungen haben, wie im folgend Beispiel gezeigt wird. Allerdings können zwei case-Bezeichnungen nicht denselben Ausdruck enthalten.  

 [!code-cs[switch#2](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch2.cs#1)]  

 Nur ein switch-Abschnitt einer switch-Anweisung wir ausgeführt. C# lässt nicht zu, dass die Ausführung von einem switch-Abschnitt zum nächsten fortgesetzt wird. Aus diesem Grund generiert der folgende Code den Compilerfehler CS0163: „Das Steuerelement kann nicht von einer case-Bezeichnung (<case label>) zur nächsten fortfahren.“   

```csharp  
switch (caseSwitch)  
{  
    // The following switch section causes an error.  
    case 1:  
        Console.WriteLine("Case 1...");  
        // Add a break or other jump statement here.  
    case 2:  
        Console.WriteLine("... and/or Case 2");  
        break;  
}  
```  
Diese Anforderung wird normalerweise erfüllt, indem der switch-Abschnitt ausdrücklich durch Verwenden einer Anweisung [break](break.md), [goto](goto.md) oder [return](return.md) beendet wird. Der folgende Code ist jedoch auch gültig, da er sicherstellt, dass die Programmsteuerung nicht im switch-Abschnitt `default` fortfährt.
  
 [!code-cs[switch#4](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch4.cs#1)]    
  
 Die Ausführung der Anweisungsliste im switch-Abschnitt mit einer case-Bezeichnung, die den Vergleichsausdruck vergleicht, beginnt mit der ersten Anweisung und durchläuft in der Regel die Anweisungsliste, bis eine jump-Anweisung erreicht wird, z.B. `break`, `goto case`, `goto label`, `return` oder `throw`. An diesem Punkt wird die Steuerung der `switch`-Anweisung entzogen oder an eine andere case-Bezeichnung übertragen. Eine `goto`-Anweisung muss bei Nichtverwendung die Steuerung an eine konstante Bezeichnung übergeben. Diese Einschränkung ist notwendig, da der Versuch, die Steuerung an eine nicht konstante Bezeichnung zu übergeben, unerwünschte Nebeneffekte haben kann, z.B. kann die Steuerung an eine nicht beabsichtigte Position im Code übergeben werden, oder es kann eine Endlosschleife entstehen.

## <a name="case-labels"></a>case-Bezeichnungen

 Jede case-Bezeichnung gibt ein Muster an, mit dem der Vergleichsausdruck verglichen werden soll (die Variable `caseSwitch` in den vorherigen Beispielen). Wenn sie übereinstimmen, wird das Steuerelement an den switch-Abschnitt übertragen, der die **erste** übereinstimmende case-Bezeichnung enthält. Wenn keine case-Bezeichnung mit dem Vergleichsausdruck übereinstimmt, wird das Steuerelement an den Abschnitt mit der `default`-case-Bezeichnung übertragen, sofern vorhanden. Wenn es kein `default`-case gibt, werden keine Anweisungen in jeglichen switch-Abschnitten ausgeführt, und ein Steuerelement wird außerhalb der `switch`-Anweisung übertragen.

 Informationen zur `switch`-Anweisung und zum Musterabgleich finden Sie im Abschnitt [Musterabgleich mit der `switch`-Anweisung](#pattern).

 Da C# 6 nur die Konstantenmuster unterstützt und die Wiederholung von Konstantenwerten nicht erlaubt, definieren case-Bezeichnungen exklusive Werte, und nur ein Muster kann mit dem Vergleichsausdruck übereinstimmen. Daher ist die Reihenfolge, in der die `case`-Anweisungen auftauchen, unwichtig.

 Da in C# 7 jedoch andere Muster unterstützt werden, müssen case-Bezeichnungen keine gegenseitig ausschließenden Werte definieren, und mehrere Muster können mit dem Vergleichsausdruck übereinstimmen. Da nur die Anweisungen im switch-Abschnitt ausgeführt werden, die das erste übereinstimmende Muster enthalten, ist die Reihenfolge, in der `case`-Anweisungen erscheinen, nun wichtig. Wenn C# einen switch-Abschnitt erkennt, dessen case-Anweisung oder Anweisungen eine Teilmenge der vorherigen Anweisungen ist oder einer entsprechen, erzeugt der Abschnitt den Compilerfehler CS8120: „Der Parameter wurde bereits von einem vorherigen Parameter verarbeitet.“ 

 Das folgende Beispiel veranschaulicht eine `switch`-Anweisung, die eine Reihe von sich nicht gegenseitig ausschließenden Mustern verwendet. Wenn Sie den switch-Abschnitt `case 0:` verschieben, sodass er nicht länger der erste Abschnitt in der `switch`-Anweisung ist, erzeugt C# einen Compilerfehler, da eine Ganzzahl, deren Wert 0 ist, eine Teilmenge aller Ganzzahlen ist, die das Muster anhand der `case int val`-Anweisung definiert.

 [!code-cs[switch#5](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch5.cs#1)]    

Sie können dieses Problem beheben und die Compilerwarnung auf eine von zwei Arten entfernen:

- Durch das Ändern der Reihenfolge der switch-Abschnitte 
 
- Durch das Verwenden einer </a name=“when“>when-Klausel</a> in der `case`-Bezeichnung
 
## <a name="the-default-case"></a>Der `default`-Case

Der `default`-Case gibt den auszuführenden switch-Abschnitt an, wenn der Vergleichsausdruck nicht mit einer anderen `case`-Bezeichnung übereinstimmt. Wenn ein `default`-Case nicht vorhanden ist, und der Vergleichsausdruck nicht einer der anderen `case`-Bezeichnung entspricht, fährt der Programmablauf mit der `switch`-Anweisung fort.

Der `default`-Case kann in beliebiger Reihenfolge in der `switch`-Anweisung auftauchen. Unabhängig von der Reihenfolge im Quellcode wird er immer zuletzt ausgewertet, nachdem alle `case`-Bezeichnungen ausgewertet wurden.

## <a name="a-namepattern--pattern-matching-with-the-switch-statement"></a><a name="pattern" /> Musterabgleich mit der `switch`-Anweisung
  
Jede `case`-Anweisung definiert ein Muster, das, wenn es mit dem Vergleichsausdruck übereinstimmt, dafür sorgt, dass seine enthaltenden switch-Abschnitte ausgeführt werden. Alle Versionen von C# unterstützen Konstantenmuster. Die übrigen Muster werden ab C# 7 unterstützt. 
  
### <a name="constant-pattern"></a>Konstantenmuster 

Das Konstantenmuster testet, ob der Vergleichsausdruck einer festgelegten Konstanten entspricht. Die Syntax lautet:

```csharp
   case constant:
```

wobei *constant* der zu testende Wert ist. *constant* kann eine der folgenden konstanten Ausdrücke sein: 

- Ein [bool](bool.md)-Literal, entweder `true` oder `false`
- Alle ganzzahligen Konstanten, z.B. [int](int.md), [lang](long.md) oder ein [Byte](byte.md) 
- Der Name einer deklarierten `const`-Variablen
- Eine Enumerationskonstante.
- Ein [char](char.md)-Literal
- Ein [Zeichenfolgenliteral](string.md).

Der Konstantenausdruck wird wie folgt ausgewertet:

- Wenn *expr* und *constant* integrale Typen sind, bestimmt der C#-Gleichheitsoperator, ob der Ausdruck `true` (d.h., ob `expr == constant`) zurückgibt.

- Andernfalls wird der Wert des Ausdrucks durch einen Aufruf der statischen Methode [Object.Equals (expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) bestimmt.  

Das folgende Beispiel verwendet das Konstantenmuster, um zu bestimmen, ob ein bestimmtes Datum ein Wochenende, der erste Tag der Arbeitswoche, der letzte Tag der Arbeitswoche oder die Mitte der Arbeitswoche ist. Es bewertet die Eigenschaft [DateTime.DayOfWeek](xref:System.DateTime.DayOfWeek) des heutigen Tags mit den Membern der @System.DayOfWeek-Enumeration. 

[!code-cs[switch#7](../../../../samples/snippets/csharp/language-reference/keywords/switch/const-pattern.cs#1)]

Im folgenden Beispiel wird das Konstantenmuster verwendet, um Benutzereingaben in einer Konsolenanwendung zu steuern, die eine automatische Kaffeemaschine simuliert.
  
 [!code-cs[switch#6](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch6.cs)]  

### <a name="type-pattern"></a>Typmuster

Das Typmuster ermöglicht die präzise Auswertung und Konvertierung des Typs. Wenn es mit der `switch`-Anweisung verwendet wird, um einen Musterabgleich auszuführen, wird getestet, ob eine Anweisung in einen bestimmten Typ konvertiert werden kann, und sofern dies möglich ist, wird es in eine Variable des Typs umgewandelt. Die Syntax lautet:

```csharp
   case type varname 
```
bei der *Typ* der Name des Typs ist, in den das Ergebnis von *expr* konvertiert wird, und *varname* das Objekt ist, in das das Ergebnis von *expr* konvertiert wird, wenn der Abgleich erfolgreich ist 

Der `case`-Ausdruck ist `true`, wenn eine der folgenden Aussagen zutrifft:

- *expr* ist eine Instanz des gleichen Typs wie *Typ*.

- *expr* ist eine Instanz eines Typs, der von *Typ* abgeleitet wird. Das Ergebnis von *expr* kann, in anderen Worten, in eine Instanz von *Typ* umgewandelt werden.

- *expr* hat einen Kompilierzeittyp, der eine Basisklasse von *type* ist, und *expr* hat einen Laufzeittyp,der *type* ist oder von *type* abgeleitet wurde. Der *Kompilierzeittyp* einer Variablen ist der Typ der Variablen, wie es in der Deklaration des Typs definiert wurde. Der *Laufzeittyp* einer Variablen ist der Typ der Instanz, die dieser Variable zugewiesen wird.

- *expr* ist eine Instanz eines Typs, der die Schnittstelle *Typ* implementiert.

Wenn der case-Ausdruck TRUE ist, ist *varname* definitiv zugewiesen und hat nur innerhalb des switch-Abschnitts einen lokalen Geltungsbereich.

Beachten Sie, dass `null` nicht mit einem Typ übereinstimmt. Verwenden Sie folgende `case`-Bezeichnung, um `null` abzugleichen:

```csharp
case null:
```
 
Im folgenden Beispiel wird mithilfe des Typmusters Informationen über die verschiedenen Arten von Auflistungstypen bereitgestellt.

[!code-cs[switch#5](../../../../samples/snippets/csharp/language-reference/keywords/switch/type-pattern.cs#1)]

Ohne Musterabgleich könnte dieser Code wie folgt geschrieben werden. Die Verwendung des Typmusterabgleichs erzeugt einen kompakteren, lesbaren Code, indem nicht mehr getestet werden muss, ob das Ergebnis einer Umwandlung `null` ist, oder um wiederholte Umwandlungen auszuführen.  

[!code-cs[switch#6](../../../../samples/snippets/csharp/language-reference/keywords/switch/type-pattern2.cs#1)]

## <a name="the-case-statement-and-the-when-clause"></a>Die `case`-Anweisung und die `when`-Klausel

Da sich ab C# 7 case-Anweisungen nicht gegenseitig ausschließen müssen, können Sie eine `when`-Klausel hinzufügen, um eine zusätzliche Bedingung anzugeben, die erfüllt werden muss, damit die case-Anweisung als TRUE ausgewertet wird. Die `when`-Klausel kann ein beliebiger Ausdruck sein, der einen booleschen Wert zurückgibt. Eine der häufigsten Verwendungsmöglichkeiten für die `when`-Klausel wird verwendet, um zu verhindern, dass ein switch-Abschnitt ausgeführt wird, wenn der Wert eines Ausdrucks mit `null` übereinstimmt. 

 Im folgenden Beispiel wird eine `Shape`-Basisklasse, eine `Rectangle`-Klasse, die von `Shape` abgeleitet wird, und eine `Square`-Klasse, die von `Rectangle` abgeleitet wird, definiert. Die `when`-Klausel wird verwendet, um sicherzustellen, dass `ShowShapeInfo` ein `Rectangle`-Objekt, dem eine gleiche Länge und Breite zugewiesen wurde, wie `Square` behandelt, selbst wenn es nicht als ein `Square`-Objekt instanziiert wurde. Diese Methode versucht weder Informationen über ein Objekt anzuzeigen, das `null` ist, noch über eine Form, deren Bereich NULL ist. 

[!code-cs[switch#8](../../../../samples/snippets/csharp/language-reference/keywords/switch/when-clause.cs#1)]
  
Beachten Sie, dass in diesem Beispiel die `when`-Klausel, die zu prüfen versucht, ob ein `Shape`-Objekt `null` ist, nicht ausgeführt wird. Das richtige Typmuster, um auf `null` zu testen, ist `case null:`.

## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  

 [C#-Referenz](../index.md)   
 [C#-Programmierhandbuch](../../programming-guide/index.md)   
 [C#-Schlüsselwörter](index.md)   
 [if-else](if-else.md)   
 [Mustervergleich](../../pattern-matching.md)   
 

 

