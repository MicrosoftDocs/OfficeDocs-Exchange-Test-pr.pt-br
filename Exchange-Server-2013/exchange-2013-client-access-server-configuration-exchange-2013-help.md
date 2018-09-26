---
title: 'Configurar servidor de Acesso p/ Cliente do Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuração do servidor de Acesso para Cliente do Exchange 2013
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50484865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuração do servidor de Acesso para Cliente do Exchange 2013

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-07-25_

Após instalar o servidor de Acesso para Cliente Exchange 2013, há diversas tarefas de configuração que podem ser realizadas. Embora o servidor de Acesso para Cliente Exchange 2013 não lide com processamento para os protocolos de cliente, várias configurações precisam ser aplicadas ao servidor de Acesso para Cliente, incluindo configurações de diretório e certificado.

## Configurando certificados de servidor

No Exchange 2013, você pode usar o Assistente de Certificado para solicitar um certificado digital a uma autoridade de certificação. Depois de solicitar o certificado digital, você precisará instalá-lo no servidor de Acesso para Cliente.

Não é necessário instalar certificados digitais nos servidores de Caixa de Correio da sua organização. Um certificado autoassinado é instalado por padrão nos servidores de Caixa de Correio e ele não precisa ser substituído. Os servidores de Acesso para Cliente de sua organização confiam implicitamente no certificado autoassinado dos servidores de Caixa de Correio. Para obter mais informações, consulte [Interface de usuário de gerenciamento de certificados do Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

## Configurando diretórios virtuais

Há várias configurações que você pode configurar nos diretórios virtuais do Catálogo de Endereços Offline (OAB), Serviços Web do Exchange, Exchange ActiveSync, Outlook Web App e o Centro de Administração do Exchange. Para obter informações adicionais sobre gerenciamento de diretórios virtuais, consulte [Gerenciamento de diretório virtual](virtual-directory-management-exchange-2013-help.md). Você pode configurar os diretórios virtuais usando os comandos a seguir.

  - O Exchange 2013 fornece dois conjuntos de configurações de conectividade HTTP para a configuração do Outlook em Qualquer Lugar, de forma que os administradores possam configurar tanto um ponto de extremidade interno quanto um ponto de extremidade externo.
    
    Para configurar o Outlook em Qualquer Lugar com uma única URL para conexão, é necessário fornecer o nome do host, indicar se o SSL é necessário e especificar um pacote de autenticação usando o seguinte comando no Shell de Gerenciamento do Exchange:
    
    ```powershell
    Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    ```
    
    Você também pode especificar um ponto de extremidade acessível externamente usando o seguinte comando no Shel de Gerenciamento do Exchange:
    
    ```powershell
    Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    ```
    

    > [!TIP]  
    > Embora o Exchange 2013 dê suporte para a autenticação HTTP do tipo Negociar para o Outlook em Qualquer Lugar, isso deve ser usado apenas quando todos os servidores no ambiente estiverem executando o Exchange 2013.


  - Para configurar o Exchange ActiveSync, execute o seguinte comando.
    
    ```powershell
    Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"
    ```

  - Para configurar o diretório virtual de Serviços Web do Exchange, execute o comando a seguir.
    
    ```powershell
    Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx
    ```

  - Para configurar o Catálogo de Endereços Offline, execute o comando a seguir.
    
    ```powershell
    Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"
    ```

  - Para configurar o Ponto de Conexão de Serviço, execute o comando a seguir.
    
    ```powershell
    Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml
    ```

## Atualize a partir Acesso para Cliente do Exchange 2007 e 2010

Use esta seção para ajudá-lo a configurar o acesso externo aos protocolos no servidor de Acesso para Cliente do Exchange 2013. Execute os comandos do Shell de Gerenciamento do Exchange na seção de configuração de diretórios virtuais acima, além dos comandos abaixo.

Será necessário executar os seguintes comandos para configurar os diretórios virtuais para Exchange 2013.

1.  Para configurar uma URL externa para Outlook Web App, execute o seguinte comando no Sheel de Gerenciamento do Exchange.
    
    ```powershell
    Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    ```
    
    Execute os seguintes comandos em um prompt de comando depois de definir o diretório virtual do Outlook Web App.
    
    ```powershell
    Net stop IISAdmin /y
    ```
    
    ```powershell
    Net start W3SVC
    ```
   
2.  Para configurar o acesso externo do EAC, execute o seguinte comando no Shell de Gerenciamento do Exchange.
    
    ```powershell
    Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 
    ```

3.  Para configurar o serviço de Disponibilidade, execute o seguinte comando no Shell de Gerenciamento do Exchange.
    
    ```powershell
    Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx
    ```

Para verificar se a URL externa foi configurada corretamente para Exchange ActiveSync ou Outlook Web App, você pode usar o analisador de conectividade remota, uma ferramenta gratuita baseada em Web fornecida pela Microsoft. Você pode encontrar o Remote Connectivity Analyzer [aqui](http://go.microsoft.com/fwlink/?linkid=154308).

Para verificar se a autenticação foi configurada corretamente para o Exchange ActiveSync ou o Outlook Web App, você também pode usar o ExRCA.

Para verificar se o acesso direto a arquivos foi configurado corretamente para o Outlook Web App, faça logon como usuário no Outlook Web App utilizando a opção de computador público e, em seguida, tentar acessar e salvar um arquivo anexado a uma mensagem de email.

## Configure os protocolos nos servidores de Acesso para Cliente do Exchange 2007

Será necessário executar os seguintes comandos para configurar os diretórios virtuais para Exchange 2007.

  - Para configurar a URL externa no diretório virtual do Exchange ActiveSync, execute o seguinte comando no Shell de Gerenciamento do Exchange.
    
    ```powershell
    Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync
    ```

  - Para configurar a URL externa no diretório virtual do Outlook Web App, execute o seguinte comando no Shell de Gerenciamento do Exchange.
    
    ```powershell
    Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa
    ```