---
title: 'Configurar autenticação OAuth entre organizações do Exchange e Exchange Online'
TOCTitle: Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170800
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Implantações híbridas exclusivas do Exchange 2013 configuram a autenticação OAuth ao usar o Assistente de Configuração Híbrida. Para implantações híbridas combinadas do Exchange 2013/2010 e do Exchange 2013/2007, a conexão de autenticação com base em OAuth da nova implantação híbrida entre o Office 365 e as organizações do Exchange local não é configurada pelo Assistente de Configuração Híbrida. Essas implantações continuam a usar o processo de relação de confiança de federação por padrão. No entanto, certos recursos do Exchange 2013 ficam totalmente disponíveis em sua organização apenas por meio do uso do novo protocolo de autenticação OAuth do Exchange.

O novo processo de autenticação OAuth do Exchange permite atualmente os seguintes recursos do Exchange:

  - Gerenciamento de Direitos de Mensagens (MRM)

  - Descoberta eletrônica in-loco do Exchange

  - Arquivamento In-loco do Exchange

Recomendamos que todas as organizações combinadas do Exchange que implementam uma implantação híbrida com o Exchange 2013 e o Exchange Online configurem a autenticação OAuth do Exchange após a configuração da implantação híbrida com o Assistente de Configuração Híbrida.


> [!IMPORTANT]
> Se sua organização local está executando apenas os servidores Exchange 2013 com 5 de atualização cumulativa ou posterior instalado, execute o Assistente de implantação híbrida em vez de executar as etapas neste tópico.<BR>Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de certificados e federação" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Concluir a configuração de sua implantação híbrida usando o Assistente de implantação híbrida. Para obter mais informações, consulte [Implantações Híbridas do Exchange Server](https://technet.microsoft.com/pt-br/library/jj200581\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como você configura a autenticação OAuth entre suas organizações do Exchange local e do Exchange Online?

## Etapa 1: criar um objeto do servidor de autorização para sua organização do Exchange Online

Para este procedimento, você precisa especificar um domínio verificado para sua organização do Exchange Online. Este domínio deve ser o mesmo usado como o domínio SMTP principal usado para as contas de email com base na nuvem. Este domínio é chamado de *\<seu domínio verificado\>* no procedimento a seguir.

Execute o comando a seguir no Shell de Gerenciamento do Exchange (o Exchange PowerShell) em sua organização local do Exchange.

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## Etapa 2: habilitar o aplicativo parceiro para sua organização do Exchange Online

Execute o seguinte comando no Exchange PowerShell em sua organização local do Exchange.

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## Etapa 3: exportar o certificado de autorização local

Nesta etapa, você precisa executar um script do PowerShell para exportar o certificado de autorização local, que será importado para sua organização do Exchange Online na próxima etapa.

1.  Salve o seguinte texto em um script do PowerShell chamado, por exemplo, de **ExportAuthCert.ps1**.
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  No Exchange PowerShell em sua organização local do Exchange, execute o script do PowerShell criado na etapa anterior. Por exemplo:
    
    ```powershell
.\ExportAuthCert.ps1
```

## Etapa 4: Carregar o certificado de autorização local no ACS do Azure Active Directory

Em seguida, você precisa usar o Windows PowerShell para carregar o certificado de autorização local que você exportou na etapa anterior para Serviços de Controle de Acesso (ACS) do Azure Active Directory. Para fazer isso, os cmdlets Módulo Azure Active Directory para Windows PowerShell tem que ser instalado. Se não estiver instalado, vá para <https://aka.ms/aadposh> para instalar o Módulo Azure Active Directory para Windows PowerShell. Conclua as etapas a seguir após o Módulo Azure Active Directory para Windows PowerShell está instalado.

1.  Clique no atalho do **Windows Azure Active Directory módulo para Windows PowerShell** para abrir um espaço de trabalho do Windows PowerShell que tenha os cmdlets AD do Azure instalados. Todos os comandos dessa etapa será executado usando o Windows PowerShell para o console de Azure Active Directory.

2.  Salve o seguinte texto em um script do PowerShell chamado, por exemplo, de **UploadAuthCert.ps1**.
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  Execute o script do PowerShell criado na etapa anterior. Por exemplo:
    
    ```powershell
.\UploadAuthCert.ps1
```

4.  Após iniciar o script, uma caixa de diálogo de credenciais é exibida. Insira as credenciais para a conta de administrador de locatário em sua organização do Microsoft Online AD do Azure. Depois de executar o script, deixe o Windows PowerShell para AD do Azure sessão aberta. Você usará isso para executar um script do PowerShell na próxima etapa.

