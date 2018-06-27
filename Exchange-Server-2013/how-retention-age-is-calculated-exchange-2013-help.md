---
title: 'Como a idade de retenção é calculada: Exchange 2013 Help'
TOCTitle: Como a idade de retenção é calculada
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50486306
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Como a idade de retenção é calculada

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-07-27_

O Assistente de Pasta Gerenciada (MFA) é um dos vários processos de *assistência de caixa de correio* executado em servidores de caixa de correio. Seu trabalho é processar caixas de correio que possuam uma Política de Retenção aplicada, adicionar as Marcas de Retenção incluídas na política à caixa de correio e processar itens na caixa de correio. Se os itens tiverem uma marca de retenção, o assistente testará a idade desses itens. Se um item tiver excedido sua *idade de retenção*, executará a *ação de retenção* especificada. As ações de retenção incluem mover um item para o arquivo do usuário, excluir o item e permitir a recuperação ou excluir o item permanentemente.

Consulte o [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md) para obter mais informações.

## Determinando a idade dos diferentes tipos de itens

A idade da retenção de itens de caixa de correio é calculada a partir da data de entrega ou no caso de itens como rascunhos que não são entregues mas criados pelo usuário, a data em que um item foi criado. Quando o Assistente de pasta gerenciada processa itens em uma caixa de correio, ele carimba uma data de início e uma data de validade para todos os itens que tenham marcas de retenção com a ação de retenção **Excluir e permitir recuperação** ou **Excluir permanentemente**. Itens que tenham uma marca de arquivamento também estão marcados com uma move date.

Os itens na pasta Itens Excluídos e os itens que podem ter uma data de início e de término, como itens de calendário (reuniões e compromissos) e tarefas, são manipulados de forma diferente, como mostra esta tabela.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se o tipo de item for...</th>
<th>E o item for...</th>
<th>A idade da retenção é calculada com base em...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Mensagem de email</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Item de diário</p></li>
<li><p>Solicitação de reunião, resposta ou cancelamento</p></li>
<li><p>Chamadas perdidas</p></li>
</ul></td>
<td><p>Não está na pasta pasta Itens Excluídos</p></td>
<td><p>Data de entrega ou data de criação</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Mensagem de email</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Item de diário</p></li>
<li><p>Solicitação de reunião, resposta ou cancelamento</p></li>
<li><p>Chamadas perdidas</p></li>
</ul></td>
<td><p>Na pasta Itens Excluídos</p></td>
<td><ul>
<li><p>Data de entrega ou criação, a menos que o item tenha sido excluído de uma pasta que não tem uma tag de retenção herdada ou implícita.</p></li>
<li><p>Se um item estiver em uma pasta que não possui uma tag de retenção herdada ou implícita aplicada, o item não será processado pelo MFA e, portanto, não terá um carimbo de data de início. Quando o usuário exclui um item como esse, e o MFA o processa pela primeira vez na pasta Itens Excluídos, ele carimba a data atual como a data de início.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Calendário</p></td>
<td><p>Não está na pasta pasta Itens Excluídos</p></td>
<td><ul>
<li><p>Itens de calendário não recorrentes expiram de acordo com a data de término.</p></li>
<li><p>Itens de calendário recorrentes expiram de acordo com a data de término de sua última ocorrência. Itens de calendário recorrentes sem data de término não expiram.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Calendário</p></td>
<td><p>Na pasta Itens Excluídos</p></td>
<td><ol>
<li><p>Um item de calendário expira de acordo com a sua <code>message-received date</code>, se houver uma.</p></li>
<li><p>Se o item de calendário não tiver uma <code>message-received date</code>, ele expirará de acordo com a sua <code>message-creation date</code>.</p></li>
<li><p>Se o item de calendário não tiver uma <code>message-received date</code> nem uma <code>message-creation date</code>, ele não expirará.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Tarefa</p></td>
<td><p>Não está na pasta pasta Itens Excluídos</p></td>
<td><ul>
<li><p>Tarefas não-recorrentes:</p>
<ol>
<li><p>Uma tarefa não-recorrente expira de acordo com a sua <code>message-received date</code>, se houver uma.</p></li>
<li><p>Se uma tarefa não recorrente não tiver uma <code>message-received date</code>, ela expirará de acordo com a sua <code>message-creation date</code>.</p></li>
<li><p>Se uma tarefa não recorrente não tiver uma <code>message-received date</code> nem uma <code></code><code>message-creation date</code>, ela não expirará.</p></li>
</ol></li>
<li><p>Uma tarefa recorrente expira de acordo com a <code>end date</code> de sua última ocorrência. Se a tarefa recorrente não tiver uma <code>end date</code>, ela não expirará.</p></li>
<li><p>Uma tarefa de regeneração (que é uma tarefa recorrente que regenera um tempo especificado depois que a instância anterior da tarefa é concluída) não expira.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tarefa</p></td>
<td><p>Na pasta Itens Excluídos</p></td>
<td><ol>
<li><p>Uma tarefa expira de acordo com a sua <code>message-received date</code>, se houver uma.</p></li>
<li><p>Se a tarefa não tiver uma <code>message-received date</code>, ela expirará de acordo com a sua <code>message-creation date</code>.</p></li>
<li><p>Se a tarefa não tiver uma <code>message-received date</code> nem uma <code>message-creation date</code>, ela não expirará.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contato</p></td>
<td><p>Em qualquer pasta</p></td>
<td><p>Contatos não estão marcados com uma data de início ou de uma data de validade, para que eles são ignorados pelo Assistente de pasta gerenciada e não expiram.</p></td>
</tr>
<tr class="even">
<td><p>Corrompido</p></td>
<td><p>Em qualquer pasta</p></td>
<td><p>Itens corrompidos são ignorados pelo Assistente de Pasta Gerenciada e não expiram.</p></td>
</tr>
</tbody>
</table>


