---
title: 'Inscrições de Borda: Exchange 2013 Help'
TOCTitle: Inscrições de Borda
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61183349
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inscrições de Borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Servidores de Transporte de Borda minimizam a superfície de ataque processando todo o fluxo de mensagens voltado para a Internet e fornecendo retransmissão de SMTP e serviços de host inteligente para a organização do Exchange. Camadas adicionais de proteção de mensagem e de segurança são fornecidas por vários agentes em execução no servidor de Transporte de Borda na rede de perímetro de sua organização. Esses agentes oferecem suporte a recursos que fornecem proteção contra vírus e spam e aplicam regras de transporte ao controle de fluxo de mensagens.

Inscrições de Borda são utilizadas para preencher a instância do AD LDS (Lightweight Directory Services) no servidor de Transporte de Borda com dados do Active Directory. Embora criar uma Inscrição de Borda seja opcional, inscrever um servidor de Transporte de Borda na organização do Exchange fornece uma experiência de gerenciamento mais simples para o administrador e melhora os recursos antispam. Você deverá criar uma Inscrição de Borda se planejar usar pesquisa de destinatário ou agregação de lista segura, ou se planejar ajudar a proteger as comunicações SMTP com domínios de parceiros usando MTLS (Mutual Transport Layer Security).

**Conteúdo**

Edge Subscription Process

Microsoft Exchange EdgeSync Service

Managing Edge Subscriptions

## Processo de Inscrição de Borda

Um servidor de Transporte de Borda não tem acesso direto ao Active Directory. As informações de configuração e de destinatário que o servidor de Transporte de Borda usa para processar mensagens estão armazenadas no AD LDS. A criação de uma Inscrição de Borda estabelece uma replicação segura e automática de informações do Active Directory para o AD LDS. O processo de Inscrição de Borda fornece as credenciais usadas para estabelecer uma conexão LDAP segura entre servidores de Caixa de Correio do Exchange 2013 e um servidor de Transporte de Borda inscrito. O serviço Microsoft Exchange EdgeSync (EdgeSync) executado em servidores de Caixa de Correio realiza a sincronização unidirecional para transferir dados atualizados para o AD LDS. Isso reduz as tarefas administrativas realizadas na rede de perímetro permitindo que você configure o servidor de Caixa de Correio e, então, sincronize essas informações com o servidor de Transporte de Borda.

Inscreva um servidor de Transporte de Borda no site do Active Directory que contém os servidores de Caixa de Correio responsáveis pela transferência de mensagens de e para seus servidores de Transportes de Borda. O processo de Inscrição de Borda cria uma afiliação de associação do site do Active Directory para o servidor de Transporte de Borda. A afiliação de site permite que os servidores de Caixa de Correio da organização do Exchange retransmitam mensagens ao servidor de Transporte de Borda para que sejam entregues na Internet, sem necessidade de configurar conectores de Envio explícitos.

Você pode inscrever um ou mais servidores de Transporte de Borda em um único site do Active Directory. Entretanto, um servidor de Transporte de Borda não pode ser inscrito em mais de um site do Active Directory. Se você tiver mais de um servidor de Transporte de Borda implantado, cada servidor poderá ser inscrito em um site diferente do Active Directory. Cada servidor de Transporte de Borda requer uma Inscrição de Borda individual.

Para implantar um servidor de Transporte de Borda e inscrevê-lo em um site do Active Directory, siga estas etapas:

1.  Instale a função de servidor Transporte de Borda.

2.  Verifique se os servidores de Caixa de Correio e o servidor de Transporte de Borda podem localizar um ao outro utilizando a resolução de nomes DNS.

3.  No servidor de Caixa de Correio, configure os objetos e defina as configurações a serem replicadas para o servidor de Transporte de Borda.

4.  Na função de servidor Transporte de Borda, exporte o arquivo de Inscrição de Borda.

5.  Copie o arquivo de Inscrição de Borda em um servidor de Caixa de Correio ou em um compartilhamento de arquivos que seja acessível do site do Active Directory que contém seus servidores de Caixa de Correio.

6.  Importe um arquivo de Inscrição de Borda para um site do Active Directory.

## O que acontece quando você cria uma nova Inscrição de Borda