## Etapa 5: Registrar todas as autoridades de nome de host para seus pontos de extremidade de HTTP do Exchange local externo com o Windows Azure Active Directory

Você precisa executar o script nesta etapa para cada ponto final em sua organização local do Exchange acessível publicamente. Recomendamos o uso de caracteres curinga, se for possível. Por exemplo, vamos supor que o Exchange esteja externamente disponível em **https://mail.contoso.com/ews/exchange.asmx**. Nesse caso, um único caractere curinga poderia ser usado: **\*.contoso.com**. Isso cobriria os pontos finais autodiscover.contoso.com e mail.contoso.com. No entanto, não cobre o domínio de nível superior, **contoso.com**. Em casos nos quais seus servidores de Acesso para Cliente do Exchange 2013 são externamente acessíveis com autoridade de nome de host de nível superior, essa autoridade de nome de host também deve ser registrada como **contoso.com**. Não há um limite para o registro de outras autoridades de nome de host externas.

Se você não tiver certeza dos pontos finais externos do Exchange em sua organização local do Exchange, será possível obter uma lista dos pontos finais externos de serviços da Web configurados por meio da execução do seguinte comando no Exchange PowerShell em sua organização local do Exchange:

```powershell
Get-WebServicesVirtualDirectory | FL ExternalUrl
```


> [!NOTE]
> Com êxito, executando o seguinte script requer que o Windows PowerShell para Azure Active Directory está conectado ao seu locatário do Microsoft Online AD do Azure, conforme explicado na etapa 4 na seção anterior.



1.  Salve o texto a seguir em um arquivo de script do PowerShell chamado, por exemplo, de **RegisterEndpoints.ps1**. Este exemplo usa um caractere curinga para registrar todos os pontos finais para contoso.com. Substitua **contoso.com** por uma autoridade de nome de host de sua organização local do Exchange.
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  No Windows PowerShell para Azure Active Directory, execute o script do Windows PowerShell que você criou na etapa anterior. Por exemplo:
    
    ```powershell
.\RegisterEndpoints.ps1
```

## Etapa 6: criar um IntraOrganizationConnector de sua organização local para o Office 365

Você precisa definir um endereço de destino para suas caixas de correio hospedadas no Exchange Online. Este endereço de destino é criado automaticamente quando seu locatário do Office 365 é criado. Por exemplo, se o domínio de sua organização hospedado no locatário do Office 365 for "contoso.com", seu endereço de serviço de destino seria "contoso.mail.onmicrosoft.com".

Usando o Exchange PowerShell, execute o seguinte cmdlet em sua organização local:

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## Etapa 7: criar um IntraOrganizationConnector de seu locatário do Office 365 para sua organização local do Exchange

Você precisa definir um endereço de destino para suas caixas de correio hospedadas na organização local. Se o endereço SMTP primário de sua organização for "contoso.com", o endereço de destino seria "contoso.com".

Também é preciso definir o ponto final externo de Descoberta automática para sua organização local. Se sua empresa for "contoso.com", o ponto final normalmente será um dos seguintes:

  - https://autodiscover.\<seu domínio SMTP primário\>/autodiscover/autodiscover.svc

  - https://\<seu domínio SMTP primário\>/autodiscover/autodiscover.svc


> [!NOTE]
> Você pode usar o cmdlet <A href="https://technet.microsoft.com/pt-br/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</A> em seus locatários local e do Office 365 a fim de determinar os valores do ponto final exigidos pelo cmdlet <A href="https://technet.microsoft.com/pt-br/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</A>.



Usando o Windows PowerShell, execute o seguinte cmdlet:

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## Etapa 8: Configure um AvailabilityAddressSpace para quaisquer servidores pré-Exchange 2013 SP1

Quando você configura uma implantação híbrida em uma organização pré- Exchange 2013, é necessário instalar pelo menos um servidor do Exchange 2013 SP1 com as funções de servidor de Caixa de Correio e de Acesso para Cliente em sua organização existente do Exchange. Os servidores de Caixa de Correio e de Acesso para Cliente do Exchange 2013 servem como servidores Front-End e coordenam as comunicações entre sua organização local do Exchange e a organização do Exchange Online. Essa comunicação inclui o transporte de mensagens e os recursos de mensagens entre a organização local e as organizações do Exchange Online. É altamente recomendada a instalação de mais de um servidor do Exchange 2013 em sua organização no local para ajudar a aumentar a confiabilidade e a disponibilidade dos recursos de implantação híbrida.

