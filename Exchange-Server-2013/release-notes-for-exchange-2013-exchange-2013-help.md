---
title: 'Notas de versão do Exchange 2013: Exchange 2013 Help'
TOCTitle: Notas de versão do Exchange 2013
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50485119
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notas de versão do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-04-16_

Bem-vindo ao Microsoft Exchange Server 2013 \! Este tópico contém informações importantes que você precisa saber para implantar o Exchange 2013 com êxito. Leia este tópico completamente antes de iniciar sua implantação.

Este tópico contém as seguintes seções:

  - Setup and deployment

  - Shell de gerenciamento do Exchange

  - Mailbox

  - Public folders

  - Mail flow

  - Client connectivity

  - Coexistência do Exchange 2010

## Configuração e implantação

  - **msExchProductId não reflete a versão de lançamento do Exchange 2013 instalado** Depois que o Exchange estende o esquema do Active Directory e prepara o Active Directory para o Exchange, várias propriedades são atualizadas para mostrar que a preparação está concluída. Uma dessas propriedades é *msExchangeProductId* sob o contêiner `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` no contexto de nomeação `Configuration` . Se nenhuma alteração de esquema do Active Directory é introduzidas na versão do Exchange 2013 que você está instalando, esta propriedade não será atualizada ou pode mostrar um valor inesperado. Isso poderia causar confusão se o valor não coincidir com a versão do Exchange 2013 está sendo instalado.
    
    Esse comportamento é esperado como o valor de *msExchProductId* não refletir a versão do Exchange 2013 está sendo instalado. Esta propriedade reflete a versão do Exchange 2013 que última feitas alterações de esquema do Active Directory. Para evitar confusão, recomendamos que você siga as etapas a [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) seção da [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md) para verificar se o seu Active Directory foi atualizado e está pronto para a versão do Exchange 2013 que você está instalando.

  - **A instalação solicita incorretamente .NET Framework 4.0** se você tentar instalar Exchange 2013 sem .NET Framework instalado no computador, a instalação solicita incorretamente que você instale o .NET Framework 4.0 quando, na verdade, .NET Framework 4.5 ou posterior é necessário.
    
    Para contornar esse problema, instale o .NET Framework 4.5 ou posterior. Você não precisa instalar .NET Framework 4.0. Para obter uma lista completa dos pré-requisitos, consulte [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - **Os arquivos de configuração XML do Exchange são substituídos durante a instalação da atualização cumulativa**   Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, arquivos web.config em servidores de Acesso para Cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, serão substituídos quando você instalar uma Atualização Cumulativa ou um Service Pack do Exchange. Certifique-se de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa ou um Service Pack do Exchange.

  - **Instalando o Exchange usando permissões de administrador delegado faz com que a falha na instalação** Quando um usuário que seja membro apenas delegada da configuração de grupo de função tenta instalar o Exchange em um servidor previamente provisionado, a instalação falhará. Isso acontece porque o grupo de instalação delegada não tem as permissões necessárias para criar e configurar determinados objetos no Active Directory.
    
    Para contornar esse problema, siga um destes procedimentos:
    
      - Adicione o usuário de instalação do Exchange ao grupo de segurança Administradores de domínio Active Directory.
    
      - Instale usando um usuário que seja membro do grupo de funções de gerenciamento da organização do Exchange.

Para obter mais informações sobre como instalar o Exchange 2013, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Shell de Gerenciamento do Exchange

  - **O Shell inesperadamente carrega o Exchange 2007 ou cmdlets do Exchange 2010** Anteriormente, abrir o Shell em um servidor Exchange 2013 for resultar no Shell abrir uma conexão para o servidor local ou em outro servidor executando o Exchange 2013. Quando a conexão é feita, o Exchange 2013 cmdlets são carregados. Iniciando com o Exchange 2013 CU11, o Shell se conectará ao servidor do Exchange onde está localizada a caixa de correio do usuário conectado. Se o usuário conectado não tiver uma caixa de correio, o Shell se conectará ao servidor em que a caixa de correio de arbitragem SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} está localizada. O servidor de destino pode ser qualquer versão com suporte do Exchange. Isso significa que se a caixa de correio do usuário conectado (ou a caixa de correio de arbitragem se o usuário não tem nenhuma caixa de correio) estiver localizada em um servidor Exchange 2010, o Shell irá se conectar a esse servidor e cmdlets do Exchange 2010 de carga. Isso pode impedir que você realizar determinadas tarefas porque os cmdlets do Exchange 2010 não é possível gerenciar a configuração do Exchange 2013 ou servidores.
    
    Iniciando com o Exchange 2013 CU11, esse comportamento é por design. Para certificar-se de que o Shell carrega os cmdlets do Exchange 2013, mova o fez logon na caixa de correio do usuário para o Exchange 2013. Se o usuário conectado não tiver uma caixa de correio, mova a caixa de correio de arbitragem SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} para um servidor Exchange 2013.
    
    Para obter informações sobre como mover a caixa de correio de arbitragem e obter detalhes, consulte [Exchange Management Shell e ancoragem de caixa de correio](https://go.microsoft.com/fwlink/?linkid=717722) no blog da equipe do Exchange.

## Caixa de Correio

  - **Servidores de caixa de correio executando versões diferentes do Exchange podem ser adicionados ao mesmo grupo de disponibilidade de banco de dados** O cmdlet **Add-DatabaseAvailabilityGroupServer** e Exchange Admin Center incorretamente permitem que um servidor de Exchange 2013 a ser adicionado a um Exchange 2016-com base em grupo de disponibilidade do banco de dados (DAG) e vice-versa. O Exchange oferece suporte a adição de servidores de caixa de correio únicos executando a mesma versão (Exchange 2013 versus Exchange 2016, por exemplo) para um DAG. Além disso, o Centro de administração do Exchange exibe servidores Exchange 2013 e o Exchange 2016 na lista de servidores disponíveis para adicionar a um DAG. Isso pode permitir que um administrador adicione inadvertidamente um servidor executando uma versão incompatível do Exchange para um DAG (por exemplo, adicionando um servidor Exchange 2013 para um Exchange 2016-based DAG).
    
    No momento, não há nenhuma solução alternativa para esse problema. Os administradores devem ser persistente ao adicionar um servidor de caixa de correio para um DAG. Adicionar apenas os servidores de Exchange 2013 a Exchange 2013-com base DAGs e apenas os servidores de Exchange 2016 para Exchange 2016-based DAGs. Você pode diferenciar cada versão do Exchange examinando a coluna **versão** na lista de servidores no Centro de administração do Exchange. Estas são as versões de servidor para Exchange 2013 e Exchange 2016:
    
      - **Exchange 2013** 15.0 (compilação xxx.xx)
    
      - **Exchange 2016** 15.1 (compilação xxx.xx)

  - **Aumento de tamanho das caixas de correio ao migrar de versões anteriores do Exchange**   Ao mover uma caixa de correio de uma versão anterior do Exchange para o Exchange 2013, o tamanho relatado da caixa de correio pode aumentar de 30% a 40%. O espaço usado pelo banco de dados de caixas de correio não aumentou, somente a atribuição de espaço usado por cada caixa de correio. O aumento no tamanho da caixa de correio se deve à inclusão de todas as propriedades de itens no cálculo da cota, o que proporciona um computação mais precisa do espaço ocupado por itens dentro da caixa de correio. Esse aumento pode fazer que alguns usuários excedam suas cotas de tamanho de caixa de correio quando a caixa deles é movida para o Exchange 2013.
    
    Para evitar que os usuários excedam suas cotas de tamanho de caixa de correio, aumente os valores de cota do banco de dados ou das caixas de correio para acomodar o novo cálculo de cota. Para configurar os valores de cota de caixa de correio ou do banco de dados, use os parâmetros *IssueWarningQuota*, *ProhibitSendQuota* e *ProhibitSendReceiveQuota* nos cmdlets **Set-MailboxDatabase** e **Set-Mailbox**, respectivamente.

  - **Talvez os clientes do Outlook 2007 e do Outlook 2010 não consigam baixar o Catálogo de Endereços Offline**   Se a URL interna do Catálogo de Endereços Offline (OAB) não puder ser acessada da Internet, talvez os clientes do Outlook 2007 e do Outlook 2010 não consigam baixar o OAB.
    
    Para contornar esse problema em clientes do Outlook 2007 e do Outlook 2010, torne a URL interna do OAB acessível pela Internet. O Outlook 2013 não é afetado pelo problema.

  - **A instalação do Exchange 2013 em uma organização existente do Exchange pode fazer com que todos os clientes baixem o OAB**    A instalação do primeiro servidor do Exchange 2013 em uma organização existente do Exchange 2007 ou do Exchange 2010 pode fazer com que todos os clientes na organização baixem uma nova cópia do OAB, causando saturação da rede e problemas de desempenho do servidor. Esse problema ocorre porque o Exchange 2013 cria um novo OAB padrão na organização que substitui o OAB do Exchange 2007 ou do Exchange 2010. As caixas de correio que não têm um OAB específico atribuído, ou que estão localizadas em um banco de dados de caixa de correios que não tem um OAB específico atribuído, baixarão o novo OAB padrão.
    
    Para impedir que os clientes baixem uma nova cópia do OAB quando o Exchange 2013 é instalado, atribua um OAB a cada caixa de correio ou ao banco de dados da caixa de correio onde as caixas estão localizadas. Isso precisa ser feito antes de o Exchange 2013 ser instalado na organização.

  - **Os usuários poderão ser roteados para uma caixa de correio de geração de OAB não responsável para o OAB solicitado** Exchange 2013 CU5 e posteriores CUs foram alteradas como OABs são vinculadas às caixas de correio de geração de OAB. Essa alteração torna possível a um usuário sejam roteadas para uma caixa de correio de geração de OAB que não é responsável pelo OAB que o usuário está solicitando. Isso pode acontecer se todos os itens a seguir forem verdadeiras:   
    
      - Você tem mais de uma caixa de correio de geração de OAB em sua organização.
    
      - Você atualizou os servidores de Caixa de correio que hospedam as caixas de correio de geração de OAB antes de atualizar seus servidores de Acesso para Cliente.
    
      - Você está atualizando seus servidores de Exchange 2013 a partir de uma versão anterior ao CU5 para uma versão posterior (por exemplo, atualizando do Exchange 2013 CU3 para Exchange 2013 CU6).
    
      - Os servidores de Acesso para Cliente estão executando uma versão anterior ao CU5.
    
    Para contornar esse problema, certifique-se de que você atualizar seus servidores de acesso para cliente para Exchange 2013 CU6 ou posterior antes de atualizar seus servidores de caixa de correio. Isso irá assegurar que os servidores de acesso para cliente saber como proxy as solicitações para a caixa de correio de geração do OAB que é responsável por gerar o OAB do usuário.
    
    Para ler mais sobre as alterações no OAB no Exchange 2013 CU5, consulte [Aprimoramentos do OAB no Exchange 2013 cumulativa atualização 5](https://go.microsoft.com/fwlink/p/?linkid=400642).

## Pastas públicas

  - **Remetentes não autorizados não podem mais enviar mensagens a pastas públicas habilitadas para email**   Antes de CU6 do Exchange 2013, remetentes não autorizados podem enviar mensagens a pastas públicas habilitadas para email. Isso permitido a possibilidade de remetentes externos enviar emails para pastas públicas habilitadas para email independentemente das permissões definidas na pasta pública.
    
    Iniciando com CU6 do Exchange 2013, se desejar que os remetentes externos para enviar email a um pastas públicas habilitadas para email, o usuário **anônimo** deve ser concedida pelo menos a permissão de **Criar itens**. Se você configurou as pastas públicas habilitadas para email e ainda não tiver feito isso, os remetentes externos receberá uma notificação de falha de entrega e as mensagens não será entregue para a pasta pública habilitada para email.
    
    Você pode usar o Shell ou o Outlook para definir as permissões do usuário anônimo. Para ler mais sobre como definir permissões em que o usuário anônimo, consulte [Email habilitar ou desabilitar email uma pasta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - O número máximo de pastas públicas que podem ser migradas para o Exchange 2013 de servidores Exchange herdados é 500.000. Para obter mais informações sobre migração de pastas públicas, consulte [Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md).

## Fluxo de mensagens

  - **Os cmdlets TransportAgent nos servidores de Acesso para Cliente exigem o Windows PowerShell local**  Existe um problema nos cmdlets **\*-TransportAgent** que os impede de instalar, desinstalar e gerenciar agentes de transporte em servidores de Acesso para Cliente usando o Shell de Gerenciamento do Exchange. Para instalar, desinstalar e gerenciar agentes de transporte em servidores de Acesso para Cliente, é necessário carregar manualmente o snap-in do Windows PowerShell do Exchange e executar os cmdlets **\*-TransportAgent**. Se você tentar instalar, desinstalar ou gerenciar agentes de transporte usando o Shell de Gerenciamento do Exchange, as suas alterações serão aplicadas ao servidor de Caixa de Correio do Exchange 2013 ao qual estiver conectado.
    
    Para instalar, desinstalar ou gerenciar agentes de transporte em servidores de Acesso para Cliente, faça o seguinte no servidor de Acesso para Cliente que deseja gerenciar:
    

    > [!WARNING]
    > O carregamento do snap-in do Windows PowerShell do <CODE>Microsoft.Exchange.Management.PowerShell.SnapIn</CODE> e a execução de cmdlets que não sejam <STRONG>*-TransportAgent</STRONG> não é suportado e pode resultar em dano irreparável à sua implantação do Exchange.<BR>É necessário ser um Administrador local no servidor de Acesso para Cliente em que você deseja instalar, desinstalar ou gerenciar agentes de transporte. Não oferecemos suporte à modificação de listas de controle de acesso (ACLs) em arquivos, diretórios ou objetos do Active Directory no Exchange.

    

    > [!IMPORTANT]
    > Execute o procedimento a seguir apenas em servidores de Acesso para Cliente. Não é necessário carregar o snap-in do Windows PowerShell do Exchange se quiser gerenciar agentes de transporte em servidores de Caixa de Correio.

    
    1.  Abra uma nova janela do Windows Power Shell.
    
    2.  Execute o seguinte comando.
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  Execute tarefas de gerenciamento de agente de transporte normalmente.
    
    4.  Repita este procedimento em cada servidor de Acesso para Cliente que deseja gerenciar.

## Conectividade de cliente

  - **A autenticação NTLM falha para clientes não pertencentes ao domínio**   A autenticação entre um cliente, como o Windows Live Mail, e o Exchange 2013 pode falhar quando as seguintes condições são verdadeiras:
    
      - Então, o método de autenticação que o cliente usa é NTLM.
    
      - O computador não ingressou no domínio.
    
    Para contornar esse problema, execute um destes procedimentos:
    
      - Ingresse o computador em que o cliente está em execução no domínio.
    
      - Altere o tipo de autenticação que o cliente usa de NTLM para autenticação Básica por TLS.

  - **A autenticação GSSAPI falha quando usada com o cmdlet Send-MailMessage**   A autenticação GSSAPI (Generic Security Service Application Program Interface, Interface de programação de aplicativo do serviço de segurança genérico) pode falhar quando o cmdlet **Send-MailMessage**, que está incluído na instalação padrão do Windows PowerShell, é usado para enviar emails autenticados para o Exchange 2013. Quando isso acontece, uma entrada será exibida no log de eventos **Aplicativo** no servidor de Acesso para Cliente no Exchange 2013 que recebeu a conexão com as seguintes informações:
    
      - **Origem**   MSExchangeFrontEndTransport
    
      - **ID do Evento**   1035
    
      - **Descrição**   Falha na autenticação de entrada com o erro `IllegalMessage` para o front-end cliente do conector de recebimento \<*nome do servidor*\>. O mecanismo de autenticação é Gssapi. O endereço IP de origem do cliente que tentou se autenticar no Exchange é \[\<*endereço IP do cliente*\>\].
    
    Para contornar esse problema, é preciso remover o método de autenticação `Integrated` do conector de recebimento do cliente nos servidores de Acesso para Cliente do Exchange 2013. Para remover o método de autenticação `Integrated` de um conector de recebimento cliente, execute o seguinte comando em cada servidor de Acesso para Cliente do Exchange 2013 que poderia receber conexões de computadores executando o cmdlet **Send-MailMessage**:
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **MAPI sobre HTTP pode ter um baixo desempenho ao atualizar para o Exchange 2013 SP1**   Se você atualizar de uma atualização cumulativa do Exchange 2013 para o Exchange 2013 SP1 e habilitar o MAPI sobre HTTP, os clientes que se conectam a um servidor do Exchange 2013 SP1 usando o protocolo poderão ter baixo desempenho. Isso acontece porque as configurações necessárias não são definidas durante uma atualização cumulativa para o Exchange 2013 SP1. Esse problema não ocorrerá se você atualizar para o Exchange 2013 SP1 do Exchange 2013 RTM ou se você instalar um novo servidor do Exchange 2013 SP1 ou mais recente.
    

    > [!TIP]
    > Isso só será um problema caso o protocolo MAPI sobre HTTP esteja habilitado em seus servidores de Acesso para Cliente. Ele está desabilitado por padrão. Se MAPI sobre HTTP estiver desabilitado, os clientes usarão o protocolo RPC sobre HTTP.

    
    Para contornar este problema, proceda da seguinte forma:
    
    1.  Em servidores que executam a função de servidor de Acesso para Cliente, execute os seguintes comandos em um Prompt de Comando do Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  Em servidores que executam a função de servidor de Caixa de Correio, execute os seguintes comandos em um Prompt de Comando do Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Coexistência com o Exchange 2010

  - **As solicitações para acessar caixas de correio do Exchange 2010 talvez não funcionem se houver proxy por meio de servidores de Acesso para Cliente do Exchange 2013**   Em alguns casos, a solicitação de proxy entre os servidores de Acesso para Cliente do Exchange 2013 e do Exchange 2010 Service Pack 3 (SP3), sem a instalação de qualquer pacote cumulativo de atualizações, pode não funcionar corretamente e gerar erros. isso pode acontecer se todas as condições a seguir forem verdadeiras:
    
      - Um usuário com uma caixa de correio do Exchange 2013 tenta abrir uma caixa de correio do Exchange 2010 usando um dos seguintes métodos:
        
          - A opção **Abrir Outra Caixa de Correio** no Outlook Web App**-OU-**
        
          - A opção **Outro usuário** no Centro de administração do Exchange
    
      - O servidor de Acesso para Cliente ao qual o usuário está conectado está executando o Exchange 2013.
    
      - O servidor de Acesso para Cliente do Exchange 2010 foi atualizado para o Exchange 2010 SP3 da versão RTM (release to manufacturing) do Exchange 2010 ou um service pack anterior do Exchange 2010.
    
    Se todas as condições acima forem verdadeiras, o usuário não poderá acessar as opções do Exchange 2010Outlook Web App do outro usuário e uma página em branco poderá aparecer.
    
    Para contornar esse problema, instale o Pacote Cumulativo de Atualizações 1 do Exchange 2010 SP3 ou posterior em cada servidor do Exchange 2010.

