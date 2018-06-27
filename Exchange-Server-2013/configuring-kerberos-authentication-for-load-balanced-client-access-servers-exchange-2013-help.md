---
title: 'Configurando a autenticação Kerberos para servidores de acesso para cliente com balanceamento de carga: Exchange 2013 Help'
TOCTitle: Configurando a autenticação Kerberos para servidores de acesso para cliente com balanceamento de carga
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835910
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando a autenticação Kerberos para servidores de acesso para cliente com balanceamento de carga

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

**Resumo:** Descreve como usar a autenticação Kerberos com servidores de acesso para cliente com balanceamento de carga no Exchange 2013.

Em ordem para utilizar a autenticação Kerberos com servidores de acesso para cliente com balanceamento de carga, você precisará concluir as etapas de configuração descritas neste artigo.

## Criar a credencial de conta de serviço alternativa nos serviços de domínio Active Directory

Todos os servidores de acesso para cliente que compartilham os mesmos namespaces e URLs precisam usar as mesmas credenciais de conta de serviço alternativa. Em geral, é suficiente para ter uma única conta para uma floresta de cada versão do Exchange. *credenciais de conta de serviço alternativa* ou *credencial ASA*.


> [!IMPORTANT]
> Exchange 2010 e Exchange 2013 não podem compartilhar a mesma credencial ASA. Você precisa criar uma nova credencial ASA para o Exchange 2013.




> [!IMPORTANT]
> Enquanto os registros CNAME são suportados para namespaces compartilhados, a Microsoft recomenda o uso de registros. Isso garante que o cliente corretamente emite uma solicitação de tíquete Kerberos com base no nome compartilhado e não o FQDN do servidor.



Quando você configura a credencial ASA, lembre-se estas diretrizes:

  - **Tipo de conta.** Recomendamos que você crie uma conta de computador, em vez de uma conta de usuário. Uma conta de computador não permite logon interativo e pode ter diretivas de segurança mais simples do que uma conta de usuário. Se você criar uma conta de computador, a senha não expirará, mas recomendamos que você atualizar a senha periodicamente mesmo assim. Você pode usar a diretiva de grupo local para especificar uma duração máxima para a conta de computador e scripts periodicamente excluir contas de computador que não atendem a políticas atuais. Sua política de segurança local também determina quando você precisa alterar a senha. Embora seja recomendável que você use uma conta de computador, você pode criar uma conta de usuário.

  - **Nome da conta.** Existem requisitos para o nome da conta. Você pode usar qualquer nome que esteja de acordo com seu esquema de nomenclatura.

  - **Grupo de conta.** A conta usada para a credencial ASA não precisa de privilégios de segurança especiais. Se você estiver usando uma conta de computador, em seguida, a conta só precisa ser membro do grupo de segurança de computadores de domínio. Se você estiver usando uma conta de usuário, em seguida, a conta só precisa ser membro do grupo de segurança usuários do domínio.

  - **Senha da conta.** A senha que você fornece ao criar a conta será usada. Portanto, ao criar a conta, você deve usar uma senha complexa e certifique-se de que a senha está em conformidade com os requisitos de senha da sua organização.

Para criar a credencial ASA como uma conta de computador

1.  Em um computador associado ao domínio, execute o Windows PowerShell ou o Shell de gerenciamento do Exchange.
    
    Use o cmdlet **Import-Module** para importar o módulo do Active Directory.
    
        Import-Module ActiveDirectory

2.  Use o cmdlet **New-ADComputer** para criar uma nova conta de computador do Active Directory usando esta sintaxe do cmdlet:
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **Exemplo:**
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    Onde *EXCH2013ASA* é o nome da conta, a descrição *Alternate Service Account credentials for Exchange* é o que quiser seja e o valor para o parâmetro *SamAccountName* , neste caso, *EXCH2013ASA*, precisa ser exclusivo em seu diretório.