Em uma implantação combinada com Exchange 2013/2010 ou Exchange 2013/2007, é recomendado que todos os servidores Front-End voltados para a Internet para sua organização local sejam servidores de Acesso para Cliente executando o Exchange 2013 SP1 ou superior. Todas as solicitações EWS (Serviços Web do Exchange) que se originam do Office 365 e do Exchange Online precisam se conectar a um servidor de Acesso para Cliente do Exchange 2013 em sua implantação local. Além disso, todas as solicitações EWS originárias em suas organizações locais do Exchange para Exchange Online devem receber proxy por meio de um servidor de Acesso para Cliente executando o Exchange 2013 SP1 ou superior. Como esses servidores de Acesso para Cliente do Exchange 2013 precisam lidar com essas solicitações adicionais de EWS de entrada e saída, é importante ter uma quantidade suficiente de servidores de Acesso para Cliente do Exchange 2013 disponíveis a fim de lidar com o processamento da carga e fornecer redundância de conexão. O número de servidores de Acesso para Cliente necessário dependerá da quantidade média de solicitações de EWS e poderá variar de acordo com a organização.

Antes de concluir esta etapa, verifique se:

  - Os servidores híbridos Front-End são Exchange 2013 SP1 ou superior

  - Você tem uma URL de EWS externa exclusiva para os servidores Exchange 2013. O locatário do Office 365 precisa se conectar a esses servidores para que as solicitações com base na nuvem para recursos híbridos funcionem corretamente.

  - Os servidores têm funções de servidor de Caixa de Correio e de Acesso para Cliente

  - Quaisquer servidores de Caixa de Correio e de Acesso para Cliente do Exchange 2010/2007 existentes têm a Atualização Cumulativa (CU) ou Service Pack (SP) mais recente aplicado.
    

    > [!NOTE]
    > Os servidores de Caixa de Correio do Exchange 2010/2007 podem continuar a usar os servidores de Acesso para Cliente do Exchange 2010/2007 para servidores Front-End para conexões de recursos não híbridos. Somente as solicitações de recurso de implantação híbrida do locatário do Office 365 precisam se conectar aos servidores do Exchange 2013.



Um *AvailabilityAddressSpace* precisa ser configurado em servidores de Acesso para Cliente pré-Exchange 2013 que apontam para o ponto de extremidade dos Serviços Web do Exchange de seus servidores de Acesso para Cliente do Exchange 2013 SP1 local. Esse ponto de extremidade é o mesmo ponto de extremidade descrito na Etapa 5 ou pode ser determinado executando o seguinte cmdlet em seu servidor local de Acesso para Cliente do Exchange 2013 SP1:

```powershell
Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl
```


> [!NOTE]
> Se as informações de diretório virtual forem retornadas de vários servidores, use o ponto de extremidade retornado para um servidor de Acesso para Cliente do Exchange 2013 SP1. Ele mostrará 15.0 (Build 847.32) ou superior para o parâmetro <EM>AdminDisplayVersion</EM>.



Para configurar o parâmetro *AvailabilityAddressSpace*, use o Exchange PowerShell e execute o seguinte cmdlet em sua organização local:

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## Como saber se funcionou?

É possível verificar se a configuração do OAuth está correta usando o cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/pt-br/library/jj218623\(v=exchg.150\)). Este cmdlet verifica se os pontos de extremidade do Exchange e do Exchange Online podem autenticar as solicitações um do outro.


> [!IMPORTANT]
> Ao conectar-se à sua organização do Exchange Online usando o PowerShell Remoto, talvez seja necessário usar o parâmetro <EM>AllowClobber</EM> com o cmdlet <STRONG>Import-PSSession</STRONG> para importar os comandos mais recentes na sessão local do PowerShell.



Para verificar se a sua organização local do Exchange pode se conectar ao Exchange Online, execute o seguinte comando no Exchange PowerShell em sua organização local:

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

Para verificar se a sua organização doExchange Online pode se conectar à sua organização local do Exchange, use o [PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)) para se conectar à sua organização do Exchange Online e execute o seguinte comando:

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

Sim, por exemplo, Test-OAuthConnectivity-https://lync.contoso.com/metadata/json/1 serviço EWS - TargetUri-ExchangeOnlineBox1 de caixa de correio-Verbose | FL


> [!IMPORTANT]
> Você pode ignorar o erro &amp;quot;O endereço SMTP não tem caixa de correio associada&amp;quot;. É importante apenas que o parâmetro <EM>ResultTask</EM> retorne um valor de <STRONG>Êxito</STRONG>. Por exemplo, a última seção da saída do teste deve mostrar:<BR><CODE>ResultType: Success</CODE><BR><CODE>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</CODE><BR><CODE>IsValid: True</CODE><BR><CODE>ObjectState: New</CODE>




> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


