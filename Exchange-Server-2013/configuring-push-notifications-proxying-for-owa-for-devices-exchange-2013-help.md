---
title: 'Configurando o proxy de notificações por push para o OWA para dispositivos: Exchange 2013 Help'
TOCTitle: Configurando o proxy de notificações por push para o OWA para dispositivos
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954066
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando o proxy de notificações por push para o OWA para dispositivos

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Habilitar notificações por push para o OWA para dispositivos (OWA para iPhone e OWA para iPad) em uma implantação do Microsoft Exchange 2013 local permitirá que os usuários recebam atualizações no ícone do Outlook Web App no OWA para iPhone e OWA para iPad indicando a quantidade de mensagens não lidas na caixa de correio do usuário. Se as notificações por push não forem configuradas nem habilitadas, o usuário que tiver o OWA para dispositivos não saberá se há mensagens não lidas na caixa de correio a menos que ele inicie o aplicativo. Quando uma nova mensagem fica disponível, o selo do OWA para dispositivos é atualizado no dispositivo do usuário e fica com essa aparência.

![Selo OWA para dispositivos](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "Selo OWA para dispositivos")

## Como faço para habilitar notificações por push?

Para habilitar as notificações por push, os servidores do Exchange 2013 locais devem se conectar ao Serviço de Notificações por Push do Office 365 para enviar notificações por push para iPhones e iPads. Os servidores locais do Exchange 2013 direcionam as notificações de atualização pelos serviços de notificação do Office 365 para eliminar a necessidade de registrar contas de desenvolvedor em serviços de notificação por push de terceiros. O diagrama a seguir mostra o processo pelo qual os usuários do iPhone e do iPad podem obter atualizações por selo para mensagens não lidas.

![Processo para Notificações por Push](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "Processo para Notificações por Push")

Para habilitar notificações por push, o administrador tem que:

1.  Registrar sua organização no Office 365 para empresas.

2.  Atualizar todos os servidores no local para a Atualização Cumulativa 3 (CU3) ou superior do Exchange Server 2013.

3.  Configurar o Exchange 2013 Local para a Autenticação do Office 365

4.  Habilitar as notificações por push do Exchange Server 2013 local para o Office 365 e verificar se as notificações por push estão funcionando.

## Registrar sua organização no Office 365 para empresas

O Microsoft Office 365 é um serviço baseado na nuvem destinado a ajudar a atender às necessidades de segurança, confiabilidade e produtividade robustas do usuário da sua organização. O Office 365 é um serviço de assinatura que inclui acesso online a aplicativos do Office e outros serviços de produtividade habilitados na Internet (serviços em nuvem), como a webconferência do Lync e o email hospedado do Exchange Online para empresas.

