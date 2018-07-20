---
title: 'Visão geral dos serviços do Exchange 2013: Exchange 2013 Help'
TOCTitle: Visão geral dos serviços do Exchange 2013
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479252
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visão geral dos serviços do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-10-20_

Durante a instalação do Exchange Server 2013, a instalação executa um conjunto de tarefas que instale novos serviços no Microsoft Windows. Um serviço é um processo em segundo plano que pode ser iniciado durante a inicialização do servidor por Windows Gerenciador de controle de serviço. Serviços são arquivos executáveis projetados para operar de forma independente e sem intervenção administrativa. Um serviço pode ser executado usando um modo de GUI (interface) gráfica do usuário ou de um modo de console.

Todas as versões anteriores do Exchange incluíam componentes que são implementados como serviços. Cada função de servidor Exchange inclui serviços que fazem parte de (ou podem ser necessários pelo) a função de servidor para desempenhar suas funções. Observe que alguns serviços somente se tornarão ativos quando recursos específicos são usados.

As seções deste tópico descrevem os vários serviços instalados pelo Exchange 2013 nos servidores de caixa de correio, servidores de acesso para cliente e servidores de transporte de borda. Para serviços que são rotulados como opcional, você pode desabilitar o serviço se você determinar que sua organização não precisa a funcionalidade fornecida pelo serviço.

## Serviços de Exchange nos servidores de caixa de correio de Exchange 2013

A tabela a seguir descreve os serviços de Exchange que são instalados em servidores de caixa de correio.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do serviço</th>
<th>Nome abreviado do serviço</th>
<th>Descrição e dependências</th>
<th>Tipo de inicialização padrão</th>
<th>Contexto de segurança</th>
<th>Dependências</th>
<th>Obrigatório ou opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fornece informações de topologia Active DirectoryExchange serviços. Se esse serviço estiver parado, a maioria dos serviços de Exchange não é possível iniciar.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Serviço de compartilhamento da porta NET. TCP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Atualização do Microsoft Exchange Anti-spam</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fornece Exchange SmartScreen atualizações de definição de spam.</p>

> [!TIP]
> Em 1 de novembro de 2016, o Microsoft interrompeu a produção de atualizações de definição de spam para os Filtros SmartScreen, no Exchange e no Outlook. As definições de spam existentes para SmartScreen permanecerão inalteradas, mas a respectiva eficácia provavelmente diminuirá ao longo do tempo. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Substituição do suporte para SmartScreen no Outlook e no Exchange</A>.


