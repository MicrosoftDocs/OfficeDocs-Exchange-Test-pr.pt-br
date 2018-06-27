---
title: 'Contadores de desempenho para gerenciamento de registros de mensagens: Exchange 2013 Help'
TOCTitle: Contadores de desempenho para gerenciamento de registros de mensagens
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51407898
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contadores de desempenho para gerenciamento de registros de mensagens

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Os contadores de desempenho neste tópico monitoram Assistente de pasta gerenciada conforme ele implementa o gerenciamento de registros mensagens (MRM) para o Microsoft Exchange Server 2010. Como executar o Assistente de pasta gerenciada é um processo de uso intenso de recursos, ele deverá ser executado somente quando seu servidor puder tolerar a carga adicional. Você também deve monitorar o desempenho do servidor quando o Assistente de pasta gerenciada está sendo executado. Além de contadores de desempenho listados neste tópico, convém também monitorar os contadores de desempenho adicional que monitorar itens como o desempenho do disco e o uso da CPU.

Para obter mais informações sobre o monitoramento de computadores que executam o MRM, consulte [Gerenciamento de registros de mensagens de monitoramento](monitoring-messaging-records-management-exchange-2013-help.md).

## Contadores de desempenho para o MRM

A tabela a seguir descreve os contadores de desempenho para MRM.

### Contadores de desempenho, objetos de desempenho e descrição

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador de desempenho</th>
<th>Objeto de desempenho</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tempo de processamento médio da caixa de correio em segundos</p></td>
<td><p>Assistentes do MSExchange</p></td>
<td><p>Calcula o tempo médio de processamento de caixas de correio para assistentes baseadas em tempo.</p></td>
</tr>
<tr class="even">
<td><p>Caixas de correio processadas</p></td>
<td><p>Assistentes do MSExchange</p></td>
<td><p>Calcula o número de caixas de correio processadas pelo assistentes baseadas em tempo desde que o serviço foi iniciado.</p></td>
</tr>
<tr class="odd">
<td><p>Caixas de correio processadas/s</p></td>
<td><p>Assistentes do MSExchange</p></td>
<td><p>Determina a taxa de caixas de correio processadas por assistentes com base em tempo por segundo.</p></td>
</tr>
<tr class="even">
<td><p>Itens excluídos, mas recuperáveis</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens excluídos pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. (Os itens são recuperáveis ainda através da pasta itens recuperáveis.) O número inclui itens nas caixas de correio agendadas para processamento durante o intervalo de agendamento e itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada intervalo de agendamento.</p></td>
</tr>
<tr class="odd">
<td><p>Itens registradas</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens registradas pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. O número inclui itens nas caixas de correio agendadas para processamento durante o ciclo de trabalho atual e os itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada ciclo de trabalho.</p></td>
</tr>
<tr class="even">
<td><p>Itens marcados como a data de retenção passada</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens marcados como fora da sua data de retenção pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. O número inclui itens em caixas de correio agendadas para processamento durante o intervalo de agendamento e itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada intervalo de agendamento.</p></td>
</tr>
<tr class="odd">
<td><p>Itens movidos</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens movidos pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. O número inclui itens nas caixas de correio agendadas para processamento durante o intervalo de agendamento e itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada intervalo de agendamento.</p></td>
</tr>
<tr class="even">
<td><p>Itens excluídos permanentemente</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens permanentemente excluídos pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. O número inclui itens nas caixas de correio agendadas para processamento durante o intervalo de agendamento e itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada intervalo de agendamento.</p></td>
</tr>
<tr class="odd">
<td><p>Itens sujeitos a política de retenção</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Calcula o número de itens sujeitos a política de retenção pelo Assistente de pasta gerenciada desde o início do intervalo de agendamento mais recente. O número inclui itens nas caixas de correio agendadas para processamento durante o intervalo de agendamento e itens em qualquer caixa de correio que você especificou para processamento. Esse contador é redefinido como zero no início de cada intervalo de agendamento. Esse contador é a soma dos seguintes quatro contadores relacionados a expiração:</p>
<ul>
<li><p>Itens registradas</p></li>
<li><p>Itens marcados como a data de retenção passada</p></li>
<li><p>Itens movidos</p></li>
<li><p>Itens excluídos permanentemente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - tamanho dos itens sujeitos a política de retenção (em Bytes)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica que o tamanho total dos itens expirados pelo Assistente de pasta gerenciada (SoftDelete, HardDelete, MoveToArchive).</p>
<p>Os seguintes itens são incluídos:</p>
<ul>
<li><p>Mensagens de entidade para exclusão ou mover para uma pasta personalizada gerenciada por uma política de caixa de correio de pasta gerenciada</p></li>
<li><p>Mensagens de entidade para exclusão ou mover para arquivo morto pela política de retenção do usuário</p></li>
<li><p>Mensagens expirou pelo dumpster política</p></li>
<li><p>Limpos pela marca de limpeza do sistema de mensagens</p></li>
</ul>
<p>Esse contador é redefinido como zero em cada ponto de verificação do ciclo de trabalho do Assistente de pasta gerenciada ciclo de trabalho.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - tamanho dos itens excluídos, mas recuperáveis (em Bytes)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o tamanho total dos itens suaves excluídos pelo Assistente de pasta gerenciada.</p>
<p>Os seguintes itens são incluídos:</p>
<ul>
<li><p>Mensagens suaves excluídas por uma diretiva de caixa de correio de pasta gerenciada</p></li>
<li><p>Mensagens suaves excluídas por uma política de retenção</p></li>
</ul>
<p>Esse contador é redefinido como zero em cada ponto de verificação do ciclo de trabalho do Assistente de pasta gerenciada ciclo de trabalho.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - tamanho dos itens excluídos permanentemente (em Bytes)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o tamanho total dos itens suaves excluídos pelo Assistente de pasta gerenciada.</p>
<p>Os seguintes itens são incluídos:</p>
<ul>
<li><p>Disco rígido de mensagens excluídas por uma política de caixa de correio de pasta gerenciada</p></li>
<li><p>Disco rígido de mensagens excluídas por uma política de retenção</p></li>
<li><p>Disco rígido de mensagens excluídas pela política de itens recuperáveis</p></li>
</ul>
<p>Esse contador é redefinido como zero em cada ponto de verificação do ciclo de trabalho do Assistente de pasta gerenciada ciclo de trabalho.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - tamanho dos itens movidos devido a uma marca de política de arquivamento (em Bytes)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o tamanho total dos itens movidos para uma pasta ou movido para arquivar pelo Assistente de pasta gerenciada.</p>
<p>Os seguintes itens são incluídos:</p>
<ul>
<li><p>As mensagens são movidas para uma pasta personalizada gerenciada por uma política de caixa de correio de pasta gerenciada</p></li>
<li><p>As mensagens são movidas para o arquivo pessoal por uma política de retenção</p></li>
</ul>
<p>Esse contador é redefinido como zero em cada ponto de verificação do ciclo de trabalho do Assistente de pasta gerenciada ciclo de trabalho.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - itens marcados com marca pessoal (expiração ou arquivo morto)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o número de vezes que um usuário marcas de itens com uma marca pessoal.</p>
<p>Isso inclui as marcas de exclusão e arquivamento.</p>
<p>Por exemplo:</p>
<ul>
<li><p>Um item marcado com uma marca pessoal.</p></li>
<li><p>Um item com uma marca pessoal é retagged com outra marca pessoal.</p></li>
</ul>
<p>Se uma pasta é marcada com uma marca pessoal, o contador é incrementado pelo número total de itens na pasta.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - itens marcados com marca padrão (expiração ou arquivo morto)</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica que o número de itens atribuído a uma marca de diretiva padrão (DPT) com base em uma ação do usuário, por exemplo, quando um usuário seleciona uma mensagem com uma marca pessoal e seleciona a <strong>usar a política de pasta</strong>.</p>
<p>Se um novo usuário é atribuído a uma política de retenção com um DPT, o contador é incrementado pelo número de itens que serão atribuídos a DPT devido à política de retenção.</p>

