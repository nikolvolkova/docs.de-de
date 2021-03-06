---
title: "Angeben eines benutzerdefinierten Kryptografiealgorithmus | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d662a305-8e09-451d-9a59-b0f12b012f1d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Angeben eines benutzerdefinierten Kryptografiealgorithmus
WCF ermöglicht es Ihnen, beim Verschlüsseln von Daten oder Berechnen digitaler Signaturen einen benutzerdefinierten Kryptografiealgorithmus anzugeben.  Dazu führen Sie die folgenden Schritte aus:  
  
1.  Leiten Sie eine Klasse von <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> ab.  
  
2.  Registrieren Sie den Algorithmus.  
  
3.  Konfigurieren Sie die Bindung mit der <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>\-Klasse.  
  
## Ableiten einer Klasse von SecurityAlgorithmSuite  
 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> ist eine abstrakte Basisklasse, mit der Sie den Algorithmus für verschiedene sicherheitsbezogene Vorgänge angeben können,  z. B. für das Berechnen eines Hash für eine digitale Signatur oder das Verschlüsseln einer Nachricht.  Der folgende Code zeigt, wie eine Klasse von <xref:System.ServiceModel.Security.SecurityAlgorithm> abgeleitet wird:  
  
```csharp  
public class MyCustomAlgorithmSuite : SecurityAlgorithmSuite  
    {  
        public override string DefaultAsymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaOaepKeyWrap; }  
        }  
  
        public override string DefaultAsymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaSha1Signature; }  
        }  
  
        public override string DefaultCanonicalizationAlgorithm  
        {  
            get { return SecurityAlgorithms.ExclusiveC14n; ; }  
        }  
  
        public override string DefaultDigestAlgorithm  
        {  
            get { return SecurityAlgorithms.MyCustomHashAlgorithm; }  
        }  
  
        public override string DefaultEncryptionAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override int DefaultEncryptionKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSignatureKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSymmetricKeyLength  
        {  
            get { return 128; }  
        }  
  
        public override string DefaultSymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override string DefaultSymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.HmacSha1Signature; }  
        }  
  
        public override bool IsAsymmetricKeyLengthSupported(int length)  
        {  
            return length >= 1024 && length <= 4096;  
        }  
  
        public override bool IsSymmetricKeyLengthSupported(int length)  
        {  
            return length >= 128 && length <= 256;  
        }  
    }  
  
```  
  
## Registrieren des benutzerdefinierten Algorithmus  
 Die Registrierung kann in einer Konfigurationsdatei oder in imperativem Code vorgenommen werden.  Zum Registrieren eines benutzerdefinierten Algorithmus wird eine Zuordnung zwischen einer Klasse, die einen Kryptografiedienstanbieter implementiert, und einem Alias erstellt.  Der Alias wird dann einem URI zugeordnet, der beim Angeben des Algorithmus in der Bindung des WCF\-Diensts verwendet wird.  Der folgende Konfigurationsausschnitt zeigt, wie ein benutzerdefinierter Algorithmus in der Konfigurationsdatei registriert wird:  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
           <cryptoClasses>  
              <cryptoClass SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
           </cryptoClasses>  
           <nameEntry name="http://constoso.com/CustomAlgorithms/CustomHashAlgorithm"  
              class="SHA256CSP" />  
           </cryptoNameMapping>  
        </cryptographySettings>  
    </mscorlib>  
</configuration>  
  
```  
  
 Durch den Abschnitt unter dem \<`cryptoClasses`\>\-Element wird die Zuordnung zwischen SHA256CryptoServiceProvider und dem Alias "SHA256CSP" erstellt.  Das \<[nameEntry](assetId:///nameEntry?qualifyHint=False&amp;autoUpgrade=True)\>\-Element erstellt die Zuordnung zwischen dem Alias "SHA256CSP" und der angegebenen URL \("http:\/\/constoso.com\/CustomAlgorithms\/CustomHashAlgorithm"\).  
  
 Verwenden Sie zum Registrieren des benutzerdefinierten Algorithmus im Code die [M:System.Security.Cryptography.CryptoConfig.AddAlgorithm\(System.Type, System.String\<xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm%2A> System.String[])?qualifyHint=False&autoUpgrade=True\-Methode.  Diese Methode erstellt beide Zuordnungen.  Das folgende Beispiel zeigt, wie diese Methode aufgerufen wird:  
  
```  
// Register the custom URI string defined for the hashAlgorithm in MyCustomAlgorithmSuite class to create the   
// SHA256CryptoServiceProvider hash algorithm object.  
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), "http://constoso.com/CustomAlgorithms/CustomHashAlgorithm");  
  
```  
  
## Konfigurieren der Bindung  
 Zum Konfigurieren der Bindung geben Sie die benutzerdefinierte abgeleitete <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>\-Klasse wie im folgenden Codeausschnitt dargestellt in den Bindungseinstellungen an:  
  
```csharp  
WSHttpBinding binding = new WSHttpBinding();  
            binding.Security.Message.AlgorithmSuite = new MyCustomAlgorithmSuite();  
  
```  
  
 Ein vollständiges Codebeispiel finden Sie im Beispiel unter [Kryptografische Flexibilität in WCF\-Sicherheit](../../../../docs/framework/wcf/samples/cryptographic-agility-in-wcf-security.md).  
  
## Siehe auch  
 [Sichern von Diensten und Clients](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Sichern von Diensten](../../../../docs/framework/wcf/securing-services.md)   
 [Übersicht über die Sicherheit](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Begriffe der Sicherheit](../../../../docs/framework/wcf/feature-details/security-concepts.md)