</td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Gerenciamento de DAG</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>Fornece gerenciamento de layout de armazenamento e o banco de dados para servidores de caixa de correio em grupos de disponibilidade de banco de dados (DAGs).</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p>
<p>Serviço de compartilhamento da porta NET. TCP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornece um operador que monitora a integridade do servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Nenhum</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Replica dados de configuração e destinatários entre o servidor de caixa de correio e o UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) nos servidores de transporte de Borda inscritos em um canal LDAP seguro.</p>
<p>Se você não tiver nenhum servidor de transporte de borda inscrito, você pode desabilitar esse serviço.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Gerenciador de integridade</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte da disponibilidade gerenciada que monitora a integridade dos componentes-chave no servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Windows Log de eventos</p>
<p>Windows Instrumentação de gerenciamento</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Back-end do IMAP4</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>Recebe as conexões de cliente intermediadas por proxy do do serviço IMAP4 nos servidores de acesso para cliente. Por padrão, esse serviço não está sendo executado, para que clientes IMAP4 não podem se conectar ao servidor Exchange até que esse serviço é iniciado.</p>
<p>Se você não tiver quaisquer clientes IMAP4, você pode desabilitar esse serviço.</p></td>
<td><p>Manual</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>repositório de Informações do Microsoft Exchange</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Gerencia os bancos de dados de caixa de correio no servidor. Se esse serviço estiver parado, bancos de dados de caixa de correio no servidor não estão disponíveis.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p>
<p>Chamada de procedimento remoto (RPC)</p>
<p>Servidor</p>
<p>Windows Log de eventos</p>
<p>Estação de trabalho</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Assistentes de Caixa de Correio do Microsoft Exchange</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Realiza o processamento de plano de fundo de caixas de correio nos bancos de dados de caixa de correio no servidor.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Replicação de caixa de correio</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>Caixa de correio de processos move e solicitações de movimentação.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p>
<p>Serviço de compartilhamento da porta NET. TCP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Entrega de transporte de caixa de correio</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Recebe mensagens SMTP do Microsoft Exchange serviço de transporte (nos servidores de caixa de correio locais ou remotos) e encaminhá-los para um banco de dados de caixa de correio local usando RPC.</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Envio de transporte de caixa de correio</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>Recebe mensagens RPC de um banco de dados de caixa de correio local e submete via SMTP ao Microsoft Exchange o serviço de transporte (nos servidores de caixa de correio locais ou remotos).</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Backend POP3</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>Recebe as conexões de cliente intermediadas por proxy do serviço POP3 nos servidores de acesso para cliente. Por padrão, esse serviço não está sendo executado, para que clientes POP3 não podem se conectar ao servidor Exchange até que esse serviço é iniciado.</p></td>
<td><p>Manual</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Serviço de Replicação do Microsoft Exchange</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>Fornece a funcionalidade de replicação para bancos de dados de caixa de correio em um banco de dados (DAGs) de grupos de disponibilidade.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Acesso para Cliente RPC do Microsoft Exchange</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Gerencia conexões do cliente RPC para Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Pesquisa</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>Fornece a indexação de conteúdo de caixa de correio, o que melhora o desempenho de pesquisa de conteúdo.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Controlador de Host de pesquisa</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fornece serviços de implantação e gerenciamento de aplicativos no servidor local Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Serviço HTTP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Extensão do Microsoft Exchange Server para Backup do Windows Server</p></td>
<td><p>WSBExchange</p></td>
<td><p>Permite Windows Server Backup para fazer e restaurar dados do servidor de Exchange.</p></td>
<td><p>Manual</p></td>
<td><p>Sistema local</p></td>
<td><p>Nenhum</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Host de Serviço do Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornece um host de serviço para componentes de Exchange que não têm seus próprios serviços.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Limitação do Microsoft Exchange</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>Fornece gerenciamento de carga de trabalho do usuário que limita a taxa de operações de usuário (anteriormente conhecido como limitação do usuário).</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Transporte do Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fornece o servidor SMTP e a pilha de transporte.</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p>
<p>Microsoft Serviço de gerenciamento de filtragem</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Pesquisa de Log de Transporte do Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Fornece a capacidade de pesquisa remota para arquivos de log de transporte (por exemplo, controle de mensagens).</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Unificação de Mensagens do Microsoft Exchange</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>Fornece recursos de Unificação de mensagens (UM): permite que mensagens de voz e fax seja armazenado na Exchange e fornece aos usuários acesso por telefone para email, caixa postal, calendário, contatos ou um atendedor automático. Se esse serviço estiver parado, a Unificação de mensagens não está disponível.</p>
<p>Se você não usar a Unificação de mensagens, você pode desabilitar esse serviço.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Isolamento de chave CNG</p>
<p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>


## Serviços de Exchange nos servidores de acesso para cliente do Exchange 2013