Muitos planos do Office 365 também incluem a versão para área de trabalho dos aplicativos do Office mais recentes, que podem ser instalados em vários computadores e dispositivos. Todos os planos do Office 365 são pagos com base em uma assinatura, mensal ou anualmente. Para saber mais ou para registrar sua organização no Office 365, consulte [O que é o Office 365 para empresas?](http://office.microsoft.com/pt-br/business/what-is-office-365-for-business-fx102997580.aspx). Para saber mais detalhes sobre cada serviço oferecido pelo Office 365, consulte [Descrições do serviço do Office 365](http://technet.microsoft.com/pt-br/library/jj819284.aspx).

## Atualizar para a CU3 ou superior

A Atualização Cumulativa 3 (CU3) para o Exchange Server 2013 soluciona problemas encontrados no Exchange Server 2013 desde o seu lançamento do software. Ela engloba todos os problemas e correções da CU1 e CU2 e inclui outras correções e atualizações desde que a CU2 foi lançada. Essa atualização é altamente recomendada para todos os clientes locais do Exchange Server 2013 e obrigatória para as notificações por push. Para ler mais sobre as atualizações cumulativas, incluindo a CU3, consulte [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

## Configurar o Exchange 2013 Local para a Autenticação do Office 365

O uso de um único método padronizado para a autenticação de servidor para servidor é a abordagem feita pelo Lync Server 2013. [O Exchange Server 2013](exchange-server-2013-exchange-2013-help.md) (além do [Lync Server 2013](http://technet.microsoft.com/pt-br/library/jj204817.aspx) e do [SharePoint 2013](http://technet.microsoft.com/pt-br/library/jj219758.aspx)) e [Office 2013](http://technet.microsoft.com/library/jj151815.aspx) oferecem suporte ao protocolo OAuth (Open Authorization) para autenticação e autorização de servidor para servidor. Com o OAuth, um protocolo de autorização padrão usado por vários sites importantes, as credenciais e senhas do usuário não são passadas de um computador a outro. Em vez disso, a autenticação e a autorização são baseadas na troca de tokens de segurança. Esses tokens concedem acesso a um conjunto específico de recursos por um período determinado.

A autenticação com o OAuth geralmente envolve três partes: um servidor de autorização individual e dois realms que precisam se comunicar entre si. Os tokens de segurança são emitidos pelo servidor de autorização (também conhecido como servidor do token de segurança) para os dois realms que precisam se comunicar. Esse tokens verificam se as comunicações originadas de um realm devem ser confiadas pelo outro realm. Por exemplo, o servidor de autorização pode emitir tokens que verificam se os usuários de um realm do Lync Server 2013 específico podem acessar um realm do Exchange 2013 e vice-versa.


> [!TIP]
> Um realm é um contêiner de segurança.

No entanto, para uma autenticação local de servidor para servidor, não é preciso usar um servidor de token terceirizado. Produtos de servidor, como o Lync Server 2013 e o Exchange 2013 têm um servidor de token integrado que pode ser usado para fins de autenticação com outros servidores da Microsoft (como o SharePoint Server) que oferecem suporte à autenticação de servidor para servidor. Por exemplo, o Lync Server 2013 pode ele mesmo gerar e assinar um token de segurança e usá-lo para se comunicar com o Exchange 2013. Em um caso como esse, não há a necessidade de um servidor de token terceirizado.

Para configurar uma autenticação de servidor para servidor de uma implantação local do Exchange Server 2013 para o Office 365, é preciso concluir duas etapas:

  -  **Etapa 1: atribuir um certificado ao emissor de token integrado do Exchange Server local.** Primeiro, um administrador local do Exchange precisa usar o seguinte script do Shell de Gerenciamento do Exchange para criar um certificado, caso ele não tenha sido previamente criado, e atribui-lo ao emissor de token integrado do Exchange Server local. Esse é um processo de ocorrência única. Após a criação do certificado, ele pode ser reutilizado em outros cenários de autenticação sem ser substituído. Certifique-se de atualizar o valor de *$tenantDomain* com o nome do seu domínio. Para fazer isso, copie e cole o seguinte código.
    

        > [!WARNING]
        > Para facilitar a execução de scripts do Shell, copie e cole o código em um editor de texto como o Bloco de Notas e salve o código com a extensão .ps1.


        ```
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
        ```

        O resultado esperado deve se parecer com a seguinte saída.
		
	```
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
	```

        > [!WARNING]
        > Antes de continuar, os cmdlets Módulo Azure Active Directory para Windows PowerShell é necessário. Se os cmdlets Módulo Azure Active Directory para Windows PowerShell (anteriormente conhecido como o Microsoft Online Services Module for Windows PowerShell) não tiver sido instalado, você pode instalá-lo a partir <A href="http://aka.ms/aadposh">Gerenciar o Azure AD usando o Windows PowerShell</A>.



  -  **Etapa 2: configurar o Office 365 para se comunicar com o Exchange 2013 local.** Configure o servidor do Office 365 com o qual o Exchange Server 2013 se comunicará para que seja um aplicativo parceiro. Por exemplo, se o Exchange Server 2013 local precisa se comunicar com o Office 365, é preciso configurar o Exchange para que ele seja um aplicativo parceiro. Um aplicativo parceiro é qualquer aplicativo com o qual o Exchange 2013 pode trocar tokens de segurança diretamente, sem ter que atravessar um servidor de token de segurança terceirizado. Os administradores locais do Exchange 2013 devem usar o seguinte script do Shell de Gerenciamento do Exchange para configurar o locatário do Office 365 com o qual o Exchange 2013 se comunicará para que ele seja um aplicativo parceiro. Durante a execução, um prompt será exibido para inserir o nome de usuário e a senha de administrador do domínio do locatário do Office 365. Por exemplo, administrador@fabrikam.com. Certifique-se de atualizar o valor do *$CertFile* com a localização do certificado, caso ele não tenha sido criado a partir do script anterior. Para fazer isso, copie e cole o seguinte código.
    
        ```
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        }
        ``` 


        O resultado esperado deve ser o seguinte.
		
	```
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.
	```
		
## Habilitar o uso de proxy para as notificações por push

Após a configuração da autenticação OAuth das etapas anteriores ter sido realizada com êxito, um administrador local precisa habilitar o uso de proxy para notificações por push usando o seguinte script. Certifique-se de atualizar o valor de *$tenantDomain* com o nome do seu domínio. Para fazer isso, copie e cole o seguinte código.

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

O resultado esperado deve se parecer com a seguinte saída.

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## Verifique se as notificações por push estão funcionando

Após a conclusão das etapas anteriores, as notificações por push podem ser testadas das seguintes formas:

  - **Enviando uma mensagem de email de teste para a caixa de correio do usuário:** 
    
    1.  Configure uma conta do OWA para Dispositivos em um dispositivo móvel para se inscrever nas notificações.
    
    2.  Retorne à tela inicial do dispositivo com o OWA para Dispositivos em segundo plano.
    
    3.  Envie uma mensagem de email a partir de outro dispositivo, como um computador, para a caixa de entrada da conta configurada no dispositivo móvel.
    
    4.  Após alguns minutos, essa mensagem gerará uma contagem de mensagem não vista indicada no ícone do aplicativo.

  - **Habilitando o monitoramento.** Como método alternativo para testar as notificações por push, ou para investigar o motivo de falhas nas notificações, habilite o monitoramento em um servidor de caixa de correio em sua organização. Os administradores de servidor do Exchange 2013 local devem invocar o monitoramento de proxy das notificações por push usando o seguinte script. Para fazer isso, copie e cole o seguinte código.
    
    ```
    # Send a push notification to verify connectivity.
    
    $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
    If ($s.Count -gt 1)
    {
        $s = $s[0]
    }
    If ($s.Count -ne 0)
    {
        # Restart the monitoring service to clear the cache from when push was previously disabled.
        Restart-Service MSExchangeHM
    
        # Give the monitoring service enough time to load.
        Start-Sleep -Seconds:120
    
        Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
    }
    Else
    {
        Write-Error "Cannot find a Mailbox server in the current site."
    }
    ```
    
    O resultado esperado deve se parecer com a seguinte saída.
    
    ```
        ResultType : Succeeded
        Error      :
        Exception  :
    ```
