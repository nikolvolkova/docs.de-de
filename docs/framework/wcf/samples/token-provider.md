---
title: "Tokenanbieter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 947986cf-9946-4987-84e5-a14678d96edb
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# Tokenanbieter
Dieses Beispiel veranschaulicht das Implementieren eines benutzerdefinierten Tokenanbieters.Ein Tokenanbieter in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] wird verwendet, um der Sicherheitsinfrastruktur Anmeldeinformationen bereitzustellen.Der Tokenanbieter untersucht im Allgemeinen das Ziel und gibt die entsprechenden Anmeldeinformationen aus, sodass die Sicherheitsinfrastruktur die Nachricht sichern kann.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ist der standardmäßige Tokenanbieter der Anmeldeinformationsverwaltung enthalten.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] wird auch mit einem [!INCLUDE[infocard](../../../../includes/infocard-md.md)] Tokenanbieter ausgeliefert.Benutzerdefinierte Tokenanbieter sind in den folgenden Fällen nützlich:  
  
-   Wenn Sie einen Speicher für Anmeldeinformationen verwenden, mit dem diese Tokenanbieter nicht umgehen können.  
  
-   Wenn Sie eigene benutzerdefinierte Mechanismen zur Transformation der Anmeldeinformationen von dem Punkt, an dem der Benutzer die Details angibt, bis zu dem Punkt, in dem das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Clientframework die Anmeldeinformationen verwendet, angeben möchten.  
  
-   Wenn Sie ein benutzerdefiniertes Token erstellen.  
  
 In diesem Beispiel wird gezeigt, wie Sie einen benutzerdefinierten Tokenanbieter erstellen können, der die Eingabe des Benutzers in ein anderes Format umwandelt.  
  
 Kurz gesagt, veranschaulicht dieses Beispiel folgende Punkte:  
  
-   Wie sich ein Client mithilfe eines Benutzername\/Kennwort\-Paars authentifizieren kann.  
  
-   Wie ein Client mit einem benutzerdefinierten Tokenanbieter konfiguriert werden kann.  
  
-   Wie der Server die Clientanmeldeinformationen anhand eines benutzerdefinierten <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> überprüfen kann, der die Übereinstimmung von Benutzername und Kennwort überprüft.  
  
-   Wie der Server über das X.509\-Zertifikat des Servers vom Client authentifiziert wird.  
  
 In diesem Beispiel wird auch gezeigt, wie auf die Identität des Aufrufers nach dem benutzerdefinierten Tokenauthentifizierungsprozess zugegriffen werden kann.  
  
 Der Dienst macht einen einzelnen Endpunkt zur Kommunikation mit dem Dienst verfügbar, der mit der App.conf\-Konfigurationsdatei definiert wird.Der Endpunkt besteht aus einer Adresse, einer Bindung und einem Vertrag.Die Bindung wird mit einer Standard\-`wsHttpBinding` konfiguriert, die standardmäßig Nachrichtensicherheit verwendet.In diesem Beispiel wird die Standard\-`wsHttpBinding` auf die Verwendung der Clientbenutzernamenauthentifizierung festgelegt.Außerdem konfiguriert der Dienst das Dienstzertifikat mit dem serviceCredentials\-Verhalten.Mit dem serviceCredentials\-Verhalten können Sie ein Dienstzertifikat konfigurieren.Ein Dienstzertifikat wird von einem Client verwendet, um den Dienst zu authentifizieren und Nachrichtenschutz bereitzustellen.Die folgende Konfiguration verweist auf das Zertifikat localhost, das während des Beispielsetups installiert wird, wie im folgenden Setup beschrieben.  
  
```  
<system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <host>  
          <baseAddresses>  
            <!-- configure base address provided by host -->  
            <add baseAddress ="http://localhost:8000/servicemodelsamples/service"/>  
          </baseAddresses>  
        </host>  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  bindingConfiguration="Binding1"   
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      </service>  
    </services>  
  
    <bindings>  
      <wsHttpBinding>  
        <binding name="Binding1">  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by a client to authenticate the service and provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
  
```  
  
 Die Clientendpunktkonfiguration besteht aus einem Konfigurationsnamen, einer absoluten Adresse für den Dienstendpunkt, der Bindung und dem Vertrag.Die Clientbindung wird mit dem entsprechenden `Mode` und der entsprechenden `clientCredentialType`\-Nachricht konfiguriert.  
  