A tabela a seguir descreve os serviços de Exchange que são instalados em servidores de acesso para cliente.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do serviço</th>
<th>Nome abreviado do serviço</th>
<th>Descrição e dependências</th>
<th>Tipo de inicialização padrão</th>
<th>Contexto de segurança</th>
<th>Dependências</th>
<th>Obrigatório ou opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fornece informações de topologia Active DirectoryExchange serviços. Se esse serviço estiver parado, a maioria dos serviços de Exchange não é possível iniciar.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Serviço de compartilhamento da porta NET. TCP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornece um operador que monitora a integridade do servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Nenhum</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transporte de front-end</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Conexões de proxies SMTP de hosts externos para Microsoft Exchange serviço transporte em servidores de caixa de correio.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Gerenciador de integridade</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte da disponibilidade gerenciada que monitora a integridade dos componentes-chave no servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Windows Log de eventos</p>
<p>Windows Instrumentação de gerenciamento</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Conexões de cliente proxies IMAP4 para o serviço IMAP4 nos servidores de caixa de correio. Por padrão, esse serviço não está sendo executado, para que clientes IMAP4 não podem se conectar ao servidor Exchange até que esse serviço é iniciado.</p>
<p>Se você não tiver quaisquer clientes IMAP4, você pode desabilitar esse serviço.</p></td>
<td><p>Manual</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Conexões de cliente proxies POP3 para o serviço IMAP4 nos servidores de caixa de correio. Por padrão, esse serviço não está sendo executado, para que clientes POP3 não podem se conectar ao servidor Exchange até que esse serviço é iniciado.</p></td>
<td><p>Manual</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Controlador de Host de pesquisa</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fornece serviços de implantação e gerenciamento de aplicativos no servidor local Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Serviço HTTP</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Host de Serviço do Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornece um host de serviço para componentes de Exchange que não têm seus próprios serviços.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Unificação de mensagens do roteador de chamada</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>Redireciona as conexões de cliente de Unificação de mensagens para o serviço de Unificação de mensagens nos servidores de caixa de correio.</p>
<p>Se você não usar a Unificação de mensagens, você pode desabilitar esse serviço.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Isolamento de chave CNG</p>
<p>Microsoft Exchange Topologia do Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>


## Exchange serviços nos servidores de transporte de borda Exchange 2013

A tabela a seguir descreve os serviços de Exchange que são instalados em servidores de transporte de borda.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do serviço</th>
<th>Nome abreviado do serviço</th>
<th>Descrição</th>
<th>Tipo de inicialização padrão</th>
<th>Contexto de segurança</th>
<th>Dependências</th>
<th>Obrigatório ou opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Armazena dados de configuração e dados de destinatário no servidor de transporte de borda. Esse serviço representa a instância nomeada do UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) que é criado automaticamente pelo Exchange instalação.</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Sistema COM + eventos</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Atualização do Microsoft Exchange Anti-spam</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fornece Exchange SmartScreen atualizações de definição de spam.</p>

> [!TIP]
> Em 1 de novembro de 2016, o Microsoft interrompeu a produção de atualizações de definição de spam para os Filtros SmartScreen, no Exchange e no Outlook. As definições de spam existentes para SmartScreen permanecerão inalteradas, mas a respectiva eficácia provavelmente diminuirá ao longo do tempo. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Substituição do suporte para SmartScreen no Outlook e no Exchange</A>.


</td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Serviço de Credencial do Microsoft Exchange</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>Monitora alterações de credencial no UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) e instala as alterações no servidor de transporte de borda.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornece um operador que monitora a integridade do servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Nenhum</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Gerenciador de integridade</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte da disponibilidade gerenciada que monitora a integridade dos componentes-chave no servidor Exchange.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Log de Eventos do Windows</p>
<p>Instrumentação de gerenciamento do Windows</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Host de Serviço do Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornece um host de serviço para componentes de Exchange que não têm seus próprios serviços.</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="odd">
<td><p>Transporte do Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fornece o servidor SMTP e a pilha de transporte.</p></td>
<td><p>Automática</p></td>
<td><p>Serviço de Rede</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obrigatório</p></td>
</tr>
<tr class="even">
<td><p>Pesquisa de Log de Transporte do Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Fornece a capacidade de pesquisa remota para arquivos de log de transporte (por exemplo, controle de mensagens).</p></td>
<td><p>Automática</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>

