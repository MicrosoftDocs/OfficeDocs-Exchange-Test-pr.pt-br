---
title: 'Configurando o descarregamento de SSL no Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurando o descarregamento de SSL no Exchange 2013
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61203506
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando o descarregamento de SSL no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-08-22_

As informações a seguir ajudam você a configurar descarregamento SSL para os protocolos e serviços relacionados em servidores de Acesso para Cliente do Exchange 2013 com Service Pack 1 (SP1) instalado. Se você tiver múltiplos servidores de Acesso para Cliente, deverá executar as etapas exigidas para cada protocolo ou serviço em cada servidor de Acesso para Cliente com SP1 instalado em sua organização local. Isso sem mencionar que cada servidor de Acesso para Cliente em sua organização deve ser configurado de modo idêntico. Se você estiver atualizando para as Atualizações Cumulativas (CUs) ou service packs mais recentes e deseja continuar usando o descarregamento SSL, execute as etapas a seguir novamente após ter atualizado ou aplicado essas atualizações em seus servidores de Acesso para Cliente do Exchange 2013.

Uma das maiores vantagens do descarregamento SSL é conseguir gerenciar com mais facilidade os certificados usados. Em vez de ter certificados SSL separados para cada servidor de Acesso para Cliente com SP1 instalado, um único certificado SSL é usado e importado para todos os servidores de Acesso para Cliente. O certificado usado pode ser um certificado SSL existente ou recém-criado.


> [!CAUTION]
> Quando você usa o Gerenciador de serviços de informações da Internet (IIS), o Shell de gerenciamento do Exchange ou uma interface de linha de comando para configurar o descarregamento de SSL, observe que há um <STRONG>Site padrão</STRONG> e um site do <STRONG>Exchange Back-End</STRONG>. Para o descarregamento de SSL, apenas configurar o <STRONG>Site padrão</STRONG> e não fizer alterações para o site do <STRONG>Exchange Back-End</STRONG>.



**Conteúdo**

Configuring SSL offloading for Outlook Web App

Configuring SSL offloading for the Exchange Admin Center (EAC)

Configuring SSL offloading for Outlook Anywhere

Configuring SSL offloading for the Offline Address Book (OAB)

Configuring SSL offloading for Exchange ActiveSync (EAS)

Configuring SSL offloading for Exchange Web Services (EWS)

Configuring SSL offloading for the Autodiscover service

Configuring SSL offloading for the Mailbox Replication Proxy Service (MRSProxy)

Configurando o descarregamento SSL para clientes do Outlook (diretório virtual MAPI)

Using a Shell script to enable SSL offloading for all protocols and services

Configuring coexistence with Exchange 2007 and Exchange 2010