```  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
              address="http://localhost:8000/servicemodelsamples/service"   
              binding="wsHttpBinding"   
              bindingConfiguration="Binding1"   
              contract="Microsoft.ServiceModel.Samples.ICalculator">  
    </endpoint>  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <binding name="Binding1">  
        <security mode="Message">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
</system.serviceModel>  
```  
  
 In den folgenden Schritten wird die Entwicklung eines benutzerdefinierten Tokenanbieters und seine Integration in das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Sicherheitsframework gezeigt:  
  
1.  Schreiben Sie einen benutzerdefinierten Tokenanbieter.  
  
     Im Beispiel wird ein benutzerdefinierter Tokenanbieter implementiert, der den Benutzernamen und das Kennwort erhält.Das Kennwort muss mit diesem Benutzernamen übereinstimmen.Dieser benutzerdefinierte Tokenanbieter ist nur für Demonstrationszwecke gedacht und wird nicht zur realen Bereitstellung empfohlen.  
  
     Zur Ausführung dieser Aufgabe leitet der benutzerdefinierte Tokenanbieter die <xref:System.IdentityModel.Selectors.SecurityTokenProvider>\-Klasse ab und überschreibt die <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29>\-Methode.Diese Methode erstellt ein neues `UserNameSecurityToken`\-Objekt und gibt es zurück.  
  
    ```  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
        // obtain username and password from the user using console window  
        string username = GetUserName();  
        string password = GetPassword();  
        Console.WriteLine("username: {0}", username);  
  
        // return new UserNameSecurityToken containing information obtained from user  
        return new UserNameSecurityToken(username, password);  
    }  
  
    ```  
  
2.  Schreiben Sie den benutzerdefinierten Sicherheitstoken\-Manager.  
  
     Die <xref:System.IdentityModel.Selectors.SecurityTokenManager> wird zur Erstellung von <xref:System.IdentityModel.Selectors.SecurityTokenProvider> für eine bestimmte <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> verwendet, die in der `CreateSecurityTokenProvider`\-Methode übergeben wird.Der Sicherheitstoken\-Manager dient außerdem zum Erstellen von Tokenauthentifizierern und eines Token\-Serialisierungsprogramms. Diese Vorgänge werden jedoch in diesem Beispiel nicht behandelt.In diesem Beispiel erbt der benutzerdefinierte Sicherheitstoken\-Manager aus der Klasse <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> und überschreibt die Methode `CreateSecurityTokenProvider`, um benutzerdefinierte Benutzernamen\-Tokenanbieter zurückzugeben, wenn die übergebenen Tokenanforderungen angeben, dass der Benutzernamenanbieter angefordert wird.  
  
    ```  
    public class MyUserNameSecurityTokenManager : ClientCredentialsSecurityTokenManager  
    {  
        MyUserNameClientCredentials myUserNameClientCredentials;  
  
        public MyUserNameSecurityTokenManager(MyUserNameClientCredentials myUserNameClientCredentials)  
            : base(myUserNameClientCredentials)  
        {  
            this.myUserNameClientCredentials = myUserNameClientCredentials;  
        }  
  
        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)  
        {  
            // if token requirement matches username token return custom username token provider  
            // otherwise use base implementation  
            if (tokenRequirement.TokenType == SecurityTokenTypes.UserName)  
            {  
                return new MyUserNameTokenProvider();  
            }  
            else  
            {  
                return base.CreateSecurityTokenProvider(tokenRequirement);  
            }  
        }  
    }  
    ```  
  
3.  Schreiben Sie benutzerdefinierte Clientanmeldeinformationen.  
  
     Die Klasse der Clientanmeldeinformationen stellt die Anmeldeinformationen dar, die für den Clientproxy konfiguriert werden, und erstellt einen Sicherheitstoken\-Manager, mit dem Tokenauthentifizierer, Tokenanbieter und Token\-Serialisierungsprogramme abgerufen werden können.  
  
    ```  
    public class MyUserNameClientCredentials : ClientCredentials  
    {  
        public MyUserNameClientCredentials()  
            : base()  
        {  
        }  
  
        protected override ClientCredentials CloneCore()  
        {  
            return new MyUserNameClientCredentials();  
        }  
  
        public override SecurityTokenManager CreateSecurityTokenManager()  
        {  
            // return custom security token manager  
            return new MyUserNameSecurityTokenManager(this);  
        }  
    }  
    ```  
  