> [!TIP]
> Se um usuário tiver uma política de retenção com um DPT, novas mensagens que chegarem por meio de transporte obtém uma marca padrão e isso não é rastreado por esse contador.


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - itens marcados com marca de limpeza do sistema</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o número de itens marcados com a marca de limpeza do sistema. Isso inclui itens de metadados de caixa de correio que não estão visíveis aos usuários.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - itens expirados devido a uma marca de expiração padrão</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica que o número de itens expirados (soft ou grave excluída) pelo Assistente de pasta gerenciada devido a qualquer marca de não-pessoais (padrão ou sistema) em uma política de retenção.</p>
<p>Isso não inclui os itens expirados pelos itens recuperáveis limpeza ou limpar do sistema.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - itens expirados devido a uma marca pessoal de expiração</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica que o número de itens expirados (soft ou grave excluída) pelo Assistente de pasta gerenciada devido a uma marca pessoal na política de retenção.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - itens movidos devido a uma marca de arquivo morto padrão</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o número de itens movidos para o arquivo morto pelo Assistente de pasta gerenciada devido a qualquer tag não pessoais (padrão ou sistema) archive uma política de retenção.</p>
<p>Isso não inclui os itens movidos para a pasta itens recuperáveis no arquivo morto com limpeza de itens recuperáveis.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - itens movidos devido a uma marca de arquivo morto</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o número de itens movidos para o arquivo morto pelo Assistente de pasta gerenciada devido a uma marca de arquivo pessoal em uma política de retenção.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - Dumpsters de caixa de correio movido itens</p></td>
<td><p>Assistente de pasta gerenciada do MSExchange</p></td>
<td><p>Indica o número de itens movidos para a pasta itens recuperáveis no arquivamento pelo limpeza de itens recuperáveis.</p></td>
</tr>
</tbody>
</table>