## O que você precisa saber antes de começar?

  - Instale todos os servidores de Acesso para Cliente e de Caixa de Correio necessários em sua organização.

  - Instale o Service Pack 1 (SP1) em cada servidor de Acesso para Cliente e de Caixa de Correio em sua organização. Para baixar o SP1, consulte [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Determine as permissões necessárias para o Exchange 2013 consultando [Permissões de recurso](feature-permissions-exchange-2013-help.md).

  - Para ver quais permissões você precisa para servidores de Acesso para Cliente, consulte "Permissões de servidores de Acesso para Cliente" em [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para ver quais permissões você precisa para servidores de Acesso para Cliente, consulte "Permissões do Outlook Web App" em [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - É provável que você só consiga usar o Shell para realizar alguns procedimentos. Para saber como abrir o Shell em sua organização Exchange local, consulte [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para usar um certificado existente em seus servidores de Acesso para Cliente e no dispositivo com o qual você está terminando conexões SSL, exporte o certificado com a chave privada em um servidor de Acesso para Cliente e importe-o ou instale-o no dispositivo. Para obter detalhes, consulte [Export-ExchangeCertificate](https://technet.microsoft.com/pt-br/library/aa996305\(v=exchg.150\)).

  - Para usar um novo certificado, você deve usar EAC ou o Shell para criar, importar e habilitar o novo certificado. Para obter detalhes, consulte [Interface de usuário de gerenciamento de certificados do Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Configure o descarregamento SSL para o Outlook Web App

Para habilitar o descarregamento SSL para o Outlook Web App, você precisa remover o requisito SSL no diretório virtual **owa** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **owa**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **owa**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeOWAAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configure o descarregamento SSL para o Centro de Administração do Exchange (EAC)

Para habilitar o descarregamento SSL para EAC, você precisa remover a exigência de SSL no diretório virtual **ecp** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar SSL no diretório virtual **ecp**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **ecp**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeECPAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeECPAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configurando o descarregamento SSL para o Outlook em Qualquer Lugar

Descarregamento SSL para o Outlook Anywhere está habilitado por padrão. Outlook em qualquer lugar os clientes podem obter email de uma rede privada ou pública. Por padrão, o nome de host interno ou FQDN do servidor é usado para permitir que os clientes internos do Outlook para se conectar. No entanto, se o Outlook em qualquer lugar não é usado internamente, você deve remover o nome de host interno. Para permitir o acesso interno e externo para clientes do Outlook, você deve configurar os nomes de host interno e externo, defina o método de autenticação para cada e definir os clientes internos e externos para exigir SSL. Para configurar o método de autenticação para os clientes externos, você pode usar o EAC ou o Shell de gerenciamento do Exchange, mas para clientes internos, você deve usar o Shell:

  - **Etapa 1**   Você pode usar o EAC ou o Shell se não tiver adicionado um nome de host externo para o Outlook em qualquer lugar:
    
      - Usando o EAC, vá até **Servidores**, selecione nome do servidor de Acesso para Cliente na lista e clique em **Editar**. Na janela **Exchange Server**, clique em **Outlook em Qualquer Lugar** e depois na caixa **Especifique o nome de host externo (por exemplo, contoso.com) que os usuários irão usar para se conectarem à sua organização**, digite o nome do host externo. Verifique se a opção **Permitir descarregamento SSL** está selecionada e clique em **Salvar**.
    
      - Usando o Shell de Gerenciamento do Exchange, clique em **Iniciar** e, no menu **Iniciar**, clique em **Shell de Gerenciamento do Exchange**. Na janela, digite o seguinte comando e pressione Enter:
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **Etapa 2**   Por padrão, o descarregamento SSL está habilitado. No entanto, você pode usar EAC ou o Shell de Gerenciamento do Exchange se o descarregamento SSL tiver sido desabilitado e você quiser habilitá-lo.
    
      - Usando o EAC, vá até **Servidores**, selecione nome do servidor de Acesso para Cliente na lista e clique em **Editar**. Na janela **Exchange Server**, clique em **Outlook em Qualquer Lugar**, clique na opção **Permitir descarregamento SSL** e depois clique em **Salvar**.
    
      - Usando o Shell, digite o seguinte comando e pressione Enter.
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **Etapa 3**   Por padrão, **Exigir SSL** não está selecionado no diretório virtual **Rpc**, mas se você quiser verificar se o SSL está desabilitado, use o Gerenciador de Serviços de Informações da Internet (IIS).
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **Rcp**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, verifique se a caixa de seleção **Exigir SSL** está marcada e clique em **Aplicar** no painel **Ações**.

  - **Etapa 4**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.


> [!IMPORTANT]
> Você deve aguardar para que o processo de Host de Serviço aplique quaisquer alterações do Active Directory nos Serviços de Informações da Internet (IIS) a cada 15 minutos, mesmo se você reiniciar o IIS em um servidor de Acesso para Cliente.



Voltar ao início

## Configurando o descarregamento SSL para o Catálogo de Endereços Offline (OAB)

Para habilitar o descarregamento SSL para o Catálogo de Endereços Offline (OAB), você precisa remover o requisito SSL no diretório virtual **OAB** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **OAB**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **OAB**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeOABAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeOABAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configurando o descarregamento SSL para Exchange ActiveSync (EAS)

Para habilitar o descarregamento SSL para o Exchange ActiveSync (EAS), você precisa remover a exigência de SSL no diretório virtual **Microsoft-Server-ActiveSync** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **Microsoft-Server-ActiveSync**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **Microsoft-Server-ActiveSync**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeSyncAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configurando o descarregamento SSL para Serviços Web do Exchange (EWS)

Para habilitar o descarregamento SSL para Serviços Web do Exchange (EWS), você precisa remover a exigência de SSL no diretório virtual **EWS** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **EWS**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **EWS**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeServicesAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configurando o descarregamento SSL para o serviço Descoberta Automática

Para habilitar o descarregamento SSL para o serviço Descoberta Automática, você precisa remover a exigência de SSL no diretório virtual **Descoberta Automática** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **Descoberta Automática**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **Descoberta Automática**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Configurando descarregamento SSL para o serviço Proxy de Replicação da Caixa de Correio (MRSProxy)

O serviço de Proxy de replicação de caixa de correio (MRSProxy) é instalado em cada servidor de acesso para cliente do Exchange 2013. Ajuda a MRSProxy que você faça a movimentação entre florestas solicitações no local, bem como mover caixas de correio para Office 365 no local. No entanto, por padrão, MRSProxy está desabilitado. Se você estiver habilitando-lo, você deve ativá-lo na floresta do Exchange remota entre florestas, movimentações de caixa de correio no local ou na floresta do Exchange local para mover uma caixa de correio para o Office 365. Embora o serviço de MRSProxy é executado em serviços de Web do Exchange (EWS), não há suporte para configurar o descarregamento de SSL.

A razão para isso é que o serviço MRSProxy espera que tráfego seja assinado/criptografado. Qualquer balanceador de carga de hardware ou firewall deve criptografar novamente o tráfego do MRSProxy enviando-o para servidores de Acesso para Cliente. Se este for o caso, recomendamos a configurção da ponte SSL para que o descarregamento funcione.

**Reverter SSL ou a ponte SSL**   Se você habilitar reverso SSL ou SSL ponte nos balanceadores de carga de hardware, você não será necessário executar as etapas anteriores em cada servidor CAS. No entanto, habilitar o SSL reverso no balanceadores de carga do hardware significa que SSL criptografia e descriptografia permanecerão com os servidores de acesso para cliente. Nesse caso, a criptografia SSL e a descriptografia ocorrerá no tanto os balanceadores de carga de hardware e os servidores de acesso para cliente. Escolha usar SSL do Exchange 2013 descarregamento ou inversa SSL (ponte SSL) é dependente os objetivos organizacionais e as práticas de segurança que devem ser implementadas. A imagem a seguir mostra a conectividade do cliente com SSL ponte (reverso SSL) habilitado.

![Ponte SSL](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "Ponte SSL")

## Configurando o descarregamento SSL para clientes do Outlook (diretório virtual MAPI)

Para habilitar o descarregamento SSL para clientes do Outlook, você precisa remover a exigência de SSL no diretório virtual **MAPI** no **Site da Web Padrão**:

  - **Etapa 1**   Você pode usar o Gerenciador de Serviços de Informações da Internet (IIS) ou uma linha de comando para desabilitar o SSL no diretório virtual **MAPI**:
    
      - Usando o Gerenciador de Serviços de Informações da Internet (IIS), expanda **Sites** \> **Site da Web Padrão** e selecione o diretório virtual **MAPI**. Na painel de resultados, em **IIS**, clique duas vezes em **Configurações de SSL**. No painel de resultados **Configurações de SSL**, desmarque a caixa de seleção **Exigir SSL** e clique em **Aplicar** no painel **Ações**.
    
      - Usando a linha de comando, digite o comando a seguir e pressione Enter.
        
            appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST

  - **Etapa 2**   Você precisa reciclar o pool de aplicativos correto ou reiniciar os Serviços de Informações da Internet usando um dos métodos a seguir:
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
    
      - Usando um cmdlet do Windows PowerShell, digite o comando a seguir e pressione Enter.
        
            IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
    
      - Usando uma linha de comando: Vá para **Iniciar** \> **Executar**, digite **cmd** e depois pressione Enter. Na janela Prompt de Comando, digite o comando a seguir e pressione ENTER.
        
            iisreset /noforce
    
      - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): No Gerenciador de Serviços de Informações da Internet (IIS), no painel **Ações**, clique em **Reiniciar**.

Voltar ao início

## Usando um script para habilitar o descarregamento SSL para todos os protocolos e serviços

Se você estiver trabalhando com uma organização grande com múltiplos servidores de Acesso para Cliente do Exchange 2013, talvez você queira agilizar as etapas anteriores pelas quais você passou. Você pode copiar e colar os comandos em qualquer um dos scripts a seguir no Bloco de Notas, fazer quaisquer alterações, salvar o arquivo com uma extensão .ps1 e depois executá-lo no Shell de Gerenciamento do Exchange. Dependendo das suas necessidades, os dois scripts podem ser usados para configurar o descarregamento SSL para todos os protocolos e serviços para um único servidor de Acesso para Cliente ou para vários deles.


> [!NOTE]
> Para que as entradas de cmdlet <STRONG>Set-OutlookAnywhere</STRONG> , substitua "Meuservidor" pelo nome do seu servidor de acesso para cliente (es).



**Usando Set-WebConfigurationProperty**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
    iisreset /noforce

**Usando appcmd**


> [!NOTE]
> Para que as entradas do cmdlet <STRONG>Set-OutlookAnywhere</STRONG> , substitua "Meuservidor" pelo nome do seu servidor de acesso para cliente (es).



    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
    iisreset /noforce

Voltar ao início

## Configurando a coexistência do Exchange 2007 e do Exchange 2010

Durante um cenário de coexistência onde você tem um misto de servidores Exchange 2003 e Exchange 2010 na organização, uma das primeiras etapas que você precisa executar após implantar os Servidores de Acesso para Cliente do Exchange 2010 é alterar o DNS para que os usuários do Exchange 2003 acessem suas caixas de correio de um grupo de servidores de Acesso para Cliente do Exchange 2010. Nesse cenário, é completamente suportado habilitar o descarregamento SSL no balanceador de carga usado para distribuir o tráfego de clientes nos servidores de Acesso para Cliente.

**Coexistência com outras versões do Outlook Web App**

Com o descarregamento SSL configurado nos servidores de Acesso para Cliente do Exchange 2013, a coexistência funciona com o Exchange 2007 e o Exchange 2010:

  - Para coexistir com o Exchange 2007, um namespace anterior é necessário e o redirecionamento acontecerá a ele apenas para o Outlook Web App e Serviços da Web do Exchange. Descoberta Automática, Outlook em Qualquer Lugar e Exchange ActiveSynk terão proxy aplicado às versões anteriores.

  - Para coexistir com o Exchange 2010, se você tiver uma URL externa definida, um redirecionamento será usado. Caso contrário, um proxy será usado.

Voltar ao início

