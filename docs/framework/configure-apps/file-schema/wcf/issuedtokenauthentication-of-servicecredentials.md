---
title: "&lt;issuedTokenAuthentication&gt; von &lt;serviceCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c2e288f-f603-4d13-839a-0fd6d1981bec
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;issuedTokenAuthentication&gt; von &lt;serviceCredentials&gt;
Gibt ein als Dienstanmeldeinformationen ausgegebenes Token an.  
  
## Syntax  
  
```  
  
<issuedTokenAuthentication   
   allowUntrustedRsaIssuers="Boolean"  
   audienceUriMode="Always/BearerKeyOnly/Never"  
      customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
   revocationMode="NoCheck/Online/Offline"  
   samlSerializer="String"  
    trustedStoreLocation="CurrentUser/LocalMachine">  
      <allowedAudienceUris>  
      <add allowedAudienceUri="String"/>  
      </allowedAudienceUris>  
      <knownCertificates>   
         <add findValue="String"  
                 storeLocation="CurrentUser/LocalMachine"  
                storeName=" CurrentUser/LocalMachine"  
                x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"/>  
      </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute, untergeordnete Elemente sowie übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|`allowedAudienceUris`|Ruft den Satz von Ziel\-URIs ab, für die das <xref:System.IdentityModel.Tokens.SamlSecurityToken>\-Sicherheitstoken verwendet werden kann, sodass diese von einer <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>\-Instanz als gültig eingestuft werden.  Weitere Informationen zur Verwendung dieses Attributs finden Sie unter <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>.|  
|`allowUntrustedRsaIssuers`|Ein boolescher Wert, der angibt, ob nicht vertrauenswürdige RSA\-Zertifikataussteller zulässig sind.<br /><br /> Zertifikate werden von Zertifizierungsstellen signiert, damit die Echtheit überprüft wird.  Ein nicht vertrauenswürdiger Aussteller ist eine Zertifizierungsstelle, die zum Signieren von Zertifikaten als nicht vertrauenswürdig gekennzeichnet ist.|  
|`audienceUriMode`|Ruft einen Wert ab, der angibt, ob <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> des <xref:System.IdentityModel.Tokens.SamlSecurityToken>\-Sicherheitstokens überprüft werden sollte.  Dieser Wert ist vom Typ <xref:System.IdentityModel.Selectors.AudienceUriMode>.  Weitere Informationen zur Verwendung dieses Attributs finden Sie unter <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>.|  
|`certificateValidationMode`|Legt den Zertifikatüberprüfungsmodus fest.  Einer der gültigen Werte von <xref:System.ServiceModel.Security.X509CertificateValidationMode>.  Wenn dies auf `Custom` festgelegt wurde, muss auch ein `customCertificateValidator` bereitgestellt werden.  Die Standardeinstellung ist `ChainTrust`.|  
|`customCertificateValidatorType`|Optionale Zeichenfolge.  Ein Typ und eine Assembly, die zum Überprüfen eines benutzerdefinierten Typs verwendet werden.  Das Attribut muss festgelegt werden, wenn für `certificateValidationMode` der Wert `Custom` festgelegt wurde.|  
|`revocationMode`|Legt den Sperrmodus fest, der angibt, ob eine Sperrüberprüfung ausgeführt wird und ob diese online oder offline erfolgt.  Dieses Attribut ist vom Typ <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.|  
|`samlSerializer`|Ein optionales Zeichenfolgenattribut, das den SamlSerializer\-Typ angibt, der für die Dienstanmeldeinformationen verwendet wird.  Der Standardwert ist eine leere Zeichenfolge.|  
|`trustedStoreLocation`|Optionale Enumeration.  Einer der beiden Systemspeicherorte: `LocalMachine` oder `CurrentUser`.|  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|`knownCertificates`|Gibt eine Auflistung von <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement>\-Elementen an, die vertrauenswürdige Aussteller für die Dienstanmeldeinformationen definieren.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Gibt die Anmeldeinformationen an, die für die Authentifizierung des Diensts verwendet werden sollen, sowie die Einstellungen für die Überprüfung der Clientanmeldeinformationen.|  
  
## Hinweise  
 Das Szenario für ausgestellte Token weist drei Phasen auf.  In der ersten Phase wird ein Client, der versucht, auf einen Dienst zuzugreifen, an einen *Sicherheitstokendienst* verwiesen.  Der Sicherheitstokendienst authentifiziert den Client und stellt dann ein Token \(in der Regel ein SAML\-Token \(SAML \= Security Assertions Markup Language, XML\-basierte Auszeichnungssprache für Sicherheitsbestätigungen\) für den Client aus.  Der Client kehrt dann mit dem Token zum Dienst zurück.  Der Dienst überprüft das Token auf Daten, die ihm die Authentifizierung des Tokens und somit des Clients erlauben.  Damit das Token authentifiziert werden kann, muss dem Dienst das vom Sicherheitstokendienst verwendete Zertifikat bekannt sein.  
  
 Dieses Element ist das Repository für die Zertifikate des Sicherheitstokendiensts.  Verwenden Sie zum Hinzufügen von Zertifikaten das [\<knownCertificates\>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md).  Fügen Sie wie im folgenden Beispiel gezeigt ein [\<add\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md) für jedes Zertifikat ein.  
  
```  
<issuedTokenAuthorization>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 Standardmäßig müssen die Zertifikate von einem Sicherheitstokendienst bezogen werden.  Durch diese "bekannten" Zertifikate wird sichergestellt, dass nur berechtigte Clients auf einen Dienst zugreifen können.  
  
 Weitere Informationen zur Verwendung dieses Konfigurationselements finden Sie unter [Vorgehensweise: Konfigurieren von Anmeldeinformationen auf einem Verbunddienst](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).  
  
## Siehe auch  
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement>   
 <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>   
 [Sichern von Diensten und Clients](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Vorgehensweise: Konfigurieren von Anmeldeinformationen auf einem Verbunddienst](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)