## Exemplos


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se o usuário...</th>
<th>As marcas de retenção na pasta...</th>
<th>O Assistente de Pasta Gerenciada...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Recebe uma mensagem na Caixa de entrada em 26/01/2013.</p></li>
<li><p>Exclui a mensagem em 27/2/2013.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>Caixa de entrada: Excluir em 365 dias</p></li>
<li><p>Itens Excluídos: Excluir em 30 dias</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>Processa a mensagem na Caixa de entrada em 26/01/2013, carimba com uma <em>data de início</em> de 26/01/2013 e uma <em>data de expiração</em> de 26/01/2014.</p></li>
<li><p>Processa a mensagem novamente na pasta Itens Excluídos em 27/02/2013. Ele recalcula a data de expiração com base na data inicial (26/01/2011).</p></li>
<li><p>Como o item tem mais de 30 dias, ele expira imediatamente.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Recebe uma mensagem na Caixa de entrada em 26/01/2013.</p></li>
<li><p>Exclui a mensagem em 27/2/2013.</p></li>
</ol></td>
<td><ul>
<li><p>Caixa de entrada: Nenhuma (herdada ou implícita)</p></li>
<li><p>Itens Excluídos: Excluir em 30 dias</p></li>
</ul></td>
<td><ol>
<li><p>Processa a mensagem na pasta Itens Excluídos em 27/02/2013 e determina que o item não tem uma data de início. Ele insere a data atual como a data inicial e 27.03.13 como a data de expiração.</p></li>
<li><p>O item expira em 27/03/2013, que são 30 dias após sua exclusão ou movimentação para a pasta Itens Excluídos.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Mais informações

  - Em Exchange Online, o Assistente de pasta gerenciada processa uma caixa de correio uma vez em sete dias. Isso pode resultar em itens sendo expirados até sete dias após a data de expiração marcada no item.

  - Itens em caixas de correio colocadas em retenção não são processados pelo Assistente de pasta gerenciada até que a retenção seja removida.

  - Se uma caixa de correio for colocada em Bloqueio In-loco ou Retenção de Litígio, os itens que estão expirando são removidos da Caixa de entrada, mas são preservados na pasta Itens Recuperáveis até que a caixa de correio seja removida do [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - Em implantações híbridas, as mesmas marcas de retenção e políticas de retenção devem existir em suas organizações local e do Exchange Online a fim de mover e expirar itens de forma consistente nas duas organizações. Consulte [Exportar e importar marcas de retenção](export-and-import-retention-tags-exchange-2013-help.md) para obter mais informações.