4.  Konfigurieren Sie den Client für die Verwendung der benutzerdefinierten Clientanmeldeinformationen.  
  
     Damit der Client die benutzerdefinierten Clientanmeldeinformationen verwenden kann, wird im Beispiel die Standardklasse für die Clientanmeldeinformationen gelöscht und die neue Klasse für Clientanmeldeinformationen angegeben.  
  
    ```  
    static void Main()  
    {  
        // ...  
           // Create a client with given client endpoint configuration  
          CalculatorClient client = new CalculatorClient();  
  
          // set new credentials  
           client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));  
         client.ChannelFactory.Endpoint.Behaviors.Add(new MyUserNameClientCredentials());  
       // ...  
    }  
  
    ```  
  
 Um beim Dienst die Informationen zu den Aufrufern anzuzeigen, können Sie <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> verwenden, wie im folgenden Beispielcode gezeigt.<xref:System.ServiceModel.ServiceSecurityContext.Current%2A> enthält Informationen zu den Ansprüchen des aktuellen Aufrufers.  
  
```  
static void DisplayIdentityInformation()  
{  
    Console.WriteLine("\t\tSecurity context identity  :  {0}",   
        ServiceSecurityContext.Current.PrimaryIdentity.Name);  
}  
  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Clientkonsolenfenster angezeigt.Drücken Sie im Clientfenster die EINGABETASTE, um den Client zu schließen.  
  
## Setupbatchdatei  
 Mit der in diesem Beispiel enthaltenen Batchdatei Setup.bat können Sie den Server mit dem relevanten Zertifikat zum Ausführen einer selbst gehosteten Anwendung konfigurieren, die serverzertifikatbasierte Sicherheit erfordert.Diese Batchdatei muss angepasst werden, wenn sie computerübergreifend oder in einem nicht gehosteten Szenario verwendet werden soll.  
  
 Nachfolgend erhalten Sie einen kurzen Überblick über die verschiedenen Abschnitte der Batchdateien, damit Sie sie so ändern können, dass sie in der entsprechenden Konfiguration ausgeführt werden:  
  
-   Erstellen des Serverzertifikats.  
  
     Mit den folgenden Zeilen aus der Batchdatei "Setup.bat" wird das zu verwendende Serverzertifikat erstellt.Die Variable `%SERVER_NAME%` gibt den Servernamen an.Ändern Sie diese Variable, und geben Sie Ihren eigenen Servernamen an.Der Standardwert in dieser Batchdatei lautet localhost.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
-   Installieren des Serverzertifikats im Speicher für vertrauenswürdige Zertifikate des Clients:  
  
     Mit den folgenden Zeilen in der Batchdatei Setup.bat wird das Serverzertifikat in den Clientspeicher für vertrauenswürdige Personen kopiert.Dieser Schritt ist erforderlich, da von Makecert.exe generierten Zertifikaten nicht implizit vom Clientsystem vertraut wird.Wenn Sie bereits über ein Zertifikat verfügen, dass von einem vertrauenswürdigen Clientstammzertifikat stammt \(z. B. ein von Microsoft ausgegebenes Zertifikat\), ist dieser Schritt zum Füllen des Clientzertifikatspeichers mit dem Serverzertifikat nicht erforderlich.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
  
    ```  
  
> [!NOTE]
>  Die Batchdatei Setup.bat ist dafür ausgelegt, von einer Windows SDK\-Eingabeaufforderung ausgeführt zu werden.Die MSSDK\-Umgebungsvariable muss auf das Verzeichnis zeigen, in dem das SDK installiert ist.Diese Umgebungsvariable wird automatisch innerhalb einer Windows SDK\-Eingabeaufforderung festgelegt.  
  
#### So richten Sie das Beispiel ein und erstellen es  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Befolgen Sie die Anweisungen unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md), um die Projektmappe zu erstellen.  
  
