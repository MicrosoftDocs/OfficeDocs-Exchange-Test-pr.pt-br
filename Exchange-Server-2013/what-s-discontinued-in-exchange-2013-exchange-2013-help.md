---
title: 'O que será descontinuado no Exchange 2013: Exchange 2013 Help'
TOCTitle: O que será descontinuado no Exchange 2013
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50484927
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O que será descontinuado no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico discute os componentes, os recursos ou as funcionalidades que foram removidos, descontinuados ou substituídos no Microsoft Exchange Server 2013.


> [!NOTE]  
> Os tópicos a seguir também podem interessar a você: 
> <UL>
> <LI>
> <P><A href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novidades do Exchange 2013</A>&nbsp;&nbsp;&nbsp;Informações sobre novos recursos e funcionalidades do Exchange Server 2013.</P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=267479">Mapa do desenvolvedor para o Exchange 2013</A>&nbsp;&nbsp;&nbsp;&nbsp;Consulte as "tecnologias de desenvolvimento removidas do Exchange? seção para obter informações sobre os recursos de API e desenvolvimento descontinuadas no Exchange 2013.</P></LI></UL>



## Recursos descontinuados do Exchange 2010 para o Exchange 2013

Essa seção lista os recursos do Exchange Server 2010 que não estão mais disponíveis no Exchange 2013.

## Arquitetura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Função de servidor Transporte de Hub</p></td>
<td><p>A função de servidor Transporte de Hub foi substituída por serviços de Transporte que são executados nas funções de servidor Caixa de Correio e Acesso para Cliente. A função de servidor Caixa de Correio inclui os serviços Transporte do Microsoft Exchange, Entrega de Transporte de Caixa de Correio do Microsoft Exchange e Envio de Transporte de Caixa de Correio do Microsoft Exchange. A função de servidor Acesso para Cliente inclui o serviço Transporte de Frontend do Microsoft Exchange. Para mais informações, consulte <a href="mail-flow-exchange-2013-help.md">Fluxo de mensagens</a>.</p></td>
</tr>
<tr class="even">
<td><p>Função de servidor Unificação de Mensagens</p></td>
<td><p>A função de servidor Unificação de Mensagens foi substituída por serviços de Unificação de Mensagens que são executados nas funções de servidor Caixa de Correio e Acesso para Cliente. A função de servidor Caixa de Correio inclui o serviço Unificação de Mensagens do Microsoft Exchange e a função de servidor Acesso para Cliente inclui o serviço de Encaminhamento de Chamadas da Unificação de Mensagens do Microsoft Exchange. Para mais informações, consulte <a href="voice-architecture-changes-exchange-2013-help.md">Mudanças de arquitetura de voz</a>.</p></td>
</tr>
</tbody>
</table>


## Interfaces de gerenciamento


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Console de Gerenciamento do Exchange e Painel de Controle do Exchange</p></td>
<td><p>O Console de Gerenciamento do Exchange e o Painel de Controle do Exchange foram substituídos pelo Centro de Administração do Exchange (EAC). O EAC usa o mesmo diretório virtual (/ecp) que o Painel de Controle do Exchange. Para mais informações, consulte <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centro de administração do Exchange no Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


