---
title: 'Registro em log de auditoria da caixa de correio: Exchange 2013 Help'
TOCTitle: Registro em log de auditoria da caixa de correio
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50485204
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro em log de auditoria da caixa de correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Caixas de correio podem conter informações confidenciais, informações HBI (de alto impacto nos negócios) e PII (informações de identificação pessoal). Por isso, é importante acompanhar quem faz logon nas caixas de correio da sua organização e rastrear as ações executadas. É especialmente importante monitorar o acesso de usuários que não sejam donos das caixas de correio em questão. Esses usuários são chamados de *usuários representantes*.

Usando o *log de auditoria de caixa de correio*, você pode registrar o acesso à caixa de correio por proprietários de caixas de correio, representantes (inclusive os administradores com total permissão de acesso a caixas de correio) e administradores.

Ao habilitar o log de auditoria para uma caixa de correio, você pode especificar quais ações do usuário (por exemplo, acesso, movimentação ou exclusão de uma mensagem) serão registradas para um tipo de logon (administrador, representante, usuário ou proprietário). As entradas de log de auditoria também incluem informações importantes como, por exemplo, endereço IP do cliente, nome do host e processo ou cliente utilizado para acessar a caixa de correio. Para itens movidos, a entrada inclui o nome da pasta de destino.

## Logs de auditoria de caixa de correio

Os logs de auditoria de caixa de correio são gerados para cada caixa de correio que tenha o registro em log de auditoria de caixa de correio habilitado. As entradas de log são armazenadas na subpasta Auditorias da pasta Itens Recuperáveis, na caixa de correio auditada. Isso garante que todas as entradas de auditoria fiquem disponíveis em um único local, independentemente do método de acesso para cliente usado para acessar a caixa de correio ou de qual servidor ou estação de trabalho foi usado pelo administrador para acessar o log de auditoria de caixa de correio. Se você mover uma caixa de correio para outro servidor de Caixa de Correio, os logs de auditoria de caixa de correio dessa caixa também serão movidos, pois estão localizados na caixa de correio.