#### So führen Sie das Beispiel auf demselben Computer aus  
  
1.  Öffnen Sie eine [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]\-Eingabeaufforderung mit Administratorrechten, und führen Sie Setup.bat aus dem Beispielinstallationsordner aus.Hiermit werden alle Zertifikate installiert, die zum Ausführen des Beispiels erforderlich sind.  
  
    > [!NOTE]
    >  Die Batchdatei Setup.bat ist darauf ausgelegt, an einer [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]\-Eingabeaufforderung ausgeführt zu werden.Die innerhalb der [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]\-Eingabeaufforderung festgelegte PATH\-Umgebungsvariable zeigt auf das Verzeichnis mit den ausführbaren Dateien, die für das Skript Setup.bat erforderlich sind.  
  
2.  Starten Sie Service.exe aus dem Ordner \\service\\bin.  
  
3.  Starten Sie Client.exe aus dem Ordner \\client\\bin.In der Clientkonsolenanwendung wird Clientaktivität angezeigt.  
  
4.  Geben Sie an der Benutzernamen\-Eingabeaufforderung einen Benutzernamen ein.  
  
5.  Verwenden Sie an der Kennworteingabeaufforderung dieselbe Zeichenfolge, die an der Benutzernamen\-Eingabeaufforderung eingegeben wurde.  
  
6.  Wenn der Client und der Dienst nicht miteinander kommunizieren können, finden Sie weitere Informationen unter [Troubleshooting Tips](http://msdn.microsoft.com/de-de/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### So führen Sie das Beispiel computerübergreifend aus  
  
1.  Erstellen Sie auf dem Dienstcomputer ein Verzeichnis für die Dienstbinärdateien.  
  
2.  Kopieren Sie die Dienstprogrammdateien in das Dienstverzeichnis auf dem Dienstcomputer.Kopieren Sie außerdem die Dateien Setup.bat und Cleanup.bat auf den Dienstcomputer.  
  
3.  Sie benötigen ein Serverzertifikat mit dem Antragstellernamen, das den vollqualifizierten Domänennamen des Computers enthält.Die Datei Service.exe.config muss so aktualisiert werden, dass sie diesem neuen Zertifikatsnamen entspricht.Sie können das Serverzertifikat erstellen, indem Sie die Batchdatei Setup.bat ändern.Beachten Sie, dass die Datei setup.bat an einer Visual Studio\-Eingabeaufforderung mit Administratorrechten ausgeführt werden muss.Sie müssen die Variable `%SERVER_NAME%` auf den vollqualifizierten Hostnamen des Computers festlegen, der als Host für den Dienst dienen soll.  
  
4.  Kopieren Sie das Serverzertifikat in den Speicher CurrentUser – TrustedPeople des Clients.Dieser Schritt muss nicht ausgeführt werden, wenn das Serverzertifikat von einem Aussteller stammt, der vom Client als vertrauenswürdig eingestuft wurde.  
  
5.  Ändern Sie in der Datei Service.exe.config auf dem Dienstcomputer den Wert der Basisadresse, und geben Sie anstelle von localhost einen vollqualifizierten Computernamen an.  
  
6.  Führen Sie auf dem Dienstcomputer service.exe an einer Eingabeaufforderung aus.  
  
7.  Kopieren Sie die Clientprogrammdateien aus dem Ordner \\client\\bin\\ \(unterhalb des sprachspezifischen Ordners\) auf den Clientcomputer.  
  
8.  Ändern Sie in der Datei Client.exe.config auf dem Clientcomputer den Wert für die Adresse des Endpunkts, sodass er mit der neuen Adresse Ihres Diensts übereinstimmt.  
  
9. Starten Sie auf dem Clientcomputer `Client.exe` in einem Eingabeaufforderungsfenster.  
  
10. Wenn der Client und der Dienst nicht miteinander kommunizieren können, finden Sie weitere Informationen unter [Troubleshooting Tips](http://msdn.microsoft.com/de-de/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### So stellen Sie den Zustand vor Ausführung des Beispiels wieder her  
  
1.  Führen Sie Cleanup.bat im Beispielordner aus, nachdem Sie das Beispiel fertig ausgeführt haben.  
  
## Siehe auch