## Acesso para cliente


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Não há suporte para o Outlook 2003</p></td>
<td><p>Para conectar o Microsoft Outlook ao Exchange 2013, é necessário usar o serviço de Descoberta Automática. No entanto, o Microsoft Outlook 2003 não suporta a utilização do serviço de Descoberta Automática.</p></td>
</tr>
<tr class="even">
<td><p>Acesso RPC/TCP para clientes Outlook</p></td>
<td><p>No Exchange 2013, clientes do Microsoft Outlook podem se conectar usando o Outlook em Qualquer Lugar (RPC/HTTP) ou MAPI sobre HTTP no Exchange 2013 Service Pack 1 e no Outlook 2013 Service Pack 1 e posterior. Se você tiver clientes do Outlook em sua organização, o uso do Outlook em Qualquer Lugar e/ou de MAPI sobre HTTP será necessário. Para obter mais informações, consulte <a href="outlook-anywhere-exchange-2013-help.md">Outlook em Qualquer Lugar</a> e <a href="mapi-over-http-exchange-2013-help.md">MAPI sobre HTTP</a>.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App e Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Verificação ortográfica</p></td>
<td><p>Outlook Web App não tem mais serviços de verificação ortográfica integrados. Em vez disso, utilize os recursos de verificação ortográfica dos seus navegadores da Web.</p></td>
</tr>
<tr class="even">
<td><p>Filtros personalizáveis</p></td>
<td><p>Outlook Web App não tem mais exibições filtradas personalizáveis e não suporta mais a gravação de exibições filtradas nos Favoritos. Os filtros personalizáveis foram substituídos por filtros fixos que podem ser usados para exibir todas as mensagens, mensagens não lidas, mensagens enviadas ao usuário ou mensagens sinalizadas.</p></td>
</tr>
<tr class="odd">
<td><p>Sinalizadores de mensagem</p></td>
<td><p>O recurso de definição de data personalizada em um sinalizador de mensagem não está disponível no Outlook Web App. Você pode usar o Outlook para definir datas personalizadas.</p></td>
</tr>
<tr class="even">
<td><p>Lista de contatos de chat</p>
<p></p></td>
<td><p>A lista de contatos de chat que aparecia na lista de pastas no Outlook Web App para Exchange 2010 não está mais disponível.</p></td>
</tr>
<tr class="odd">
<td><p>Pastas de pesquisa</p></td>
<td><p>O recurso para os usuários usarem as pastas de pesquisa não está disponível atualmente no Outlook Web App.</p></td>
</tr>
</tbody>
</table>


## Fluxo de mensagens


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Conectores vinculados</p></td>
<td><p>A habilidade de vincular um conector de Envio a um conector de Recebimento foi removida. Especificamente, ao parâmetro <em>LinkedReceiveConnector</em> foi removido do <a href="https://technet.microsoft.com/pt-br/library/aa998936(v=exchg.150)">New-SendConnector</a> e do <a href="https://technet.microsoft.com/pt-br/library/aa998294(v=exchg.150)">Set-SendConnector</a>.</p></td>
</tr>
</tbody>
</table>


## Antispam e antimalware


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento de agentes antispam no EMC</p></td>
<td><p>No Exchange 2010, quando você habilitava os agentes antispam no servidor de Transporte de Hub, podia gerenciar os agentes antispam no Console de Gerenciamento do Exchange (EMC). No Exchange 2013, quando você habilita os agentes antispam em um servidor de Caixa de Correio, não pode gerenciar os agentes no EAC. Só é possível usar o Shell. Para informações sobre como habilitar os agentes antispam em um servidor de Caixa de Correio <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar a funcionalidade anti-spam em servidores de caixa de correio</a>.</p></td>
</tr>
<tr class="even">
<td><p>Agente de Filtragem de Conexão em servidores de Transporte de Hub</p></td>
<td><p>No Exchange 2010, quando você habilitar os agentes antispam em um servidor de Transporte de Hub, o agente do Filtro de Anexos era o único agente antispam que não estava disponível. No Exchange 2013, quando você habilita os agentes antispam no servidor Caixa de Correio, o agente Filtro de Anexos e o agente Filtragem de Conexão não ficam disponíveis. O agente do Filtro de Conexão oferece os recursos Lista de IP Permitidos e Lista de IP Bloqueados. Para informações sobre como habilitar os agentes antispam em um servidor de Caixa de Correio <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar a funcionalidade anti-spam em servidores de caixa de correio</a>.</p>

> [!NOTE]  
> Não é possível habilitar os agentes antispam em um servidor de Acesso para Cliente do Exchange 2013. Portanto, a única maneira de obter o agente Filtragem de Conexão é instalando um servidor de Transporte de Borda na rede de perímetro. Para obter mais informações, consulte <A href="edge-transport-servers-exchange-2013-help.md">Servidores de Transporte de Borda</A>.


</td>
</tr>
</tbody>
</table>


## Conformidade e política de sistema de mensagens


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pastas gerenciadas</p></td>
<td><p>Exchange 2010, você usa pastas gerenciadas para mensagens (MRM) de gerenciamento de retenção. Em Exchange 2013, pastas gerenciadas não são suportadas. Você deve usar políticas de retenção para MRM.</p>