Por padrão, as entradas do log de auditoria de caixa de correio são mantidas na caixa de correio por 90 dias e depois excluídas. Esse período de retenção pode ser modificado com o uso do parâmetro *AuditLogAgeLimit* com o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)). Se uma caixa de correio estiver em Retenção In-Loco ou em Retenção de Litígio, as entradas de log de auditoria só serão retidas até que o período de retenção de log da caixa de correio seja atingido. Para reter as entradas de log de auditoria por mais tempo, é preciso aumentar o período de retenção alterando o valor do parâmetro *AuditLogAgeLimit*. Também é possível exportar as entradas de log de auditoria antes de o período de retenção terminar. Para mais informações, consulte:

  - [Exportar logs de auditoria de caixas de correio](export-mailbox-audit-logs-exchange-2013-help.md)

  - [Criar uma pesquisa de log de auditoria de caixas de correio](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## Habilitar o registro em log de auditoria de caixa de correio

O registro em log de auditoria de caixa de correio é habilitado por caixa de correio. Use o cmdlet **Set-Mailbox** para habilitar ou desabilitar o log de auditoria de caixa de correio. Para detalhes, consulte [Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

Quando você habilita o log de auditoria de caixa de correio para uma caixa de correio, o acesso à caixa de correio e algumas ações executadas por administradores e representantes são registradas no log por padrão. Para registrar em log as ações executadas pelo proprietário da caixa de correio, você deve especificar quais ações do proprietário devem ser auditadas.

## Ações de caixa de correio registradas pelo log de auditoria de caixa de correio

A tabela a seguir lista as ações registradas pelo log de auditoria de caixa de correio, incluindo os tipos de logon para os quais a ação pode ser registrada.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Ação</th>
<th>Descrição</th>
<th>Administrador</th>
<th>Delegar</th>
<th>Owner</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cópia</p></td>
<td><p>Um item é copiado para outra pasta.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Criar</p></td>
<td><p>Um item é criado nas pastas Calendário, Contatos, Anotações ou Tarefas na caixa de correio; por exemplo, é criada uma nova solicitação de reunião. Observe que a mensagem ou a criação da pasta não são auditadas.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>Uma pasta da caixa de correio é acessada.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim**</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>Um item é excluído permanentemente da pasta Itens Recuperáveis.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>Um item é acessado no painel de leitura ou aberto.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Mover</p></td>
<td><p>Um item é movido para outra pasta.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>Um item é movido para a Itens Excluídos.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>Uma mensagem é enviada usando permissões Enviar como.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
<td><p>Não se aplica</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>Uma mensagem é enviada usando permissões Enviar em nome de.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
<td><p>Não se aplica</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>Um item é excluído da pasta Itens Excluídos.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Update</p></td>
<td><p>As propriedades de um item são atualizadas.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Auditado por padrão se a auditoria estiver habilitada para uma caixa de correio.

\* \* Entradas para ações de vincular pasta executadas por representantes são consolidadas. Uma entrada de log é gerada para acesso a pastas individuais dentro de um período de tempo de 24 horas.

Caso não seja mais necessário fazer a auditoria de alguns tipos de ações da caixa de correio, modifique a configuração de registro em log de auditoria da caixa de correio para desabilitar essas ações. Entradas de log existentes não serão limpas enquanto o limite de idade das entradas de log de auditoria não for atingido.

## Pesquisar entradas de log de auditoria de caixa de correio

Você pode usar os seguintes métodos para pesquisar entradas de log de auditoria de caixa de correio:

  - **Pesquisa síncrona de uma única caixa de correio**   Você pode usar o cmdlet [Search-MailboxAuditLog](https://technet.microsoft.com/pt-br/library/ff522360\(v=exchg.150\)) para pesquisa síncrona de entradas de log de auditoria de caixa de correio de uma única caixa de correio. O cmdlet exibe os resultados da pesquisa na janela do Shell de Gerenciamento do Exchange. Para detalhes, consulte [Pesquisar o log de auditoria de caixa de correio para uma caixa de correio](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

  - **Pesquisa assíncrona de uma ou mais caixas de correio**   Você pode criar uma pesquisa de log de auditoria de caixa de correio para pesquisa assíncrona de logs de auditoria de caixa de correio para uma ou mais caixas de correio, e enviar os resultados da pesquisa para um email especificado. Os resultados da pesquisa são enviados como um anexo XML. Para criar a pesquisa, use o cmdlet [New-MailboxAuditLogSearch](https://technet.microsoft.com/pt-br/library/ff522362\(v=exchg.150\)). Para detalhes, consulte [Criar uma pesquisa de log de auditoria de caixas de correio](create-a-mailbox-audit-log-search-exchange-2013-help.md).

  - **Usar relatórios de auditoria do EAC (Centro de Administração do Exchange)**   Você pode usar a guia **Auditoria** no EAC para executar um relatório de acesso a caixas de correio não proprietárias ou para exportar entradas do log de auditoria de caixa de correio. Para ver detalhes, consulte:
    
      - [Executar um relatório de acesso não proprietário da caixa de correio](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [Exportar logs de auditoria de caixas de correio](export-mailbox-audit-logs-exchange-2013-help.md)

## Entradas de log de auditoria de caixa de correio

A tabela a seguir descreve os campos registrados em uma entrada de log de auditoria de caixa de correio.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Populado com</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>Uma destas ações:</p>
<ul>
<li><p>Copiar</p></li>
<li><p>Criar</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Mover</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Atualizar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>Um destes resultados:</p>
<ul>
<li><p>Falha</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Com Êxito</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>Tipo de logon do usuário que realizou a operação. Os tipos de logon incluem:</p>
<ul>
<li><p>Owner</p></li>
<li><p>Delegar</p></li>
<li><p>Admin</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>GUID da pasta de destino para operações de movimentação.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>Caminho da pasta de destino para operações de movimentação.</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>GUID da pasta.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>Caminho da pasta.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>Detalhes que identificam qual cliente ou componente do Exchange realizou a operação.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>Endereço IP do computador cliente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>Nome do computador cliente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>O nome do processo do aplicativo cliente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>Versão do aplicativo do cliente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>Tipo de logon do usuário que realizou a operação. Os tipos de logon incluem:</p>
<ul>
<li><p>Owner</p></li>
<li><p>Delegar</p></li>
<li><p>Admin</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>Nome UPN do proprietário da caixa de correio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>SID (identificador de segurança) do proprietário da caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>Nome UPN do proprietário da caixa de correio de destino, registrado em log para operações entre caixas de correio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>SID do proprietário da caixa de correio de destino, registrado em log para operações entre caixas de correio.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>GUID do proprietário da caixa de correio de destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>Informações sobre se a operação registrada é uma operação de caixas de correio cruzadas (por exemplo, copiar ou mover mensagens entre caixas de correio).</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>Nome para exibição do usuário que está conectado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>Nome para exibição do usuário representado.</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>SID do usuário que está conectado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>ItemID dos itens de caixa de correio nos quais a ação registrada foi realizada (por exemplo, mover ou excluir). Para operações realizadas em diversos itens, o campo é retornado como uma coleção de itens.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>GUID da pasta de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>ID do item.</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>Assunto do item.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>GUID da caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>Nome resolvido do usuário da caixa de correio no formato <em>DOMÍNIO</em>\<em>NomeDeContaSAM</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>A hora na qual a operação foi realizada.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>ID da entrada do log de auditoria.</p></td>
</tr>
</tbody>
</table>


## Mais informações

  - **Acesso de administrador a caixas de correio**   Considera-se que caixas de correio são acessadas por um administrador apenas nestes cenários:
    
      - A [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) é usada para pesquisar uma caixa de correio.
    
      - O cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/pt-br/library/ff607299\(v=exchg.150\)) é usado para exportar uma caixa de correio.
    
      - [Editor de MAPI do Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=204086) é usado para acessar a caixa de correio.

  - **Ignorando o log de auditoria de caixa de correio**   O acesso a caixas de correio por processos automatizados – por exemplo, contas usadas por ferramentas de terceiros ou contas utilizadas para fins de monitoramento por força de lei – pode criar um grande número de entradas de log de auditoria, e isso talvez não interesse à sua organização. Essas contas podem ser configuradas para ignorar o registro em log de auditoria de caixa de correio. Para detalhes, consulte [Bypass de um usuário da conta de auditoria de caixa de correio log](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md).

  - **Registrando ações de proprietários de caixas de correio**   Para caixas de correio como, por exemplo, Caixa de Correio de Pesquisa de Descoberta, as quais podem conter informações confidenciais, considere habilitar o log de auditoria de caixa de correio para ações do proprietário da caixa de correio; por exemplo, exclusão de mensagens.

Voltar ao início