Quando você cria um arquivo de Inscrição de Borda (executando o cmdlet **New-EdgeSubscription** no servidor de Transporte de Borda), ocorre o seguinte:

  - Uma conta do AD LDS que chamou a conta de replicação de inicialização do EdgeSync (ESBRA) é criada. Estas credenciais ESBRA são usadas para autenticar a primeira conexão do EdgeSync com o servidor de Transporte de Borda. Essa conta está configurada para expirar 24 horas após sua criação. Portanto, é necessário concluir o processo de inscrição de seis etapas descrito na seção anterior em até 24 horas. Se a ESBRA expirar antes da conclusão do processo de Inscrição de Borda, será necessário executar o cmdlet **New-EdgeSubscription** no servidor de Transporte de Borda novamente para criar um novo arquivo de Inscrição de Borda.

  - As credenciais da ESBRA são recuperadas do AD LDS e gravadas no arquivo de Inscrição de Borda. A chave pública do certificado auto-assinado do servidor de Transporte de Borda também é exportada para o arquivo de Inscrição de Borda. As credenciais gravadas no servidor de Transporte de Borda são específicas para o servidor do qual o arquivo foi exportado.

  - Quaisquer objetos de configuração criados anteriormente no servidor de Transporte de Borda, que agora serão replicados para o AD LDS do Active Directory, serão excluídos do AD LDS e os cmdlets do Shell de Gerenciamento do Exchange usados para configurar esses objetos serão desabilitados. Entretanto, você ainda poderá usar os cmdlets **Get-\*** para exibir esses objetos. A execução do cmdlet **New-EdgeSubscription** desabilita os seguintes cmdlets no servidor de Transporte de Borda:
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

Quando você importa o arquivo de Inscrição de Borda no servidor de Caixa de Correio (executando o cmdlet **New-EdgeSubscription** no servidor de Caixa de Correio):

  - A Inscrição de Borda é criada, fazendo o ingresso do servidor de Transporte de Borda em uma organização do Exchange. O EdgeSync propagará dados de configuração para este servidor de Transporte de Borda, criando um objeto de configuração de Borda no Active Directory.

  - Todos os servidores de Caixa de Correio no site do Active Directory recebem uma notificação do Active Directory de que um novo servidor de Transporte de Borda foi inscrito. O servidor de Caixa de Correio recupera a ESBRA do arquivo de Inscrição de Borda. Em seguida, o servidor de Caixa de Correio criptografa a ESBRA usando a chave pública do certificado autoassinado do servidor de Transporte de Borda. As credenciais criptografadas são gravadas no objeto de configuração de Borda.

  - Cada servidor de Caixa de Correio também criptografa a ESBRA usando sua própria chave pública e armazena as credenciais em seu próprio objeto de configuração.

  - As contas de replicação do EdgeSync (ESRAs) são criadas no Active Directory para cada par de servidores de Transporte de Borda-Caixa de Correio. Cada servidor de Caixa de Correio armazena suas credenciais de ESRA como um atributo do objeto de configuração do servidor de Caixa de Correio.

  - Conectores de envio são criados automaticamente para retransmitir mensagens de saída do servidor de Transporte de Borda para a Internet, e de entrada do servidor de Transporte de Borda para a organização do Exchange.

  - O serviço do EdgeSync do Microsoft Exchange, que é executado em servidores de Caixa de Correio, usa as credenciais da ESBRA para estabelecer uma conexão LDAP segura entre um servidor de Caixa de Correio e o servidor de Transporte de Borda e realiza a replicação inicial de dados. Os seguintes dados são replicados para o AD LDS:
    
      - Dados de topologia
    
      - Dados de configuração
    
      - Dados de destinatário
    
      - Credenciais de ESRA

  - O Serviço de Credencial do Microsoft Exchange que é executado no servidor de Transporte de Borda instala as credenciais de ESRA. Essas credenciais são usadas para autenticar e proteger conexões de sincronização posteriores.

  - O agendamento de sincronização EdgeSync é estabelecido.

O serviço do EdgeSync do Microsoft Exchange em execução nos servidores de Caixa de Correio no site do Active Directory inscrito realiza a replicação unidirecional de dados do Active Directory para o AD LDS regularmente. Também é possível usar o cmdlet **Start-EdgeSynchronization** para substituir a programação de sincronização do EdgeSync e iniciar imediatamente a sincronização.