> [!NOTE]  
> Cmdlets relacionados a pastas gerenciadas ainda estão disponíveis. Você pode criar pastas gerenciadas, configurações de conteúdo gerenciado e políticas de caixa de correio de pasta gerenciada e aplicar uma política de caixa de correio de pasta gerenciada a um usuário, mas o assistente MRM ignora o processamento das caixas de correio a que tenha sido aplicada uma política de caixa de correio de pasta pública.


</td>
</tr>
<tr class="even">
<td><p>Assistente Portar Pasta Gerenciada</p></td>
<td><p>No Exchange 2010, você usa o assistente Portar Pasta Gerenciada, para criar marcas de retenção com base nas configurações de pasta gerenciada e conteúdo gerenciado. No Exchange 2013, o Centro de administração do Exchange não inclui essa funcionalidade. Você pode usar o cmdlet <strong>New-RetentionPolicyTag</strong> com o parâmetro <em>ManagedFolderToUpgrade</em> para criar a marca de retenção com base em uma pasta gerenciada.</p></td>
</tr>
</tbody>
</table>


## Unificação de Mensagens e caixa postal


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e mitigação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pesquisas de diretório usando o Reconhecimento Automático de Fala (ASR)</p></td>
<td><p>No Exchange 2010, os usuários do Outlook Voice Access podem usar entradas de fala usando o Reconhecimento Automático de Fala (ASR) para pesquisar por usuários listados no diretório. As entradas de fala também podem ser usadas no Outlook Voice Access para a navegação em menus, mensagens e outras opções. No entanto, mesmo que um usuário do Outlook Voice Access possa usar as entradas de fala, ele precisará utilizar o teclado do telefone para inserir o PIN e navegar em opções pessoais.</p>
<p>No Exchange 2013, os usuários autenticados e não autenticados do Outlook Voice Access não podem pesquisar usuários no diretório utilizando entradas de fala ou o ASR em qualquer idioma. Contudo, os chamadores que realizarem chamadas para um atendedor automático poderão usar as entradas de fala em vários idiomas para navegar pelos menus de atendimento automático e pesquisar usuários no diretório.</p></td>
</tr>
</tbody>
</table>


## Ferramentas


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Analisador de Melhores Práticas do Exchange</p></td>
<td><p>Em Exchange 2010, o analisador de práticas recomendadas do Exchange examinados sua implantação do Exchange e determinado se a configuração foi alinhado com as práticas recomendadas da Microsoft. Em Exchange 2013, o analisador de práticas recomendadas do Exchange foi substituído pelo <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Office 365 Best Practices Analyzer para o Exchange Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Solução de problemas do fluxo de emails</p></td>
<td><p>No Exchange 2010, a solução de problemas de fluxo de email ajudava você a solucionar problemas comuns de fluxo de email. No Exchange 2013, a solução de problemas de fluxo de emails foi descontinuado. Agora, você pode usar o recurso de monitoramento de mensagens do EAC, no Exchange 2013. Para mais informações, consulte <a href="track-messages-with-delivery-reports-exchange-2013-help.md">Acompanhar mensagens com notificações de entrega</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Monitor de desempenho</p></td>
<td><p>No Exchange 2010, o Monitor de Desempenho fazia parte da caixa de ferramentas do Exchange, para permitir quer você colete informações sobre o desempenho o seu sistema de mensagens. O Monitor de Desempenho é comumente usado para exibir parâmetros-chave enquanto soluciona problemas de desempenho. No Exchange 2013, o Monitor de Desempenho não faz mais parte da caixa de ferramentas. Você ainda poderá encontrar o Monitor de Desempenho nas <strong>Ferramentas Administrativas</strong> do Windows Server 2008.</p></td>
</tr>
<tr class="even">
<td><p>Solução de problemas de Desempenho</p></td>
<td><p>No Exchange 2013, a solução de Problemas de Desempenho foi descontinuada.</p></td>
</tr>
<tr class="odd">
<td><p>Visualizador de Logs de Roteamento</p></td>
<td><p>No Exchange 2013, o visualizador de log de roteamento foi descontinuado.</p></td>
</tr>
</tbody>
</table>