3.  Use o cmdlet **Set-ADComputer** para habilitar o suporte de codificação de criptografia AES 256 usado por Kerberos usando esta sintaxe do cmdlet:
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **Exemplo:**
    
        Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    
    Onde *EXCH2013ASA* é o nome da conta e o atributo a ser modificada é *msDS-SupportedEncryptionTypes* com um valor decimal de 28, que permite que as seguintes codificações: RC4-HMAC, AES128-CTS-HMAC-SHA1-96, AES256-CTS-HMAC-SHA1-96.

Para obter mais informações sobre esses cmdlets, consulte [Import-Module](https://technet.microsoft.com/library/hh849725.aspx) e [New-ADComputer](https://technet.microsoft.com/library/ee617245.aspx).

## Cenários de entre florestas

Se você possuir uma implantação entre florestas ou floresta de recursos, e você tiver usuários que estão fora da floresta Active Directory que contém Exchange, você precisará configurar relações de confiança de floresta entre as florestas. Além disso, para cada floresta na implantação, você precisará configurar uma regra de roteamento que permite a relação de confiança entre todos os sufixos de nome dentro da floresta e entre florestas. Para obter mais informações sobre como gerenciar relações de confiança entre florestas, consulte [Managing relações de confiança de floresta](https://technet.microsoft.com/library/cc772440.aspx).

## Identificar os nomes de entidade de serviço para associar a credencial ASA

Depois de criar a credencial ASA, você precisa associar Exchange nomes de entidade de serviço (SPNs) a credencial ASA. A lista de Exchange SPNs variam de acordo com sua configuração, mas deve incluir pelo menos o seguinte:

  - **http /**   Use esse SPN para o Outlook em qualquer lugar, MAPI sobre HTTP, serviços Web do Exchange, descoberta automática e catálogo de Endereços Offline.

Os valores SPN precisam corresponder ao nome de serviço no balanceador de carga de rede em vez de em servidores individuais. Para ajudar a planejar quais valores SPN, você deve usar, considere os seguintes cenários:

  - Site único do Active Directory

  - Vários sites do Active Directory

Em cada um desses cenários, pressupõem que os nomes de domínio totalmente qualificado com balanceamento de carga (FQDNs) foram implantados para as URLs internas, URLs externas e a descoberta automática interno URI usado pelos membros de servidor de acesso para cliente. Para obter mais informações, consulte redirecionamento e proxy Understanding.

## Site único do Active Directory

Se você tiver um único site do Active Directory, seu ambiente pode se parecer com aquele na figura a seguir:

![Matriz CAS com AD único e autenticação Kerberos](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "Matriz CAS com AD único e autenticação Kerberos")

Com base nos FQDNs que são usados pelos clientes Outlook internos na figura anterior, você precisa associar os seguintes SPNs a credencial ASA:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## Vários sites do Active Directory

Se você tiver vários sites do Active Directory, seu ambiente pode se parecer com aquele na figura a seguir:

![Matriz CAS com vários sites AD e autenticação Kerberos](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "Matriz CAS com vários sites AD e autenticação Kerberos")

Com base nos FQDNs que são usados pelos clientes do Outlook na figura anterior, você precisaria associar os seguintes SPNs a credencial ASA que é usada pelos servidores de acesso para cliente no ADSite 1:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

Você também precisaria associar os seguintes SPNs a credencial ASA que é usada pelos servidores de acesso para cliente no ADSite 2:

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## Configurar e, em seguida, verifique se a configuração da credencial ASA em cada servidor de acesso para cliente

Depois que você criou a conta, você precisará verificar se a conta tem replicadas para todos os controladores de domínio do AD DS. Especificamente, a conta precisa estar presentes em cada servidor de acesso para cliente que usará a credencial ASA. Em seguida, configure a conta como a credencial ASA em cada servidor de acesso para cliente em sua implantação.

Você pode configurar a credencial ASA usando o Shell de gerenciamento do Exchange, conforme descrito em um dos seguintes procedimentos:

  - Implantar a credencial ASA no primeiro servidor de acesso para cliente do Exchange 2013

  - Implantar a credencial ASA para servidores de acesso para cliente do Exchange 2013 subsequentes

O único método suportado para implantar a credencial ASA é usar o script RollAlternateServiceAcountPassword.ps1. Para obter mais informações, consulte [Usando o Script de RollAlternateserviceAccountCredential.ps1 no Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md). Depois que o script foi executado, é recomendável verificar se todos os servidores de destino foram atualizados corretamente.

## Implantar a credencial de ASA no primeiro servidor de acesso para cliente do Exchange 2013

1.  Abra o Shell de gerenciamento do Exchange em um servidor Exchange 2013.

2.  Altere os diretórios para *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Execute o comando a seguir para implantar a credencial ASA no primeiro servidor de acesso para cliente do Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  Quando for perguntado se deseja alterar a senha da conta de serviço alternativo, clique em **Sim**.

O exemplo a seguir é um exemplo da saída que tem mostrado ao executar o script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Implantar a credencial ASA para outro servidor de acesso para cliente do Exchange 2013

1.  Abra o Shell de gerenciamento do Exchange em um servidor Exchange 2013.

2.  Altere os diretórios para *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Execute o comando a seguir para implantar a credencial ASA para outro servidor de acesso para cliente do Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  Repita a etapa 3 para cada servidor de acesso para cliente que você deseja implantar as credenciais a serem ASA.

O exemplo a seguir é um exemplo da saída que tem mostrado ao executar o script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Verifique se a implantação da credencial ASA

  - Abra o Shell de gerenciamento do Exchange em um servidor Exchange 2013.

  - Execute o seguinte comando para verificar as configurações em um servidor de acesso para cliente:
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - Repita a etapa 2 em cada servidor de acesso para cliente onde você deseja verificar a implantação da credencial ASA.

O exemplo a seguir é um exemplo da saída que tem mostrados quando você executar o comando Get-ClientAccessServer acima e nenhuma credencial ASA anterior foi definida.

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

O exemplo a seguir é um exemplo da saída que tem mostrados quando você executar o comando Get-ClientAccessServer acima e uma credencial ASA definida anteriormente. A credencial ASA anterior e a data e hora que ele foi definido são retornadas.

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## Associar nomes de entidade de serviço (SPNs) a credencial ASA


> [!IMPORTANT]
> Não associe SPNs uma credencial ASA até que você implantou essa credencial pelo menos um servidor do Exchange, conforme descrito anteriormente em Deploy a credencial de ASA no primeiro servidor de acesso para cliente do Exchange 2013. Caso contrário, você irá enfrentar erros de autenticação Kerberos.



Antes de associar os SPNs com a credencial ASA, você precisará verificar se o destino SPNs não já estejam associados a uma conta diferente na floresta. A credencial ASA precisa ser a única conta na floresta com os quais essas SPNs estão associados. Você pode verificar que nenhuma outra conta na floresta está associada os SPNs executando o comando **setspn** da linha de comando.

Verifique se que um SPN não ainda estiver associado a uma conta em uma floresta executando o comando setspn

1.  Pressione **Iniciar**. Na caixa **Pesquisar**, digite o **Prompt de comando**, em seguida, na lista de resultados, selecione **Prompt de comando**.

2.  No prompt de comando, digite o seguinte comando:
    
        setspn -F -Q <SPN>
    
    Onde \< SPN \> é o SPN que você deseja associar a credencial ASA. Por exemplo:
    
        setspn -F -Q http/mail.corp.tailspintoys.com
    
    O comando deve retornar nothing. Se ela retorna algo, outra conta já está associada com o SPN. Repita essa etapa uma vez para cada SPN para o qual você deseja associar a credencial ASA.

Associar um SPN uma credencial ASA usando o comando setspn

1.  Pressione **Iniciar**. Na caixa **Pesquisar**, digite o **Prompt de comando**, em seguida, na lista de resultados, selecione **Prompt de comando**.

2.  No prompt de comando, digite o seguinte comando:
    
        setspn -S <SPN> <Account>$
    
    Onde \< SPN \> é o SPN que você deseja associar a credencial ASA e \< conta \> é a conta associada a credencial ASA. Por exemplo:
    
        setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    
    Uma vez para cada SPN para o qual você deseja associar a credencial ASA, execute este comando.

Verifique se que você associados os SPNs as credenciais ASA usando o comando setspn

1.  Pressione **Iniciar**. Na caixa **Pesquisar**, digite o **Prompt de comando**, em seguida, na lista de resultados, selecione **Prompt de comando**.

2.  No prompt de comando, digite o seguinte comando:
    
        setspn -L <Account>$
    
    Onde \< conta \> é a conta associada a credencial ASA. Por exemplo:
    
        setspn -L tailspin\EXCH2013ASA$
    
    Você precisará executar este comando uma vez.

## Habilitar a autenticação Kerberos para clientes do Outlook

1.  Abra o Shell de gerenciamento do Exchange em um servidor Exchange 2013.

2.  Para habilitar a autenticação Kerberos para clientes do Outlook em qualquer lugar, execute o seguinte comando no seu servidor de acesso para cliente:
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  Para habilitar a autenticação Kerberos para MAPI sobre HTTP clientes, execute o seguinte em seu servidor de acesso para cliente do Exchange 2013:
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  Repita as etapas 2 e 3 para cada servidor de acesso para cliente do Exchange 2013 onde você deseja habilitar a autenticação Kerberos.

## Validar a autenticação de Kerberos de cliente do Exchange

Depois que você configurou com êxito Kerberos e a credencial ASA, verifique se que os clientes podem autenticar com êxito, conforme descrito nessas tarefas.

## Verifique se o serviço de Host de serviço do Microsoft Exchange está em execução

O serviço de Host de serviço do Microsoft Exchange (MSExchangeServiceHost) no servidor de acesso para cliente é responsável pelo gerenciamento da credencial ASA. Se esse serviço não está em execução, a autenticação Kerberos não é possível. Por padrão, o serviço é configurado para ser iniciado automaticamente quando o computador inicia.

Para verificar se o serviço de Host de serviço do Microsoft Exchange foi iniciado

1.  Clique em **Iniciar**, digite **Services. msc** e, em seguida, selecione **Services. msc** na lista.

2.  Na janela **Serviços**, localize o serviço de **Host de serviço do Microsoft Exchange** na lista de serviços.

3.  O status do serviço deve estar **executando**. Se o status não está **sendo executado**, clique com o botão direito e clique em **Iniciar**.

## Validar Kerberos a partir do servidor de acesso para cliente

Quando você configurou a credencial ASA em cada servidor de acesso para cliente, você executou o cmdlet **set-ClientAccessServer** . Depois de executar esse cmdlet, você pode usar os logs para verificar as conexões de Kerberos bem-sucedidas.

Para validar que o Kerberos está funcionando corretamente usando o arquivo de log HttpProxy

1.  Em um editor de texto, navegue até a pasta onde o log de HttpProxy é armazenado. Por padrão, o log é armazenado na seguinte pasta:
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  Abra o arquivo de log mais recente e procure a palavra **negociar**. A linha no arquivo de log se parecerá com o exemplo a seguir:
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    Se você vir o valor de **AuthenticationType** é **negociar**, então, o servidor está conexões autenticadas com êxito a criação de Kerberos.

## Manter a credencial ASA

Se você precisar atualizar a senha na credencial ASA periodicamente, use as etapas para configurar a credencial ASA neste artigo. Considere a possibilidade de configurar uma tarefa agendada para executar a manutenção de senha regular. Certifique-se de monitorar a tarefa agendada para garantir a sobreposições de senha em tempo hábil e evitar interrupções de autenticação possíveis.

## Desativar a autenticação Kerberos

Para configurar seu servidor de acesso para cliente para que ele não usa Kerberos, desassociar ou remova os SPNs a credencial ASA. Se os SPNs forem removidos, a autenticação Kerberos não ser tentada por seus clientes e clientes configurados para usar a autenticação negociar usarão NTLM em vez disso. Clientes configurados para usar apenas Kerberos poderão se conectar. Depois que os SPNs são removidos, você também deve excluir a conta.

Para remover a credencial ASA

1.  Abra o Shell de gerenciamento do Exchange em um servidor Exchange 2013 e execute o seguinte comando:
    
        Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials

2.  Embora não seja necessário fazer isso imediatamente, você deve reiniciar eventualmente todos os computadores cliente para limpar o cache de tíquetes Kerberos do computador.