Para mais informações sobre contas ESRA e como elas são usadas para ajudar a proteger o processo de sincronização EdgeSync, consulte [Credenciais de inscrição de borda](edge-subscription-credentials-exchange-2013-help.md).

Este exemplo inscreve um servidor de Transporte de Borda no site especificado e cria automaticamente o conector de Envio da Internet e o conector de Envio a partir do servidor de Transporte de Borda para os servidores de Caixa de Correio.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 


> [!NOTE]  
> Os valores padrão dos parâmetros <EM>CreateInternetSendConnector</EM> e <EM>CreateInboundSendConnector</EM> são ambos <CODE>$true</CODE>. Eles são mostrados aqui apenas para fins demonstrativos.



Este exemplo exporta um arquivo de Inscrição de Borda.

    New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"


> [!NOTE]  
> Quando o cmdlet <STRONG>New-EdgeSubscription</STRONG> for executado no servidor de Transporte de Borda, você receberá uma solicitação de confirmação dos comandos que serão desabilitados e a configuração que será substituída no servidor de Transporte de Borda. Para ignorar essa confirmação, use o parâmetro <EM>Force</EM>. Esse parâmetro é útil quando você cria um script com o cmdlet <STRONG>New-EdgeSubscription</STRONG>. O parâmetro <EM>Force</EM> é usado também para substituir um arquivo existente com o mesmo nome do arquivo que você está criando ao reinscrever um servidor de Transporte de Borda.



Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-EdgeSubscription](https://technet.microsoft.com/pt-br/library/bb123800\(v=exchg.150\)).

## Conectores de Envio criados durante o processo de Inscrição de Borda

Por padrão, quando você conclui o processo de Inscrição de Borda recomendado importando o arquivo de Inscrição de Borda para um servidor de Caixa de Correio, os conectores de Envio necessários para habilitar todo o fluxo de mensagens entre a Internet e a organização do Exchange são criados automaticamente, e qualquer conector de Envio no servidor de Transporte de Borda será excluído. Em alguns cenários, talvez você opte por suprimir a criação automática de conectores de Envio e configurar os conectores de Envio manualmente. Para obter mais informações sobre a configuração manual de conectores de Envio, consulte [Configurar manualmente o fluxo de emails do servidor de transporte de borda](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md) e [Configurar o fluxo de emails da Internet através de um servidor de transporte de borda sem usar o EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md).

O processo de Inscrição de Borda configura os seguintes conectores de Envio:

  - Um conector de Envio configurado para retransmitir mensagens de email da organização do Exchange para a Internet.

  - Um conector de Envio configurado para retransmitir mensagens de email do servidor de Transporte de Borda para a organização do Exchange.

Além disso, inscrever um servidor de Transporte de Borda na organização do Exchange permite que os servidores de Caixa de Correio no site do Active Directory inscrito usem o conector de Envio de dentro da organização para retransmitir mensagens para esse servidor de Transporte de Borda.

## Criar automaticamente um conector de Envio de entrada para receber mensagens da Internet

Por padrão, quando você executa o cmdlet **New-EdgeSubscription** no servidor de Caixa de Correio, o parâmetro *CreateInboundSendConnector* do conector de Envio é definido como o valor `$true`. Isso cria o conector de Envio necessário para enviar mensagens para a organização do Exchange. A tabela a seguir mostra a configuração desse Conector de Envio.

### Configuração automática do Conector de Envio de entrada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Entrada para &lt;<em>Nome do Site</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>O valor <code>--</code> do espaço de endereçamento representa todos os domínios aceitos de retransmissão interna e autoritativos da organização do Exchange. Quaisquer mensagens que o servidor de Transporte de Borda receber para esses domínios aceitos serão direcionadas para esse conector de Envio e retransmitidas para os hosts inteligentes.</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nome de Inscrição de Borda</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>O valor <code>--</code> na lista de hosts inteligentes representa todos os servidores de Caixa de Correio no site do Active Directory inscrito. Qualquer servidor de Caixa de Correio adicionado ao site do Active Directory inscrito estabelecido na Inscrição de Borda não participa do processo de sincronização do EdgeSync. Entretanto, eles são adicionados automaticamente à lista de hosts inteligentes do conector de Envio de entrada criado automaticamente. Se mais de um servidor de Caixa de Correio estiver localizado no site do Active Directory inscrito, ocorrerá o balanceamento de carga das conexões de entrada nos hosts inteligentes.</p></td>
</tr>
</tbody>
</table>


Você não pode modificar o espaço de endereçamento, nem a lista de hosts inteligentes durante a criação para o conector de Envio de entrada criado automaticamente. Entretanto, pode definir o parâmetro *CreateInboundSendConnector* como o valor `$false` ao criar uma Inscrição de Borda. Isso permite a você configurar manualmente um conector de Envio do servidor de Transporte de Borda para a organização do Exchange.

## Criar automaticamente um conector de Envio de saída para enviar mensagens para a Internet

Por padrão, quando você executa o cmdlet **New-EdgeSubscription** no servidor de Caixa de Correio, o parâmetro *CreateInternetSendConnector* é definido como o valor `$true`. Isso cria o conector de Envio necessário para enviar mensagens para a Internet. A tabela a seguir mostra a configuração-padrão desse conector de Envio.

### Configuração automática do Conector de Envio da Internet

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>Nome do Site</em>&gt; para Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nome de Inscrição de Borda</em>&gt;</p>

> [!NOTE]  
> O nome da Inscrição de Borda é o mesmo do servidor de Transporte de Borda inscrito.


</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Verdadeiro</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>Verdadeiro</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>Verdadeiro</p></td>
</tr>
</tbody>
</table>


Se mais de um servidor de Transporte de Borda estiver inscrito no mesmo site do Active Directory, nenhum conector de Envio adicional para a Internet será criado. Em vez disso, todas as Inscrições de Borda serão adicionadas ao mesmo conector de Envio do servidores de origem. Isso faz o balanceamento de carga de conexões de saída para a Internet entre os servidores de Transporte de Borda inscritos.

O conector de Envio de saída está configurado para enviar mensagens de email da organização do Exchange para todos os domínios SMTP remotos, usando roteamento de DNS para resolver nomes de domínio para registros de recurso MX. Para obter detalhes sobre a definição manual da configuração de um conector, consulte [Configurar manualmente o fluxo de emails do servidor de transporte de borda](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md).

## Serviço Microsoft Exchange EdgeSync

Depois de inscrever um servidor de Transporte de Borda em um site do Active Directory, o EdgeSync replicará dados de configuração e de destinatário para os servidores de Transporte de Borda. O serviço replica os seguintes dados do Active Directory para o AD LDS:

  - Configuração do conector de envio

  - Domínios aceitos

  - Domínios remotos

  - Classificações da mensagem

  - Listas de remetentes seguros

  - Lista de remetentes bloqueados

  - Destinatários

  - Lista de domínios de envio e recebimento usados nas comunicações seguras de domínio com parceiros

  - Lista de servidores SMTP listados como internos na configuração de transporte da organização

  - Lista de servidores de Caixa de Correio no site do Active Directory inscrito

Para obter mais informações sobre os dados replicados para o AD LDS e como eles são usados, consulte [Dados de replicação do EdgeSync](edgesync-replication-data-exchange-2013-help.md).

O EdgeSync usa um canal LDAP seguro autorizado e autenticado mutuamente para transferir dados do servidor de Caixa de Correio para o servidor de Transporte de Borda.

Para replicar dados para o AD LDS, o servidor de Caixa de Correio associa-se a um servidor de catálogo global para recuperar dados atualizados. O EdgeSync inicia uma sessão LDAP segura entre um servidor de Caixa de Correio e o servidor de Transporte de Borda inscrito na porta TCP não-padrão 50636.

Quando você inscreve pela primeira vez um servidor de Transporte de Borda em um site do Active Directory, a replicação inicial que preenche o AD LDS com dados do Active Directory pode demorar algum tempo, dependendo da quantidade de dados no serviço do diretório. Após a replicação inicial, o EdgeSync só sincroniza objetos novos e alterados, além de remover qualquer objeto excluído.

## Programação de sincronização

Tipos diferentes de sincronização de dados em agendas diferentes. A programação de sincronização do EdgeSync especifica o tempo máximo entre sincronizações do EdgeSync. A sincronização EdgeSync ocorre nos seguintes intervalos:

  - Dados de configuração: 3 minutos.

  - Dados de destinatário: 5 minutos.

  - Dados de topologia: 5 minutos

Se quiser alterar esses intervalos, use o cmdlet **Set-EdgeSyncService**. O uso do cmdlet **Start-EdgeSynchronization** no servidor de Caixa de Correio para forçar a sincronização de Inscrição de Borda substitui o temporizador para a próxima sincronização programada do EdgeSync e inicia imediatamente o EdgeSync.

## Seleção de servidores de Caixa de Correio

Cada servidor de Transporte de Borda inscrito está associado a um site específico do Active Directory. Se mais de um servidor de Caixa de Correio existir no site, qualquer um deles poderá replicar os dados para os servidores de Transporte de Borda inscritos. Para evitar a contenção entre servidores de Caixa de Correio durante a sincronização, o servidor de Caixa de Correio será selecionado como a seguir:

1.  O primeiro servidor de Caixa de Correio no site do Active Directory a executar uma verificação de topologia e a descobrir a Inscrição de Borda executa a replicação inicial. Como a descoberta é baseada no tempo da verificação de topologia, qualquer servidor de Caixa de Correio no site pode realizar a replicação inicial.

2.  O servidor de Caixa de Correio que executa a replicação inicial estabelece uma opção de concessão do EdgeSync e define um bloqueio na Inscrição de Borda. A opção de concessão estabelece esse servidor de Caixa de Correio como preferencial para fornecer serviços de sincronização ao servidor de Transporte de Borda. O bloqueio impede que o serviço do EdgeSync em execução em outro servidor de Caixa de Correio assuma a opção de concessão.

3.  A opção de concessão do EdgeSync dura uma hora. Durante essa hora, nenhum outro serviço do EdgeSync poderá assumir a opção, a menos que uma sincronização manual seja iniciada antes do término da hora. Se o servidor de Caixa de Correio preferencial não estiver disponível para fornecer o serviço do EdgeSync quando a sincronização manual for executada, após uma espera de cinco minutos, o bloqueio será liberado e outro serviço do EdgeSync assumirá a opção de concessão e executará a sincronização.

4.  A menos que a sincronização manual seja iniciada, a sincronização ocorrerá com base na programação de sincronização do EdgeSync. Se o servidor preferencial não estiver disponível quando a sincronização programada ocorrer, após uma espera de cinco minutos, o bloqueio será liberado e outro serviço do EdgeSync assumirá a opção de concessão e executará a sincronização.

Esse método de bloqueio e concessão impede que mais de uma instância do serviço do EdgeSync envie dados por push ao mesmo servidor de Transporte de Borda ao mesmo tempo.


> [!NOTE]  
> Se você também tiver servidores de Caixa de Correio do Exchange 2010 ou do Exchange 2007 inscritos no site do Active Directory, os servidores de Caixa de Correio do Exchange 2013 sempre terão precedência e executarão a replicação.




> [!NOTE]  
> Quando você inscreve um servidor de Transporte de Borda em um site do Active Directory, todos os servidores de Caixa de Correio instalados nesse site do Active Directory naquele momento poderão participar do processo de sincronização do EdgeSync. Se um desses servidores for removido, o serviço do EdgeSync que estiver sendo executado nos servidores de Caixa de Correio restantes continuará o processo de sincronização de dados. Entretanto, se posteriormente você instalar novos servidores de Caixa de Correio no site do Active Directory, eles não participarão automaticamente da sincronização do EdgeSync. Se quiser permitir que esses servidores de Caixa de Correio novos participem da sincronização do EdgeSync, será preciso inscrever o servidor de Transporte de Borda novamente.



A tabela a seguir lista as propriedades do EdgeSync relacionadas ao processo de bloqueio e concessão. Você pode usar o cmdlet **Set-EdgeSyncServiceConfig** para configurar essas propriedades.

### Propriedades de concessão do EdgeSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code> (5 minutos)</p></td>
<td><p>Essa configuração determina por quanto tempo um serviço do EdgeSync específico obterá um bloqueio. Se o serviço do EdgeSync do servidor de Caixa de Correio que está mantendo esse bloqueio não responder, levará cinco minutos para que o serviço do EdgeSync de outro servidor de Caixa de Correio assuma a concessão. Forçar a sincronização imediata do EdgeSync não substitui essa configuração.</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code> (1 hora)</p></td>
<td><p>Essa configuração determina por quanto tempo um serviço do EdgeSync pode declarar uma opção de concessão em um servidor de Transporte de Borda. Se o serviço do EdgeSync que está mantendo a concessão estiver indisponível e se ele não for reiniciado durante esse período de opção, nenhum outro serviço do Exchange EdgeSync assumirá a opção de concessão, a menos que você force a sincronização do EdgeSync.</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code> (1 minuto)</p></td>
<td><p>Essa configuração determina com que frequência o campo de bloqueio será atualizado quando um serviço do EdgeSync tiver sido bloqueado para um servidor de Transporte de Borda.</p></td>
</tr>
</tbody>
</table>


## Preparar para executar o serviço do EdgeSync

Antes de inscrever o servidor de Transporte de Borda em sua organização do Exchange, você deve garantir que a sua infraestrutura e o seus servidores de Caixa de Correio estejam preparados para o serviço do EdgeSync. Para se preparar para a sincronização do EdgeSync, você precisa:

  - Verificar se o firewall do perímetro de rede que separa o servidor de Transporte de Borda da organização do Exchange está configurado para permitir a comunicação nas portas corretas. O servidor Transporte de Borda usa portas LDAP não padrão. Se o seu ambiente exigir portas específicas, você poderá modificar as portas usadas pelo AD LDS usando o script ConfigureAdam.ps1 fornecido com o Exchange. Para mais informações, consulte [Modificar a configuração do AD LDS](modify-ad-lds-configuration-exchange-2013-help.md). Modifique as portas antes de criar a Inscrição de Borda. Se você modificar as portas depois de criar a Inscrição de Borda, deverá remover a Inscrição de borda e criar uma nova. Por padrão, as seguintes portas LDAP são usadas para acessar o AD LDS:
    
      - **LDAP**   A porta 50389/TCP é usada localmente para ligação com a instância do AD LDS. Essa porta não precisa estar aberta no firewall da rede de perímetro.
    
      - **LDAP Seguro**   A porta 50636/TCP é usada para sincronização de diretório dos servidores de Caixa de Correio com o AD LDS. Essa porta deve estar aberta no firewall para que ocorra a sincronização bem-sucedida do EdgeSync.

  - Verifique se a resolução de nomes de host DNS teve êxito do servidor de Transporte de Borda para os servidores de Caixa de Correio e dos servidores de Caixa de Correio para o servidor de Transporte de Borda.

  - Licencie o servidor de Transporte de Borda. As informações de licenciamento para o servidor de Transporte de Borda são capturadas quando a Inscrição de Borda é criada. Servidores de Transporte de Borda inscritos precisam ser inscritos na organização do Exchange após a aplicação da chave de licença no servidor de Transporte de Borda. Se a chave de licença for aplicada ao servidor de Transporte de Borda depois que você executar o processo de Inscrição de Borda, as informações de licença não serão atualizadas na organização do Exchange e você deverá inscrever novamente o servidor de Transporte de Borda.

  - Defina as seguintes configurações de transporte para a propagação ao servidor de Transporte de Borda:
    
      - **Servidores SMTP internos**   Use o parâmetro *InternalSMTPServers* no cmdlet **Set-TransportConfig** para especificar uma lista de endereços IP ou intervalos de endereços IP para o servidor SMTP interno a serem ignorados pela ID do Remetente e por agentes de Filtragem de Conexão no servidor de Transporte de Borda.
    
      - **Domínios aceitos**   Configure todos os domínios autoritativos, domínios de retransmissão interna e domínios de retransmissão externa.
    
      - **Domínios remotos**   Configure definições de domínios remotos.

Voltar ao início

## Gerenciando Inscrições de Borda

Para obter instruções detalhadas sobre tarefas de gerenciamento da Inscrição de Borda, consulte [Gerenciar inscrições de borda](manage-edge-subscriptions-exchange-2013-help.md).