## Cópias de banco de dados de caixa de correio


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>Assistente de atualização de cópia de banco de dados de caixa de correio</p></li>
</ul></td>
<td><p>Propagação do catálogo de índice de conteúdo não é mais possível na rede de replicação. ela só pode ser feita por uma rede MAPI. Isso acontece mesmo quando você usa o parâmetro <code>-Network</code> no cmdlet Update-MailboxDatabaseCopy.</p></td>
</tr>
</tbody>
</table>


## Recursos descontinuados do Exchange 2007 para o Exchange 2013

Essa seção lista os recursos do Exchange Server 2007 que não estão mais disponíveis no Exchange 2013.

## APIs e desenvolvimento


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p>Usar <a href="https://go.microsoft.com/fwlink/p/?linkid=167197">serviços Web do Exchange</a> ou <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">API gerenciada do EWS</a>. Como alternativa, você pode manter um servidor Exchange 2007 para caixas de correio que são gerenciados por aplicativos que usam o WebDAV. Para obter mais informações, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">Migrando de WebDAV</a>.</p></td>
</tr>
</tbody>
</table>


## Arquitetura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupos de repositório</p></td>
<td><p>O Exchange 2013 não usa mais a construção de grupo de armazenamento, basta gerenciar os bancos de dados de caixa de correio. Para obter mais informações, consulte <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gerenciar bancos de dados de caixa de correio no Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>APIs de backup de streaming do Mecanismo de Armazenamento Extensível (ESE)</p></td>
<td><p>O Exchange 2013 é compatível apenas com backups que reconheçam o Exchange, baseados no Serviço de Cópias de Sombra de Volume (VSS). O Exchange 2013 inclui um plugin para o Backup do Windows Server que permite que você faça backup e restaure dados. Para obter informações, consulte <a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Backup, restauração e recuperação de desastres</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Notificações de protocolo UDP</p></td>
<td><p>O suporte para notificações de protocolo UDP foi removido do Exchange 2013. Isso afeta a experiência, quando clientes do Outlook 2003 se conectam a suas caixas de correio em um servidor do Exchange 2013. Para mais informações sobre esse problema, consulte o artigo 2009942 da Base de Conhecimento da Microsoft <a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2009942">Pastas levam muito tempo para atualizar quando um usuário do Exchange Server 2010 usa o Outlook 2003 no modo online</a>.</p></td>
</tr>
</tbody>
</table>


## Alta disponibilidade


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CCR (Replicação contínua em cluster)</p></td>
<td><p>Exchange 2013 usa grupos de disponibilidade de banco de dados (DAGs) e cópias de banco de dados de caixa de correio. Para obter informações, consulte <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidade e resiliência de site</a>.</p></td>
</tr>
<tr class="even">
<td><p>LCR (Replicação contínua local)</p></td>
<td><p>Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio. Para obter informações, consulte <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidade e resiliência de site</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Replicação contínua em espera (SCR)</p></td>
<td><p>Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio. Para obter informações, consulte <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidade e resiliência de site</a>.</p></td>
</tr>
<tr class="even">
<td><p>SCC (cluster de cópia única)</p></td>
<td><p>Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio. Para obter informações, consulte <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidade e resiliência de site</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 usa Setup /m:recoverServer. Para obter informações, consulte <a href="recover-an-exchange-server-exchange-2013-help.md">Recuperar um Exchange Server</a>.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de caixa de correio em cluster</p></td>
<td><p>Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio. Para obter informações, consulte <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidade e resiliência de site</a>.</p></td>
</tr>
</tbody>
</table>


## Acesso para cliente


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticação de cliente usando a autenticação integrada do Windows (NTLM) para usuários POP3 e IMAP4</p></td>
<td><p>Conectividade de cliente POP3 ou IMAP4 em Exchange 2013 não é compatível com NTLM. Conexões de programas cliente POP3 ou IMAP4, usando NTLM falhará. Se você estiver executando a versão RTM do Exchange 2013, a alternativa recomendado como NTLM é usar a autenticação de texto sem formatação com SSL.</p>
<p>Se você estiver usando o Exchange 2013, para usar o NTLM, você deverá manter um servidor do Exchange 2007 na sua organização do Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App e Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso a documentos</p></td>
<td><p>O Outlook Web App não pode ser usado para acessar bibliotecas de documentos do Microsoft SharePoint e compartilhamento de arquivos do Windows.</p></td>
</tr>
<tr class="even">
<td><p>Sinalizadores de mensagem</p></td>
<td><p>A capacidade de definir uma data personalizada em um sinalizador de mensagem não está disponível no Outlook Web App 2013. Você pode usar o Outlook para definir datas personalizadas.</p></td>
</tr>
<tr class="odd">
<td><p>Verificação ortográfica</p></td>
<td><p>O Outlook Web App usa os recursos de verificação ortográfica do seu navegador da Web.</p></td>
</tr>
<tr class="even">
<td><p>Pastas de pesquisa</p></td>
<td><p>O recurso para os usuários usarem as pastas de pesquisa não está disponível atualmente no Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Modos de exibição de cache máximo</p></td>
<td><p>Suporte do Exchange 2007 para modificar o número máximo de visualizações em cache por parâmetro database (msExchMaxCachedViews) para clientes do Outlook. Exchange 2013 deixa de usar este parâmetro.</p></td>
</tr>
</tbody>
</table>


## Recursos relacionados a destinatários


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e redução</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cmdlets <strong>Export-Mailbox</strong> e <strong>Import-Mailbox</strong></p></td>
<td><p>No Exchange 2013, use as solicitações de exportação ou importação. Para mais informações, consulte <a href="mailbox-import-and-export-requests-exchange-2013-help.md">Solicitações de importação e exportação da caixa de correio</a>.</p></td>
</tr>
<tr class="even">
<td><p>Conjunto de cmdlets <strong>Move-Mailbox</strong></p></td>
<td><p>No Exchange 2013, use solicitações de movimentação para mover caixas de correio. Para obter informações, consulte <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>No Exchange 2013, use <a href="https://technet.microsoft.com/pt-br/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>.</p></td>
</tr>
</tbody>
</table>


## Conformidade e política de sistema de mensagens


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e mitigação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pastas gerenciadas</p></td>
<td><p>No Exchange 2007, você usa pastas gerenciadas para gerenciamento de retenção de mensagens (MRM). No Exchange 2013, pastas gerenciadas não são suportadas. Você deve usar políticas de retenção para MRM.</p>

> [!NOTE]  
> Cmdlets relacionados a pastas gerenciadas ainda estão disponíveis. Você pode criar pastas gerenciadas, configurações de conteúdo gerenciado e políticas de caixa de correio de pasta gerenciada e aplicar uma política de caixa de correio de pasta gerenciada a um usuário, mas o assistente MRM ignora o processamento das caixas de correio a que tenha sido aplicada uma política de caixa de correio de pasta pública.


</td>
</tr>
</tbody>
</table>


## Unificação de Mensagens e caixa postal


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Comentários e mitigação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pesquisas de diretório usando o Reconhecimento Automático de Fala (ASR) para o Outlook Voice Access</p></td>
<td><p>No Exchange 2007, os usuários do Outlook Voice Access podem usar entradas de fala usando o Reconhecimento Automático de Fala (ASR) em inglês (EUA) – (en-US) para pesquisar por usuários listados no diretório. As entradas de fala também podem ser usadas no Outlook Voice Access para a navegação em menus, mensagens e outras opções. No entanto, mesmo que um usuário do Outlook Voice Access possa usar as entradas de fala, ele precisará utilizar o teclado do telefone para inserir o PIN e navegar em opções pessoais.</p>
<p>No Exchange 2013, os usuários autenticados e não autenticados do Outlook Voice Access não podem pesquisar usuários no diretório utilizando entradas de fala ou o ASR em qualquer idioma. Contudo, os chamadores que realizarem chamadas para um atendedor automático poderão usar as entradas de fala em vários idiomas para navegar pelos menus de atendimento automático e pesquisar usuários no diretório.</p></td>
</tr>
</tbody>
</table>

